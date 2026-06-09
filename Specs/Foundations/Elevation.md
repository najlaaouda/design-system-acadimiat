---
name: Elevation Primitives
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Elevation System — Primitive Tokens

## Philosophy

Acadimiat's elevation system conveys depth and hierarchy through refined, subtle shadows. Shadows are soft and elegant — never harsh. Two shadow families are provided: **Neutral** (general UI) and **Brand** (purple-tinted, for key interactive elements). These are **Primitive Tokens** — applied through Semantic Tokens in components.

> **Important — Do not use raw box-shadow values in components.**
> Always use elevation tokens through the Semantic layer.

---

## Elevation Scale

### Neutral Shadows

| Token | Value | Usage |
|-------|-------|-------|
| `elevation-0` | `none` | Flat — no shadow |
| `elevation-1` | `0 1px 2px rgba(0, 0, 0, 0.05)` | Resting cards, subtle separation |
| `elevation-2` | `0 2px 8px rgba(0, 0, 0, 0.08)` | Interactive cards, table rows on hover |
| `elevation-3` | `0 4px 16px rgba(0, 0, 0, 0.10)` | Dropdowns, popovers, tooltips |
| `elevation-4` | `0 8px 24px rgba(0, 0, 0, 0.12)` | Modals, drawers, side panels |
| `elevation-5` | `0 16px 40px rgba(0, 0, 0, 0.16)` | Full-screen overlays, sticky headers |

### Brand Shadows (Purple-tinted)

Used on primary interactive elements to reinforce brand identity.

| Token | Value | Usage |
|-------|-------|-------|
| `elevation-brand-1` | `0 1px 4px rgba(101, 57, 141, 0.10)` | Resting primary button |
| `elevation-brand-2` | `0 4px 12px rgba(101, 57, 141, 0.18)` | Hovered / focused primary button |
| `elevation-brand-3` | `0 8px 24px rgba(101, 57, 141, 0.24)` | Active primary button, highlighted card |

---

## Usage Guidelines

| Context | Token |
|---------|-------|
| Card (resting) | `elevation-1` |
| Card (hover) | `elevation-2` |
| Dropdown / Menu | `elevation-3` |
| Popover / Tooltip | `elevation-3` |
| Modal / Dialog | `elevation-4` |
| Drawer | `elevation-4` |
| Sticky header / Navbar | `elevation-5` |
| Toast / Notification | `elevation-5` |
| Primary button (resting) | `elevation-brand-1` |
| Primary button (hover) | `elevation-brand-2` |
| Primary button (active/focus) | `elevation-brand-3` |
| Flat surface / Table cell | `elevation-0` |

---

## CSS Custom Properties

```css
:root {
  /* Neutral Elevation */
  --elevation-0: none;
  --elevation-1: 0 1px 2px  rgba(0, 0, 0, 0.05);
  --elevation-2: 0 2px 8px  rgba(0, 0, 0, 0.08);
  --elevation-3: 0 4px 16px rgba(0, 0, 0, 0.10);
  --elevation-4: 0 8px 24px rgba(0, 0, 0, 0.12);
  --elevation-5: 0 16px 40px rgba(0, 0, 0, 0.16);

  /* Brand Elevation */
  --elevation-brand-1: 0 1px 4px  rgba(101, 57, 141, 0.10);
  --elevation-brand-2: 0 4px 12px rgba(101, 57, 141, 0.18);
  --elevation-brand-3: 0 8px 24px rgba(101, 57, 141, 0.24);
}
```

---

## Dark Mode

In dark mode, shadows have reduced opacity and rely more on surface color contrast than shadow depth. Semantic tokens handle this automatically — primitive values remain unchanged.

| Token | Dark Mode Adjustment |
|-------|----------------------|
| `elevation-1` | Reduce opacity to `0.03` |
| `elevation-2` | Reduce opacity to `0.06` |
| `elevation-3` | Reduce opacity to `0.08` |
| `elevation-4` | Reduce opacity to `0.10` |
| `elevation-5` | Reduce opacity to `0.14` |

---

## Rules

- Never hardcode `box-shadow` values in components — use elevation tokens only
- Do not skip more than 2 elevation levels within the same UI context
- Brand shadows are reserved for primary actions only — never use on neutral or secondary elements
- In dark mode, elevation is expressed through surface lightness, not shadow depth
