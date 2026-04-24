---
version: alpha
name: DCS — Forest Dark
description: Color-only variant of DCS. Forest scheme (hue=150, green) in dark theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#141B16"
  bg-secondary: "#1B241D"
  bg-tertiary: "#273228"
  fg-primary: "#EBF2EB"
  fg-secondary: "#A9C4AE"
  fg-muted: "#73907B"
  accent: "#79C08A"
  accent-hover: "#A1D4AD"
  accent-fg: "#1A2A1E"
  accent-subtle: "#2F402F"
  border: "#394C3D"
  border-muted: "#273228"
  success: "#79C08A"
  danger: "#E08879"
  warning: "#DFB670"
  glass: "#1B241D"
  glass-border: "#394C3D"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- `accent` and `success` converge on the same value (`#79C08A`) because both resolve to `oklch(70% 0.12 150)` at dark-theme lightness. On Forest dark, success badges are therefore visually indistinguishable from primary-branded elements — place status toasts where brand accent isn't competing for attention.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 262–279 (`.scheme-forest.dark`).
- Activate at runtime via `html.scheme-forest` + `html.dark`.
