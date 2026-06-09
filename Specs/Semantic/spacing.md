---
name: Spacing Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Spacing — Semantic Tokens

## Philosophy

Semantic spacing tokens sit on top of the raw 8px-grid scale and give each value a **spatial purpose**. Instead of choosing between `space-3` and `space-4`, you choose between `spacing-inset-md` (padding inside a button) and `spacing-inset-lg` (padding inside a card). This eliminates arbitrary spacing decisions and keeps spatial rhythm consistent across all components and layouts.

> **Use these tokens for all margins, paddings, and gaps.**
> Never use arbitrary pixel values or reference Primitive Tokens directly in components.

---

## How to Read This File

### What Are Semantic Spacing Tokens?

Instead of picking a raw number from the spacing scale, you pick a **role** — a named token that describes the spatial relationship between elements. Each role answers the question: *what is this space for?*

### Naming Pattern

```
spacing-[category]-[size]
```

| Segment | Meaning |
|---------|---------|
| `spacing` | Indicates this is a spacing token |
| `category` | The spatial relationship — `inset`, `stack`, `inline`, `layout` |
| `size` | Relative size within the category — `xs`, `sm`, `md`, `lg`, `xl`, `2xl` |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Spacing.md`.

### Categories at a Glance

| Category | Applied To | CSS Property |
|----------|-----------|--------------|
| `inset` | Padding inside a component | `padding` / `padding-block` + `padding-inline` |
| `stack` | Vertical gap between elements | `gap` / `margin-block` |
| `inline` | Horizontal gap between elements | `gap` / `margin-inline` |
| `layout` | Page-level and section-level spacing | `padding-inline` / `gap` / `margin-block` |

> Always use logical CSS properties: `padding-inline`, `margin-block`, `gap`.
> Never use `margin-left`, `padding-right`, or other direction-specific properties — the system is RTL-first.

---

## Inset — Padding

Applied inside a component as uniform or asymmetric padding.

| Token | Primitive | Value | Usage |
|-------|-----------|-------|-------|
| `spacing-inset-xs` | → `space-1` | `4px` | Tight chips, icon buttons, badges |
| `spacing-inset-sm` | → `space-2` | `8px` | Small buttons, tags, compact inputs |
| `spacing-inset-md` | → `space-3` | `12px` | Default inputs, default buttons |
| `spacing-inset-lg` | → `space-4` | `16px` | Compact cards, dropdowns, menus |
| `spacing-inset-xl` | → `space-6` | `24px` | Default cards, modals, panels |
| `spacing-inset-2xl` | → `space-8` | `32px` | Large cards, section containers |

---

## Stack — Vertical Gap

Applied as the gap between elements laid out vertically.

| Token | Primitive | Value | Usage |
|-------|-----------|-------|-------|
| `spacing-stack-xs` | → `space-1` | `4px` | Label above input, icon above text |
| `spacing-stack-sm` | → `space-2` | `8px` | List items, form field rows |
| `spacing-stack-md` | → `space-4` | `16px` | Card content rows, grouped fields |
| `spacing-stack-lg` | → `space-6` | `24px` | Component groups within a section |
| `spacing-stack-xl` | → `space-8` | `32px` | Between page sub-sections |
| `spacing-stack-2xl` | → `space-12` | `48px` | Between major layout sections |

---

## Inline — Horizontal Gap

Applied as the gap between elements laid out horizontally.

| Token | Primitive | Value | Usage |
|-------|-----------|-------|-------|
| `spacing-inline-xs` | → `space-1` | `4px` | Icon + label (tight), badge + text |
| `spacing-inline-sm` | → `space-2` | `8px` | Icon + label (default), avatar + name |
| `spacing-inline-md` | → `space-3` | `12px` | Button group gap, tab items |
| `spacing-inline-lg` | → `space-4` | `16px` | Nav items, toolbar buttons |
| `spacing-inline-xl` | → `space-6` | `24px` | Wide toolbar items, split layouts |

---

## Layout — Page & Section Spacing

Applied at the macro layout level — page margins, section gaps, and container padding.

| Token | Primitive | Value | Usage |
|-------|-----------|-------|-------|
| `spacing-layout-page-sm` | → `space-4` | `16px` | Page horizontal margin on mobile |
| `spacing-layout-page` | → `space-6` | `24px` | Page horizontal margin on tablet |
| `spacing-layout-page-lg` | → `space-10` | `40px` | Page horizontal margin on desktop |
| `spacing-layout-section` | → `space-12` | `48px` | Gap between page sections |
| `spacing-layout-section-lg` | → `space-16` | `64px` | Gap between major page sections |
| `spacing-layout-container` | → `space-8` | `32px` | Inner padding of a full-width container |

---

## Quick Reference

| Token | Value | Used For |
|-------|-------|----------|
| `spacing-inset-xs` | 4px | Chips, badges |
| `spacing-inset-sm` | 8px | Small buttons, tags |
| `spacing-inset-md` | 12px | Inputs, default buttons |
| `spacing-inset-lg` | 16px | Compact cards, menus |
| `spacing-inset-xl` | 24px | Default cards, modals |
| `spacing-inset-2xl` | 32px | Large cards, containers |
| `spacing-stack-xs` | 4px | Label + input |
| `spacing-stack-sm` | 8px | List items, form rows |
| `spacing-stack-md` | 16px | Card rows, grouped fields |
| `spacing-stack-lg` | 24px | Component groups |
| `spacing-stack-xl` | 32px | Sub-sections |
| `spacing-stack-2xl` | 48px | Major sections |
| `spacing-inline-xs` | 4px | Icon + label (tight) |
| `spacing-inline-sm` | 8px | Icon + label (default) |
| `spacing-inline-md` | 12px | Button groups, tabs |
| `spacing-inline-lg` | 16px | Nav items |
| `spacing-inline-xl` | 24px | Wide toolbars |
| `spacing-layout-page-sm` | 16px | Page margin — mobile |
| `spacing-layout-page` | 24px | Page margin — tablet |
| `spacing-layout-page-lg` | 40px | Page margin — desktop |
| `spacing-layout-section` | 48px | Section gap |
| `spacing-layout-section-lg` | 64px | Major section gap |
| `spacing-layout-container` | 32px | Container inner padding |

---

## CSS Custom Properties

```css
:root {
  /* ── Inset (Padding) ─────────────────────────────────── */
  --spacing-inset-xs:  var(--space-1);   /*  4px */
  --spacing-inset-sm:  var(--space-2);   /*  8px */
  --spacing-inset-md:  var(--space-3);   /* 12px */
  --spacing-inset-lg:  var(--space-4);   /* 16px */
  --spacing-inset-xl:  var(--space-6);   /* 24px */
  --spacing-inset-2xl: var(--space-8);   /* 32px */

  /* ── Stack (Vertical Gap) ────────────────────────────── */
  --spacing-stack-xs:  var(--space-1);   /*  4px */
  --spacing-stack-sm:  var(--space-2);   /*  8px */
  --spacing-stack-md:  var(--space-4);   /* 16px */
  --spacing-stack-lg:  var(--space-6);   /* 24px */
  --spacing-stack-xl:  var(--space-8);   /* 32px */
  --spacing-stack-2xl: var(--space-12);  /* 48px */

  /* ── Inline (Horizontal Gap) ─────────────────────────── */
  --spacing-inline-xs: var(--space-1);   /*  4px */
  --spacing-inline-sm: var(--space-2);   /*  8px */
  --spacing-inline-md: var(--space-3);   /* 12px */
  --spacing-inline-lg: var(--space-4);   /* 16px */
  --spacing-inline-xl: var(--space-6);   /* 24px */

  /* ── Layout ──────────────────────────────────────────── */
  --spacing-layout-page-sm:    var(--space-4);   /* 16px */
  --spacing-layout-page:       var(--space-6);   /* 24px */
  --spacing-layout-page-lg:    var(--space-10);  /* 40px */
  --spacing-layout-section:    var(--space-12);  /* 48px */
  --spacing-layout-section-lg: var(--space-16);  /* 64px */
  --spacing-layout-container:  var(--space-8);   /* 32px */
}
```

### Usage Pattern

```css
/* Padding inside a card */
.card {
  padding: var(--spacing-inset-xl);
}

