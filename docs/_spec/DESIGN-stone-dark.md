---
version: alpha
name: DCS — Stone Dark
description: Color-only variant of DCS. Stone scheme (hue=60, warm neutral) in dark theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#181612"
  bg-secondary: "#21201A"
  bg-tertiary: "#2F2D25"
  fg-primary: "#EEEAE0"
  fg-secondary: "#BCB5A4"
  fg-muted: "#8A8270"
  accent: "#CEC1A3"
  accent-hover: "#E6DEC8"
  accent-fg: "#2F291D"
  accent-subtle: "#3B3527"
  border: "#484331"
  border-muted: "#2F2D25"
  success: "#79C08A"
  danger: "#E08879"
  warning: "#DFB670"
  glass: "#21201A"
  glass-border: "#484331"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Dark Stone inverts the light-scheme's contrast convention: `accent` is the *lightest* color in the palette (80% lightness, warm cream), not the brightest saturated hue. This matches the "ink on parchment" mental model read in reverse — warm paper-colored strokes on dark leather.
- `accent-fg` is a dark warm brown, picked so filled buttons look like embossed leather rather than tinted plastic.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 224–241 (`.scheme-stone.dark`).
- Activate at runtime via `html.scheme-stone` + `html.dark`.
