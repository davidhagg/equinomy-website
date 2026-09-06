# Handoff: Equinomy marketing site redesign

## Overview
A redesign of the public marketing site at https://equinomyapp.com. Equinomy is an
AI-powered expense tracker for horse owners; the site's job is to explain the product
and drive App Store / Google Play downloads.

The redesign brings the site into the same visual language as the redesigned mobile app
(see `design_handoff_horse_economy/`) — warm cream ground, plum ink, pink accent — but
scaled up for marketing: large display type, one full-bleed dark section, and a
colour-blocked download panel.

All body and heading copy is taken **verbatim** from the existing live site. Do not rewrite it.

## About the Design Files
The files in this bundle are **design references created in HTML**. They are prototypes
showing intended look and behaviour — not production code to lift wholesale.

The task is to recreate this design in the site's real environment using its established
patterns (whatever static-site or framework setup equinomyapp.com is built on). If there
is no established setup, a static HTML/CSS build or a small Astro/Next static export are
all appropriate — the page has no dynamic behaviour beyond anchor scrolling.

One caveat about the source file: it is authored in a component runtime that compiles
inline `style="..."` attributes to React style objects, and uses `style-hover="..."` for
hover states. When porting, convert these to ordinary CSS — hover rules cannot stay
inline. `<sc-if value="{{ showIncome }}">` is a conditional wrapper around one feature
card; treat it as "include this card" (see Content Flags below).

## Fidelity
**High-fidelity.** Colours, type sizes, spacing, and radii are final and should be matched.
Recreate pixel-perfectly, substituting the codebase's own utility/token layer where one exists.

## Page Structure
Single long page, max content width **1140px**, horizontal padding **22px**, centred.
Sections top to bottom:

1. Sticky nav
2. Hero (copy + phone mockup)
3. Features grid (9 cards)
4. "See it in action" — full-bleed plum band with 3 phone mockups
5. "AI-powered" — copy + checklist
6. Download panel (pink)
7. Footer

### 1. Sticky nav
- `position:sticky; top:0; z-index:40`
- Background `rgba(251,247,246,.72)` with `backdrop-filter: blur(22px) saturate(1.5)`
  (include the `-webkit-` prefix), bottom border `1px solid rgba(42,20,32,.06)`
- Inner: `padding:13px 22px`, flex, `flex-wrap:wrap`, `justify-content:space-between`, `gap:10px 20px`
- Left: logo image 32×32, `border-radius:9px`, `object-fit:contain`; wordmark "Equinomy"
  at `700 18px`, `letter-spacing:-.028em`
- Right: links Features / Download / Privacy at `500 14.5px`, colour `rgba(42,20,32,.6)`,
  `padding:9px 13px`, `border-radius:10px`; hover → `background:rgba(42,20,32,.05)`, ink `#2a1420`
- CTA "Get the app": `590 14.5px`, white on `linear-gradient(150deg,#f0407a,#cf0a4f)`,
  `padding:11px 17px`, `border-radius:12px`, `box-shadow:0 8px 20px -10px rgba(224,22,95,.9)`

### 2. Hero
- Two radial glow blobs behind the content, both `pointer-events:none`:
  - top `-260px`, left 50% `translateX(-42%)`, 1100×760, `radial-gradient(circle,rgba(224,22,95,.16),rgba(224,22,95,0) 62%)`
  - top `60px`, right `-180px`, 700×620, `radial-gradient(circle,rgba(217,130,0,.14),rgba(217,130,0,0) 64%)`
- Layout: flex, `flex-wrap:wrap`, `gap:40px`, `align-items:center`, `padding:56px 22px 20px`.
  Copy column `flex:1 1 380px`; phone column `flex:1 1 300px`. Collapses to one column below ~760px.
- Eyebrow pill: star icon + "AI-powered expense tracking" at `590 12.5px` `#cf0a4f`,
  background `rgba(224,22,95,.09)`, border `1px solid rgba(224,22,95,.18)`, `border-radius:999px`, `padding:8px 14px 8px 11px`
- H1: `700 clamp(42px,6.2vw,72px)/1.02`, `letter-spacing:-.038em`, `text-wrap:balance`.
  Line 1 "Track what you spend." in `#2a1420`; line 2 "Stay in the saddle." in `rgba(42,20,32,.42)`
- Sub: `400 clamp(16px,1.6vw,19px)/1.55`, `rgba(42,20,32,.6)`, `max-width:460px`
- Buttons: primary pink gradient `590 16px`, `padding:16px 26px`, `border-radius:15px`,
  `box-shadow:0 16px 34px -14px rgba(224,22,95,.95)`; secondary white with
  `1px solid rgba(42,20,32,.09)`, hover `background:#fff8f7`
