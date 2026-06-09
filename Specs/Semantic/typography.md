---
name: Typography Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Typography — Semantic Tokens

## Philosophy

Semantic typography tokens translate the raw type scale into named **text roles** that describe intent rather than appearance. A component never picks `font-size-base` + `font-weight-semibold` + `line-height-normal` manually — it uses `type-label`, which bundles all three. This guarantees that the same UI element looks identical everywhere, and that changing a role's definition updates every instance at once.

> **Use these tokens on all text elements in components.**
> Never compose font properties manually from Primitive Tokens in a component.

---

## How to Read This File

### What Are Semantic Typography Tokens?

Instead of picking a raw font-size or weight from the primitive scale, you pick a **role** — a named text style that bundles all typographic properties together. Each role answers the question: *what is this text for?*

### Naming Pattern

```
type-[role]
```

| Segment | Meaning |
|---------|---------|
| `type` | A bundled typographic style |
| `role` | The UI purpose — `display`, `heading-1`, `body`, `label`, `caption`, etc. |

In CSS, each role expands into four individual properties:

```
--type-[role]-family
--type-[role]-size
--type-[role]-weight
--type-[role]-line-height
```

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Typography.md`.

### RTL & Language Notes

- All roles use `font-family-arabic` by default — Arabic is the primary language.
- `type-display` uses `font-family-display`, which can be swapped per product at the theme level.
- When English content is present, swap `font-family-arabic` for `font-family-latin` at the component level. Token names stay the same.
- Never apply `letter-spacing` to Arabic text.

---

## Type Roles

### Display

Used for hero sections and large marketing headlines. Largest text in the system.

| Property | Token | Primitive | Value |
|----------|-------|-----------|-------|
| Family | `type-display-family` | → `font-family-display` | IBM Plex Sans Arabic |
| Size | `type-display-size` | → `font-size-10xl` | 72px / 4.5rem |
| Weight | `type-display-weight` | → `font-weight-bold` | 700 |
| Line Height | `type-display-line-height` | → `line-height-tight` | 1.2 |

---

### Headings

Structural hierarchy for page, section, and panel titles.

| Role | Property | Primitive | Value |
|------|----------|-----------|-------|
| `type-heading-1` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-8xl` | 56px / 3.5rem |
| | Weight | → `font-weight-bold` | 700 |
| | Line Height | → `line-height-tight` | 1.2 |
| `type-heading-2` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-7xl` | 48px / 3rem |
| | Weight | → `font-weight-bold` | 700 |
| | Line Height | → `line-height-tight` | 1.2 |
| `type-heading-3` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-6xl` | 40px / 2.5rem |
| | Weight | → `font-weight-semibold` | 600 |
| | Line Height | → `line-height-snug` | 1.35 |
| `type-heading-4` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-5xl` | 36px / 2.25rem |
| | Weight | → `font-weight-semibold` | 600 |
| | Line Height | → `line-height-snug` | 1.35 |
| `type-heading-5` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-4xl` | 32px / 2rem |
| | Weight | → `font-weight-medium` | 500 |
| | Line Height | → `line-height-normal` | 1.5 |

---

### Body

Long-form readable content. The default text style for paragraphs and descriptions.

