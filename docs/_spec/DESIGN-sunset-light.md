---
version: alpha
name: DCS — Sunset Light
description: Color-only variant of DCS. Sunset scheme (hue=45, orange-amber) in light theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#FCF6F1"
  bg-secondary: "#F8EFE6"
  bg-tertiary: "#EFDFCD"
  fg-primary: "#56391F"
  fg-secondary: "#795129"
  fg-muted: "#8E6944"
  accent: "#C97431"
  accent-hover: "#DB8237"
  accent-fg: "#FCF7F2"
  accent-subtle: "#F0E0D0"
  border: "#DDCCB8"
  border-muted: "#EADBC8"
  success: "#2E7D4A"
  danger: "#C85038"
  warning: "#D4A23F"
  glass: "#FCF6F1"
  glass-border: "#DDCCB8"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Sunset has the highest foreground chroma of any light scheme (0.08 on `fg-primary`). Body copy reads as warm brown, not neutral gray — the scheme is intentionally saturated into its ink so the accent doesn't have to carry all the warmth.
- `warning` (hue 85 amber) sits adjacent to `accent` (hue 45 orange) on the color wheel. Reserve `warning` for toasts and status pills; the two will fight if placed on the same card.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 282–299 (`.scheme-sunset:not(.dark)`).
- Activate at runtime via `html.scheme-sunset` (plus `html.light` or no class for auto light).