- Three trust pills (dot + label): white, `1px solid rgba(42,20,32,.07)`, `border-radius:999px`,
  `padding:8px 14px`, label `500 13px` `rgba(42,20,32,.62)`. Dots `#17a05f` / `#0e8fa0` / `#6a4fe0`
- Entrance animation: `@keyframes bloom` (opacity 0→1, `translateY(18px)`→0),
  `620ms cubic-bezier(.2,.8,.2,1)` on the copy, `760ms` with `90ms` delay on the phone
- Hero phone: see **Phone mockups** below

### 3. Features grid
- Eyebrow "Features" `590 12.5px`, `letter-spacing:.1em`, uppercase, `#cf0a4f`
- H2 `700 clamp(32px,4.2vw,50px)/1.05`, `letter-spacing:-.032em`, `max-width:720px`
- Sub `400 clamp(15px,1.5vw,18px)/1.55`, `rgba(42,20,32,.55)`, `max-width:560px`
- Grid: `repeat(auto-fit,minmax(300px,1fr))`, `gap:16px`, `margin-top:38px`
- **Card shell** (used by every card): `background:#fff`, `1px solid rgba(42,20,32,.06)`,
  `border-radius:28px`, `padding:30px`, `box-shadow:0 30px 60px -50px rgba(60,15,35,.7)`
- Card title `700 22px/1.15`, `letter-spacing:-.024em` (24px / `-.026em` on the two wide cards).
  Card body `400 15px/1.55` (15.5px on wide cards), `rgba(42,20,32,.55)`, `text-wrap:pretty`
- **No icon tiles.** An earlier pass had a 44×44 tinted rounded square with a stroke icon on
  every card; it was removed deliberately because nine identical tiles read as template filler.
  Each card's own mini-visual does the work instead. Do not reintroduce them.
- Two cards span the full row width (`grid-column:1/-1`) and lay out as flex/wrap with
  `gap:26px`, each half `flex:1 1 280px` (health log: `1 1 300px`):
  - **AI Receipt Scanning** — copy + two side-by-side panels: a cream receipt facsimile
    (Equine Supply Co. / 8 Mar 2026 / Horseshoes × 4 €32.00 / Hoof oil €13.00 / Total €45.00)
    and a pink-tinted "AI EXTRACTED" panel (Amount €45.00, Category Farrier, Date Mar 8 2026,
    Horse Bella). Extracted panel: `linear-gradient(160deg,rgba(224,22,95,.09),rgba(224,22,95,.03))`,
    border `1px solid rgba(224,22,95,.16)`, `border-radius:16px`
  - **Health Log & Reminders** — copy + a mock push notification, plus four status rows with a
    3px left border and `border-radius:6px 14px 14px 6px`: Deworming (overdue, `#c8104c`),
    Farrier visit (due soon, `#d98200`, badge ink `#a36200`), Vaccination and Dental checkup
    (on track, `#17a05f`, badge ink `#0f7345`). Badges `590 11px`, `border-radius:999px`, `padding:6px 10px`
- Single-width cards:
  - **Multi-Horse Support** — three rows, 30px circular avatar with initial on a per-horse
    gradient (Bella `#8f72ff→#5a3ed0` €384, Shadow `#37b4c4→#0a7f8e` €255, Misty `#f0407a→#cf0a4f` €149)
  - **Smart Expense Overviews** — "€700 this month", a 10px segmented stacked bar
    (flex weights 280/175/140/105 in `#d98200` / `#0e8fa0` / `#17a05f` / `#8a8f9c`), then a
    2-column legend with dot, label and amount
  - **Budget Planning** — four labelled progress bars (Feed 68% `#d98200`, Farrier 92% `#c8104c`,
    Vet 35% `#17a05f`, Supplies 54% `#c1349a`); track `rgba(42,20,32,.07)`, 7px tall,
    `border-radius:4px`. Below: a warning row "Farrier budget nearly reached" on
    `rgba(200,16,76,.07)`, ink `#c8104c`
  - **Spending Analytics** — two stat tiles (vs last month **+12%** in `#c8104c`; Annual
    forecast **€9,840**), then a 12-column heatmap of `aspect-ratio:1` squares in
    increasing `rgba(193,52,154,α)` (.14 .26 .18 .40 .55 .30 .22 .34 .72 .46 .20 .12),
    with month initials **in a matching 12-column grid underneath** so each letter sits
    under its own square (they were a single letter-spaced string before; that was wrong)
  - **Income Too, Not Just Costs** — two green income rows (+€240 box rented out,
    +€150 prize money) and a "Net this month €310" total row. This card is behind a content flag
  - **Synced Across Devices** — three device tiles (iPhone / iPad / Web, "Synced now") and a
    green "Always up to date" pill
  - **Private by Design** — the one dark card: `background:#2a1420`, no border, white title,
    body `rgba(255,255,255,.62)`, shield icon in `#ff8fb4`, three white-on-`rgba(255,255,255,.1)` pills

