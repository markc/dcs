---
version: alpha
name: DCS — Mono Light
description: Color-only variant of DCS. Mono scheme (chroma=0, pure grayscale) in light theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#F8F8F8"
  bg-secondary: "#F1F1F1"
  bg-tertiary: "#E3E3E3"
  fg-primary: "#242424"
  fg-secondary: "#525252"
  fg-muted: "#787878"
  accent: "#303030"
  accent-hover: "#454545"
  accent-fg: "#F8F8F8"
  accent-subtle: "#DCDCDC"
  border: "#CECECE"
  border-muted: "#DCDCDC"
  success: "#2E7D4A"
  danger: "#C85038"
  warning: "#D4A23F"
  glass: "#F8F8F8"
  glass-border: "#CECECE"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Chroma is exactly zero on every non-semantic token — this is the only scheme where hue is meaningless. `accent` is effectively near-black (lightness 25%), giving the scheme its signature "text wants to be a button" feel.
- Semantic tokens (`success`, `danger`, `warning`) intentionally break neutrality. Status information cannot be reliably encoded by grayscale alone, so Mono inherits the Ocean-family semantic hues unchanged. If you need a *truly* monochrome scheme for print or e-ink, override these three to grayscale values at the consumer site.
- Inside `.hero-bg` (overlaid on the dark hero image) the `accent` is overridden at runtime from dark-gray to light-gray so the shimmer effect on hero headings stays visible. See `site.css` lines 475–478.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 320–337 (`.scheme-mono:not(.dark)`).
- Activate at runtime via `html.scheme-mono` (plus `html.light` or no class for auto light).
