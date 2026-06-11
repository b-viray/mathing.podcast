# Mathing with Dan and Bianca — website

A Quarto website for the podcast. Same workflow as a personal Quarto site:
edit `.qmd` files, run `quarto render`, push.

## Files

- `_quarto.yml` — site config (navbar, theme, footer, Spotify link)
- `index.qmd` — homepage (tagline, subscribe button, 3 most recent episodes)
- `episodes.qmd` — auto-generated list of all episodes
- `episodes/` — one `.qmd` file per episode
  - `_template.qmd` — copy this to create a new episode (underscore-prefixed files are never published)
  - `ep-000-trailer.qmd` — example episode; edit or delete
- `about.qmd` — host bios (placeholders to fill in)
- `styles.scss` — colors and styling; change `$primary` to re-theme the site
- `CNAME` — your custom domain (see below)

## Before launch — things to replace

1. **Spotify link**: search for `YOUR_SHOW_ID` in `_quarto.yml` and `index.qmd`
   and replace with your show's Spotify URL once it's live.
2. **Bios + contact email** in `about.qmd`.
3. **Your domain** in `CNAME` (e.g. `www.yourdomain.com`) and `site-url` in `_quarto.yml`.

## Publishing on GitHub Pages

This project renders into `docs/` (set in `_quarto.yml`), which is the
simplest GitHub Pages setup:

1. Create a new GitHub repo (e.g. `podcast-site`) and push this folder to it.
2. Run `quarto render` locally — this creates `docs/`. Commit and push it.
3. In the repo: **Settings → Pages → Deploy from a branch → `main` / `docs/`**.
4. Workflow from then on: edit → `quarto render` → commit → push.

(Alternative: `quarto publish gh-pages` if you prefer the gh-pages branch
workflow — then remove `output-dir: docs`.)

## Connecting your Squarespace domain

1. In the repo's **Settings → Pages → Custom domain**, enter your domain
   (e.g. `www.yourdomain.com`) and enable **Enforce HTTPS** once available.
2. The `CNAME` file in this project is copied into `docs/` on every render
   so the domain setting survives re-renders — make sure it contains your
   real domain.
3. In Squarespace: **Domains → your domain → DNS settings**, add:
   - `CNAME` record: host `www` → `USERNAME.github.io`
   - Four `A` records for the apex/root (`@`):
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
4. DNS can take up to a few hours to propagate.

## Adding a new episode

```bash
cp episodes/_template.qmd episodes/ep-001-my-topic.qmd
# edit title, description, date, show notes
quarto render
git add -A && git commit -m "Add episode 1" && git push
```

The episode automatically appears on the Episodes page and homepage —
no other files need editing.
