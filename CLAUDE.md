# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Equinomy is a static marketing website for an AI-powered horse expense tracking mobile app. Hosted on GitHub Pages at `equinomyapp.com`.

## Development

No build system. Edit HTML/CSS files directly and push to `main` — GitHub Pages deploys automatically.

To preview locally, open any `.html` file directly in a browser or use a simple HTTP server:

```bash
python3 -m http.server 8080
```

## Architecture

**Pure static site** — no JavaScript, no frameworks, no bundler.

| File | Purpose |
|------|---------|
| `index.html` | Main landing page |
| `assets/style.css` | All styles (1100+ lines, single stylesheet) |
| `privacy-policy-{en,de,fr,se}.html` | GDPR privacy policies in 4 languages |
| `terms-{en,de,fr,se}.html` | Terms of Service in 4 languages |
| `CNAME` | GitHub Pages custom domain (`equinomyapp.com`) |

## CSS Architecture

All styling is in `assets/style.css`. Key sections:
- **Design tokens**: CSS variables for colors, gradients (purple `#8B5CF6` → magenta `#AE2E8A` → pink `#F472B6`), dark background (`#0d0d14`)
- **Font**: Bricolage Grotesque (headings, loaded from Google Fonts), system fonts (body)
- **Animations**: CSS-only — `float` (hero orbs), `scan-beam` (receipt mockup), `pulse-dot` (status indicators)
- **Responsive breakpoints**: 920px, 860px, 680px, 560px

## Multilingual Pages

Legal pages exist in English, German (`de`), French (`fr`), and Swedish (`se`). Each page includes a language switcher linking to the other language variants. When updating legal content, all 4 language versions must be updated.

## Content Structure (index.html)

The landing page has these sections in order:
1. Sticky navigation bar
2. Hero (gradient headline, CTA buttons, floating orbs)
3. Features bento grid (6 cards with pure-CSS illustrations)
4. App screenshots carousel (staggered phone mockups)
5. AI highlight strip
6. Download section (App Store + Google Play badges)
7. Footer (links to legal pages in all 4 languages)
