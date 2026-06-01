# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static personal portfolio site for Andrey A. Sidorenko, hosted on GitHub Pages. No build system — edit files and open in browser.

## Preview

```bash
open index.html                          # Main portfolio
open projects/weatherApp/index.html
open projects/wikiViewer/index.html
open projects/quote/index.html
```

## Deployment

```bash
git push origin master   # Deploys to GitHub Pages automatically
```

## Architecture

Single-page portfolio (`index.html`) with anchor-based navigation. Sections: `#welcome-section` (parallax hero) → `#about-section` → `#projects-section` → `#presentations-section` → `#tools-section` (MOOCs) → `#contact-section`.

Three self-contained mini-apps under `projects/`, each with their own HTML/CSS/JS. They use external APIs (weather via geolocation, Wikipedia search, quote API) with jQuery AJAX.

**Key dependency versions (pinned via CDN):**
- Bootstrap 3.3.7
- jQuery 3.3.1
- Font Awesome 5.0.6 (JS) + 5.0.13 (CSS) — both loaded simultaneously in `index.html`

## Gotchas

- `docs/` contains personal documents (CV PDFs, business plan) — do not move or rename
- `css/___portfolio.css` is a backup variant — not loaded by any HTML
- `index.html` has a typo-tag `<diResponsive Web Design Certificatev>` inside the MOOCs section (line ~200) — leave it unless fixing that section
- All asset paths must stay relative (no absolute `/` paths) — GitHub Pages serves from the repo root
- The navbar links to `#tools-section` but the label reads "MOOCs"
