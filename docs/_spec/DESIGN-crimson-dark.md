---
version: alpha
name: DCS — Crimson Dark
description: Color-only variant of DCS. Crimson scheme (hue=25, warm red) in dark theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#171110"
  bg-secondary: "#201815"
  bg-tertiary: "#2E2320"
  fg-primary: "#F3EBE9"
  fg-secondary: "#C3B2AD"
  fg-muted: "#8B7872"
  accent: "#D14C37"
  accent-hover: "#E75B44"
  accent-fg: "#FCF7F6"
  accent-subtle: "#342420"
  border: "#40332F"
  border-muted: "#2E2320"
  success: "#79C08A"
  danger: "#E08879"
  warning: "#DFB670"
  glass: "#201815"
  glass-border: "#40332F"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- `accent` pushes to chroma 0.23 in dark mode to compensate for perceived desaturation against very dark backgrounds. `accent-fg` stays near-white because the accent remains dark enough (54% lightness) to anchor white text.
- `accent-subtle` is a dark warm-black, not a tint — it fills active nav backgrounds where a light-mode-style pale red would glow against `bg-primary`.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 186–203 (`.scheme-crimson.dark`).
- Activate at runtime via `html.scheme-crimson` + `html.dark`.
