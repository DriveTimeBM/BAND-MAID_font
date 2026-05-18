# BAND-MAID Unofficial — Design System

A reference design system distilled from **BAND-MAID Unofficial**, a fan-built
data web app for the Japanese rock band BAND-MAID. The app is a single dark
"fan dashboard" that aggregates ~40 different views — songs, releases, okyu-ji
setlists, YouTube projections, milestones, Instagram/Twitter archives,
streaming counts, anniversaries, etc. — all powered by static JSON files that
update daily.

> **Unofficial fan project.** Not affiliated with BAND-MAID, MAIDIT, or Pony
> Canyon. This design system exists to help fans build well-branded tools,
> mocks, and prototypes that look and feel like the existing app.

## Source material

This system was built by reading the canonical fan-app codebase.

- **GitHub repo:** <https://github.com/DriveTimeBM/BAND-MAID_unofficial>
  - `index.html` — the iframe-shell app: header, side-nav (desktop) + bottom
    nav (mobile), URL bar, sliding drawer
  - `views/*.html` — ~40 self-contained view pages, each its own dense data UI
  - `views.json` — nav config; every view's icon is an emoji
  - `views/songs.html` / `views/about.html` — the two views that establish
    most of the heavier components (detail panel, deck grid, group sections)
- **Live app:** <https://drivetimebm.github.io/BAND-MAID_unofficial/>
- **Discord:** <https://discord.gg/tfpJ6xBWEN>
- **Public data sheet:** <https://docs.google.com/spreadsheets/d/1fUGjjPOjFFWoh8TbHOfgB4L6N0GmZIfo2JrPghNZsZU/edit>
- **User-supplied logo** — `assets/bm-circular-saw.png`, the band's own
  cracked-blackletter / circular-saw mark.

Explore the repo above to ground any design work in the actual product code —
this system summarises it but the source is the canonical truth.

---

## What's in this folder

| Path | Purpose |
|------|---------|
| `README.md` | This file — brand context, content + visual rules, index |
| `colors_and_type.css` | All tokens (`--bm-*`) + semantic type classes |
| `SKILL.md` | Cross-compatible skill manifest |
| `assets/logo.png` | The 512×512 logo used in the actual app (saw blade) |
| `assets/bm-circular-saw.png` | High-res user-uploaded version of the band's logo |
| `assets/social-preview.png` | Social preview image from the repo |
| `assets/screens/*.png` | Reference screenshots of real app views |
| `preview/*.html` | Design-system "cards" — one per token group / component |
| `ui_kits/unofficial-app/` | Click-thru recreation of the iframe-shell app |
| `ui_kits/unofficial-app/*.jsx` | Modular JSX components (header, nav, song row, detail panel, etc.) |

---

## CONTENT FUNDAMENTALS

The voice is **fan-to-fan reference**, not marketing. Tone is matter-of-fact,
data-first, lightly enthusiastic. Pull lines from the source README and view
headers like:

> "Upcoming BAND-MAID happenings. Updated as needed."
> "All BAND-MAID songs with member quotes where available. Spotify stream counts updated weekly."
> "Unofficial fan project. Not affiliated with BAND-MAID, MAIDIT, or Pony Canyon."

### Rules of thumb

- **Casing.** Sentence case for UI strings. **ALL CAPS** + wide letter-spacing
  is reserved for group labels, eyebrows, and the band name. The band itself
  is always rendered **BAND-MAID** (all caps, hyphen, no space). Member names
  use proper case: Saiki, Miku, Kanami, Akane, MISA. The fan club is
  **OMEISYUSAMA-NO-KAI** (all caps). Live show is **okyu-ji** (lower).
- **Person.** Third-person, neutral. The app does not address the user as
  "you" except in the feedback form and quiz. No "we" — the project credits
  itself as "DriveTime" but writes about the band, not itself.
- **Tone.** Reference book + sports-stats vibe. Confident counts ("400+
  GIFs"), dates always explicit, sources always cited inline. Never breathy
  or hyperbolic — the data does the talking.
- **Numbers.** Always formatted with thousands separators. Streaming counts
  shown with the platform's color (Spotify green, YouTube red is implied by
  context). "Streams" not "plays".
