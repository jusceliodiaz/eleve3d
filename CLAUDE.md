# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-file static website for **Eleve 3D Studio** — a Brazilian architectural visualization studio. The entire site lives in `index.html` with all CSS and JavaScript inlined.

## Running the site

No build step. Open `index.html` directly in a browser, or serve locally:

```bash
# Python
python -m http.server 8080

# Node (npx)
npx serve .
```

## Architecture

Everything is in `index.html`:

- **CSS** — pure custom properties (`--bg`, `--fg`, `--fg2`, `--fg3`, `--border`, `--display`, `--ui`, `--body`) with no framework. All classes use short, abbreviated names (e.g. `.rev` for scroll-reveal, `.pi` for portfolio item, `.sc-card` for service card).
- **Fonts** — `Cormorant Garamond` (display/headings), `Syne` (UI/labels/nav), `DM Sans` (body text) — loaded from Google Fonts.
- **JavaScript** — vanilla, all inline at the bottom of `<body>`. Key systems:
  - Loader: hides after 2.3s on `window load`
  - Custom cursor: `#cur-dot` (snaps) + `#cur-ring` (lerp follow at 12%)
  - Navbar: adds class `.sc` on scroll > 50px for blur/background
  - Scroll reveal: `IntersectionObserver` adds `.vis` to `.rev` elements
  - Counter animation: `IntersectionObserver` on `[data-count]` attributes
  - Portfolio filter: `.fb` buttons toggle `.on`, filter `.pi` by `data-cat`

## Key design decisions

- **No dependencies** — intentional. The site must remain a single deployable file.
- **Abbreviated class names** — kept short to reduce file size (`.pi`, `.fb`, `.tc`, `.rev`, `.d1`–`.d4`).
- **Images** — sourced from Unsplash with query params `?q=80&w=...&auto=format&fit=crop`. Replace URLs to swap project images.
- **Contact/WhatsApp links** use placeholder numbers (`5511999999999`) — update before going live.
- **Responsive breakpoints**: `≤1050px` (collapse about/portfolio), `≤860px` (mobile layout, hamburger), `≤580px` (single column footer).