### 4. See it in action
- Full-bleed `background:#2a1420`, `overflow:hidden`, `margin-top:88px`, inner `padding:80px 22px`
- Two glow blobs: top-left 660×560 `rgba(224,22,95,.3)`; bottom-right 700×600 `rgba(14,143,160,.26)`
- Eyebrow "The app" in `#ff8fb4`; H2 "See it in action" white; sub `rgba(255,255,255,.6)`.
  Heading and sub sit in a wrapping flex row, both `flex:1 1 300px`, `align-items:flex-end`
- Three feature pills on `rgba(255,255,255,.08)` with a `#7ce0aa` check, label `500 13.5px` `rgba(255,255,255,.82)`
- Phone row: `repeat(auto-fit,minmax(230px,1fr))`, `gap:22px`, `align-items:start`.
  The centre phone is raised with `transform:translateY(-18px)`

### 5. AI-powered
- Flex, `flex-wrap:wrap`, `gap:36px 52px`, both columns `flex:1 1 340px`, `padding:88px 22px 0`
- Left: eyebrow + the H1 headline repeated (same two-tone treatment) + sub
- Right: five rows on white cards, `border-radius:18px`, `padding:16px 18px`, `gap:9px`;
  each has a 28px `rgba(224,22,95,.1)` circle with a `#cf0a4f` check and a `590 15.5px` label

### 6. Download panel
- `border-radius:36px`, `background:linear-gradient(150deg,#f0407a,#cf0a4f)`,
  `padding:clamp(44px,6vw,76px) clamp(26px,5vw,64px)`, centred text,
  `box-shadow:0 50px 90px -50px rgba(224,22,95,.9)`, plus a white radial glow top-right
- Eyebrow `rgba(255,255,255,.72)`; H2 `700 clamp(32px,4.4vw,52px)/1.05` white;
  body **full-opacity white** (do not use alpha here — contrast)
- Store badges: real SVG badges, `height:54px`, `width:auto`, in a centred wrapping flex row with `gap:12px`

### 7. Footer
- `padding:56px 22px 48px`; wrapping flex row: logo + wordmark on the left,
  link grid `repeat(auto-fit,minmax(150px,max-content))` `gap:8px 34px` on the right
- Links `400 13.5px/1.6` `rgba(42,20,32,.55)`, hover `#e0165f`. All eight legal pages
  (privacy + terms × EN/DE/FR/SE) and a `mailto:` contact
- `1px` `rgba(42,20,32,.07)` rule, then "© 2026 Equinomy. All rights reserved." at
  `400 13px` `rgba(42,20,32,.42)`

## Phone mockups
Four mockups, all drawn in HTML/CSS — no screenshots. They depict the redesigned app, so
they must stay in sync with it; if the app ships different screens, re-shoot these from the
real app rather than editing the drawings.

- **Bezel**: `border-radius:44px` (38px for the small trio), `background:#1a0c14` / `#120810`,
  `padding:9px` / `8px`, screen `border-radius:36px` / `31px`, `overflow:hidden`
- **Shadow (hero)**: `0 44px 90px -40px rgba(60,15,35,.55), 0 8px 24px -12px rgba(60,15,35,.3)`
- **Aspect**: hero `aspect-ratio:314/650` (max-width 314px); trio `aspect-ratio:280/580`
- Every screen has a status row ("9:41" + a small battery rectangle) and, except the scan
  screen, a floating glass tab bar: `rgba(255,255,255,.85)`, `blur(18px)`,
  `1px solid rgba(42,20,32,.06)`, `border-radius:20-22px`, four icons with the active one in `#e0165f`
- **Hero screen** — period pill "SEPTEMBER 2026", hero figure "700 €" at `700 46px`
  `letter-spacing:-.034em`, caption, a 6-bar chart with **APR–SEP labels underneath**
  (current month bar in the amber gradient `#e8a13a→#d98200`, others `rgba(42,20,32,.09)`),
  a 3-row entry card, tab bar, and a 46px pink gradient FAB
- **Expenses screen** — title, search field, filter chips (All active, dark pill), a five-row
  entry card with **real category glyphs** in tinted 28px squares, and the tab bar with the
  log tab active
- **Home / donut screen** — `conic-gradient(#d98200 0 40%,#0e8fa0 40% 65%,#17a05f 65% 85%,#8a8f9c 85% 100%)`
  ring 150px with a 19px inset hole showing "€700 / 4 categories", plus a legend card
