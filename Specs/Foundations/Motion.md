---
name: Motion Primitives
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Motion System — Primitive Tokens

## Philosophy

Acadimiat's motion system is purposeful and restrained. Animations guide attention, confirm interactions, and provide spatial context — never decorate. All motion is fast and precise, respecting users who prefer reduced motion.

> **Important — No animation may exceed 350ms.**
> Always respect `prefers-reduced-motion`.

---

## Duration

| Token | Value | Usage |
|-------|-------|-------|
| `duration-fast` | `150ms` | Micro-interactions: hover states, toggles, button press |
| `duration-normal` | `250ms` | Standard transitions: dropdowns, tooltips, tabs |
| `duration-slow` | `350ms` | Larger elements: modals, drawers, page transitions |

---

## Easing

| Token | Value | Usage |
|-------|-------|-------|
| `easing-out` | `cubic-bezier(0, 0, 0.2, 1)` | Default — elements entering the screen |
| `easing-in` | `cubic-bezier(0.4, 0, 1, 1)` | Elements leaving the screen |
| `easing-in-out` | `cubic-bezier(0.4, 0, 0.2, 1)` | Elements moving position (transitions) |
| `easing-linear` | `linear` | Looping animations (spinners, progress bars) |

---

## Transition Combinations

Pre-composed duration + easing pairs for common use cases.

| Token | Value | Usage |
|-------|-------|-------|
| `transition-fast` | `150ms cubic-bezier(0, 0, 0.2, 1)` | Hover, focus, active states |
| `transition-normal` | `250ms cubic-bezier(0, 0, 0.2, 1)` | Dropdowns, menus, tooltips |
| `transition-slow` | `350ms cubic-bezier(0.4, 0, 0.2, 1)` | Modals, drawers, panels |

---

## Usage Guidelines

| Interaction | Duration Token | Easing Token |
|-------------|---------------|--------------|
| Button hover / active | `duration-fast` | `easing-out` |
| Toggle / Switch | `duration-fast` | `easing-in-out` |
| Tooltip appear | `duration-fast` | `easing-out` |
| Dropdown open | `duration-normal` | `easing-out` |
| Dropdown close | `duration-normal` | `easing-in` |
| Tab indicator | `duration-normal` | `easing-in-out` |
| Badge / Tag appear | `duration-normal` | `easing-out` |
| Modal enter | `duration-slow` | `easing-out` |
| Modal exit | `duration-slow` | `easing-in` |
| Drawer slide in | `duration-slow` | `easing-out` |
| Drawer slide out | `duration-slow` | `easing-in` |
| Page transition | `duration-slow` | `easing-in-out` |
| Spinner / Loader | `duration-normal` | `easing-linear` |

---

## CSS Custom Properties

```css
:root {
  /* Duration */
  --duration-fast:   150ms;
  --duration-normal: 250ms;
  --duration-slow:   350ms;

  /* Easing */
  --easing-out:     cubic-bezier(0, 0, 0.2, 1);
  --easing-in:      cubic-bezier(0.4, 0, 1, 1);
  --easing-in-out:  cubic-bezier(0.4, 0, 0.2, 1);
  --easing-linear:  linear;

  /* Transitions */
  --transition-fast:   150ms cubic-bezier(0, 0, 0.2, 1);
  --transition-normal: 250ms cubic-bezier(0, 0, 0.2, 1);
  --transition-slow:   350ms cubic-bezier(0.4, 0, 0.2, 1);
}
```

---

## Reduced Motion

All animated components must respect the user's motion preference.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

> Components should convey state changes through color or opacity when motion is disabled — never rely on animation alone to communicate meaning.

---

## Rules

- No animation above `350ms` — ever
- `easing-out` is the default for all entering elements
- `easing-in` is used only for exiting elements
- `easing-linear` is reserved for looping animations only
- Enter and exit animations must use matching durations
- Never animate more than 2 properties simultaneously on the same element
- Always include `prefers-reduced-motion` fallback in every animated component
