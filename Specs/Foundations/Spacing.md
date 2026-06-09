---
name: Spacing Primitives
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Spacing System — Primitive Tokens

## Philosophy

Acadimiat's spacing system is built on an **8px grid**. All spacing values are multiples of 4px, ensuring visual consistency and alignment across all products. These are **Primitive Tokens** — raw spacing values used to build Semantic Tokens.

> **Important — Do not use arbitrary spacing values.**
> Every margin, padding, and gap must map to a token from this scale.

---

## Grid Base

| Property | Value |
|----------|-------|
| Base unit | `4px` |
| Grid unit | `8px` |
| Scale type | Multiples of 4 |

---

## Spacing Scale

The token name suffix reflects the multiplier of the **4px base unit** (e.g., `space-2` = 2 × 4px = 8px).

| Token | px | rem | Multiplier |
|-------|----|-----|------------|
| `space-0` | `0px` | `0` | 0 |
| `space-1` | `4px` | `0.25rem` | 1 |
| `space-2` | `8px` | `0.5rem` | 2 |
| `space-3` | `12px` | `0.75rem` | 3 |
| `space-4` | `16px` | `1rem` | 4 |
| `space-5` | `20px` | `1.25rem` | 5 |
| `space-6` | `24px` | `1.5rem` | 6 |
| `space-8` | `32px` | `2rem` | 8 |
| `space-10` | `40px` | `2.5rem` | 10 |
| `space-12` | `48px` | `3rem` | 12 |
| `space-16` | `64px` | `4rem` | 16 |
| `space-20` | `80px` | `5rem` | 20 |
| `space-24` | `96px` | `6rem` | 24 |

---

## Spacing Patterns

These patterns describe how spacing tokens combine to form consistent component anatomy.

### Inset (Padding)

Uniform padding applied inside a container.

| Pattern | Token | Value | Usage |
|---------|-------|-------|-------|
| `inset-xs` | `space-1` | `4px` | Tight chips, badges |
| `inset-sm` | `space-2` | `8px` | Small buttons, tags |
| `inset-md` | `space-3` | `12px` | Inputs, default buttons |
| `inset-lg` | `space-4` | `16px` | Cards (compact) |
| `inset-xl` | `space-6` | `24px` | Cards (default) |
| `inset-2xl` | `space-8` | `32px` | Section containers |

### Stack (Vertical Gap)

Gap between vertically stacked elements.

| Pattern | Token | Value | Usage |
|---------|-------|-------|-------|
| `stack-xs` | `space-1` | `4px` | Label + input gap |
| `stack-sm` | `space-2` | `8px` | List items, form fields |
| `stack-md` | `space-4` | `16px` | Card rows, sections |
| `stack-lg` | `space-6` | `24px` | Component groups |
| `stack-xl` | `space-8` | `32px` | Page sections |
| `stack-2xl` | `space-12` | `48px` | Major layout sections |

### Inline (Horizontal Gap)

Gap between horizontally aligned elements.

| Pattern | Token | Value | Usage |
|---------|-------|-------|-------|
| `inline-xs` | `space-1` | `4px` | Icon + label tight |
| `inline-sm` | `space-2` | `8px` | Icon + label default |
| `inline-md` | `space-3` | `12px` | Button group gap |
| `inline-lg` | `space-4` | `16px` | Nav items |
| `inline-xl` | `space-6` | `24px` | Toolbar items |

---

## CSS Custom Properties

```css
:root {
  --space-0:  0px;
  --space-1:  0.25rem;   /* 4px */
  --space-2:  0.5rem;    /* 8px */
  --space-3:  0.75rem;   /* 12px */
  --space-4:  1rem;      /* 16px */
  --space-5:  1.25rem;   /* 20px */
  --space-6:  1.5rem;    /* 24px */
  --space-8:  2rem;      /* 32px */
  --space-10: 2.5rem;    /* 40px */
  --space-12: 3rem;      /* 48px */
  --space-16: 4rem;      /* 64px */
  --space-20: 5rem;      /* 80px */
  --space-24: 6rem;      /* 96px */
}
```

---

## Usage Guidelines

| Context | Recommended Token | Value |
|---------|-------------------|-------|
| Input padding (inline) | `space-3` | 12px |
| Card padding | `space-4` – `space-6` | 16px – 24px |
| Section gap | `space-8` – `space-12` | 32px – 48px |
| Page margin | `space-6` – `space-10` | 24px – 40px |

---

## Rules

- No custom spacing values — every value must map to a token
- All values must align to the 4px base unit
- Do not skip more than 2 steps in a single component
- Use logical CSS properties only: `padding-inline`, `margin-block`, `gap` — never `margin-left`, `padding-right`