| Role | Property | Primitive | Value |
|------|----------|-----------|-------|
| `type-body-lg` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-xl` | 20px / 1.25rem |
| | Weight | → `font-weight-regular` | 400 |
| | Line Height | → `line-height-normal` | 1.5 |
| `type-body` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-base` | 16px / 1rem |
| | Weight | → `font-weight-regular` | 400 |
| | Line Height | → `line-height-normal` | 1.5 |
| `type-body-sm` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-sm` | 14px / 0.875rem |
| | Weight | → `font-weight-regular` | 400 |
| | Line Height | → `line-height-relaxed` | 1.65 |

---

### Label

Short UI text — buttons, form labels, navigation items, tabs. Never wraps to multiple lines.

| Role | Property | Primitive | Value |
|------|----------|-----------|-------|
| `type-label-lg` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-lg` | 18px / 1.125rem |
| | Weight | → `font-weight-semibold` | 600 |
| | Line Height | → `line-height-normal` | 1.5 |
| `type-label` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-base` | 16px / 1rem |
| | Weight | → `font-weight-semibold` | 600 |
| | Line Height | → `line-height-normal` | 1.5 |
| `type-label-sm` | Family | → `font-family-arabic` | IBM Plex Sans Arabic |
| | Size | → `font-size-sm` | 14px / 0.875rem |
| | Weight | → `font-weight-medium` | 500 |
| | Line Height | → `line-height-normal` | 1.5 |

---

### Caption

Supplemental text — timestamps, metadata, footnotes, helper text. Always the smallest text in a layout.

| Property | Token | Primitive | Value |
|----------|-------|-----------|-------|
| Family | `type-caption-family` | → `font-family-arabic` | IBM Plex Sans Arabic |
| Size | `type-caption-size` | → `font-size-xs` | 12px / 0.75rem |
| Weight | `type-caption-weight` | → `font-weight-regular` | 400 |
| Line Height | `type-caption-line-height` | → `line-height-loose` | 1.8 |

---

### Overline

Short category or section labels placed above headings. Always uppercase.

| Property | Token | Primitive | Value |
|----------|-------|-----------|-------|
| Family | `type-overline-family` | → `font-family-arabic` | IBM Plex Sans Arabic |
| Size | `type-overline-size` | → `font-size-xs` | 12px / 0.75rem |
| Weight | `type-overline-weight` | → `font-weight-semibold` | 600 |
| Line Height | `type-overline-line-height` | → `line-height-normal` | 1.5 |

> Overline is always rendered uppercase via `text-transform: uppercase` in CSS. This is applied at the component level, not in the token.

---

## Quick Reference

| Role | Size | Weight | Line Height | Used For |
|------|------|--------|-------------|----------|
| `type-display` | 72px | Bold | 1.2 | Hero / marketing headlines |
| `type-heading-1` | 56px | Bold | 1.2 | Page titles |
| `type-heading-2` | 48px | Bold | 1.2 | Section titles |
| `type-heading-3` | 40px | Semibold | 1.35 | Subsection titles |
| `type-heading-4` | 36px | Semibold | 1.35 | Card / panel titles |
| `type-heading-5` | 32px | Medium | 1.5 | Widget titles |
| `type-body-lg` | 20px | Regular | 1.5 | Large body copy |
| `type-body` | 16px | Regular | 1.5 | Default body copy |
| `type-body-sm` | 14px | Regular | 1.65 | Small body copy |
| `type-label-lg` | 18px | Semibold | 1.5 | Large buttons, nav |
| `type-label` | 16px | Semibold | 1.5 | Buttons, form labels |
| `type-label-sm` | 14px | Medium | 1.5 | Chips, badges, small buttons |
| `type-caption` | 12px | Regular | 1.8 | Timestamps, metadata |
| `type-overline` | 12px | Semibold | 1.5 | Section labels (uppercase) |

> Sizes shown are **desktop (xl ≥ 1280px)** values. See **Responsive Scale** below for all breakpoints.

---

## Responsive Scale

Only display, heading, and body-lg roles change size across breakpoints. Body, label, caption, and overline remain fixed at all viewport sizes — they are small enough that scaling adds no readability benefit.

| Role | xs — Mobile (base) | md — Tablet ≥ 768px | xl — Desktop ≥ 1280px |
|------|-------------------|---------------------|----------------------|
| `type-display` | `font-size-5xl` — 36px | `font-size-7xl` — 48px | `font-size-10xl` — 72px |
| `type-heading-1` | `font-size-3xl` — 30px | `font-size-6xl` — 40px | `font-size-8xl` — 56px |
| `type-heading-2` | `font-size-2xl` — 24px | `font-size-4xl` — 32px | `font-size-7xl` — 48px |
| `type-heading-3` | `font-size-xl` — 20px | `font-size-3xl` — 30px | `font-size-6xl` — 40px |
| `type-heading-4` | `font-size-lg` — 18px | `font-size-2xl` — 24px | `font-size-5xl` — 36px |
| `type-heading-5` | `font-size-base` — 16px | `font-size-xl` — 20px | `font-size-4xl` — 32px |
| `type-body-lg` | `font-size-base` — 16px | `font-size-lg` — 18px | `font-size-xl` — 20px |
| `type-body` | `font-size-base` — 16px | same | same |
| `type-body-sm` | `font-size-sm` — 14px | same | same |
| `type-label-lg` | `font-size-lg` — 18px | same | same |
| `type-label` | `font-size-base` — 16px | same | same |
| `type-label-sm` | `font-size-sm` — 14px | same | same |
| `type-caption` | `font-size-xs` — 12px | same | same |
| `type-overline` | `font-size-xs` — 12px | same | same |

---

## CSS Custom Properties

```css
:root {
  /* ── Display ─────────────────────────────────────────── */
  --type-display-family:      var(--font-family-display);
  --type-display-size:        var(--font-size-5xl);    /* 36px — mobile base */
  --type-display-weight:      var(--font-weight-bold);
  --type-display-line-height: var(--line-height-tight);

  /* ── Heading 1 ───────────────────────────────────────── */
  --type-heading-1-family:      var(--font-family-arabic);
  --type-heading-1-size:        var(--font-size-3xl);  /* 30px — mobile base */
  --type-heading-1-weight:      var(--font-weight-bold);
  --type-heading-1-line-height: var(--line-height-tight);

  /* ── Heading 2 ───────────────────────────────────────── */
  --type-heading-2-family:      var(--font-family-arabic);
  --type-heading-2-size:        var(--font-size-2xl);  /* 24px — mobile base */
  --type-heading-2-weight:      var(--font-weight-bold);
  --type-heading-2-line-height: var(--line-height-tight);

  /* ── Heading 3 ───────────────────────────────────────── */
  --type-heading-3-family:      var(--font-family-arabic);
  --type-heading-3-size:        var(--font-size-xl);   /* 20px — mobile base */
  --type-heading-3-weight:      var(--font-weight-semibold);
  --type-heading-3-line-height: var(--line-height-snug);

  /* ── Heading 4 ───────────────────────────────────────── */
  --type-heading-4-family:      var(--font-family-arabic);
  --type-heading-4-size:        var(--font-size-lg);   /* 18px — mobile base */
  --type-heading-4-weight:      var(--font-weight-semibold);
  --type-heading-4-line-height: var(--line-height-snug);

  /* ── Heading 5 ───────────────────────────────────────── */
  --type-heading-5-family:      var(--font-family-arabic);
  --type-heading-5-size:        var(--font-size-base); /* 16px — mobile base */
  --type-heading-5-weight:      var(--font-weight-medium);
  --type-heading-5-line-height: var(--line-height-normal);

  /* ── Body Large ──────────────────────────────────────── */
  --type-body-lg-family:      var(--font-family-arabic);
  --type-body-lg-size:        var(--font-size-base);   /* 16px — mobile base */
  --type-body-lg-weight:      var(--font-weight-regular);
  --type-body-lg-line-height: var(--line-height-normal);

  /* ── Body ────────────────────────────────────────────── */
  --type-body-family:      var(--font-family-arabic);
  --type-body-size:        var(--font-size-base);
  --type-body-weight:      var(--font-weight-regular);
  --type-body-line-height: var(--line-height-normal);

  /* ── Body Small ──────────────────────────────────────── */
  --type-body-sm-family:      var(--font-family-arabic);
  --type-body-sm-size:        var(--font-size-sm);
  --type-body-sm-weight:      var(--font-weight-regular);
  --type-body-sm-line-height: var(--line-height-relaxed);

  /* ── Label Large ─────────────────────────────────────── */
  --type-label-lg-family:      var(--font-family-arabic);
  --type-label-lg-size:        var(--font-size-lg);
  --type-label-lg-weight:      var(--font-weight-semibold);
  --type-label-lg-line-height: var(--line-height-normal);

  /* ── Label ───────────────────────────────────────────── */
  --type-label-family:      var(--font-family-arabic);
  --type-label-size:        var(--font-size-base);
  --type-label-weight:      var(--font-weight-semibold);
  --type-label-line-height: var(--line-height-normal);

  /* ── Label Small ─────────────────────────────────────── */
  --type-label-sm-family:      var(--font-family-arabic);
  --type-label-sm-size:        var(--font-size-sm);
  --type-label-sm-weight:      var(--font-weight-medium);
  --type-label-sm-line-height: var(--line-height-normal);

  /* ── Caption ─────────────────────────────────────────── */
  --type-caption-family:      var(--font-family-arabic);
  --type-caption-size:        var(--font-size-xs);
  --type-caption-weight:      var(--font-weight-regular);
  --type-caption-line-height: var(--line-height-loose);

  /* ── Overline ────────────────────────────────────────── */
  --type-overline-family:      var(--font-family-arabic);
  --type-overline-size:        var(--font-size-xs);
  --type-overline-weight:      var(--font-weight-semibold);
  --type-overline-line-height: var(--line-height-normal);
}