- **Time.** ISO-style relative phrases for cadence — "Updated daily",
  "Updated every 10 minutes", "Updated weekly". Calendar dates use
  `toLocaleDateString` long form ("September 11, 2025").
- **Emoji are first-class.** Every view has an emoji icon. They're a core
  navigation element, not decoration — see ICONOGRAPHY below.
- **Honor the fan vocabulary.** "Okyu-ji", "Maiko-version", "Kobato lead",
  "BAND-MAID Prime", "OMEISYUSAMA-NO-KAI" — these are proper nouns. Don't
  translate or simplify them.
- **Always disclaim.** Any deliverable that reads like it could be official
  should carry the *Unofficial fan project. Not affiliated with…* line.

### Example copy patterns

- View descriptors: `"<plural noun>. Updated <cadence>."` — keep it under 12
  words. e.g. *"Anniversaries for song releases, birthdays, live debuts,
  okyuji, and YouTube videos. Updated daily."*
- Empty states: lowercase one-liners — "No songs match your search.", "No
  records found".
- Error states: `⚠️` emoji + brief reason. e.g. "⚠️ Could not load songs ·
  HTTP 503".
- Stat pills: `"<n> songs · <total> Spotify streams"` — middot-separated.
- Section labels: `Songs *improved*` — asterisks for in-progress markers,
  used sparingly in the live nav.

---

## VISUAL FOUNDATIONS

The visual identity is a deliberate tension: the band's actual logo is
**cracked-blackletter on a circular-saw blade** — heavy metal, gothic,
hand-drawn — but the app wrapping that brand is a **clean, dense,
near-monochrome data dashboard** with one champagne-gold accent. The
juxtaposition is the brand: maids serving you data on a saw blade.

### Colors

- **Background ladder.** Five near-black surfaces stacked by contrast, not
  shadow. `#0a0a0a` (page) → `#141414` (chrome) → `#1c1c1c` (cards / hover)
  → `#242424` (raised / pressed) → `#000` (rare, behind iframes). All
  layering is achieved through this ladder; surfaces don't cast shadows.
- **Borders are hairlines.** Always 1px, always `#2a2a2a` (default) or
  `#3a3a3a` (hover/focus). Borders do almost all the visual separation work.
- **Text scale.** `#f0f0f0` → `#999` → `#555`. Some data-heavy views shift to
  a cooler muted scale (`#b8c8d8` / `#7a8a9a`) for variety on long lists.
- **Accent.** A single **champagne gold** `#c8a96e`. Used for: logo border,
  active nav item, active row left-stripe, group labels, link hover, the
  "play" button on the detail panel. Tinted forms (`rgba(200,169,110,0.12)`
  for backgrounds, `0.3` for borders) are used for active states and the
  accent flags on the song detail panel.
- **Secondary hues are semantic.** Spotify green `#1db954` ONLY for Spotify
  streams. Red `#ef4444` for MV badges, errors, danger. Violet `#8b5cf6` for
  Live badges. Pink `#ec4899` for the "Kobato lead" badge. These are never
  used decoratively — each carries meaning.
- **Imagery.** Photographs (album art, daily photos, news thumbs) are loaded
  un-tinted at their native color. Cards use `object-fit: cover` and a 1px
  hairline border. There is no grain, vignette, or saturation treatment.

### Type

- **System stack.** `'Segoe UI', system-ui, -apple-system, …` — no
  webfonts. Mono is `Consolas, Monaco, …` and shows up in URL bars and
  copy-link affordances. This is intentional: a fan tool that loads fast,
  uses zero kilobytes of font.
- **Scale (base 14px).** 9, 10, 11, 12, 13, 14, 15, 18, 22, 28 — and that's
  it. Everything below 12px is uppercase + tracked.
- **Tracking.** Eyebrows / group labels are uppercase with `0.10–0.14em`
  letter-spacing. The app name uses a gentler `0.04em`. Body text is at
  default tracking.
- **Numeric.** `font-variant-numeric: tabular-nums` on every stat. Numbers
  in the detail panel and inside pills are tabular and accent-coloured.
- **Display type.** The band's logo is its own display face — cracked
  blackletter, hand-drawn. We do not have a webfont equivalent. **Substitute
  flag:** for any poster / display moment, fall back to `Metal Mania` or
  `UnifrakturCook` from Google Fonts (closest free analogues) and treat
  output as "in the spirit of" — never as the official lockup. The
  saw-blade logo PNG should carry the brand instead of recreated type.

