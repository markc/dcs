---
version: alpha
name: DCS — Ocean Dark
description: Color-only variant of DCS. Ocean scheme (hue=220, cyan-blue) in dark theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#161B1F"
  bg-secondary: "#1E2429"
  bg-tertiary: "#2B3339"
  fg-primary: "#EAF0F4"
  fg-secondary: "#AAB8C3"
  fg-muted: "#75818B"
  accent: "#85B4D5"
  accent-hover: "#A7CEE6"
  accent-fg: "#1A2229"
  accent-subtle: "#2F3A44"
  border: "#3B454D"
  border-muted: "#2B3339"
  success: "#79C08A"
  danger: "#E08879"
  warning: "#DFB670"
  glass: "#1E2429"
  glass-border: "#3B454D"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Accent lightness is raised from 55% (light) to 75% (dark) so it reads against near-black `bg-primary`. `accent-fg` flips to near-black so contrast on filled buttons stays correct.
- Shadows in dark mode use alpha 0.4 instead of 0.1 (see `DESIGN.md` § Elevation); this variant assumes that override is applied at runtime via `html.dark`.
- Semantic tokens (`success`, `danger`, `warning`) lighten toward 70–80% lightness to stay legible on dark surfaces.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 87–140 (`@media (prefers-color-scheme: dark)` and `html.dark`).
- Activate at runtime with no scheme class plus `html.dark` (Ocean is the default scheme).
