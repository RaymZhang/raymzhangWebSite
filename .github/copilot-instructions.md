# Copilot instructions for this repo

## Big picture
- This is a Hugo Blox “Academic CV” site. Hugo config lives in [config/_default/hugo.yaml](config/_default/hugo.yaml) and site params in [config/_default/params.yaml](config/_default/params.yaml).
- Hugo modules define the theme/plugins in [config/_default/module.yaml](config/_default/module.yaml) and the Go module metadata in [go.mod](go.mod).
- The rendered site is committed under [public/](public/) and is generated output; don’t hand-edit it.

## Content & structure
- The homepage is a “landing” page defined in [content/_index.md](content/_index.md) with a `sections` list of Hugo Blox blocks (e.g., `resume-biography-3`, `collection`).
- Publications live under [content/publication/](content/publication/) with one folder per item (e.g., [content/publication/Thompson_Sampling/index.md](content/publication/Thompson_Sampling/index.md)). Front matter carries fields like `authors`, `publication`, and `url_pdf`; optional `cite.bib` files sit next to the entry.
- Teaching pages are section pages under [content/teaching/](content/teaching/).
- Author profile data is in [content/authors/](content/authors/), and the navbar is configured in [config/_default/menus.yaml](config/_default/menus.yaml).

## Assets & customization
- Images referenced by blocks are stored in [assets/media/](assets/media/). Downloadables (e.g., CV) are expected under [static/uploads/](static/uploads/).
- Custom HTML injections are placed under [layouts/partials/hooks/](layouts/partials/hooks/) (e.g., GitHub button script in [layouts/partials/hooks/head-end/github-button.html](layouts/partials/hooks/head-end/github-button.html)).

## Build & deploy
- Netlify build settings are in [netlify.toml](netlify.toml). The build command is:
  - `hugo --gc --minify -b $URL && npx pagefind --source 'public'`
- The repo pins Hugo 0.136.5 in [hugoblox.yaml](hugoblox.yaml) and Netlify sets `HUGO_VERSION` to match.

## Conventions to follow
- Keep content updates in `content/` and config changes in `config/_default/` rather than editing generated output in `public/`.
- When adding a new publication, follow the folder-per-publication pattern used in [content/publication/](content/publication/).