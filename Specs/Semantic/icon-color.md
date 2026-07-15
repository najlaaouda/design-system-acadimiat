---
name: Icon Color Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-07-07
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Icon Color — Semantic Tokens

## Philosophy

Icon color tokens define the fill of SVG icons based on their purpose in the interface. The role vocabulary intentionally mirrors text color tokens — `primary`, `secondary`, `brand`, `on-brand`, status roles — making it straightforward to pair an icon with its adjacent label using the same semantic role without guesswork.

> **Use these tokens on all SVG icon fills and decorative graphic elements.**
> Never reference Primitive Tokens directly in components.

---

## How to Read This File

### Naming Pattern

```
icon-color-[role]
```

| Segment | Meaning |
|---------|---------|
| `icon` | Applied to SVG icons, icon buttons, and decorative graphic elements |
| `color` | Indicates this is a color token |
| `role` | The semantic purpose — `primary`, `brand`, `on-brand`, `error`, etc. |

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
| `icon-color-primary` | → `neutral-700` | → `white-alpha-90` | Default icon color |
| `icon-color-secondary` | → `neutral-400` | → `white-alpha-60` | Secondary / supporting icons |
| `icon-color-tertiary` | → `neutral-300` | → `white-alpha-40` | Decorative or low-priority icons |
| `icon-color-disabled` | → `neutral-300` | → `white-alpha-30` | Disabled icon state |
| `icon-color-brand` | → `purple-500` | → `purple-300` | Brand-colored icons — active nav, highlights |
| `icon-color-on-brand` | → `base-white` | → `base-white` | Icons on top of a brand-colored background |
| `icon-color-on-error` | → `base-white` | → `base-white` | Icons on top of an error/destructive-colored background |
| `icon-color-success` | → `green-500` | → `green-400` | Success state icons |
| `icon-color-warning` | → `yellow-500` | → `yellow-400` | Warning state icons |
| `icon-color-error` | → `red-500` | → `red-400` | Error state icons |
| `icon-color-info` | → `blue-500` | → `blue-400` | Info state icons |

---

## CSS Custom Properties

```css
/* ─── Light Theme ────────────────────────────────────────── */
:root,
[data-theme="light"] {
  --icon-color-primary:   var(--neutral-700);
  --icon-color-secondary: var(--neutral-400);
  --icon-color-tertiary:  var(--neutral-300);
  --icon-color-disabled:  var(--neutral-300);
  --icon-color-brand:     var(--purple-500);
  --icon-color-on-brand:  var(--base-white);
  --icon-color-on-error:  var(--base-white);
  --icon-color-success:   var(--green-500);
  --icon-color-warning:   var(--yellow-500);
  --icon-color-error:     var(--red-500);
  --icon-color-info:      var(--blue-500);
}

/* ─── Dark Theme ─────────────────────────────────────────── */
[data-theme="dark"] {
  --icon-color-primary:   var(--white-alpha-90);
  --icon-color-secondary: var(--white-alpha-60);
  --icon-color-tertiary:  var(--white-alpha-40);
  --icon-color-disabled:  var(--white-alpha-30);
  --icon-color-brand:     var(--purple-300);
  --icon-color-on-brand:  var(--base-white);
  --icon-color-on-error:  var(--base-white);
  --icon-color-success:   var(--green-400);
  --icon-color-warning:   var(--yellow-400);
  --icon-color-error:     var(--red-400);
  --icon-color-info:      var(--blue-400);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Icon Color`

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `icon/primary` | `primitive/neutral-700` | `primitive/white-alpha-90` | Fill color |
| `icon/secondary` | `primitive/neutral-400` | `primitive/white-alpha-60` | Fill color |
| `icon/tertiary` | `primitive/neutral-300` | `primitive/white-alpha-40` | Fill color |
| `icon/disabled` | `primitive/neutral-300` | `primitive/white-alpha-30` | Fill color |
| `icon/brand` | `primitive/purple-500` | `primitive/purple-300` | Fill color |
| `icon/on-brand` | `primitive/base-white` | `primitive/base-white` | Fill color |
| `icon/on-error` | `primitive/base-white` | `primitive/base-white` | Fill color |
| `icon/success` | `primitive/green-500` | `primitive/green-400` | Fill color |
| `icon/warning` | `primitive/yellow-500` | `primitive/yellow-400` | Fill color |
| `icon/error` | `primitive/red-500` | `primitive/red-400` | Fill color |
| `icon/info` | `primitive/blue-500` | `primitive/blue-400` | Fill color |
