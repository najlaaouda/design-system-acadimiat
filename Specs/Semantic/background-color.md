---
name: Background Color Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Background Color — Semantic Tokens

## Philosophy

Background color tokens define the fill of surfaces — from the main page background to cards, overlays, and interactive states. They establish the **visual depth hierarchy** of the interface and ensure surfaces remain distinguishable across both Light and Dark themes.

> **Use these tokens on all background and surface fills.**
> Never reference Primitive Tokens directly in components.

---

## How to Read This File

### Naming Pattern

```
bg-color-[role]
```

| Segment | Meaning |
|---------|---------|
| `bg` | Applied to background fills — page, card, panel, modal, badge, overlay |
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
| `bg-color-primary` | → `base-white` | → `neutral-900` | Main app / page background |
| `bg-color-secondary` | → `neutral-50` | → `neutral-800` | Cards, sidebars, panels |
| `bg-color-tertiary` | → `neutral-100` | → `neutral-700` | Nested surfaces, input fills, code blocks |
| `bg-color-disabled` | → `neutral-100` | → `neutral-700` | Disabled input or button backgrounds |
| `bg-color-overlay` | `rgba(13, 8, 18, 0.60)` | `rgba(13, 8, 18, 0.80)` | Modal / drawer backdrop overlay |
| `bg-color-brand` | → `purple-500` | → `purple-500` | Primary buttons, active highlights, CTAs |
| `bg-color-brand-subtle` | → `purple-50` | → `purple-900` | Chips, tags, soft brand-tinted backgrounds |
| `bg-color-brand-hover` | → `purple-600` | → `purple-600` | Hover state on brand backgrounds |
| `bg-color-brand-pressed` | → `purple-700` | → `purple-700` | Pressed / active state on brand backgrounds |
| `bg-color-success` | → `green-50` | → `green-900` | Success alert backgrounds, toasts |
| `bg-color-warning` | → `yellow-50` | → `yellow-900` | Warning alert backgrounds |
| `bg-color-error` | → `red-50` | → `red-900` | Error alert backgrounds, field error fills |
| `bg-color-info` | → `blue-50` | → `blue-900` | Info alert backgrounds |

---

## CSS Custom Properties

```css
/* ─── Light Theme ────────────────────────────────────────── */
:root,
[data-theme="light"] {
  --bg-color-primary:        var(--base-white);
  --bg-color-secondary:      var(--neutral-50);
  --bg-color-tertiary:       var(--neutral-100);
  --bg-color-disabled:       var(--neutral-100);
  --bg-color-overlay:        rgba(13, 8, 18, 0.60);
  --bg-color-brand:          var(--purple-500);
  --bg-color-brand-subtle:   var(--purple-50);
  --bg-color-brand-hover:    var(--purple-600);
  --bg-color-brand-pressed:  var(--purple-700);
  --bg-color-success:        var(--green-50);
  --bg-color-warning:        var(--yellow-50);
  --bg-color-error:          var(--red-50);
  --bg-color-info:           var(--blue-50);
}

/* ─── Dark Theme ─────────────────────────────────────────── */
[data-theme="dark"] {
  --bg-color-primary:        var(--neutral-900);
  --bg-color-secondary:      var(--neutral-800);
  --bg-color-tertiary:       var(--neutral-700);
  --bg-color-disabled:       var(--neutral-700);
  --bg-color-overlay:        rgba(13, 8, 18, 0.80);
  --bg-color-brand:          var(--purple-500);
  --bg-color-brand-subtle:   var(--purple-900);
  --bg-color-brand-hover:    var(--purple-600);
  --bg-color-brand-pressed:  var(--purple-700);
  --bg-color-success:        var(--green-900);
  --bg-color-warning:        var(--yellow-900);
  --bg-color-error:          var(--red-900);
  --bg-color-info:           var(--blue-900);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Background Color`

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `bg/primary` | `primitive/base-white` | `primitive/neutral-900` | Fill color |
| `bg/secondary` | `primitive/neutral-50` | `primitive/neutral-800` | Fill color |
| `bg/tertiary` | `primitive/neutral-100` | `primitive/neutral-700` | Fill color |
| `bg/disabled` | `primitive/neutral-100` | `primitive/neutral-700` | Fill color |
| `bg/overlay` | `rgba(13, 8, 18, 0.60)` | `rgba(13, 8, 18, 0.80)` | Fill color |
| `bg/brand` | `primitive/purple-500` | `primitive/purple-500` | Fill color |
| `bg/brand-subtle` | `primitive/purple-50` | `primitive/purple-900` | Fill color |
| `bg/brand-hover` | `primitive/purple-600` | `primitive/purple-600` | Fill color |
| `bg/brand-pressed` | `primitive/purple-700` | `primitive/purple-700` | Fill color |
| `bg/success` | `primitive/green-50` | `primitive/green-900` | Fill color |
| `bg/warning` | `primitive/yellow-50` | `primitive/yellow-900` | Fill color |
| `bg/error` | `primitive/red-50` | `primitive/red-900` | Fill color |
| `bg/info` | `primitive/blue-50` | `primitive/blue-900` | Fill color |
