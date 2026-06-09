---
name: Radius Primitives
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Radius System — Primitive Tokens

## Philosophy

Acadimiat's radius system reflects a modern, refined SaaS aesthetic. Larger radii (12–16px) are preferred to convey softness and approachability while maintaining professional elegance. These are **Primitive Tokens** — raw border-radius values applied through Semantic Tokens.

> **Important — Do not use arbitrary radius values.**
> Every border-radius must map to a token from this scale.

---

## Radius Scale

| Token | Value | rem |
|-------|-------|-----|
| `radius-0` | `0px` | `0` |
| `radius-2` | `2px` | `0.125rem` |
| `radius-4` | `4px` | `0.25rem` |
| `radius-8` | `8px` | `0.5rem` |
| `radius-12` | `12px` | `0.75rem` |
| `radius-16` | `16px` | `1rem` |
| `radius-24` | `24px` | `1.5rem` |
| `radius-full` | `9999px` | — |

---

## Usage Guidelines

| Component | Token | Value |
|-----------|-------|-------|
| Cards | `radius-16` | 16px |
| Modals / Drawers | `radius-16` | 16px |
| Inputs | `radius-12` | 12px |
| Buttons (default) | `radius-12` | 12px |
| Buttons (large) | `radius-16` | 16px |
| Dropdowns / Menus | `radius-8` | 8px |
| Tooltips | `radius-8` | 8px |
| Badges | `radius-4` | 4px |
| Tags / Chips | `radius-full` | 9999px |
| Avatars | `radius-full` | 9999px |
| Progress bars | `radius-full` | 9999px |
| Dividers / Sharp UI | `radius-0` | 0px |
| Subtle rounding | `radius-2` | 2px |

---

## CSS Custom Properties

```css
:root {
  --radius-0:    0px;
  --radius-2:    0.125rem;  /* 2px */
  --radius-4:    0.25rem;   /* 4px */
  --radius-8:    0.5rem;    /* 8px */
  --radius-12:   0.75rem;   /* 12px */
  --radius-16:   1rem;      /* 16px */
  --radius-24:   1.5rem;    /* 24px */
  --radius-full: 9999px;
}
```

---

## Rules

- Prefer `radius-12` and `radius-16` for all SaaS UI components
- Never mix more than 2 different radius values within the same component
- Use `radius-full` only for pill shapes, avatars, and circular elements
- Use `radius-0` only for intentionally sharp UI (e.g., full-width banners, table cells)
