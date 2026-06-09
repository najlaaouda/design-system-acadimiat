---
name: Breakpoints Primitives
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Breakpoints System — Primitive Tokens

## Philosophy

Acadimiat's breakpoint system is based on **Tailwind CSS v3** defaults. The approach is **mobile-first** — styles apply at the defined breakpoint and above. Base desktop target is **1440px**. The system is fully RTL-compatible using logical CSS properties throughout.

> **Mobile-first:** Write base styles for mobile, then override with breakpoint prefixes for larger screens.

---

## Breakpoint Scale

| Token | Min-Width | Target Device |
|-------|-----------|---------------|
| `screen-xs` | `0px` | Mobile (base — no prefix needed) |
| `screen-sm` | `640px` | Large mobile / small tablet |
| `screen-md` | `768px` | Tablet |
| `screen-lg` | `1024px` | Small desktop / laptop |
| `screen-xl` | `1280px` | Desktop |
| `screen-2xl` | `1536px` | Large desktop / widescreen |

> **Base desktop width:** `1440px` — all desktop designs are produced at this width and scale down responsively.

---

## Container Widths

Max-width containers centered per breakpoint. All containers include horizontal padding.

| Breakpoint | Max-Width | Inline Padding |
|------------|-----------|----------------|
| `xs` (base) | `100%` | `16px` |
| `sm` ≥ 640px | `640px` | `24px` |
| `md` ≥ 768px | `768px` | `32px` |
| `lg` ≥ 1024px | `1024px` | `40px` |
| `xl` ≥ 1280px | `1280px` | `48px` |
| `2xl` ≥ 1536px | `1440px` | `48px` |

> **Note:** At `2xl`, the container is capped at `1440px` regardless of viewport width.

---

## CSS Custom Properties

```css
:root {
  /* Breakpoint values */
  --screen-sm:  640px;
  --screen-md:  768px;
  --screen-lg:  1024px;
  --screen-xl:  1280px;
  --screen-2xl: 1536px;

  /* Container max-widths */
  --container-sm:      640px;
  --container-md:      768px;
  --container-lg:      1024px;
  --container-xl:      1280px;
  --container-2xl:     1440px;
  --container-max:     1440px;

  /* Container padding (inline) */
  --container-padding-xs:  16px;
  --container-padding-sm:  24px;
  --container-padding-md:  32px;
  --container-padding-lg:  40px;
  --container-padding-xl:  48px;
  --container-padding-2xl: 48px;
}
```

---

## Media Query Reference

```css
/* sm — ≥ 640px */
@media (min-width: 640px) { }

/* md — ≥ 768px */
@media (min-width: 768px) { }

/* lg — ≥ 1024px */
@media (min-width: 1024px) { }

/* xl — ≥ 1280px */
@media (min-width: 1280px) { }

/* 2xl — ≥ 1536px */
@media (min-width: 1536px) { }

/* Max container cap */
@media (min-width: 1440px) {
  .container { max-width: 1440px; }
}
```

---

## Container Base CSS

```css
.container {
  width: 100%;
  margin-inline: auto;
  padding-inline: var(--container-padding-xs);
}

@media (min-width: 640px) {
  .container {
    max-width: var(--container-sm);
    padding-inline: var(--container-padding-sm);
  }
}

@media (min-width: 768px) {
  .container {
    max-width: var(--container-md);
    padding-inline: var(--container-padding-md);
  }
}

@media (min-width: 1024px) {
  .container {
    max-width: var(--container-lg);
    padding-inline: var(--container-padding-lg);
  }
}

@media (min-width: 1280px) {
  .container {
    max-width: var(--container-xl);
    padding-inline: var(--container-padding-xl);
  }
}

@media (min-width: 1536px) {
  .container {
    max-width: var(--container-2xl);
    padding-inline: var(--container-padding-2xl);
  }
}
```

---

## Layout Columns per Breakpoint

| Breakpoint | Columns | Gap |
|------------|---------|-----|
| `xs` | 4 | `16px` |
| `sm` | 8 | `24px` |
| `md` | 8 | `24px` |
| `lg` | 12 | `24px` |
| `xl` | 12 | `32px` |
| `2xl` | 12 | `32px` |

---

## Usage Guidelines

| Context | Breakpoint |
|---------|------------|
| Mobile navigation (hamburger) | below `lg` |
| Desktop navigation (horizontal) | `lg` and above |
| Single column layout | `xs` – `sm` |
| Two column layout | `md` and above |
| Sidebar + content layout | `lg` and above |
| Full dashboard layout | `xl` and above |
| Marketing / landing page full layout | `lg` and above |

---

## Rules

- Mobile-first always — no `max-width` media queries
- Use logical CSS properties: `padding-inline`, `margin-inline`, `inset-inline` — never `left` / `right`
- Container max-width never exceeds `1440px`
- All designs at `xs` must be fully functional — desktop is an enhancement
- Breakpoints are used for layout only — component variants use their own logic
