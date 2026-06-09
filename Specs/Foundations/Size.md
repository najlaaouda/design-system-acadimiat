---
name: Size Primitives
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Size System — Primitive Tokens

## Philosophy

Acadimiat's size system defines fixed dimensions for UI elements such as icons, avatars, buttons, and inputs. All values align to the **4px base unit** and are distinct from spacing — size controls the dimensions of an element, not the space around it.

> **Important — Do not use arbitrary size values.**
> Every width, height, and icon dimension must map to a token from this scale.

---

## Size Scale

| Token | px | rem |
|-------|----|-----|
| `size-3` | `12px` | `0.75rem` |
| `size-4` | `16px` | `1rem` |
| `size-4-5` | `18px` | `1.125rem` |
| `size-5` | `20px` | `1.25rem` |
| `size-6` | `24px` | `1.5rem` |
| `size-8` | `32px` | `2rem` |
| `size-10` | `40px` | `2.5rem` |
| `size-11` | `44px` | `2.75rem` |

---

## Icon Sizes

| Token | px | Usage |
|-------|----|-------|
| `size-4` | `16px` | Small icon (inline text, badges) |
| `size-5` | `20px` | Default icon (buttons, nav, inputs) |
| `size-6` | `24px` | Large icon (section headers, empty states) |

---

## Avatar Sizes

| Token | px | Usage |
|-------|----|-------|
| `size-6` | `24px` | Avatar (XS — comments, compact lists) |
| `size-8` | `32px` | Avatar (SM — table rows, dropdowns) |
| `size-10` | `40px` | Avatar (MD — profile headers, cards) |
| `size-11` | `44px` | Avatar (LG — user profile page) |

---

## Component Heights

| Token | px | Usage |
|-------|----|-------|
| `size-3` | `12px` | Progress bar track, divider thickness |
| `size-4-5` | `18px` | Badge, tag, chip (compact) |
| `size-8` | `32px` | Button (SM), input (SM) |
| `size-10` | `40px` | Button (MD — default), input (MD — default) |
| `size-11` | `44px` | Button (LG), input (LG) |

> **Accessibility:** Minimum interactive touch target is `40px` (`size-10`). Never use a smaller height for clickable elements.

---

## CSS Custom Properties

```css
:root {
  --size-3:   0.75rem;   /* 12px */
  --size-4:   1rem;      /* 16px */
  --size-4-5: 1.125rem;  /* 18px */
  --size-5:   1.25rem;   /* 20px */
  --size-6:   1.5rem;    /* 24px */
  --size-8:   2rem;      /* 32px */
  --size-10:  2.5rem;    /* 40px */
  --size-11:  2.75rem;   /* 44px */
}
```

---

## Quick Reference

| Element | Token | px |
|---------|-------|----|
| Icon — small | `size-4` | 16px |
| Icon — default | `size-5` | 20px |
| Icon — large | `size-6` | 24px |
| Avatar — XS | `size-6` | 24px |
| Avatar — SM | `size-8` | 32px |
| Avatar — MD | `size-10` | 40px |
| Avatar — LG | `size-11` | 44px |
| Button — SM | `size-8` | 32px |
| Button — MD | `size-10` | 40px |
| Button — LG | `size-11` | 44px |
| Input — SM | `size-8` | 32px |
| Input — MD | `size-10` | 40px |
| Input — LG | `size-11` | 44px |
| Min touch target | `size-10` | 40px |

---

## Rules

- Minimum interactive element height is `size-10` (40px) — WCAG AA requirement
- Icons must always use `size-4`, `size-5`, or `size-6` — no other values
- Never mix more than 2 size variants within the same component group
- Size tokens define dimensions only — use spacing tokens for padding and gap
