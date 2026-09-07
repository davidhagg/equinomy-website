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

## Design System (v2)

The site was redesigned to match the redesigned mobile app's visual language — warm
cream ground, plum ink, pink accent. The full handoff spec (colours, type scale,
spacing, radii, per-section markup) lives in `design/README.md`; the two `.dc.html`
files in that folder are pixel-reference prototypes, not code to copy verbatim — see
that README before touching layout/visuals again.

All styling is in `assets/style.css`. Key points:
- **Design tokens**: CSS variables for the cream/plum/pink palette — cream `#fbf7f6`,
  plum ink `#2a1420`, pink accent `#e0165f` (gradient stops `#f0407a`→`#cf0a4f`), plus
  amber/teal/green/violet/magenta category colours. See `:root` in `assets/style.css`.
- **Font**: pure system stack (`-apple-system, ... system-ui, sans-serif`) everywhere —
  no webfont, no icon font, no emoji icons. Every feature card's own mini-visual (built
  from HTML/CSS/inline SVG) does the illustration work; don't add a leading icon tile.
- **Phone mockups**: the dark bezel is CSS (`.phone-shell`/`.phone-screen` for the hero
  phone, `.phone-shell-sm`/`.phone-screen-sm` for the "see it in action" trio) — the
  screen content itself is a real app screenshot (`assets/screenshots/`, a `.phone-
  screenshot` `<img>`), not hand-drawn. Source screenshots come from the mobile repo's
  `app-screenshots/` (fresh simulator captures); when swapping in new ones, resize with
  `sips -Z 640` first (see git history for the exact command) rather than committing
  full-resolution captures. The features grid's own small in-card visuals (bar/donut/
  budget-row previews inside `Multi-Horse Support`, `Smart Expense Overviews`, etc.) are
  a separate thing and stay hand-drawn HTML/CSS/inline SVG — only the two full-phone
  mockup areas use screenshots.
- **Responsive**: everything wraps via `flex-wrap`/`auto-fit` grids, no fixed
  two-column tracks — the page collapses to one column below ~620–760px depending on
  section. Breakpoints used: 920px, 860px, 680px, 560px.

## Multilingual Pages

Legal pages exist in English, German (`de`), French (`fr`), and Swedish (`se`). Each page includes a language switcher linking to the other language variants. When updating legal content, all 4 language versions must be updated. Nav/footer markup (`.nav-inner`, `.nav-cta`, `.footer-top`/`.footer-brand`) must stay identical across all 8 legal pages and `index.html` — copy any nav/footer structure change to all of them.

## Content Structure (index.html)

The landing page has these sections in order, per `design/README.md` (note: the card
count/badges below have drifted from that doc — Health Log & Reminders and Synced
Across Devices were removed since those features don't exist/apply, and the Google
Play badge is off until Android ships; update `design/README.md` if it's revised):
1. Sticky nav (blurred cream bar, "Get the app" pink CTA)
2. Hero — no badge above the headline (removed; was "AI-powered expense tracking").
   Two-tone headline, CTA buttons, trust pills (iOS only, not "iOS & Android"), real
   screenshot in the CSS-drawn phone bezel.
3. Features grid (7 cards — 1 wide, 6 single; the "Income Too, Not Just Costs" card
   is behind a content flag, on by default — see `design/README.md`'s Content Flags).
   The AI/receipt-scanning card is deliberately soft-pedaled — "Add Expenses in
   Seconds", framed as manual entry OR camera scan, not an AI pitch.
4. "See it in action" — full-bleed dark plum band, 3 real screenshots in CSS-drawn
   phone bezels (Log, horse profile w/ shared costs, Budget)
5. "Effortless" (was "AI-powered") — repeated headline + a 5-row checklist, reworded
   to lead with manual-or-camera entry rather than "AI"
6. Download panel (pink gradient block, App Store badge only — no Google Play)
7. Footer (logo + link grid to all 4 languages × privacy/terms + contact)
