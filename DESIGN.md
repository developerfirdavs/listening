# Listening Coursebook Design System

## 1. Atmosphere & Identity

A warm "study-paper" coursebook. The page feels like a well-bound practice
book: a tactile cream canvas, deep slate ink, one confident indigo accent
used only where the user acts. The signature is the serif display type for
practice numbers and the page title — reading like printed text against a
clean digital quiz surface, not a SaaS dashboard. Correct/incorrect answers
read instantly through green/red across the cream paper.

## 2. Color

### Palette (light theme)

| Role | Token | Value | Usage |
|------|-------|-------|-------|
| Canvas | --paper | #F5EFE3 | Page background |
| Surface | --card | #FCFAF5 | Cards |
| Surface raised | --card-strong | #FFFFFF | Option pills |
| Ink | --ink | #212A35 | Headlines, body |
| Ink muted | --ink-2 | #66727F | Instructions, meta |
| Ink faint | --ink-3 | #98A3AE | Disabled numbers |
| Border | --line | #E4DCCB | Card edges, dividers |
| Border strong | --line-2 | #D6CDB8 | Focused/active edges |
| Accent | --indigo | #4F5BE8 | Actions, live progress |
| Accent hover | --indigo-2 | #3B46CC | Hover state |
| Accent tint | --indigo-soft | #EDEFFC | Chips, pressed option |
| Success | --green | #1E9E5A | Correct answer |
| Success tint | --green-soft | #E4F5EB | Correct fill |
| Error | --red | #D63B47 | Wrong answer |
| Error tint | --red-soft | #FBE9EA | Wrong fill |
| Warn | --amber | #C07A1B | Unanswered (check) |
| Warn tint | --amber-soft | #FBF0DC | Unanswered fill |

### Rules
- Accent is interactive-only. Correctness uses green/red, never accent.
- Dark mode intentionally out of scope (single-file, QA-light) — accepted debt.

## 3. Typography

- Display: `Fraunces`, Georgia, serif — page title, practice numbers.
- Body/UI: `Manrope`, system-ui, sans-serif — everything else.
- Loaded from Google Fonts with system fallbacks (works offline).
- Base 16px (prevents iOS input zoom). Body never below 14px.

| Level | Size | Weight | Usage |
|-------|------|--------|-------|
| Display | clamp(34px, 8vw, 56px) | 600 | Hero title |
| H2 (practice) | 20px | 700 | Card titles in Manrope |
| Q number | 15px | 600 | Serif Fraunces badge |
| Body | 16px | 400 | Options, text |
| Small | 14px | 500 | Instructions, meta |
| Caption | 12px | 600 | Stats labels, uppercase |

## 4. Spacing & Layout

- Base unit 4px. Mobile padding 20px, desktop gap 24.
- Max content 900px, single column cards; questions 2-up above 1100px.
- Breakpoint: tablet/desktop ≥ 768px.
- Touch targets ≥ 48px. `min-height: 100dvh` on hero. Safe-area insets for the fixed bottom bar.

## 5. Components

### Hero
- Warm canvas + soft indigo aurora (radial gradient, GPU-composited), headphones SVG in a tonal rounded tile. Stats row (answered / total / score).

### Progress track
- Fixed 4px top bar, indigo fill = % answered. Animated via `transform` only.

### Practice card
- Cream card, hairline border, rounded 20px. Header = serif practice number (P1…P5) chip + title + instruction.

### Question block / Option pill
- Structure: number badge (serif) + mark, then 3 option rows.
- Option = full-width label: letter badge (A/B/C) in a 30px rounded square + text. States: default (white, hairline), hover (indigo border + soft tint), checked (indigo border + indigo-soft), focus-visible (2px indigo ring, offset), correct (green), wrong (red), unanswered-reveal (amber outline shows correct in green).
- Motion: 150ms background/border on state change only.

### Action bar
- Fixed bottom bar (mobile) / floating top toolbar (desktop): result readout (live, aria-live) + Tekshirish (primary solid) / Javoblar (ghost) / Tozalash (ghost). 44px+ buttons, safe-area padding.

## 6. Motion & Interaction

| Type | Duration | Easing | Usage |
|------|----------|--------|-------|
| Micro | 150ms | ease-out | Option hover/press, mark pop |
| Standard | 250ms | ease-in-out | Progress fill, bar slide-in |

- Only `transform` + `opacity` + colors animated. Respect `prefers-reduced-motion`.

## 7. Depth & Surface

Borders-only strategy: hairline `--line` edges + a whisper shadow
`0 1px 0 rgba(33,42,53,.04)` on cards. No heavy shadows — paper, not plastic.

## 8. Accessibility Constraints & Accepted Debt

- Contrast: ink on paper ≥ 7:1 (AA); green/red + icon tick/cross so color isn't the only signal; visible `:focus-visible` ring; full keyboard reachability; `role="status"` on result; `prefers-reduced-motion`.
- Accepted debt: no dark theme (single-file, unused on this canvas); Google Fonts external dependency (graceful system-fallback); no image/audio (static quiz, no assets).

## Files
- `index.html` — the app (all CSS/JS inline, zero build).
- `Coursebook - LP1-1-5.html` — original source, unchanged.