/* Gap between stacked form fields */
.form {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-stack-sm);
}

/* Gap between icon and label in a button */
.btn {
  display: flex;
  align-items: center;
  gap: var(--spacing-inline-sm);
  padding-block:  var(--spacing-inset-sm);
  padding-inline: var(--spacing-inset-md);
}

/* Page horizontal margin — responsive */
.page-wrapper {
  padding-inline: var(--spacing-layout-page-sm); /* mobile  */
}
@media (min-width: 768px) {
  .page-wrapper {
    padding-inline: var(--spacing-layout-page);   /* tablet  */
  }
}
@media (min-width: 1280px) {
  .page-wrapper {
    padding-inline: var(--spacing-layout-page-lg); /* desktop */
  }
}
```

---

## Figma Variables

> **Collection:** `Semantic/Spacing`

| Variable | Primitive | Value | Scope |
|----------|-----------|-------|-------|
| `spacing/inset/xs` | `primitive/space-1` | 4px | Horizontal padding, Vertical padding |
| `spacing/inset/sm` | `primitive/space-2` | 8px | Horizontal padding, Vertical padding |
| `spacing/inset/md` | `primitive/space-3` | 12px | Horizontal padding, Vertical padding |
| `spacing/inset/lg` | `primitive/space-4` | 16px | Horizontal padding, Vertical padding |
| `spacing/inset/xl` | `primitive/space-6` | 24px | Horizontal padding, Vertical padding |
| `spacing/inset/2xl` | `primitive/space-8` | 32px | Horizontal padding, Vertical padding |
| `spacing/stack/xs` | `primitive/space-1` | 4px | Gap |
| `spacing/stack/sm` | `primitive/space-2` | 8px | Gap |
| `spacing/stack/md` | `primitive/space-4` | 16px | Gap |
| `spacing/stack/lg` | `primitive/space-6` | 24px | Gap |
| `spacing/stack/xl` | `primitive/space-8` | 32px | Gap |
| `spacing/stack/2xl` | `primitive/space-12` | 48px | Gap |
| `spacing/inline/xs` | `primitive/space-1` | 4px | Gap |
| `spacing/inline/sm` | `primitive/space-2` | 8px | Gap |
| `spacing/inline/md` | `primitive/space-3` | 12px | Gap |
| `spacing/inline/lg` | `primitive/space-4` | 16px | Gap |
| `spacing/inline/xl` | `primitive/space-6` | 24px | Gap |
| `spacing/layout/page-sm` | `primitive/space-4` | 16px | Horizontal padding |
| `spacing/layout/page` | `primitive/space-6` | 24px | Horizontal padding |
| `spacing/layout/page-lg` | `primitive/space-10` | 40px | Horizontal padding |
| `spacing/layout/section` | `primitive/space-12` | 48px | Gap |
| `spacing/layout/section-lg` | `primitive/space-16` | 64px | Gap |
| `spacing/layout/container` | `primitive/space-8` | 32px | Horizontal padding, Vertical padding |

---

## Responsive Layout Spacing

Layout tokens are the only spacing category that changes across breakpoints. Inset, stack, and inline tokens are component-scoped and remain fixed — only page margins and section gaps need to adapt to viewport size.

### Breakpoint Scale

| Breakpoint | Min-Width | `spacing-layout-page` | `spacing-layout-section` |
|------------|-----------|----------------------|--------------------------|
| xs — Mobile | 0px | `spacing-layout-page-sm` — 16px | `spacing-layout-section` — 48px |
| md — Tablet | 768px | `spacing-layout-page` — 24px | `spacing-layout-section` — 48px |
| xl — Desktop | 1280px | `spacing-layout-page-lg` — 40px | `spacing-layout-section-lg` — 64px |

### Responsive CSS Pattern

```css
/* ── Page horizontal margin ──────────────────────────────── */
.page-wrapper {
  padding-inline: var(--spacing-layout-page-sm); /* mobile */
}

@media (min-width: 768px) {
  .page-wrapper {
    padding-inline: var(--spacing-layout-page);   /* tablet */
  }
}

@media (min-width: 1280px) {
  .page-wrapper {
    padding-inline: var(--spacing-layout-page-lg); /* desktop */
  }
}

/* ── Section vertical gap ────────────────────────────────── */
.page-sections {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-layout-section); /* mobile + tablet */
}

@media (min-width: 1280px) {
  .page-sections {
    gap: var(--spacing-layout-section-lg); /* desktop */
  }
}
```
