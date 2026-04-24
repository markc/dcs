---
version: alpha
name: DCS — Mono Dark
description: Color-only variant of DCS. Mono scheme (chroma=0, pure grayscale) in dark theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#131313"
  bg-secondary: "#1C1C1C"
  bg-tertiary: "#2B2B2B"
  fg-primary: "#EEEEEE"
  fg-secondary: "#B8B8B8"
  fg-muted: "#787878"
  accent: "#D3D3D3"
  accent-hover: "#E9E9E9"
  accent-fg: "#181818"
  accent-subtle: "#303030"
  border: "#3B3B3B"
  border-muted: "#2B2B2B"
  success: "#79C08A"
  danger: "#E08879"
  warning: "#DFB670"
  glass: "#1C1C1C"
  glass-border: "#3B3B3B"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Inverts Mono Light's "accent = near-black" rule — here `accent` is near-white (85% lightness) and `accent-fg` is near-black. Filled buttons read as embossed light panels on a dark field.
- `fg-muted` (78%) is identical between Mono Light and Mono Dark — at chroma zero a single mid-gray works on either background, which is why `docs/site.css` duplicates the value across modes rather than flipping it.
- Semantic tokens inherit the dark-theme Ocean values (70–80% lightness greens/reds/ambers) for legibility on dark surfaces.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 338–355 (`.scheme-mono.dark`).
- Activate at runtime via `html.scheme-mono` + `html.dark`.
