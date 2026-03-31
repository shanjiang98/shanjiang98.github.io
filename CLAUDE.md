# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Personal academic website for Shan Jiang (Ph.D. candidate, UT Austin) built with [al-folio](https://github.com/alshedivat/al-folio), a Jekyll theme for academics. Deployed to `https://shanjiang98.github.io`.

## Build & Development

Docker is the recommended approach:

```bash
docker compose pull && docker compose up    # Start dev server at http://localhost:8080
docker compose up --build                   # Rebuild after dependency/Dockerfile changes
docker compose down                         # Stop and free port 8080
```

Legacy (without Docker):
```bash
bundle install && pip install jupyter
bundle exec jekyll serve --port 4000
```

### Pre-Commit

1. **Format:** `npx prettier . --write` (requires `npm install --save-dev prettier @shopify/prettier-plugin-liquid` first time)
2. **Build & verify:** `docker compose up --build`, check http://localhost:8080

CI runs a Prettier check on PRs — unformatted code will fail the build.

## Architecture

- **Jekyll static site** using Ruby, with Liquid templates and SCSS
- **`_config.yml`** — central configuration: site metadata, feature flags (`enable_*`), plugin settings, Jekyll Scholar config for publications
- **`_bibliography/papers.bib`** — BibTeX publications, rendered by jekyll-scholar. Supports custom keys: `pdf`, `code`, `preview`, `selected`, `arxiv`, `blog`, `slides`, `video`, `website`
- **`_data/`** — YAML data files: `socials.yml`, `coauthors.yml`, `cv.yml`, `citations.yml`, `venues.yml`, `repositories.yml`
- **`_pages/`** — top-level pages (about.md, cv.md, publications.md, projects.md, teaching.md)
- **`_posts/`** — blog posts (YYYY-MM-DD-title.md format)
- **`_news/`** — news/announcement entries shown on the about page
- **`_projects/`**, **`_teachings/`** — collection items
- **`_layouts/`** — page templates (Liquid); **`_includes/`** — reusable components
- **`_sass/`** — SCSS stylesheets; **`_scripts/`** — JavaScript
- **`assets/img/`** — images (processed by ImageMagick into responsive WebP)

### Key Config Relationships

- `url` + `baseurl` must be consistent: for personal sites, `url: https://username.github.io` with empty `baseurl:`
- Jekyll Scholar uses `scholar.last_name` and `scholar.first_name` in `_config.yml` to highlight the site owner in publication lists
- Feature flags in `_config.yml` (e.g., `enable_math`, `enable_darkmode`, `enable_masonry`) toggle site-wide behavior

### YAML Gotcha

Quote strings with special characters in `_config.yml`: `title: "My: Cool Site"`

## File-Specific Guidance

| File Type | Reference |
|---|---|
| Markdown content (`_posts/`, `_pages/`) | `.github/instructions/markdown-content.instructions.md` |
| YAML config (`_config.yml`, `_data/`) | `.github/instructions/yaml-configuration.instructions.md` |
| BibTeX (`_bibliography/`) | `.github/instructions/bibtex-bibliography.instructions.md` |
| Liquid templates (`_includes/`, `_layouts/`) | `.github/instructions/liquid-templates.instructions.md` |
| JavaScript (`_scripts/`) | `.github/instructions/javascript-scripts.instructions.md` |
