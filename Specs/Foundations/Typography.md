---
name: Typography Primitives
tier: Primitive
status: Active
last-updated: 2026-06-07
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Typography System — Primitive Tokens

## Philosophy

Acadimiat's typography reflects elegance and sophistication. These are **Primitive Tokens** — raw typographic values used to build Semantic Tokens. Applied consistently across all Acadimiat products: landing pages, dashboards, websites, and mobile apps. The system is RTL-first with Arabic as the primary language.

> **Important — Do not use these tokens directly in components.**
> Always use Semantic Tokens in code and design.

---

## Font Families

### Primary — Arabic

| Token | Value | Usage |
|-------|-------|-------|
| `font-family-arabic` | `'IBM Plex Sans Arabic', sans-serif` | Primary Arabic body and UI text |
| `font-family-arabic-alt` | `'Readex Pro', sans-serif` | Alternative for dashboard-heavy interfaces |

### Optional — Latin (English)

| Token | Value | Usage |
|-------|-------|-------|
| `font-family-latin` | `'Inter', system-ui, sans-serif` | English body and UI text |

### Display — Large Headings

| Token | Value | Usage |
|-------|-------|-------|
| `font-family-display` | `'IBM Plex Sans Arabic', sans-serif` | Default display headings — dashboard, app UI |
| `font-family-display-landing` | `'El Messiri', sans-serif` | Landing page hero and section headings |

> **Note:** `font-family-display` is the default. On the landing page, `--font-family-display` is overridden to `El Messiri` via the `[data-product="landing"]` theme block — token names never change, only the resolved value.

---

## Font Weights

| Token | Value | Name |
|-------|-------|------|
| `font-weight-regular` | `400` | Regular |
| `font-weight-display` | `480` | Display — El Messiri variable font only |
| `font-weight-medium` | `500` | Medium |
| `font-weight-semibold` | `600` | Semibold |
| `font-weight-bold` | `700` | Bold |

> `font-weight-display` (480) is a variable font axis value. It is only valid with El Messiri — do not apply it to IBM Plex Sans Arabic or Inter.

---

## Font Sizes

Base: **16px** — Curated scale optimized for Arabic UI readability.

| Token | px | rem |
|-------|----|-----|
| `font-size-xs` | `12px` | `0.75rem` |
| `font-size-sm` | `14px` | `0.875rem` |
| `font-size-base` | `16px` | `1rem` |
| `font-size-lg` | `18px` | `1.125rem` |
| `font-size-xl` | `20px` | `1.25rem` |
| `font-size-2xl` | `24px` | `1.5rem` |
| `font-size-3xl` | `30px` | `1.875rem` |
| `font-size-4xl` | `32px` | `2rem` |
| `font-size-5xl` | `36px` | `2.25rem` |
| `font-size-6xl` | `40px` | `2.5rem` |
| `font-size-7xl` | `48px` | `3rem` |
| `font-size-8xl` | `56px` | `3.5rem` |
| `font-size-9xl` | `60px` | `3.75rem` |
| `font-size-10xl` | `72px` | `4.5rem` |

---

## Line Heights

Range: **1.2 – 2.0**

| Token | Value | Usage |
|-------|-------|-------|
| `line-height-tight` | `1.2` | Display headings, large text |
| `line-height-snug` | `1.35` | Subheadings |
| `line-height-normal` | `1.5` | Body text (default) |
| `line-height-relaxed` | `1.65` | Long-form readable content |
| `line-height-loose` | `1.8` | Small text, captions |
| `line-height-spacious` | `2.0` | High-readability contexts |

---

## Paragraph Spacing

| Token | Value |
|-------|-------|
| `paragraph-spacing-1` | `8px` |
| `paragraph-spacing-2` | `10px` |
| `paragraph-spacing-3` | `12px` |
| `paragraph-spacing-4` | `14px` |
| `paragraph-spacing-5` | `16px` |
| `paragraph-spacing-6` | `18px` |
| `paragraph-spacing-7` | `20px` |
| `paragraph-spacing-8` | `24px` |
| `paragraph-spacing-9` | `28px` |
| `paragraph-spacing-10` | `30px` |
| `paragraph-spacing-11` | `32px` |
| `paragraph-spacing-12` | `36px` |
| `paragraph-spacing-13` | `38px` |
| `paragraph-spacing-14` | `40px` |
| `paragraph-spacing-15` | `46px` |

