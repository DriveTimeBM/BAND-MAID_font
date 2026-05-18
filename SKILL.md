---
name: band-maid-design
description: Use this skill to generate well-branded interfaces and assets for BAND-MAID Unofficial (a fan dashboard for the Japanese rock band BAND-MAID), either for production or throwaway prototypes / mocks. Contains essential design guidelines, colors, type, fonts, assets, and a UI kit recreating the live app shell.
user-invocable: true
---

# BAND-MAID Unofficial — Design Skill

Read **`README.md`** in this skill folder first — it has the full brand
context, content rules, visual foundations, and an index of every other
file. Then orient yourself with these:

- `colors_and_type.css` — every token (`--bm-*`) plus drop-in semantic
  classes (`.bm-eyebrow`, `.bm-group-label`, `.bm-h1`, `.bm-app-name`,
  `.bm-body`, `.bm-stat-num`, `.bm-pill` …).
- `preview/*.html` — small cards demonstrating each token group and
  component recipe in isolation. Useful as copy-paste references.
- `ui_kits/unofficial-app/` — a click-thru React recreation of the live
  app shell. `app.css` there is a complete style sheet for the chrome,
  song list, detail panel, deck-grid, and countdown patterns.
- `assets/` — the band's saw-blade logo (PNG only — no SVG / webfont),
  the social-preview image, and screenshots of real views.

## How to use this skill

If creating **visual artifacts** (slides, mocks, throwaway prototypes,
landing pages, etc.):
1. Copy the assets you need out of this folder into your output (logo,
   screenshots).
2. Import `colors_and_type.css` (or inline the tokens) so the system
   variables are available.
3. Build with the recipes in `preview/` and `ui_kits/unofficial-app/`.
   Most surfaces are: dark `--bm-bg2` chrome + 1px `--bm-border` hairlines
   + `--bm-accent` (champagne gold) for active state + a single emoji
   per nav slot.
4. Keep density high (4–14px spacing) and radii small (4–8px). No drop
   shadows on surfaces; depth comes from the bg ladder.
5. Use **system fonts** — there's no webfont in the source. For poster
   display type only, fall back to `Metal Mania` / `UnifrakturCook` from
   Google Fonts and flag the substitution.
6. Always include the disclaimer *"Unofficial fan project. Not affiliated
   with BAND-MAID, MAIDIT, or Pony Canyon."* on anything that could read
   as official.

If working on **production code**: cite this folder's CSS tokens as your
source of truth, and lift component patterns directly from
`ui_kits/unofficial-app/`. The source repo is
<https://github.com/DriveTimeBM/BAND-MAID_unofficial> — that's the
canonical implementation if you need to verify a behaviour this skill
summarises.

## If invoked with no other guidance

Ask the user what they want to build (a new view? a poster? a landing
page? a deck announcing a tour date?), confirm the audience (fellow
fans vs. casual visitor), and confirm whether they want it as throwaway
HTML or as production code aimed back at the fan-app repo. Then act as
an expert designer and ship.

## Things to avoid

- Hand-drawn SVG icons. The product is emoji-driven; if you need a
  non-emoji icon use Lucide via CDN (lucide-static@latest) so the stroke
  vocabulary matches.
- Gradients, drop shadows, blur, backdrop-filter — none of these
  appear in the source. Solid colors and 1px hairlines do the work.
- Recolouring the logo. Always rendered on dark, never tinted.
- Translating fan vocabulary. "okyu-ji", "OMEISYUSAMA-NO-KAI",
  "Kobato lead", "BAND-MAID Prime" are proper nouns.
- Loud headers / 40px+ type in dense data views. The biggest type in the
  product is 28px on a welcome screen.
