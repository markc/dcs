# CLAUDE.md

Project guidance for Claude Code when working with this repository.

## Project Overview

**DCS (Dual Carousel Sidebar)** is the canonical reference implementation of Mark's preferred web interface pattern. It is a modular CSS/JS design system featuring dual sidebars, OKLCH color schemes, dark/light modes, mobile-first responsive layout, and marketing components. Zero dependencies, no build step.

**This repo is the single source of truth.** Every project that uses DCS (plain PHP, static HTML, Laravel+React) should reference `~/.gh/dcs` as the authority. When told "use the DCS interface", read these files and reproduce the pattern.

**Showcase:** [dcs.spa](https://dcs.spa) (GitHub Pages, self-documenting SPA built with DCS)

## File Structure

```
dcs/
├── docs/                   # Real files (GitHub Pages source at dcs.spa)
│   ├── index.html          # Self-documenting SPA showcase
│   ├── base.css            # Generic framework (705 lines)
│   ├── base.js             # Generic JavaScript (245 lines)
│   ├── site.css            # Marketing theme with OKLCH colors + components
│   ├── site.js             # Marketing JavaScript (particles, scroll reveal)
│   ├── md.js               # Markdown renderer (for documentation sites)
│   └── Server_Room_Dark.webp # Default background image
├── base.css                 → symlink → docs/base.css
├── base.js                  → symlink → docs/base.js
├── site.css                 → symlink → docs/site.css
├── site.js                  → symlink → docs/site.js
├── md.js                    → symlink → docs/md.js
├── Server_Room_Dark.webp    → symlink → docs/Server_Room_Dark.webp
├── base.txt                # Structure spec for AI site generation
├── themes/                 # Standalone color-only themes (no marketing)
│   └── stone.css           # Example: documentation-focused theme
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

- **Tokens:** Typography (6 sizes), spacing (0-8), radius, shadows, transitions, z-index
- **Reset:** Box-sizing, reduced motion, contrast preferences
- **Base:** Headings, links, code blocks, tables
- **Components:** Container, cards, buttons, forms, dropdowns, toast, topnav, sidebars, prose
- **Utilities:** Display, flex, grid, spacing, text, glass morphism
- **Animations:** Toast-in, fade-in, hover-lift

Key design decisions:
- Color-agnostic: defines NO colors (all from site.css CSS vars)
- Mobile-first: base styles are single column, enhanced at 768px and 1280px
- Cards: no radius/border on mobile, full styling on desktop

### base.js (Generic JavaScript)

Single `Base` object with localStorage state management:
- Theme toggle (dark/light via `.dark`/`.light` class on `<html>`)
- Color scheme switching (`.scheme-{name}` class)
- Sidebar open/close/pin (left and right, pinnable at 1280px+)
- Toast notifications
- Event delegation (single click handler)
- Lucide icon integration
- Preload class prevents flash of transitions

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

5 schemes: Ocean (H=220, default), Crimson (H=25), Stone (H=60), Forest (H=150), Sunset (H=45)

### site.js (Optional Marketing)

Particle effects, scroll reveal animations, dynamic footer year.

### md.js (Optional Documentation)

Lightweight markdown-to-HTML renderer for documentation sites. Supports headings, lists, code blocks, tables, links, images, emphasis.

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
<link rel="stylesheet" href="themes/stone.css">  <!-- colors only -->
<script src="base.js"></script>
<script src="md.js"></script>
```

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
├── div.overlay
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
1. Read `~/.gh/dcs/CLAUDE.md` (this file) for the canonical pattern
2. Copy files from `~/.gh/dcs/docs/` (the real files, not root symlinks)
3. Customize `site.css` for project-specific colors and branding
4. Never modify `base.css` or `base.js` — they are framework files

For Laravel + React projects, adapt the OKLCH color tokens into Tailwind v4 `@theme` blocks and use React context for theme state.

## License

MIT License - Copyright (C) 2015-2026 Mark Constable <mc@netserva.org>
