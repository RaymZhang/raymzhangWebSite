# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Raymond Zhang's personal academic website (https://raymzhang.com), built on the Hugo Blox
"Academic CV" starter. The upstream theme is a Hugo **module** (see `config/_default/module.yaml`),
not a vendored `themes/` folder — so the bulk of the templates live in the Go module cache, and
this repo contains only content, config, and a handful of template *overrides*.

## Commands

```bash
pnpm install
pnpm dev                 # hugo server --disableFastRender  → http://localhost:1313
pnpm build               # hugo --minify && pagefind --site public
pnpm pagefind            # rebuild the Pagefind search index only
hugo --gc --minify -b https://raymzhang.com/    # what CI/Netlify effectively runs
```

There is no test suite and no linter.

**A `go` toolchain is required to build.** The theme is fetched as a Hugo module, and without `go`
on PATH every build fails with `failed to download modules: binary with name "go" not found in
PATH`. Note `hugo --quiet` *swallows* this error and merely exits 1 — always build without
`--quiet`, or check the exit code, before believing a build succeeded. Netlify installs Go 1.21.5
for this reason; it is not currently installed on this machine.

To pull a newer theme: `hugo mod get -u ./...` (the `.github/workflows/upgrade.yml` cron does this
weekly and opens a `chore/upgrade-hugoblox-*` PR).

## Where things live

- **Config**: `config/_default/` — `hugo.yaml` (site-wide, incl. the `cascade` block that disables
  reading time/share and hides event dates), `params.yaml` (appearance, features), `menus.yaml`
  (navbar), `module.yaml` (theme + mounts).
- **Content**: `content/` — `_index.md` is the landing page, composed of a `sections:` list of Hugo
  Blox blocks (`resume-biography-3`, `collection`, …). Sections: `publications/`, `research/`,
  `teaching/`, `events/`, `authors/`.
- **Overrides**: `layouts/` shadows theme templates. `layouts/_partials/` is the Hugo ≥0.146
  partial path used by the theme; `layouts/partials/hooks/head-end/*.html` are injection points
  (GitHub button, forced dark mode, JSON-LD).
- **Assets**: images for blocks in `assets/media/`; downloadables (CV, etc.) in `static/uploads/`.
- `public/` and `resources/` are generated and gitignored — never edit them.

## Conventions that are easy to get wrong

- **One folder per publication**: `content/publications/<Name>/index.md`. Front matter uses
  `authors:` (list of slugs) and a `links:` list for PDF/code — not the deprecated
  `url_pdf` / `url_code`.
- **Author slugs must match filenames in `data/authors/`** (lowercase, URL-safe). `content/authors/me.yaml`
  is the site owner's profile (`is_owner: true`); co-authors live in `data/authors/`.
- **Author-name linking** is custom: `layouts/_partials/author_link.html` returns a dict and picks,
  in order, the site baseURL for the owner → a link labelled `Website`/`Site` → any http(s) link →
  `/authors/<slug>/`. So when adding a co-author, give them a link labelled `Website`. The
  `resume-biography-3` override deliberately hides the Website icon in social links because that
  link is consumed for name-linking instead.
- **Custom list views** live in `layouts/_partials/views/`: `date-title-summary-period` (teaching,
  renders a `period` param or derives `date_start`–`date_end`) and `date-title-summary-event`
  (news/events). They are selected via `view:` in a collection block or section `_index.md`.

## Theme mode: dark only — do not break this

The site is designed and visually verified **only in dark mode**; the light palette is unchecked
(text becomes unreadable over the hero background image). Light mode must never be served.

Three things enforce this — keep all three:

1. `hugoblox.theme.mode: dark` in [config/_default/params.yaml](config/_default/params.yaml). This is
   the *only* key the theme reads; it renders into `<html data-wc-theme-default="dark">` (see the
   module's `layouts/baseof.html`). A top-level `appearance:` block is **legacy and ignored** by
   blox v0.11+ — do not "fix" the mode there.
2. `hugoblox.header.theme_toggle` / `theme_picker` stay `false`, so no visitor can switch.
3. [layouts/_partials/hooks/head-end/force-dark-mode.html](layouts/_partials/hooks/head-end/force-dark-mode.html)
   clears any stale `wc-color-theme` in a returning visitor's localStorage. The key is
   **`wc-color-theme`** (read by the module's `assets/js/hb-init.js`) — not `hb-appearance`.

## Hooks must live in `layouts/_partials/hooks/`

The theme's `functions/get_hook` does a literal `os.ReadDir "layouts/_partials/hooks/<name>/"`.
A hook placed in the pre-0.146 `layouts/partials/hooks/` path is **silently ignored** — no error,
it just never renders. Current head-end hooks: forced dark mode, dark-mode background-image CSS,
GitHub button, homepage JSON-LD.

## Adding content

Every content item is a **page bundle**: a folder with `index.md` plus its assets, so downloadable
files sit next to the page that links them. This is how students get slides/notes.

- **Teaching** — `content/teaching/<Course Name>/index.md`. Front matter: `title`, `summary`,
  `date`, `period` (e.g. `"2023-2025"`, drives the `date-title-summary-period` view), `type: docs`,
  `tags`, `math: true` if LaTeX is used. Put course resources in the same folder and expose them
  with a `links:` list, e.g.
  ```yaml
  links:
    - type: slides
      url: lecture01.pdf
      label: Lecture 1 — slides
    - type: pdf
      url: notes.pdf
  ```
  Link types come from the module's `data/link_types.yaml`: `pdf, preprint, doi, code, dataset,
  model, slides, video, poster, project, site, source, bibtex, demo, event, …`. For a longer list of
  materials, a Markdown table in the page body linking the bundle files works too.
- **Publications** — `content/publications/<Key>/index.md`, alongside `cite.bib`, `featured.jpg`,
  and the paper PDF. Use `links:` (types `pdf`, `code`, `preprint`, …); the deprecated
  `url_pdf`/`url_code` fields still work but emit warnings. A PDF named after the *folder*
  (e.g. `E2TC/E2TC.pdf`) and a `cite.bib` are auto-detected and linked without any front matter.
- **News/events** — `content/events/<slug>/index.md`, rendered by the `date-title-summary-event`
  view; the `cascade` in `hugo.yaml` hides the date section on these pages.

Note the existing teaching folders use spaces in names (`Machine Learning`), so quote paths in shell
commands.

## Deployment

Netlify is the live deploy path (`netlify.toml`; production/preview/branch-deploy each run
`pnpm install` → `hugo --gc --minify -b $URL` → `pagefind`, with a 301 from the `.netlify.com`
domain to `raymzhang.com`). Hugo is pinned to **0.154.5** in both `netlify.toml` and `hugoblox.yaml`
— bump both together.

**Netlify is the only deploy target.** GitHub Pages is deliberately disabled: the `publish.yaml`
workflow was deleted and `hugoblox.yaml` declares `host: 'netlify'`. Do not re-add a Pages workflow.

`import-publications.yml` (BibTeX → Markdown) and `upgrade.yml` trigger on `main`, but this repo's
default branch is `master`, so the import workflow does not fire — add publications by hand instead.
