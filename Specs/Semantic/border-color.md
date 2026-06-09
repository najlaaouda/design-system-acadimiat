---
name: Border Color Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Border Color — Semantic Tokens

## Philosophy

Border color tokens define the color of strokes, dividers, and focus rings. They ensure that boundaries and interactive affordances remain clear and accessible across both themes. The `border-color-focus` token is especially critical — it must always be visible against any background to meet WCAG 2.4.11 focus appearance requirements.

> **Use these tokens on all borders, outlines, dividers, and focus rings.**
> Never reference Primitive Tokens directly in components.

---

## How to Read This File

### Naming Pattern

```
border-color-[role]
```

| Segment | Meaning |
|---------|---------|
| `border` | Applied to borders, outlines, dividers, separators, and focus rings |
| `color` | Indicates this is a color token |
| `role` | The semantic purpose — `primary`, `brand`, `focus`, `error`, etc. |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Color.md`.

### Theme Architecture

Set `data-theme` on the root element. Adding a new theme requires only a new CSS block — token names never change.

```html
<html data-theme="light"> ... </html>
<html data-theme="dark"> ... </html>
```

---

## Tokens

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `border-color-primary` | → `neutral-200` | → `white-alpha-20` | Default borders — inputs, cards, dividers |
| `border-color-secondary` | → `neutral-100` | → `white-alpha-10` | Subtle separators, de-emphasized borders |
| `border-color-strong` | → `neutral-500` | → `white-alpha-60` | High-emphasis borders, selected outlines |
| `border-color-brand` | → `purple-500` | → `purple-400` | Selected / active state borders |
| `border-color-focus` | → `purple-500` | → `purple-300` | Keyboard focus ring |
| `border-color-disabled` | → `neutral-200` | → `white-alpha-10` | Disabled input or element borders |
| `border-color-success` | → `green-500` | → `green-400` | Success state borders |
| `border-color-warning` | → `yellow-500` | → `yellow-400` | Warning state borders |
| `border-color-error` | → `red-500` | → `red-400` | Error / invalid state borders |
| `border-color-info` | → `blue-500` | → `blue-400` | Info state borders |

---

## CSS Custom Properties

```css
/* ─── Light Theme ────────────────────────────────────────── */
:root,
[data-theme="light"] {
  --border-color-primary:   var(--neutral-200);
  --border-color-secondary: var(--neutral-100);
  --border-color-strong:    var(--neutral-500);
  --border-color-brand:     var(--purple-500);
  --border-color-focus:     var(--purple-500);
  --border-color-disabled:  var(--neutral-200);
  --border-color-success:   var(--green-500);
  --border-color-warning:   var(--yellow-500);
  --border-color-error:     var(--red-500);
  --border-color-info:      var(--blue-500);
}

/* ─── Dark Theme ─────────────────────────────────────────── */
[data-theme="dark"] {
  --border-color-primary:   var(--white-alpha-20);
  --border-color-secondary: var(--white-alpha-10);
  --border-color-strong:    var(--white-alpha-60);
  --border-color-brand:     var(--purple-400);
  --border-color-focus:     var(--purple-300);
  --border-color-disabled:  var(--white-alpha-10);
  --border-color-success:   var(--green-400);
  --border-color-warning:   var(--yellow-400);
  --border-color-error:     var(--red-400);
  --border-color-info:      var(--blue-400);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Border Color`

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `border/primary` | `primitive/neutral-200` | `primitive/white-alpha-20` | Stroke color |
| `border/secondary` | `primitive/neutral-100` | `primitive/white-alpha-10` | Stroke color |
| `border/strong` | `primitive/neutral-500` | `primitive/white-alpha-60` | Stroke color |
| `border/brand` | `primitive/purple-500` | `primitive/purple-400` | Stroke color |
| `border/focus` | `primitive/purple-500` | `primitive/purple-300` | Stroke color |
| `border/disabled` | `primitive/neutral-200` | `primitive/white-alpha-10` | Stroke color |
| `border/success` | `primitive/green-500` | `primitive/green-400` | Stroke color |
| `border/warning` | `primitive/yellow-500` | `primitive/yellow-400` | Stroke color |
| `border/error` | `primitive/red-500` | `primitive/red-400` | Stroke color |
| `border/info` | `primitive/blue-500` | `primitive/blue-400` | Stroke color |
