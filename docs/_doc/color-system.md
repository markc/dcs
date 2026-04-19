# Color System

DCS uses **OKLCH** — a perceptually uniform color space — for all color definitions.

## Why OKLCH?

Traditional color spaces (HSL, RGB) produce uneven perceived brightness across hues. A "50% lightness" blue looks much darker than a "50% lightness" yellow.

OKLCH fixes this with three independent axes:

| Axis | Range | Controls |
|------|-------|----------|
| **L** (Lightness) | 0–100% | Perceived brightness |
| **C** (Chroma) | 0–0.4 | Color intensity/saturation |
| **H** (Hue) | 0–360 | Color wheel position |

```css
color: oklch(55% 0.12 220);  /* L=55%, C=0.12, H=220 (blue) */
```

## The 6 Schemes

Each scheme changes **only the hue**. Lightness and chroma ratios stay consistent. Mono is the exception: it sets chroma to 0 so hue is irrelevant, producing pure grayscale.

| Scheme | Hue | Character |
|--------|-----|-----------|
| **Ocean** | 220 | Cyan-blue, professional (default) |
| **Crimson** | 25 | Bold red, high energy |
| **Stone** | 60 | Warm neutral, minimal |
| **Forest** | 150 | Natural green, calming |
| **Sunset** | 45 | Warm orange-amber |
| **Mono** | — | Pure grayscale (C=0); status colors retained for usability |

## Light and Dark Modes

Each scheme defines both light and dark variants. The toggle works by swapping a class on `<html>`:

- `html.light` — Light mode colors
- `html.dark` — Dark mode colors
- No class — follows `@media (prefers-color-scheme: dark)`

## CSS Variable Contract

`site.css` **must** define these variables for `base.css` to work:

```css
/* Backgrounds */
--bg-primary        /* Main background */
--bg-secondary      /* Cards, sidebars */
--bg-tertiary       /* Hover states */

/* Foregrounds */
--fg-primary        /* Main text */
--fg-secondary      /* Secondary text */
--fg-muted          /* Placeholder, disabled */

/* Accent */
--accent            /* Primary brand color */
--accent-hover      /* Accent on hover */
--accent-fg         /* Text on accent background */
--accent-subtle     /* Light accent tint */

/* Borders */
--border            /* Default borders */
--border-muted      /* Subtle borders */

/* Status */
--success           /* Green */
--danger            /* Red */
--warning           /* Yellow/amber */

/* Glass morphism */
--glass             /* Semi-transparent background */
--glass-border      /* Glass panel border */
```

## Creating a New Scheme

1. Pick a hue (0–360)
2. Copy an existing scheme block in `site.css`
3. Replace the hue value throughout
4. Add the scheme name to `Base.setScheme()` cleanup list
5. Add a selector button to the Appearance panel
6. Add the scheme name to `Base.setScheme()`'s cleanup list in `base.js`

Example — a purple scheme (H=290):

```css
.scheme-purple { --accent: oklch(55% 0.15 290); }
.scheme-purple.light { --bg-primary: oklch(98% 0.01 290); }
.scheme-purple.dark { --bg-primary: oklch(15% 0.02 290); }
```
