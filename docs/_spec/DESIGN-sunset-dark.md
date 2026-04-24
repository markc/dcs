---
version: alpha
name: DCS — Sunset Dark
description: Color-only variant of DCS. Sunset scheme (hue=45, orange-amber) in dark theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#1E140B"
  bg-secondary: "#291C10"
  bg-tertiary: "#3A2918"
  fg-primary: "#F4E9D9"
  fg-secondary: "#CAAB89"
  fg-muted: "#91724F"
  accent: "#E8A262"
  accent-hover: "#F1BB87"
  accent-fg: "#291911"
  accent-subtle: "#412B17"
  border: "#513821"
  border-muted: "#3A2918"
  success: "#79C08A"
  danger: "#E08879"
  warning: "#DFB670"
  glass: "#291C10"
  glass-border: "#513821"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Dark Sunset backgrounds tint toward near-black brown rather than neutral black (`bg-primary` chroma 0.02). On OLED displays this reads as a warm cast; on LCD the tint is subtle but keeps the warm family coherent with the accent.
- `accent` at 72% lightness is the brightest foreground in any dark variant — Sunset leans into glow rather than restraint.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 300–317 (`.scheme-sunset.dark`).
- Activate at runtime via `html.scheme-sunset` + `html.dark`.
