# DCS - Design Color System

A modular CSS/JS design system with OKLCH color schemes, dark/light modes, mobile-first responsive layout, and marketing components. Zero dependencies, no build step.

## Quick Start

```bash
# Clone
git clone https://github.com/markc/dcs.git
cd dcs

# Serve the demo
php -S localhost:8000 -t docs
# or
npx serve docs
```

Open `http://localhost:8000` to see the self-documenting showcase.

## Files

| File | Lines | Purpose |
|------|-------|---------|
| `base.css` | 705 | Generic framework (layout, components, utilities) |
| `base.js` | 245 | App shell JavaScript (theme, sidebars, toast) |
| `site.css` | ~530 | Marketing theme (OKLCH colors, hero, cards, pricing) |
| `site.js` | 83 | Marketing enhancements (particles, scroll reveal) |
| `md.js` | 97 | Markdown renderer (for documentation sites) |

## Architecture

```
base.css  ← Generic, color-agnostic, NEVER modify per-site
base.js   ← Generic, NEVER modify per-site
site.css  ← YOUR colors + marketing components (customize this)
site.js   ← YOUR JavaScript enhancements (optional)
```

**base.css** defines structure with CSS cascade layers (`reset`, `tokens`, `base`, `components`, `utilities`, `animations`) but zero colors. All colors come from CSS custom properties defined in **site.css**.

## Color Schemes

5 OKLCH color schemes, each with light + dark mode:

| Scheme | Hue | Character | Best For |
|--------|-----|-----------|----------|
| **Ocean** | 220 | Professional cyan-blue | Default, corporate |
| **Crimson** | 25 | Bold red | High energy, alerts |
| **Stone** | 60 | Warm neutral | Documentation, minimal |
| **Forest** | 150 | Natural green | Environmental, calm |
| **Sunset** | 45 | Warm amber | Inviting, creative |

Switch schemes live via the right sidebar, or programmatically:

```javascript
Base.setScheme('forest');  // ocean, crimson, stone, forest, sunset
Base.toggleTheme();        // dark ↔ light
```

## Usage

### 1. Marketing / Brochure Site

Copy `base.css`, `base.js`, `site.css`, `site.js` and a background image. Edit `site.css` to change the default color scheme hue.

```html
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="site.css">
<script src="base.js"></script>
<script src="site.js"></script>
```

### 2. Documentation Site

Use `base.css` + `base.js` with a minimal `site.css` (colors only, no marketing). Add `md.js` for markdown rendering.

```html
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="site.css">
<script src="base.js"></script>
<script src="md.js"></script>
```

### 3. Laravel + React (Inertia v2)

Import the OKLCH color tokens into your Tailwind v4 `@theme` block. Use React context for theme state instead of `base.js`.

## Components

### App Shell
- Fixed topnav with glassmorphism
- Dual sidebars (left: navigation, right: settings)
- Pinnable on desktop (1280px+)
- Collapsible sidebar groups

### Cards
- Mobile: edge-to-edge (no radius, no side borders)
- Desktop: rounded corners, shadows, hover lift
- Size variants: `.card-sm`, `.card-md`, `.card-lg`

### Buttons
- `.btn` (filled), `.btn-outline`, `.btn-ghost`
- `.btn-success`, `.btn-danger`, `.btn-warning`
- `.btn-sm`, `.btn-lg`

### Marketing
- Hero section (100vh with background overlay)
- Service cards with glass morphism
- Pricing tables
- CTA buttons (`.cta-btn.primary`, `.cta-btn.secondary`)
- Floating particles
- Scroll reveal animations

### Content
- `.prose` class for markdown/article rendering
- Forms with focus rings
- Dropdowns with animation
- Toast notifications
- Data tables, admin tables

## CSS Variable Contract

Your `site.css` must define these variables for `base.css` to work:

```css
--bg-primary, --bg-secondary, --bg-tertiary
--fg-primary, --fg-secondary, --fg-muted
--accent, --accent-hover, --accent-fg, --accent-subtle
--border, --border-muted
--success, --danger, --warning
--glass, --glass-border
```

## Built With DCS

- [motd.com](https://motd.com) — AI via email
- [renta.net](https://renta.net) — Managed Linux hosting
- [SPE](https://github.com/markc/spe) — PHP 8.5 tutorial documentation

## License

MIT License - Copyright (C) 2015-2026 Mark Constable <mc@netserva.org>
