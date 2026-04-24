---
version: alpha
name: DCS — Forest Light
description: Color-only variant of DCS. Forest scheme (hue=150, green) in light theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#F5FAF5"
  bg-secondary: "#EFF5EF"
  bg-tertiary: "#DFEBDF"
  fg-primary: "#1F3D27"
  fg-secondary: "#3A6043"
  fg-muted: "#5E7D63"
  accent: "#3D8759"
  accent-hover: "#489968"
  accent-fg: "#F6FBF6"
  accent-subtle: "#DEEDDD"
  border: "#CCDCCE"
  border-muted: "#D9E6DA"
  success: "#2E7D4A"
  danger: "#C85038"
  warning: "#D4A23F"
  glass: "#F5FAF5"
  glass-border: "#CCDCCE"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Forest shares the base-chroma structure with Ocean (both 0.12 at 50–55% lightness) — they are the two "mid-saturation brand hues" in the scheme family, swap-safe for A/B demos.
- `success` and `accent` are both green and share hue 145/150. The intentional overlap is fine because `success` appears only on status badges/toasts, never adjacent to a primary button.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 244–261 (`.scheme-forest:not(.dark)`).
- Activate at runtime via `html.scheme-forest` (plus `html.light` or no class for auto light).
