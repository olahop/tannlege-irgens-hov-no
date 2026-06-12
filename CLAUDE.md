# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static single-page website for dentist Marit Irgens Hov, hosted on GitHub Pages at [tannlege-irgens-hov.no](https://tannlege-irgens-hov.no). No build step, no dependencies, no framework — plain HTML/CSS/JS served as-is.

The site is in Norwegian (`lang="no"`). Keep all user-facing copy in Norwegian.

## Develop & deploy

- **Preview locally:** open `index.html` directly, or run `python3 -m http.server` and visit `http://localhost:8000` (use a server so relative font/image paths and the manifest resolve correctly).
- **Deploy:** push to `main`. GitHub Pages publishes automatically. `CNAME` pins the custom domain.

## Architecture

The entire page is three files:

- `index.html` — one page, four `<section>` blocks (`#om`, `#behandling`, `#time`, `#kontakt`). Also holds all SEO/meta: Open Graph tags, favicons, font/image preloads, and a JSON-LD `schema.org` block describing the `Dentist` business and its two branch locations (Frogner/Oslo and Harestua/Lunner). When clinic addresses, phone numbers, or services change, update both the visible markup **and** the matching JSON-LD entry.
- `styles.css` — all styling. Design tokens (colors, radius, shadows) live in the `:root` CSS custom properties at the top; reuse them rather than hardcoding values. Mobile breakpoints are inline `@media` queries per component.
- `script.js` — two small vanilla-JS behaviors: a scroll shadow on the sticky header, and an `IntersectionObserver` that adds `.visible` to `.fade-up` sections for scroll-in animations. Any new section needs the `fade-up` class to animate.

## Assets & performance

Performance is deliberately hand-tuned — preserve these when editing `<head>`:

- Fonts (Cormorant Garamond) are **self-hosted** in `fonts/` as woff2 with explicit `unicode-range` splits (latin + latin-ext for Norwegian å/ø/æ). Do not reintroduce Google Fonts — that was removed to eliminate render-blocking.
- `marit.webp` is the optimized hero image used on the page and is preloaded as the LCP image. `marit.jpg` is kept only for social/`og:image` sharing compatibility.
