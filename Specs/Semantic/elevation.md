---
name: Elevation Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Elevation — Semantic Tokens

## Philosophy

Semantic elevation tokens replace raw `box-shadow` values with roles that describe **where in the z-axis stack a surface lives**. The system uses two shadow families — Neutral (black-tinted) for general surfaces, and Brand (purple-tinted) for primary interactive elements. In Dark mode, neutral shadow opacity is reduced because surface lightness contrast already carries depth; brand shadows remain unchanged.

> **Use these tokens on all box-shadow properties.**
> Never hardcode shadow values in components.

---

## How to Read This File

### Naming Pattern

```
elevation-[role]
```

| Segment | Meaning |
|---------|---------|
| `elevation` | Indicates this is a shadow / depth token |
| `role` | The UI context — `flat`, `card`, `dropdown`, `modal`, `sticky`, `brand`, etc. |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Elevation.md`.

### Theme Notes

- **Neutral tokens** change between Light and Dark mode — opacity decreases in dark mode because surface color contrast replaces shadow depth.
- **Brand tokens** remain the same in both modes — purple-tinted shadows remain visible on dark surfaces.

---

## Neutral Elevation Tokens

Applied to general surfaces — cards, menus, modals, headers.

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `elevation-flat` | → `elevation-0` — none | same | Flat surfaces, table cells, borderless panels |
| `elevation-card` | → `elevation-1` | `0 1px 2px rgba(0,0,0,0.03)` | Cards (resting), subtle separation |
| `elevation-card-hover` | → `elevation-2` | `0 2px 8px rgba(0,0,0,0.06)` | Cards on hover, interactive table rows |
| `elevation-dropdown` | → `elevation-3` | `0 4px 16px rgba(0,0,0,0.08)` | Dropdowns, menus, tooltips, popovers |
| `elevation-modal` | → `elevation-4` | `0 8px 24px rgba(0,0,0,0.10)` | Modals, dialogs, side drawers |
| `elevation-sticky` | → `elevation-5` | `0 16px 40px rgba(0,0,0,0.14)` | Sticky headers, toasts, floating notifications |

---

## Brand Elevation Tokens

Applied to primary interactive elements only. Reinforces brand identity on key actions.

| Token | Light & Dark | Usage |
|-------|-------------|-------|
| `elevation-brand` | → `elevation-brand-1` | Primary button (resting) |
| `elevation-brand-hover` | → `elevation-brand-2` | Primary button (hover / focus) |
| `elevation-brand-active` | → `elevation-brand-3` | Primary button (active / pressed), highlighted card |

---

## Z-Index Reference

Elevation tokens control visual depth (shadow). Pair them with these z-index values for correct stacking.

| Token | Suggested z-index | Layer |
|-------|------------------|-------|
| `elevation-flat` | `0` | Base content |
| `elevation-card` | `1` | Card layer |
| `elevation-card-hover` | `2` | Hovered card |
| `elevation-dropdown` | `100` | Overlapping UI (menus, tooltips) |
| `elevation-modal` | `200` | Modal layer |
| `elevation-sticky` | `300` | Always-on-top layer |

---

## CSS Custom Properties

```css
/* ─── Light Theme ────────────────────────────────────────── */
:root,
[data-theme="light"] {

  /* Neutral */
  --elevation-flat:        none;
  --elevation-card:        var(--elevation-1);   /* 0 1px 2px  rgba(0,0,0,0.05) */
  --elevation-card-hover:  var(--elevation-2);   /* 0 2px 8px  rgba(0,0,0,0.08) */
  --elevation-dropdown:    var(--elevation-3);   /* 0 4px 16px rgba(0,0,0,0.10) */
  --elevation-modal:       var(--elevation-4);   /* 0 8px 24px rgba(0,0,0,0.12) */
  --elevation-sticky:      var(--elevation-5);   /* 0 16px 40px rgba(0,0,0,0.16) */

  /* Brand */
  --elevation-brand:        var(--elevation-brand-1); /* 0 1px 4px  rgba(101,57,141,0.10) */
  --elevation-brand-hover:  var(--elevation-brand-2); /* 0 4px 12px rgba(101,57,141,0.18) */
  --elevation-brand-active: var(--elevation-brand-3); /* 0 8px 24px rgba(101,57,141,0.24) */
}

/* ─── Dark Theme ─────────────────────────────────────────── */
[data-theme="dark"] {

  /* Neutral — reduced opacity; depth is expressed via surface lightness */
  --elevation-flat:        none;
  --elevation-card:        0 1px 2px  rgba(0, 0, 0, 0.03);
  --elevation-card-hover:  0 2px 8px  rgba(0, 0, 0, 0.06);
  --elevation-dropdown:    0 4px 16px rgba(0, 0, 0, 0.08);
  --elevation-modal:       0 8px 24px rgba(0, 0, 0, 0.10);
  --elevation-sticky:      0 16px 40px rgba(0, 0, 0, 0.14);

  /* Brand — unchanged; purple tint remains visible on dark surfaces */
  --elevation-brand:        var(--elevation-brand-1);
  --elevation-brand-hover:  var(--elevation-brand-2);
  --elevation-brand-active: var(--elevation-brand-3);
}
```

### Usage Pattern

```css
.card {
  box-shadow: var(--elevation-card);
  transition: box-shadow 150ms ease;
}

.card:hover {
  box-shadow: var(--elevation-card-hover);
}

.dropdown {
  box-shadow: var(--elevation-dropdown);
}

.modal {
  box-shadow: var(--elevation-modal);
}

.btn-primary {
  box-shadow: var(--elevation-brand);
}

.btn-primary:hover {
  box-shadow: var(--elevation-brand-hover);
}

.btn-primary:active {
  box-shadow: var(--elevation-brand-active);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Elevation`

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `elevation/flat` | `none` | `none` | Effect |
| `elevation/card` | `primitive/elevation-1` | `0 1px 2px rgba(0,0,0,0.03)` | Effect |
| `elevation/card-hover` | `primitive/elevation-2` | `0 2px 8px rgba(0,0,0,0.06)` | Effect |
| `elevation/dropdown` | `primitive/elevation-3` | `0 4px 16px rgba(0,0,0,0.08)` | Effect |
| `elevation/modal` | `primitive/elevation-4` | `0 8px 24px rgba(0,0,0,0.10)` | Effect |
| `elevation/sticky` | `primitive/elevation-5` | `0 16px 40px rgba(0,0,0,0.14)` | Effect |
| `elevation/brand` | `primitive/elevation-brand-1` | `primitive/elevation-brand-1` | Effect |
| `elevation/brand-hover` | `primitive/elevation-brand-2` | `primitive/elevation-brand-2` | Effect |
| `elevation/brand-active` | `primitive/elevation-brand-3` | `primitive/elevation-brand-3` | Effect |
