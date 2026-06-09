---
name: Radius Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Radius — Semantic Tokens

## Philosophy

Semantic radius tokens map the raw radius scale to component roles, so every designer and developer picks a role — not a number. The system prefers `radius-lg` and `radius-xl` (12–16px) across most UI components, reflecting Acadimiat's modern, refined SaaS aesthetic. Radius does not change between themes.

> **Use these tokens on all border-radius properties.**
> Never use arbitrary radius values or reference Primitive Tokens directly in components.

---

## How to Read This File

### Naming Pattern

```
radius-[role]
```

| Segment | Meaning |
|---------|---------|
| `radius` | Indicates this is a border-radius token |
| `role` | The relative size and context — `none`, `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `full` |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Radius.md`.

### Theme Notes

Radius tokens are theme-neutral — they do not change between Light and Dark mode.

---

## Tokens

| Token | Primitive | Value | Usage |
|-------|-----------|-------|-------|
| `radius-none` | → `radius-0` | 0px | Sharp elements — full-width banners, table cells, edge-to-edge strips |
| `radius-xs` | → `radius-2` | 2px | Subtle rounding — secondary tags, scrollbar thumbs, image overlays |
| `radius-sm` | → `radius-4` | 4px | Badges, notification dots, small status indicators |
| `radius-md` | → `radius-8` | 8px | Dropdowns, context menus, tooltips, popovers |
| `radius-lg` | → `radius-12` | 12px | Inputs, default buttons, compact cards, tabs |
| `radius-xl` | → `radius-16` | 16px | Cards, modals, dialogs, drawers, large buttons |
| `radius-2xl` | → `radius-24` | 24px | Featured cards, hero containers, large surface panels |
| `radius-full` | → `radius-full` | 9999px | Pills, avatars, circular buttons, progress bars, chips |

---

## Component Reference

Quick lookup — which token to use per component.

| Component | Token | Value |
|-----------|-------|-------|
| Card (default) | `radius-xl` | 16px |
| Card (compact) | `radius-lg` | 12px |
| Modal / Dialog | `radius-xl` | 16px |
| Drawer | `radius-xl` | 16px (top corners only) |
| Input | `radius-lg` | 12px |
| Button (default) | `radius-lg` | 12px |
| Button (large) | `radius-xl` | 16px |
| Dropdown / Menu | `radius-md` | 8px |
| Tooltip / Popover | `radius-md` | 8px |
| Badge | `radius-sm` | 4px |
| Tag / Chip | `radius-full` | 9999px |
| Avatar | `radius-full` | 9999px |
| Progress bar | `radius-full` | 9999px |
| Table cell | `radius-none` | 0px |
| Full-width banner | `radius-none` | 0px |
| Subtle container | `radius-xs` | 2px |

---

## CSS Custom Properties

```css
:root {
  --radius-none: var(--radius-0);      /*    0px */
  --radius-xs:   var(--radius-2);      /*   2px  */
  --radius-sm:   var(--radius-4);      /*   4px  */
  --radius-md:   var(--radius-8);      /*   8px  */
  --radius-lg:   var(--radius-12);     /*  12px  */
  --radius-xl:   var(--radius-16);     /*  16px  */
  --radius-2xl:  var(--radius-24);     /*  24px  */
  --radius-full: var(--radius-full);   /* 9999px */
}
```

### Usage Pattern

```css
.card {
  border-radius: var(--radius-xl);
}

.input {
  border-radius: var(--radius-lg);
}

.badge {
  border-radius: var(--radius-sm);
}

.avatar {
  border-radius: var(--radius-full);
}

/* Drawer — only top corners rounded */
.drawer {
  border-start-start-radius: var(--radius-xl);
  border-start-end-radius:   var(--radius-xl);
  border-end-start-radius:   0;
  border-end-end-radius:     0;
}
```

---

## Figma Variables

> **Collection:** `Semantic/Radius`

| Variable | Primitive | Value | Scope |
|----------|-----------|-------|-------|
| `radius/none` | `primitive/radius-0` | 0px | Corner radius |
| `radius/xs` | `primitive/radius-2` | 2px | Corner radius |
| `radius/sm` | `primitive/radius-4` | 4px | Corner radius |
| `radius/md` | `primitive/radius-8` | 8px | Corner radius |
| `radius/lg` | `primitive/radius-12` | 12px | Corner radius |
| `radius/xl` | `primitive/radius-16` | 16px | Corner radius |
| `radius/2xl` | `primitive/radius-24` | 24px | Corner radius |
| `radius/full` | `primitive/radius-full` | 9999px | Corner radius |