### Spacing & density

- 4px base unit. The app uses the full ladder 4 → 24 but lives mostly at
  6–14px. This is a deliberately **dense** product: 8px between most card
  fields, 6px gutter on toolbars, 1px borders.
- Toolbars / nav rows are ~48px tall. Detail panel sections are stacked with
  14–16px gaps and 1px hairline dividers — not larger gaps.

### Shape

- **Radii are small.** 4px (badges, chips) / 6px (logo tile, search) / 8px
  (default — buttons, cards) / 10px (Spotify embed) / 20px (pill counts).
  Nothing ever fully rounds except the "pill" tag.
- **No big rounded cards.** Cards are flat rectangles separated by 1px
  borders. The "deck grid" pattern uses borders as gutters
  (`gap: 1px; background: var(--border);`).

### Layout

- **Fixed chrome.** Header (52px) is fixed top. Toolbar (48px) sits under it
  fixed. Mobile bottom-nav (96px) is fixed bottom with safe-area padding.
  Desktop side-nav (220px) is fixed left.
- **Group + list.** Most views are vertical lists chunked by sticky group
  headers (`position: sticky; top: 0`). Each header carries a chevron
  (toggles collapsed), a label, and a count pill.
- **Detail panel.** Drawer sliding in from the right at 440px wide;
  full-screen on mobile (`<700px`). Closes on Escape.

### Effects

- **No drop shadows on surfaces.** All depth is via the bg ladder. The
  drawer overlay is the only place a shadow is even hinted at (and it's a
  dim modal scrim, not a card shadow).
- **No gradients.** Anywhere. Solids only.
- **Transparency.** Used purposefully for accent / semantic tints
  (`rgba(<accent>, 0.10–0.30)`) and for the drawer overlay
  (`rgba(0,0,0,0.6)`). Never blurred — no `backdrop-filter` in the source.
- **Borders accent state.** Focus / active = swap `--bm-border` to
  `--bm-accent`. There's no glow, no outline-offset ring.
- **Hover.** Background lifts one bg-ladder step (`bg2` → `bg3`). Text
  goes from muted to full white. Borders go to `--bm-border-2` or
  `--bm-accent` on action elements.
- **Press / active.** No `transform: scale()`. Active nav items get the
  accent left-stripe + accent text colour + tinted background.
- **Transitions.** 0.12–0.15s on background/color/border; 0.20–0.28s on
  drawer slide (`cubic-bezier(0.4, 0, 0.2, 1)`). No bounce, no springs, no
  decorative motion.
- **Loading.** A single 28px spinner — 2px accent ring on a `--bm-border-2`
  track, spinning at 0.7s linear. Same spinner everywhere.

### Cards

A "card" here is rarely shadowed and rarely rounded. The two canonical card
recipes:

1. **List row** — `padding: 8px 16px; border-bottom: 1px solid var(--bm-border);
   cursor: pointer; transition: background 0.1s;` Hover → `bg3`. Active row
   gets a 3px accent left-border + `accent-dim` background.
2. **Deck card** — image (1:1 cover, hairline border) + body (10–12px
   padding) + optional external-link icon overlay. Grid uses 1px borders as
   gutters: `display: grid; gap: 1px; background: var(--bm-border);` and
   each card is `background: var(--bm-bg2);`.

### Animation

- Strictly **functional**. Drawer slides, panel slides, chevron rotates,
  spinner spins. That's the entire motion vocabulary.
- Easing: `cubic-bezier(0.4, 0, 0.2, 1)` (Material-style ease-in-out) is
  used on drawer slides. Everything else is the browser default linear/ease.

---

## ICONOGRAPHY

The app is **emoji-driven**. Every nav item in `views.json` ships with a
unicode emoji as its icon. Some examples directly from the live config:

