# Copilot instructions for this repo

## Big picture
- This is a Hugo Blox “Academic CV” site. Hugo config lives in [config/_default/hugo.yaml](config/_default/hugo.yaml) and site params in [config/_default/params.yaml](config/_default/params.yaml).
- Hugo modules define the theme/plugins in [config/_default/module.yaml](config/_default/module.yaml) and the Go module metadata in [go.mod](go.mod).
- The rendered site is committed under [public/](public/) and is generated output; don’t hand-edit it.

## Content & structure
- The homepage is a “landing” page defined in [content/_index.md](content/_index.md) with a `sections` list of Hugo Blox blocks (e.g., `resume-biography-3`, `collection`).
- Publications live under [content/publications/](content/publications/) with one folder per item (e.g., [content/publications/Thompson_Sampling/index.md](content/publications/Thompson_Sampling/index.md)). Front matter uses `authors` plus `links` for PDF/code; avoid deprecated `url_pdf`/`url_code`.
- Teaching pages are under [content/teaching/](content/teaching/) and use a custom period view (`date-title-summary-period`).
- Author profiles are stored in [data/authors/](data/authors/) (slugs must match filenames), and the navbar is configured in [config/_default/menus.yaml](config/_default/menus.yaml).
- Events live under [content/events/](content/events/); the event page template hides the date section via `hide_event_date_section` (set globally in [config/_default/hugo.yaml](config/_default/hugo.yaml)).

## Assets & customization
- Images referenced by blocks are stored in [assets/media/](assets/media/). Downloadables (e.g., CV) are expected under [static/uploads/](static/uploads/).
- Custom HTML injections are placed under [layouts/partials/hooks/](layouts/partials/hooks/) (e.g., GitHub button script in [layouts/partials/hooks/head-end/github-button.html](layouts/partials/hooks/head-end/github-button.html)).
- Custom template overrides live in [layouts/_partials/](layouts/_partials/) and [layouts/](layouts/). Notable overrides:
  - Resume block override: [layouts/_partials/hbx/blocks/resume-biography-3/block.html](layouts/_partials/hbx/blocks/resume-biography-3/block.html)
  - Author link logic: [layouts/_partials/author_link.html](layouts/_partials/author_link.html)
  - Author lists/cards: [layouts/_partials/page_metadata_authors.html](layouts/_partials/page_metadata_authors.html), [layouts/_partials/page_author_card.html](layouts/_partials/page_author_card.html)
  - Single and event page overrides: [layouts/single.html](layouts/single.html), [layouts/events/page.html](layouts/events/page.html)

## Build & deploy
- Netlify build settings are in [netlify.toml](netlify.toml). The build command is:
  - `hugo --gc --minify -b $URL && npx pagefind --source 'public'`
- The repo pins Hugo 0.136.5 in [hugoblox.yaml](hugoblox.yaml) and Netlify sets `HUGO_VERSION` to match.

## Conventions to follow
- Keep content updates in `content/` and config changes in `config/_default/` rather than editing generated output in `public/`.
- When adding a new publication, follow the folder-per-publication pattern used in [content/publications/](content/publications/).
- Author slugs in `authors:` must match filenames in [data/authors/](data/authors/) (lowercase, URL-safe).
- Author names should link to personal websites (label links as `Website` or `Site` in author profiles). The shared logic is in [layouts/_partials/author_link.html](layouts/_partials/author_link.html).
- The resume-biography-3 block hides the Website icon in social links; if you add a Website link, it is used for author-name linking, not as a visible icon.
- Global page params are set in [config/_default/hugo.yaml](config/_default/hugo.yaml) (e.g., `reading_time: false`, `share: false`).