/* ── md — Tablet ≥ 768px ────────────────────────────────── */
@media (min-width: 768px) {
  :root {
    --type-display-size:   var(--font-size-7xl);  /* 48px */
    --type-heading-1-size: var(--font-size-6xl);  /* 40px */
    --type-heading-2-size: var(--font-size-4xl);  /* 32px */
    --type-heading-3-size: var(--font-size-3xl);  /* 30px */
    --type-heading-4-size: var(--font-size-2xl);  /* 24px */
    --type-heading-5-size: var(--font-size-xl);   /* 20px */
    --type-body-lg-size:   var(--font-size-lg);   /* 18px */
  }
}

/* ── xl — Desktop ≥ 1280px ──────────────────────────────── */
@media (min-width: 1280px) {
  :root {
    --type-display-size:   var(--font-size-10xl); /* 72px */
    --type-heading-1-size: var(--font-size-8xl);  /* 56px */
    --type-heading-2-size: var(--font-size-7xl);  /* 48px */
    --type-heading-3-size: var(--font-size-6xl);  /* 40px */
    --type-heading-4-size: var(--font-size-5xl);  /* 36px */
    --type-heading-5-size: var(--font-size-4xl);  /* 32px */
    --type-body-lg-size:   var(--font-size-xl);   /* 20px */
  }
}
```

### Usage Pattern

```css
.page-title {
  font-family:   var(--type-heading-1-family);
  font-size:     var(--type-heading-1-size);
  font-weight:   var(--type-heading-1-weight);
  line-height:   var(--type-heading-1-line-height);
}