- **Scan screen** — dark screen `#1a0f16`; column flex so the receipt (`flex:1`) fills the
  space, corner brackets in `#ff5c92`, an "AI EXTRACTED" glass panel, and a pink
  "Save expense" button at the bottom

## Interactions & Behavior
Static marketing page. The only behaviour is:
- Anchor links `#features` / `#download` scroll to their sections
- Hover states on nav links, footer links, and buttons (specified above)
- The `bloom` entrance animation on the hero, once, on load
- No JS state, no forms, no fetching

## Responsive behavior
Every multi-column block uses `flex-wrap` with `flex:1 1 <basis>` rather than fixed grid
tracks, so the page collapses to a single column below roughly 620–760px depending on the
section. The features grid uses `auto-fit`/`minmax`. The nav wraps. This was fixed
deliberately after the first pass used hardcoded two-column grids that overflowed on mobile —
do not reintroduce fixed `grid-template-columns` with two tracks.

## Content Flags
`showIncome` (boolean, default **true**) — shows the "Income Too, Not Just Costs" feature card.
It exists because the income feature is new in the app; turn it off if the site should not
announce income tracking yet. Implement as a build-time flag or simply include/omit the card.

## Design Tokens

Colours
| Token | Value | Use |
| --- | --- | --- |
| Cream | `#fbf7f6` | page background, phone screens |
| Cream (warm) | `#f3ecea` | app-side background, reference only |
| Plum ink | `#2a1420` | all primary text, dark section, dark cards |
| Plum deep | `#1a0c14` / `#120810` | phone bezels |
| Pink | `#e0165f` | accent, active icons, link colour |
| Pink light / deep | `#f0407a` / `#cf0a4f` | gradient stops |
| Pink hover | `#c8104c` | link hover, over-budget, negative delta |
| Pink pale | `#ff8fb4` / `#ff5c92` | accent on dark |
| Amber | `#d98200` | Feed category |
| Teal | `#0e8fa0` | Farrier category |
| Green | `#17a05f` | Vet, income, positive |
| Green deep | `#0f7345` | green text on tint |
| Violet | `#6a4fe0` | horses |
| Magenta | `#c1349a` | Supplies, analytics |
| Grey | `#8a8f9c` / `#5f6878` | Other category, sync |
| Mint | `#7ce0aa` | checks on dark |

Ink opacities on cream: `.6` body, `.55` secondary body, `.5`/`.45` meta, `.42` muted
headline, `.35` axis labels. On plum: `.82` pill labels, `.62`/`.6` body.
Hairlines: `rgba(42,20,32,.06)` borders, `.07` rules, `.055` fills.

Radii — `999px` pills · `36px` download panel · `28px` cards · `20px` tab bar ·
`18px` list cards · `16px` inner panels · `15px` buttons · `14px` rows · `12px` chips · `9-10px` icon squares

Shadows — cards `0 30px 60px -50px rgba(60,15,35,.7)` · pink CTA `0 16px 34px -14px rgba(224,22,95,.95)` ·
download panel `0 50px 90px -50px rgba(224,22,95,.9)` · phones `0 40px 80px -40px rgba(0,0,0,.7)`

Type — system stack `-apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", system-ui, sans-serif`.
Weights 400 / 500 / 590 / 700 (590 is the SF semibold-ish weight; map to 600 if the stack
doesn't support it). Display sizes use `clamp()`; tracking tightens as size grows
(`-.038em` at H1 down to `-.012em` at 14.5px). `text-wrap:balance` on headings,
`pretty` on paragraphs. `font-variant-numeric:tabular-nums` on every currency figure.

## Assets
- `https://equinomyapp.com/assets/logo-icon.png` — nav and footer logo, referenced from the
  live site. Use the local asset in the repo instead of hotlinking
- `https://equinomyapp.com/assets/badge-appstore.svg`, `badge-googleplay.svg` — official
  store badges, also from the live site
- Every other graphic is inline SVG or CSS. No raster imagery, no icon font, no webfont
- **There is no photography on the page.** This is the biggest open gap: a real photo band
  above the download panel and a portrait beside the hero would both help. Nothing is stubbed
  in for them, so adding them is a design change, not a fill-in

## Files
- `Equinomy Site.dc.html` — the site design (this handoff's subject)
- `Horse Economy App v8.dc.html` — the app design the mockups depict, for cross-checking
  screens and colour use
- `support.js` — runtime needed to open either HTML file in a browser. Not part of the
  deliverable

## Known gaps
1. No photography (above)
2. Store badge links are `href="#"` — wire to the real store listings
3. Copy is English only; the live site has DE/FR/SE legal pages, so localised marketing copy
   may be wanted. Ask before writing it — the existing English copy is the client's own
4. The app mockups are drawings of an unshipped app; verify against the built app before launch