---

## CSS Custom Properties

```css
:root {
  /* Font Families */
  --font-family-arabic:           'IBM Plex Sans Arabic', sans-serif;
  --font-family-arabic-alt:       'Readex Pro', sans-serif;
  --font-family-latin:            'Inter', system-ui, sans-serif;
  --font-family-display:          'IBM Plex Sans Arabic', sans-serif; /* default */
  --font-family-display-landing:  'El Messiri', sans-serif;

  /* Font Weights */
  --font-weight-regular:  400;
  --font-weight-display:  480; /* El Messiri variable font only */
  --font-weight-medium:   500;
  --font-weight-semibold: 600;
  --font-weight-bold:     700;

  /* Font Sizes */
  --font-size-xs:   0.75rem;    /* 12px */
  --font-size-sm:   0.875rem;   /* 14px */
  --font-size-base: 1rem;       /* 16px */
  --font-size-lg:   1.125rem;   /* 18px */
  --font-size-xl:   1.25rem;    /* 20px */
  --font-size-2xl:  1.5rem;     /* 24px */
  --font-size-3xl:  1.875rem;   /* 30px */
  --font-size-4xl:  2rem;       /* 32px */
  --font-size-5xl:  2.25rem;    /* 36px */
  --font-size-6xl:  2.5rem;     /* 40px */
  --font-size-7xl:  3rem;       /* 48px */
  --font-size-8xl:  3.5rem;     /* 56px */
  --font-size-9xl:  3.75rem;    /* 60px */
  --font-size-10xl: 4.5rem;     /* 72px */

  /* Line Heights */
  --line-height-tight:    1.2;
  --line-height-snug:     1.35;
  --line-height-normal:   1.5;
  --line-height-relaxed:  1.65;
  --line-height-loose:    1.8;
  --line-height-spacious: 2.0;

  /* Paragraph Spacing */
  --paragraph-spacing-1:  8px;
  --paragraph-spacing-2:  10px;
  --paragraph-spacing-3:  12px;
  --paragraph-spacing-4:  14px;
  --paragraph-spacing-5:  16px;
  --paragraph-spacing-6:  18px;
  --paragraph-spacing-7:  20px;
  --paragraph-spacing-8:  24px;
  --paragraph-spacing-9:  28px;
  --paragraph-spacing-10: 30px;
  --paragraph-spacing-11: 32px;
  --paragraph-spacing-12: 36px;
  --paragraph-spacing-13: 38px;
  --paragraph-spacing-14: 40px;
  --paragraph-spacing-15: 46px;
}
```

---

## Type Scale Reference

| Role | Size Token | px | Weight Token | Line Height Token |
|------|------------|----|--------------|-------------------|
| Display | `font-size-10xl` | 72px | `font-weight-bold` | `line-height-tight` |
| Heading 1 | `font-size-8xl` | 56px | `font-weight-bold` | `line-height-tight` |
| Heading 2 | `font-size-7xl` | 48px | `font-weight-bold` | `line-height-tight` |
| Heading 3 | `font-size-6xl` | 40px | `font-weight-semibold` | `line-height-snug` |
| Heading 4 | `font-size-5xl` | 36px | `font-weight-semibold` | `line-height-snug` |
| Heading 5 | `font-size-4xl` | 32px | `font-weight-medium` | `line-height-normal` |
| Body Large | `font-size-xl` | 20px | `font-weight-regular` | `line-height-normal` |
| Body | `font-size-base` | 16px | `font-weight-regular` | `line-height-normal` |
| Body Small | `font-size-sm` | 14px | `font-weight-regular` | `line-height-relaxed` |
| Caption | `font-size-xs` | 12px | `font-weight-regular` | `line-height-loose` |

---

## Notes

- All tokens are primitives — do not apply directly to components
- RTL is the default direction; Arabic font stack takes priority
- Latin font stack is optional — applied only when English content is present
- Display font can be swapped per product line at the theme level without changing token names
- Semantic typography tokens (e.g., `--app-text-heading`, `--app-text-body`) are defined in the Semantic layer
- No `letter-spacing` for Arabic text — ever
- El Messiri is loaded as a variable font from Google Fonts — request the full weight axis range:
  ```html
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=El+Messiri:wght@400..700&display=swap">
  ```
- `font-weight-display` (480) is only valid with El Messiri — variable axis value between Regular and Medium
