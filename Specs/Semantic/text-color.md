---
name: Text Color Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-07-07
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Text Color — Semantic Tokens

## Philosophy

Text color tokens define the color of typographic elements based on their **role in the interface**, not their visual appearance. A developer or designer never asks "which neutral shade goes here?" — instead they ask "is this primary text, secondary text, or a brand link?" These tokens answer that question and adapt automatically between Light and Dark themes.

> **Use these tokens on all text and typographic elements.**
> Never reference Primitive Tokens directly in components.

---

## How to Read This File

### Naming Pattern

```
text-color-[role]
```

| Segment | Meaning |
|---------|---------|
| `text` | Applied to any typographic element — headings, body, labels, captions, links |
| `color` | Indicates this is a color token |
| `role` | The semantic purpose — `primary`, `brand`, `error`, etc. |

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
| `text-color-primary` | → `neutral-900` | → `base-white` | Main body text, headings |
| `text-color-secondary` | → `neutral-500` | → `white-alpha-70` | Subtitles, descriptions, supporting copy |
| `text-color-tertiary` | → `neutral-400` | → `white-alpha-50` | Captions, timestamps, metadata |
| `text-color-placeholder` | → `neutral-400` | → `white-alpha-40` | Input placeholder text |
| `text-color-disabled` | → `neutral-300` | → `white-alpha-30` | Disabled labels and text |
| `text-color-inverse` | → `base-white` | → `neutral-900` | Text on dark/filled surfaces (e.g., tooltips) |
| `text-color-brand` | → `purple-500` | → `purple-300` | Links, active nav items, brand emphasis |
| `text-color-on-brand` | → `base-white` | → `base-white` | Text sitting on a brand-colored background |
| `text-color-on-error` | → `base-white` | → `base-white` | Text sitting on an error/destructive-colored background |
| `text-color-success` | → `green-700` | → `green-400` | Success messages, confirmation text |
| `text-color-warning` | → `yellow-700` | → `yellow-400` | Warning messages, caution labels |
| `text-color-error` | → `red-700` | → `red-400` | Error messages, validation feedback |
| `text-color-info` | → `blue-700` | → `blue-400` | Informational messages, hints |

---

## CSS Custom Properties

```css
/* ─── Light Theme ────────────────────────────────────────── */
:root,
[data-theme="light"] {
  --text-color-primary:     var(--neutral-900);
  --text-color-secondary:   var(--neutral-500);
  --text-color-tertiary:    var(--neutral-400);
  --text-color-placeholder: var(--neutral-400);
  --text-color-disabled:    var(--neutral-300);
  --text-color-inverse:     var(--base-white);
  --text-color-brand:       var(--purple-500);
  --text-color-on-brand:    var(--base-white);
  --text-color-on-error:    var(--base-white);
  --text-color-success:     var(--green-700);
  --text-color-warning:     var(--yellow-700);
  --text-color-error:       var(--red-700);
  --text-color-info:        var(--blue-700);
}

/* ─── Dark Theme ─────────────────────────────────────────── */
[data-theme="dark"] {
  --text-color-primary:     var(--base-white);
  --text-color-secondary:   var(--white-alpha-70);
  --text-color-tertiary:    var(--white-alpha-50);
  --text-color-placeholder: var(--white-alpha-40);
  --text-color-disabled:    var(--white-alpha-30);
  --text-color-inverse:     var(--neutral-900);
  --text-color-brand:       var(--purple-300);
  --text-color-on-brand:    var(--base-white);
  --text-color-on-error:    var(--base-white);
  --text-color-success:     var(--green-400);
  --text-color-warning:     var(--yellow-400);
  --text-color-error:       var(--red-400);
  --text-color-info:        var(--blue-400);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Text Color`

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `text/primary` | `primitive/neutral-900` | `primitive/base-white` | Text color |
| `text/secondary` | `primitive/neutral-500` | `primitive/white-alpha-70` | Text color |
| `text/tertiary` | `primitive/neutral-400` | `primitive/white-alpha-50` | Text color |
| `text/placeholder` | `primitive/neutral-400` | `primitive/white-alpha-40` | Text color |
| `text/disabled` | `primitive/neutral-300` | `primitive/white-alpha-30` | Text color |
| `text/inverse` | `primitive/base-white` | `primitive/neutral-900` | Text color |
| `text/brand` | `primitive/purple-500` | `primitive/purple-300` | Text color |
| `text/on-brand` | `primitive/base-white` | `primitive/base-white` | Text color |
| `text/on-error` | `primitive/base-white` | `primitive/base-white` | Text color |
| `text/success` | `primitive/green-700` | `primitive/green-400` | Text color |
| `text/warning` | `primitive/yellow-700` | `primitive/yellow-400` | Text color |
| `text/error` | `primitive/red-700` | `primitive/red-400` | Text color |
| `text/info` | `primitive/blue-700` | `primitive/blue-400` | Text color |