.btn-label {
  font-family:   var(--type-label-family);
  font-size:     var(--type-label-size);
  font-weight:   var(--type-label-weight);
  line-height:   var(--type-label-line-height);
}
```

---

## Figma Text Styles

> **Collection:** `Semantic/Typography` — Create as Text Styles in Figma, not variables.

| Style Name | Family | Size | Weight | Line Height |
|------------|--------|------|--------|-------------|
| `type/display` | IBM Plex Sans Arabic | 72 | Bold (700) | 1.2 |
| `type/heading-1` | IBM Plex Sans Arabic | 56 | Bold (700) | 1.2 |
| `type/heading-2` | IBM Plex Sans Arabic | 48 | Bold (700) | 1.2 |
| `type/heading-3` | IBM Plex Sans Arabic | 40 | SemiBold (600) | 1.35 |
| `type/heading-4` | IBM Plex Sans Arabic | 36 | SemiBold (600) | 1.35 |
| `type/heading-5` | IBM Plex Sans Arabic | 32 | Medium (500) | 1.5 |
| `type/body-lg` | IBM Plex Sans Arabic | 20 | Regular (400) | 1.5 |
| `type/body` | IBM Plex Sans Arabic | 16 | Regular (400) | 1.5 |
| `type/body-sm` | IBM Plex Sans Arabic | 14 | Regular (400) | 1.65 |
| `type/label-lg` | IBM Plex Sans Arabic | 18 | SemiBold (600) | 1.5 |
| `type/label` | IBM Plex Sans Arabic | 16 | SemiBold (600) | 1.5 |
| `type/label-sm` | IBM Plex Sans Arabic | 14 | Medium (500) | 1.5 |
| `type/caption` | IBM Plex Sans Arabic | 12 | Regular (400) | 1.8 |
| `type/overline` | IBM Plex Sans Arabic | 12 | SemiBold (600) | 1.5 |
