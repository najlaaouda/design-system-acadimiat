---
name: Icon Size Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Icon Size — Semantic Tokens

## Philosophy

Icon size tokens define how large an icon appears based on its **role in the interface**, not a raw pixel value. The system uses three primitive sizes — 16px, 20px, 24px — plus an additional 18px size for compact UI contexts. Semantic tokens decide which size applies where. Some roles scale up on larger screens where there is more visual space; others stay fixed at all breakpoints.

> **Use these tokens on all icon width and height properties.**
> Never hardcode icon sizes directly in components.

---

## How to Read This File

### Naming Pattern

```
icon-size-[role]
```

| Segment | Meaning |
|---------|---------|
| `icon` | Applied to icon elements (SVG, `lucide-icon`) |
| `size` | Indicates this is a size token — controls width and height |
| `role` | The context in which the icon appears — `inline`, `default`, `nav`, `feature` |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Icon.md`.

### Breakpoints Used

Follows the breakpoint scale from `Foundations/Breakpoints.md` — mobile-first.

| Breakpoint | Min-Width | Applied To |
|------------|-----------|-----------|
| xs (base) | 0px | Mobile |
| md | 768px | Tablet |
| xl | 1280px | Desktop |

---

## Tokens

| Token | xs — Mobile | md — Tablet ≥ 768px | xl — Desktop ≥ 1280px | Scope (Figma) | Usage |
|-------|-------------|---------------------|----------------------|---------------|-------|
| `icon-size-inline` | → `icon-sm` — 16px | same | same | Width, Height | In-text icons, badge indicators — always tight |
| `icon-size-sm` | 18px | same | same | Width, Height | Compact form fields, dense lists, small cards |
| `icon-size-default` | → `icon-md` — 20px | same | same | Width, Height | Buttons, inputs, dropdowns — default icon size |
| `icon-size-nav` | → `icon-md` — 20px | same | → `icon-lg` — 24px | Width, Height | Sidebar and top navigation icons |
| `icon-size-feature` | → `icon-lg` — 24px | same | same | Width, Height | Empty states, section headers, standalone icons |

---

## Breakpoint Behavior

| Token | Scales? | Why |
|-------|---------|-----|
| `icon-size-inline` | No | Always paired with body text — size must match line height |
| `icon-size-sm` | No | Compact contexts are consistent across all viewports |
| `icon-size-default` | No | Component-bound — button and input sizes don't change with viewport |
| `icon-size-nav` | Yes (md → xl) | Navigation has more visual space on desktop; larger icons improve scannability |
| `icon-size-feature` | No | Already the largest size in the system — no need to scale further |

---

## CSS Custom Properties

```css
/* ── Base — xs Mobile ────────────────────────────────────── */
:root {
  --icon-size-inline:  16px;
  --icon-size-sm:      18px;
    --icon-size-default: 20px;
    --icon-size-nav:     20px;
  --icon-size-feature: 24px;
}

/* ── xl — Desktop ≥ 1280px ───────────────────────────────── */
@media (min-width: 1280px) {
  :root {
    --icon-size-nav: 24px;
  }
}
```

### Usage Pattern

```css
/* Icon inside a button */
.btn .icon {
  width:  var(--icon-size-default);
  height: var(--icon-size-default);
}

/* Icon in a nav item */
.nav-item .icon {
  width:  var(--icon-size-nav);
  height: var(--icon-size-nav);
}
```

```html
<!-- Angular / Lucide — bind size from token via component input -->
<lucide-icon name="home"
  [size]="20"
  class="nav-icon" />
```

```css
/* CSS-driven sizing — preferred over inline [size] binding */
.nav-icon {
  width:  var(--icon-size-nav);
  height: var(--icon-size-nav);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Icon Size`

| Variable | xs Value | xl Value | Scope |
|----------|----------|----------|-------|
| `icon-size/inline` | 16 | 16 | Width, Height |
| `icon-size/sm` | 18 | 18 | Width, Height |
| `icon-size/default` | 20 | 20 | Width, Height |
| `icon-size/nav` | 20 | 24 | Width, Height |
| `icon-size/feature` | 24 | 24 | Width, Height |

> In Figma, create two modes for this collection: **Mobile** and **Desktop**. Apply the correct mode per frame/section.
