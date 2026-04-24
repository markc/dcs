---
version: alpha
name: DCS — Crimson Light
description: Color-only variant of DCS. Crimson scheme (hue=25, warm red) in light theme. Typography, layout, shapes, and component structure inherit from DESIGN.md.
colors:
  bg-primary: "#FBF6F5"
  bg-secondary: "#F7F0EE"
  bg-tertiary: "#EEE2DE"
  fg-primary: "#3F2A27"
  fg-secondary: "#644339"
  fg-muted: "#7A5A55"
  accent: "#B23D2E"
  accent-hover: "#A32F21"
  accent-fg: "#FCF7F6"
  accent-subtle: "#F0DED9"
  border: "#D9CEC9"
  border-muted: "#E4DBD7"
  success: "#2E7D4A"
  danger: "#C85038"
  warning: "#D4A23F"
  glass: "#FBF6F5"
  glass-border: "#D9CEC9"
---

## Overview

Color-only palette. Read [`DESIGN.md`](./DESIGN.md) for the full token contract — typography, spacing, rounded, components, and design rationale. This file overrides `colors:` and nothing else.

## Colors

- Chroma on the `accent` is 0.2 — the hottest of the six schemes — because red at lower chroma desaturates into muted terracotta. Backgrounds tint subtly (chroma 0.008–0.018) toward warm off-white.
- Used by [motd.com](https://motd.com) and [renta.net](https://renta.net).
- `danger` happens to share hue 25 with `accent`; the two are differentiated by lightness (47% accent vs. 55% danger) and are never used adjacently on the same surface.

## Notes

- Authoritative OKLCH source: `docs/site.css` lines 168–185 (`.scheme-crimson:not(.dark)`).
- Activate at runtime via `html.scheme-crimson` (plus `html.light` or no class for auto light).
