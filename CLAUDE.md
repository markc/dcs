# CLAUDE.md

Project guidance for Claude Code when working with this repository.

## Project Overview

**DCS (Dual Carousel Sidebars)** is the canonical reference implementation of Mark's preferred web interface pattern. It is a modular CSS/JS design system featuring dual sidebars, OKLCH color schemes, dark/light modes, mobile-first responsive layout, and marketing components. Zero dependencies, no build step.

**This repo is the single source of truth.** Every project that uses DCS (plain PHP, static HTML, Laravel+React) should reference `~/.gh/dcs` as the authority. When told "use the DCS interface", read these files and reproduce the pattern.

**Showcase:** [dcs.spa](https://dcs.spa) (GitHub Pages, self-documenting SPA built with DCS)

## File Structure

```
dcs.spa/
├── docs/                   # Real files (GitHub Pages source at dcs.spa)
│   ├── index.html          # Self-documenting SPA showcase
│   ├── base.css            # Generic framework (~900 lines)
│   ├── base.js             # Generic JavaScript (~420 lines)
│   ├── site.css            # Marketing theme with OKLCH colors + components
│   ├── site.js             # Marketing JavaScript (particles, scroll reveal)
│   ├── md.js               # Markdown renderer (for documentation sites)
│   ├── _doc/               # In-page doc viewer content (architecture, color-system, components, usage-patterns)
│   ├── Server_Room_Dark.webp # Default background image
│   ├── CNAME               # dcs.spa custom domain
│   └── .nojekyll           # Let Pages serve _doc/ without Jekyll rewrite
├── base.css                 → symlink → docs/base.css
├── base.js                  → symlink → docs/base.js
├── site.css                 → symlink → docs/site.css
├── site.js                  → symlink → docs/site.js
├── md.js                    → symlink → docs/md.js
├── Server_Room_Dark.webp    → symlink → docs/Server_Room_Dark.webp
├── ai.txt                   → symlink → docs/ai.txt
├── CLAUDE.md               # This file
└── README.md               # Project documentation
```

Real files live in `docs/` (deployed to GitHub Pages). Root symlinks provide convenient access for development and for other projects to reference.

## Architecture

### Two-Layer System

| Layer | Files | Purpose | Modify? |
|-------|-------|---------|---------|
| **Base** | `base.css`, `base.js` | Generic framework, color-agnostic | Never |
| **Site** | `site.css`, `site.js` | Theme colors, marketing components | Per project |

### base.css (Generic Framework)

CSS cascade layers: `@layer reset, tokens, base, components, utilities, animations`

- **Tokens:** Typography (6 sizes), spacing (0-8), radius, shadows, transitions, z-index, `--sidebar-width-left`/`--sidebar-width-right` (user-adjustable, 25–75%)
- **Reset:** Box-sizing, reduced motion, contrast preferences
- **Base:** Headings, links, code blocks, tables, blockquotes
- **Components:** Container, cards, buttons, forms, dropdowns, toast, topnav (flow element), sidebars, panel carousel (slide/fade), tree widget, prose
- **Utilities:** Display, flex, grid, spacing, text, glass morphism
- **Animations:** Toast-in, fade-in, hover-lift

Key design decisions:
- Color-agnostic: defines NO colors (all from site.css CSS vars)
- Mobile-first: base styles are single column, enhanced at 768px and 1280px
- Cards: no radius/border on mobile, full styling on desktop
- Hamburger buttons are 48×48 for mobile tap targets and remain visible when sidebars are pinned

### base.js (Generic JavaScript)

Single `Base` object with localStorage state management. Public API:
- `state(updates)` — read/write persistent JSON state
- `toggleTheme()` — dark/light via `.dark`/`.light` class on `<html>`
- `setScheme(name)` — apply `.scheme-{name}` class
- `toggleSidebar(side)` / `pinSidebar(side)` — open/close (pin at 1280px+)
- `setPanel(side, index)` — navigate sidebar panel carousel
- `toast(msg, type, ms)` — notifications
- `restore()` — rehydrate UI on load, remove `preload` class

All clicks use a single delegated listener; Lucide icons render after restore.

### site.css (Theme Layer)

CSS cascade layers: `@layer site-tokens, site-components, site-utilities`

- **Tokens:** Extended spacing (10-24), typography (3xl-6xl), OKLCH color definitions
- **Components:** Hero, sections, service cards, pricing tables, CTAs, particles, footer
- **Utilities:** Marketing-specific spacing, container variants

### Color System (OKLCH)

All colors use `oklch(lightness% chroma hue)`:
- Only the **hue** changes between schemes
- Lightness/chroma ratios stay consistent
- Each scheme has light + dark definitions
- Toggle override via `html.dark` / `html.light` classes
- System preference via `@media (prefers-color-scheme: dark)`

6 schemes: Ocean (H=220, default), Crimson (H=25), Stone (H=60), Forest (H=150), Sunset (H=45), Mono (C=0, pure grayscale with colored status)

### site.js (Optional Marketing)

Particle effects, scroll reveal animations, dynamic footer year.

### md.js (Optional Documentation)

Lightweight markdown-to-HTML renderer for documentation sites. Exposes `md()` (string → HTML) and `loadDoc()` (fetch + render `.md`). Add `data-md-auto` to a container to opt in to automatic loading. Supports headings, lists, code blocks, tables, links, images, emphasis.

### Sidebar Panel Carousel

Each sidebar holds a horizontal carousel of panels (e.g. Navigation, Appearance, Tree/Docs). Two modes:
- **Slide** — panels translate horizontally (default)
- **Fade** — panels cross-fade via opacity + grid stacking

Mode switching suppresses transitions briefly to avoid flicker. Navigate via chevrons, dots, or `Base.setPanel(side, index)`.

### Appearance Panel

Built-in right-sidebar panel exposing theme toggle, carousel mode toggle, sidebar width slider, and color-scheme dots. State persists via `base-state` in localStorage.

### Tree Widget

Hierarchical navigation component (`.tree` → `.tree-branch`/`.tree-toggle`/`.tree-item`). Depth via `--tree-depth` CSS var; collapse animates `grid-template-rows`. Used by the left-sidebar doc viewer that renders files from `docs/_doc/`.

## Usage Patterns

### 1. Marketing/Brochure Site
```html
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="site.css">
<script src="base.js"></script>
<script src="site.js"></script>
```

### 2. Documentation Site
```html
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="site.css">
<script src="base.js"></script>
<script src="md.js"></script>
```
Same two stylesheets as a marketing site — if your HTML never uses the hero / service-card / pricing / CTA components, those rules never render. Pick a scheme via `Base.setScheme('stone')` (or similar) on init.

### 3. Laravel + React (Inertia)
Import OKLCH color tokens into Tailwind v4 `@theme` block. Use React context for theme state instead of base.js.

## Key Patterns

### FOUC Prevention
```html
<script>(function(){var s=JSON.parse(localStorage.getItem('base-state')||'{}'),
t=s.theme,c=s.scheme,h=document.documentElement;h.className='preload '+
(t||(matchMedia('(prefers-color-scheme:dark)').matches?'dark':'light'))+
(c&&c!=='default'?' scheme-'+c:'');})()</script>
```

### HTML Structure
```
body
├── div.particles#particles
├── nav.topnav (fixed, glassmorphism)
├── aside.sidebar.sidebar-left (off-canvas)
├── aside.sidebar.sidebar-right (off-canvas)
├── main#content
│   ├── section.hero.hero-bg (100vh)
│   ├── section.content-section (solid bg, cards)
│   ├── section.bg-image-section (banner/divider)
│   └── footer.footer-main
├── script base.js
└── script site.js
```

### Relative Path Strategy

Root pages use `href="base.css"`, subpages use `href="../base.css"`. This allows serving from any directory depth.

## CSS Variable Contract

site.css MUST define these variables for base.css to work:

```
--bg-primary, --bg-secondary, --bg-tertiary
--fg-primary, --fg-secondary, --fg-muted
--accent, --accent-hover, --accent-fg, --accent-subtle
--border, --border-muted
--success, --danger, --warning
--glass, --glass-border
```

## Production Sites Using DCS

- [dcs.spa](https://dcs.spa) — Canonical self-documenting showcase (Ocean scheme)
- [motd.com](https://motd.com) — AI via email (Crimson scheme)
- [renta.net](https://renta.net) — Managed Linux hosting (Crimson scheme)
- [SPE Docs](https://github.com/markc/spe) — PHP tutorial (Stone scheme)

## Using DCS in Other Projects

When working in any project that uses DCS:
1. Read `~/.gh/dcs.spa/CLAUDE.md` (this file) for the canonical pattern
2. Copy files from `~/.gh/dcs.spa/docs/` (the real files, not root symlinks)
3. Customize `site.css` for project-specific colors and branding
4. Never modify `base.css` or `base.js` — they are framework files

For deeper reference, `docs/_doc/` contains the in-tree docs: `architecture.md`, `color-system.md`, `components.md`, `usage-patterns.md`.

For Laravel + React projects, adapt the OKLCH color tokens into Tailwind v4 `@theme` blocks and use React context for theme state.

## License

MIT License — Copyright © 2026 Mark Constable <mc@dcs.spa>
