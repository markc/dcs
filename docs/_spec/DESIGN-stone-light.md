---
version: alpha
name: DCS — Stone Light
description: Color-only variant of DCS. Stone scheme (hue=60, warm neutral) in light theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#FAF8F4"
  bg-secondary: "#F4F1EB"
  bg-tertiary: "#E9E4D9"
  fg-primary: "#3A3325"
  fg-secondary: "#6F6755"
  fg-muted: "#8A8270"
  accent: "#746841"
  accent-hover: "#574D2D"
  accent-fg: "#FAF8F4"
  accent-subtle: "#EAE5D5"
  border: "#D6D2C8"
  border-muted: "#E3DFD6"
  success: "#2E7D4A"
  danger: "#C85038"
  warning: "#D4A23F"
  glass: "#FAF8F4"
  glass-border: "#D6D2C8"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Chroma is intentionally low (0.005–0.05) across the board — Stone is the documentation-oriented scheme, tuned for long reading sessions where a saturated accent would fatigue.
- Uniquely among schemes, `accent-hover` is *darker* than `accent` (35% vs. 45% lightness). On this muted palette a brighter hover disappears; a darker one reads as pressed-in ink.
- Used by the [SPE PHP tutorial](https://github.com/markc/spe) and suits any doc-heavy project where a saturated accent would fatigue over long reading sessions.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 206–223 (`.scheme-stone:not(.dark)`).
- Activate at runtime via `html.scheme-stone` (plus `html.light` or no class for auto light).
