---
name: Spacing Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-07-06
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Spacing — Semantic Tokens

## Philosophy

Semantic spacing tokens sit on top of the raw 8px-grid scale and give each value a **relative size role** — `spacing-xs` through `spacing-2xl` — rather than asking a component to pick a raw number like `space-3` or `space-4` directly. The scale is intentionally flat: one ramp shared by every gap and padding decision in the system, so spatial rhythm stays consistent without a category taxonomy to maintain.

> **Use these tokens for all margins, paddings, and gaps.**
> Never use arbitrary pixel values or reference Primitive Tokens directly in components.

---

## How to Read This File

### Naming Pattern

```
spacing-[size]
```

| Segment | Meaning |
|---------|---------|
| `spacing` | Indicates this is a spacing token |
| `size` | Relative size on the scale — `xs`, `sm`, `md`, `lg`, `xl`, `2xl` |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Spacing.md`.

### Theme Notes

Spacing tokens are theme-neutral — they do not change between Light and Dark mode.

> Always use logical CSS properties: `padding-inline`, `margin-block`, `gap`.
> Never use `margin-left`, `padding-right`, or other direction-specific properties — the system is RTL-first.

---

## Spacing Scale

| Token | Primitive | Value | Usage |
|-------|-----------|-------|-------|
| `spacing-xs` | → `space-1` | `4px` | Label above input, icon above text |
| `spacing-sm` | → `space-2` | `8px` | List items, form field rows |
| `spacing-md` | → `space-4` | `16px` | Card content rows, grouped fields |
| `spacing-lg` | → `space-6` | `24px` | Component groups within a section |
| `spacing-xl` | → `space-8` | `32px` | Between page sub-sections |
| `spacing-2xl` | → `space-12` | `48px` | Between major layout sections |

---

## CSS Custom Properties

```css
:root {
  --spacing-xs:  var(--space-1);   /*  4px */
  --spacing-sm:  var(--space-2);   /*  8px */
  --spacing-md:  var(--space-4);   /* 16px */
  --spacing-lg:  var(--space-6);   /* 24px */
  --spacing-xl:  var(--space-8);   /* 32px */
  --spacing-2xl: var(--space-12);  /* 48px */
}
```

### Usage Pattern

```css
/* Gap between stacked form fields */
.form {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);
}

/* Gap between card content rows */
.card {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

/* Gap between component groups within a section */
.section {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}
```

---

## Figma Variables

> **Collection:** `Semantic`

| Variable | Primitive | Value | Scope |
|----------|-----------|-------|-------|
| `Spacing/XS` | `Primitives/Spacing/space-1` | 4px | Gap |
| `Spacing/SM` | `Primitives/Spacing/space-2` | 8px | Gap |
| `Spacing/MD` | `Primitives/Spacing/space-4` | 16px | Gap |
| `Spacing/LG` | `Primitives/Spacing/space-6` | 24px | Gap |
| `Spacing/XL` | `Primitives/Spacing/space-8` | 32px | Gap |
| `Spacing/2XL` | `Primitives/Spacing/space-12` | 48px | Gap |