| Emoji | View | Emoji | View |
|---|---|---|---|
| 🗓️ | Calendar | 📝 | Songs |
| 💿 | Releases | ▶️ | Videos |
| 🟢 | Spotify | 🎶 | Streaming |
| 🗺️ | Okyu-ji | 🎬 | Prime |
| 🏮 | Fan Club | 🖼️ | Gallery |
| 📸 | Daily Photos | ⏳ | Upcoming |
| 🎯 | Next Million | 📍 | Milestones |
| 🎉 | Anniversaries | 🎞️ | GIFs |
| ❓ | Quiz | 💵 | Shop |
| 🔟 | Top 10 | 👥 | Followers |
| 🎟️ | Tickets | 🐦 | Twitter |
| 📈 | Charts | 🔗 | Links |

A handful even combine two emoji for clarity: `📝🟢` (Songs + Spotify),
`🈯🔤` (Translations), `Top🔟`.

### Inline SVG icons (the small set)

When a single emoji can't carry an action, the app inlines a tiny set of
SVG icons. The only ones present:

- **Search** — `circle r=8 + diagonal line` (lucide-style, stroke 2,
  rendered in `--bm-text-3`)
- **Spotify wordmark** — the brand glyph, rendered in `currentColor` so it
  inherits `--bm-spotify`
- **Play** — solid triangle (`<path d="M8 5v14l11-7z"/>`)
- **External-link** — square with arrow out of corner (lucide-style,
  stroke 2.5)

**No icon font** is loaded. No Feather/Lucide/Heroicons CDN. If you need
icons outside this set when designing new surfaces, **use Lucide via CDN**
(`https://unpkg.com/lucide-static@latest/icons/<name>.svg`) — same stroke
language as the four already in-app — and **flag** the substitution.

### Brand mark

The logo (`assets/logo.png` / `assets/bm-circular-saw.png`) is a black
circular saw blade with the band name rendered twice in mirrored
cracked-blackletter and a bat-cross glyph at center. It always reads on a
dark background. **Do not recolor it.** Always rendered at 22–48px inside
the app, sometimes at 512px+ for splash / social preview. The "app-logo"
chrome tile is a 32–34px square: `background: #111; border: 1px solid
var(--bm-accent); border-radius: 6px;` containing the logo at 20–22px.

### Imagery

- **No illustrations are shipped.** No hand-drawn art, no decorative SVGs.
- **Background images?** No. Backgrounds are flat near-black.
- **Photos** come straight from official band socials (Instagram daily
  photos, OMEISYUSAMA gallery, album cover URLs from JSON). They are not
  filtered, cropped editorially, or grained — `object-fit: cover` + a
  hairline border is the entire treatment.
- For your own designs, treat photography as **warm-leaning, high contrast,
  on a black canvas** — that's what most band photos already are.

---

## Component manifest

Cards are registered into the Design System tab. Quick map of what's there:

- **Type:** `type-eyebrows`, `type-headers`, `type-body`, `type-stats`,
  `type-mono`
- **Colors:** `colors-surfaces`, `colors-text`, `colors-accent`,
  `colors-semantic`
- **Spacing:** `radii`, `spacing-scale`, `chrome-heights`, `density-example`
- **Components:** `app-logo-tile`, `buttons`, `pills-and-badges`,
  `search-input`, `list-row`, `group-header`, `deck-card`,
  `detail-stats-grid`, `quote-block`, `spinner-and-states`,
  `bottom-nav`, `side-nav`, `url-bar`
- **Brand:** `brand-logo`, `brand-screenshots`, `emoji-iconography`

---

## UI Kit index

| Kit | Path | Demonstrates |
|-----|------|--------------|
| Unofficial App | `ui_kits/unofficial-app/index.html` | The full shell — desktop side-nav + bottom-nav, URL bar, Songs view with detail panel, drawer, group sections, deck grid (About-style), Upcoming/countdown widget |

The kit is a **click-thru recreation**, not production. You can navigate
views, open the songs list, click a song row to slide in the detail panel,
toggle the drawer, switch between sample views. State is in React, data is
sample JSON, but visuals are pulled directly from the live CSS.

---

## Caveats / known substitutions

- **No display webfont shipped.** The cracked-blackletter wordmark in the
  logo is image-only. For poster/display type, use `Metal Mania` or
  `UnifrakturCook` from Google Fonts as a stand-in. Flagged in
  `colors_and_type.css`.
- **Iconography is emoji-first.** Where designs need a non-emoji icon, use
  Lucide via CDN to match the four existing inline SVGs.
- **No motion library.** Everything in the source is CSS transition; no JS
  animation framework. Stay there.
