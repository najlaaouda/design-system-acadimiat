---
name: Card
tier: Component
status: Active
last-updated: 2026-07-07
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Card — Component Spec

## Philosophy

The Card is the primary content-grouping surface in the Acadimiat design system. It bundles related information — media, title, description, actions — into a single visually distinct unit. Cards communicate depth through three visual weights — **Elevated** (shadow-based, floats above the page), **Outlined** (border-based, sits flush with the page), and **Filled** (tinted surface, no boundary line). Every visual property — color, spacing, radius, elevation, typography — is resolved from semantic tokens, never from raw values.

> All spacing uses logical CSS properties (`padding-inline`, `padding-block`, `gap`).
> The card is RTL-first — header/footer layout and icon positions flip automatically via the document `dir` attribute.
> A Card is either **static** (a passive content container) or **interactive** (the whole surface acts as a single action) — never both halfway. Mixing nested interactive elements into an interactive card requires the stretched-link pattern documented in Accessibility.

---

## When to Use

- Elevated: content that should visually float above the page — dashboard widgets, metric summaries, featured items
- Outlined: content inside an already-elevated context (modals, panels) where another shadow would compound — forms, settings rows, list items
- Filled: low-emphasis grouping — nested content inside another card, secondary information blocks
- Interactive card: the entire surface represents one navigable action (open a course, view a report)
- Static card: the surface groups content but action happens on specific controls inside it (buttons, links, form fields)

## When to Avoid

- Don't nest a card of the same style variant inside another — stack Outlined or Filled inside Elevated instead, never Elevated-in-Elevated
- Don't make a card interactive if it contains more than one primary action — use a static card with explicit buttons instead
- Don't use Filled for the outermost surface on a plain page background — there's no contrast to separate it
- Don't put a card's entire surface behind `onclick` on a `<div>` — see Accessibility for the correct pattern

---

## Anatomy

```
┌─────────────────────────────────────────────┐
│                                               │
│                   [ media ]                  │  ← optional, edge-to-edge, no padding
│                                               │
├───────────────────────────────────────────── ┤
│  [icon]  OVERLINE                    [•••]   │  ← header: eyebrow + title + trailing action
│  Card title                                  │
│                                               │
│  Supporting body text goes here and can      │  ← body: description or custom content
│  wrap across multiple lines.                 │
│                                               │
│  ─────────────────────────────────────────   │  ← optional divider
│  [Button] [Button]              meta text    │  ← footer: actions + meta
└───────────────────────────────────────────────┘
```

| Part | Description | Always Present |
|------|-------------|----------------|
| Container | The surface — carries background, border, radius, shadow | Yes |
| Media | Edge-to-edge image/video/illustration at the block-start | No |
| Header | Overline (eyebrow), title, optional trailing action (e.g. icon-only menu) | No |
| Body | Supporting text or arbitrary composed content | No |
| Divider | Hairline separating body from footer | No |
| Footer | Actions (buttons/links) and/or meta text (timestamp, status) | No |

> A card with none of Header/Body/Footer populated is not a valid card — it must carry at least one content region.

> Three composed patterns built on this anatomy — **Course Card**, **Progress Card**, **Cart Item Card** — are documented in **Content Patterns** at the end of this file.

---

## Variants & States

### Elevated

The default floating surface. Use for content on a plain page background.

| State | Background | Border | Shadow |
|-------|-----------|--------|--------|
| Default | `bg-color-secondary` | none | `elevation-card` |
| Hover *(interactive only)* | `bg-color-secondary` | none | `elevation-card-hover` |
| Pressed *(interactive only)* | `bg-color-secondary` | none | `elevation-card` |
| Disabled *(interactive only)* | `bg-color-disabled` | none | `elevation-flat` |
| Focus *(interactive only)* | `bg-color-secondary` | none | Focus ring — see Focus section |
| Selected *(interactive only)* | `bg-color-secondary` | `border-color-brand` — 2px | `elevation-card-hover` |

### Outlined

A flush surface bounded by a hairline. Use inside modals, panels, or wherever a shadow would compound.

| State | Background | Border | Shadow |
|-------|-----------|--------|--------|
| Default | `bg-color-primary` | `border-color-primary` — 1px | none |
| Hover *(interactive only)* | `bg-color-secondary` | `border-color-primary` — 1px | none |
| Pressed *(interactive only)* | `bg-color-tertiary` | `border-color-primary` — 1px | none |
| Disabled *(interactive only)* | `bg-color-disabled` | `border-color-disabled` — 1px | none |
| Focus *(interactive only)* | `bg-color-primary` | `border-color-primary` — 1px | Focus ring — see Focus section |
| Selected *(interactive only)* | `bg-color-brand-subtle` | `border-color-brand` — 2px | none |

### Filled

A tinted surface with no boundary line. Use for nested or low-emphasis grouping.

| State | Background | Border | Shadow |
|-------|-----------|--------|--------|
| Default | `bg-color-tertiary` | none | none |
| Hover *(interactive only)* | `bg-color-brand-subtle` | none | none |
| Pressed *(interactive only)* | `bg-color-secondary` | none | none |
| Disabled *(interactive only)* | `bg-color-disabled` | none | none |
| Focus *(interactive only)* | `bg-color-tertiary` | none | Focus ring — see Focus section |
| Selected *(interactive only)* | `bg-color-brand-subtle` | `border-color-brand` — 2px | none |

> Hover, Pressed, Focus, and Selected only apply to `.card-interactive`. A static card never changes appearance on pointer interaction.

---

## Focus State

Focus applies only to interactive cards. Never suppress the focus ring.

| Property | Value | Token |
|----------|-------|-------|
| Outline color | `border-color-focus` | `--border-color-focus` |
| Outline width | 2px | — |
| Outline offset | 2px | — |
| Outline style | solid | — |

```css
.card-interactive:focus-visible {
  outline: 2px solid var(--border-color-focus);
  outline-offset: 2px;
}
```

> Use `:focus-visible` — not `:focus` — so the ring appears on keyboard navigation but not on mouse click.

---

## Sizes

Card height is content-driven — width and height are never fixed. Padding, radius, and internal gap scale together as one size step.

| Size | padding-inline / padding-block | Radius | Gap between regions | Title Typography | Body Typography |
|------|-------------------------------|--------|---------------------|-------------------|-------------------|
| Compact | `spacing-md` — 16px | `radius-lg` — 12px | `spacing-sm` — 8px | `type-label-lg` | `type-body-sm` |
| Default | `spacing-lg` — 24px | `radius-xl` — 16px | `spacing-md` — 16px | `type-heading-4` | `type-body` |
| Large | `spacing-xl` — 32px | `radius-2xl` — 24px | `spacing-lg` — 24px | `type-heading-3` | `type-body-lg` |

> Media regions are always edge-to-edge — they ignore the card's `padding-inline` and inherit only the container's `border-radius` on their outer corners.

### Media Corner Radius

Since media sits flush against the container edge, only the corners touching the container boundary are rounded.

| Media Position | Rounded Corners |
|----------------|-----------------|
| Block-start (top) | `border-start-start-radius` + `border-start-end-radius` = card radius |
| Block-end (bottom, no footer below) | `border-end-start-radius` + `border-end-end-radius` = card radius |

---

## Design Tokens Reference

### Color Tokens

| Role | Elevated | Outlined | Filled |
|------|----------|----------|--------|
| **Background (default)** | `--bg-color-secondary` | `--bg-color-primary` | `--bg-color-tertiary` |
| **Background (hover)** | `--bg-color-secondary` | `--bg-color-secondary` | `--bg-color-brand-subtle` |
| **Background (pressed)** | `--bg-color-secondary` | `--bg-color-tertiary` | `--bg-color-secondary` |
| **Background (disabled)** | `--bg-color-disabled` | `--bg-color-disabled` | `--bg-color-disabled` |
| **Background (selected)** | `--bg-color-secondary` | `--bg-color-brand-subtle` | `--bg-color-brand-subtle` |
| **Border (default)** | none | `--border-color-primary` | none |
| **Border (disabled)** | none | `--border-color-disabled` | none |
| **Border (selected)** | `--border-color-brand` | `--border-color-brand` | `--border-color-brand` |
| **Shadow (default)** | `--elevation-card` | none | none |
| **Shadow (hover)** | `--elevation-card-hover` | none | none |
| **Title text** | `--text-color-primary` | `--text-color-primary` | `--text-color-primary` |
| **Body text** | `--text-color-secondary` | `--text-color-secondary` | `--text-color-secondary` |
| **Overline text** | `--text-color-tertiary` | `--text-color-tertiary` | `--text-color-tertiary` |
| **Meta text (footer)** | `--text-color-tertiary` | `--text-color-tertiary` | `--text-color-tertiary` |
| **Disabled text** | `--text-color-disabled` | `--text-color-disabled` | `--text-color-disabled` |
| **Header action icon** | `--icon-color-secondary` | `--icon-color-secondary` | `--icon-color-secondary` |
| **Focus ring** | `--border-color-focus` | `--border-color-focus` | `--border-color-focus` |

### Spacing Tokens

| Property | Compact | Default | Large |
|----------|---------|---------|-------|
| `padding-inline` / `padding-block` | `--spacing-md` (16px) | `--spacing-lg` (24px) | `--spacing-xl` (32px) |
| Gap between regions | `--spacing-sm` (8px) | `--spacing-md` (16px) | `--spacing-lg` (24px) |
| Footer action gap | `--spacing-sm` (8px) | `--spacing-sm` (8px) | `--spacing-sm` (8px) |
| Header icon ↔ overline gap | `--spacing-xs` (4px) | `--spacing-xs` (4px) | `--spacing-sm` (8px) |

### Typography Tokens

| Element | Compact | Default | Large |
|---------|---------|---------|-------|
| Overline | `type-overline` | `type-overline` | `type-overline` |
| Title | `type-label-lg` | `type-heading-4` | `type-heading-3` |
| Body | `type-body-sm` | `type-body` | `type-body-lg` |
| Footer meta | `type-caption` | `type-caption` | `type-caption` |

### Icon Size Tokens

| Context | Token | Value |
|---------|-------|-------|
| Header overline icon | `--icon-size-inline` | 16px |
| Header trailing action (icon-only button) | `--icon-size-default` | 20px |
| Empty-state / standalone feature icon | `--icon-size-feature` | 24px |

### Radius Tokens

| Size | Token | Value |
|------|-------|-------|
| Compact | `--radius-lg` | 12px |
| Default | `--radius-xl` | 16px |
| Large | `--radius-2xl` | 24px |

### Elevation Tokens

| State | Token |
|-------|-------|
| Elevated / Default | `--elevation-card` |
| Elevated / Hover (interactive) | `--elevation-card-hover` |
| Elevated / Disabled | `--elevation-flat` |

---

## RTL Behavior

| Property | Approach |
|----------|----------|
| Text direction | Inherited from `dir="rtl"` on `<html>` — no override needed |
| Header layout | `flex` row — overline+icon at inline-start, trailing action at inline-end, reverses automatically in RTL |
| Footer layout | `justify-content: space-between` — actions at inline-start, meta at inline-end, reverses automatically |
| Horizontal padding | `padding-inline` — resolves to start/end, not left/right |
| Divider | Full-bleed `border-block-start`, direction-agnostic |
| Selected accent border | Applied on all four sides via `border`, not a single directional side — never use `border-left`/`border-right` for an accent |
| Media / images | Never mirrored — photographic and illustrative content is not directional |
| Header action icon (e.g. kebab `⋯`) | Non-directional — never mirrored |

---

## Motion & Animation

| Interaction | Property | Duration | Easing | Effect |
|------------|----------|----------|--------|--------|
| Hover enter *(interactive, Elevated)* | `box-shadow`, `transform` | 200ms | `cubic-bezier(0, 0, 0.2, 1)` — easing-out | Lifts `translateY(-2px)` + shadow deepens |
| Hover enter *(interactive, Outlined/Filled)* | `background-color`, `border-color` | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Background tints, no lift |
| Hover leave | same as enter | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Returns to resting state |
| Press (active) | `transform` | 150ms | `cubic-bezier(0, 0, 0.2, 1)` | Sinks `scale(0.99)` |
| Selected transition | `border-color`, `background-color` | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Accent border and tint fade in |
| Skeleton shimmer | `background-position` | 1400ms | `linear` — infinite | Light band sweeps across skeleton blocks |
| Progress fill update *(Progress Card)* | `inline-size` | 300ms | `cubic-bezier(0, 0, 0.2, 1)` | Bar grows/shrinks to the new completion value |

> Elevated cards are the only variant that lifts on hover — a border-based surface tinting instead communicates the same affordance without implying elevation change.
> `prefers-reduced-motion` removes the lift/scale transforms and the shimmer sweep, falling back to color-only transitions.

---

## CSS Implementation

```css
/* ── Base ─────────────────────────────────────────────── */
.card {
  display:        flex;
  flex-direction: column;
  border-radius:  var(--card-radius);
  background-color: var(--card-bg);
  border:         var(--card-border, none);
  box-shadow:     var(--card-shadow, none);
  overflow:       hidden;
  transition:
    background-color 200ms cubic-bezier(0, 0, 0.2, 1),
    border-color     200ms cubic-bezier(0, 0, 0.2, 1),
    box-shadow       200ms cubic-bezier(0, 0, 0.2, 1),
    transform        150ms cubic-bezier(0, 0, 0.2, 1);
}

/* ── Sizes ────────────────────────────────────────────── */
.card-compact {
  --card-radius: var(--radius-lg);   /* 12px */
  --card-gap:    var(--spacing-sm); /* 8px */
}
.card-compact .card-body-region {
  padding: var(--spacing-md);  /* 16px */
  gap:     var(--card-gap);
}

.card-default {
  --card-radius: var(--radius-xl);   /* 16px */
  --card-gap:    var(--spacing-md); /* 16px */
}
.card-default .card-body-region {
  padding: var(--spacing-lg);  /* 24px */
  gap:     var(--card-gap);
}

.card-lg {
  --card-radius: var(--radius-2xl);  /* 24px */
  --card-gap:    var(--spacing-lg); /* 24px */
}
.card-lg .card-body-region {
  padding: var(--spacing-xl); /* 32px */
  gap:     var(--card-gap);
}

/* ── Style Variants ───────────────────────────────────── */

/* Elevated */
.card-elevated {
  --card-bg:     var(--bg-color-secondary);
  --card-border: none;
  --card-shadow: var(--elevation-card);
}
.card-elevated.card-interactive:hover {
  --card-shadow: var(--elevation-card-hover);
  transform: translateY(-2px);
}
.card-elevated.card-interactive:active {
  --card-shadow: var(--elevation-card);
  transform: translateY(0);
}
.card-elevated.card-interactive:disabled,
.card-elevated.card-interactive[aria-disabled="true"] {
  --card-bg:     var(--bg-color-disabled);
  --card-shadow: var(--elevation-flat);
}

/* Outlined */
.card-outlined {
  --card-bg:     var(--bg-color-primary);
  --card-border: var(--border-1) var(--border-style-solid) var(--border-color-primary);
  --card-shadow: none;
}
.card-outlined.card-interactive:hover {
  --card-bg: var(--bg-color-secondary);
}
.card-outlined.card-interactive:active {
  --card-bg: var(--bg-color-tertiary);
}
.card-outlined.card-interactive:disabled,
.card-outlined.card-interactive[aria-disabled="true"] {
  --card-bg:     var(--bg-color-disabled);
  --card-border: var(--border-1) var(--border-style-solid) var(--border-color-disabled);
}

/* Filled */
.card-filled {
  --card-bg:     var(--bg-color-tertiary);
  --card-border: none;
  --card-shadow: none;
}
.card-filled.card-interactive:hover {
  --card-bg: var(--bg-color-brand-subtle);
}
.card-filled.card-interactive:active {
  --card-bg: var(--bg-color-secondary);
}
.card-filled.card-interactive:disabled,
.card-filled.card-interactive[aria-disabled="true"] {
  --card-bg: var(--bg-color-disabled);
}

/* ── Interactive Modifier ─────────────────────────────── */
.card-interactive {
  cursor:          pointer;
  text-decoration: none;
  color:           inherit;
  text-align:      inherit;
  border:          var(--card-border, none); /* re-declared: <button> resets border */
  font:            inherit;
  position:        relative; /* anchors the stretched-link overlay */
}

.card-interactive:focus-visible {
  outline:        2px solid var(--border-color-focus);
  outline-offset: 2px;
}

.card-interactive:disabled,
.card-interactive[aria-disabled="true"] {
  cursor:         not-allowed;
  pointer-events: none;
  transform:      none;
}

/* ── Selected State ───────────────────────────────────── */
.card-interactive.card-selected {
  --card-border: var(--border-2) var(--border-style-solid) var(--border-color-brand);
}
.card-elevated.card-interactive.card-selected {
  --card-shadow: var(--elevation-card-hover);
}
.card-filled.card-interactive.card-selected,
.card-outlined.card-interactive.card-selected {
  --card-bg: var(--bg-color-brand-subtle);
}

/* ── Stretched Link (whole-card click target) ─────────── */
/* Use when the card contains its own nested interactive elements
   (e.g. a header action button) alongside the primary card action. */
.card-stretched-link {
  position: static;
}
.card-stretched-link::after {
  content:  '';
  position: absolute;
  inset:    0;
  z-index:  1;
}
.card-interactive :where(button, a, input, select, textarea) {
  position: relative;
  z-index:  2; /* stays clickable above the stretched-link overlay */
}

/* ── Content Regions ──────────────────────────────────── */
.card-media {
  width:      100%;
  display:    block;
  object-fit: cover;
  flex-shrink: 0;
}
.card-media:first-child {
  border-start-start-radius: var(--card-radius);
  border-start-end-radius:   var(--card-radius);
}
.card-media:last-child {
  border-end-start-radius: var(--card-radius);
  border-end-end-radius:   var(--card-radius);
}

.card-body-region {
  display:        flex;
  flex-direction: column;
}

.card-header {
  display:         flex;
  align-items:     flex-start;
  justify-content: space-between;
  gap:             var(--spacing-sm);
}

.card-overline {
  display:     inline-flex;
  align-items: center;
  gap:         var(--spacing-xs);
  color:       var(--text-color-tertiary);
  font-family: var(--type-overline-family);
  font-size:   var(--type-overline-size);
  font-weight: var(--type-overline-weight);
  line-height: var(--type-overline-line-height);
  text-transform: uppercase;
}

.card-title {
  color: var(--text-color-primary);
  margin: 0;
}

.card-body {
  color: var(--text-color-secondary);
}

.card-divider {
  border: none;
  border-block-start: var(--border-1) var(--border-style-solid) var(--border-color-secondary);
  margin: 0;
}

.card-footer {
  display:         flex;
  align-items:     center;
  justify-content: space-between;
  gap:             var(--spacing-sm);
}

.card-footer-actions {
  display:     flex;
  align-items: center;
  gap:         var(--spacing-sm);
}

.card-footer-meta {
  color:       var(--text-color-tertiary);
  font-family: var(--type-caption-family);
  font-size:   var(--type-caption-size);
  font-weight: var(--type-caption-weight);
  line-height: var(--type-caption-line-height);
}

/* ── Header Action Icon ───────────────────────────────── */
.card-header-action {
  color:       var(--icon-color-secondary);
  width:       var(--icon-size-default);
  height:      var(--icon-size-default);
  flex-shrink: 0;
}

/* ── Skeleton Loading ─────────────────────────────────── */
.card-skeleton .card-media,
.card-skeleton .card-title,
.card-skeleton .card-body,
.card-skeleton .card-footer-actions {
  background-color: var(--bg-color-tertiary);
  background-image: linear-gradient(
    90deg,
    var(--bg-color-tertiary) 0%,
    var(--bg-color-secondary) 50%,
    var(--bg-color-tertiary) 100%
  );
  background-size: 200% 100%;
  animation: card-shimmer 1400ms linear infinite;
  color:            transparent;
  border-radius:    var(--radius-sm);
  pointer-events:   none;
  user-select:      none;
}

@keyframes card-shimmer {
  from { background-position: 200% 0; }
  to   { background-position: -200% 0; }
}

/* ── Reduced Motion ───────────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  .card {
    transition: background-color 150ms ease, border-color 150ms ease, box-shadow 150ms ease;
  }
  .card-elevated.card-interactive:hover,
  .card-elevated.card-interactive:active {
    transform: none;
  }
  .card-skeleton .card-media,
  .card-skeleton .card-title,
  .card-skeleton .card-body,
  .card-skeleton .card-footer-actions {
    animation: none;
    background-image: none;
  }
}
```

---

## Accessibility

### Static vs. Interactive Cards

| Type | Element | ARIA / Semantics |
|------|---------|-------------------|
| Static | `<div class="card">` or `<section class="card">` | No interactive role. Use a real `<h3>`/`<h4>` for the title so it participates in the page's heading outline. |
| Interactive (single action) | `<a class="card card-interactive" href="…">` or `<button class="card card-interactive">` | Native semantics — no `role` override needed. The entire surface is the accessible name's target; keep the title as the primary text inside it. |
| Interactive with nested controls | `<article>` wrapping a non-interactive card shell, with the card title wrapped in `<a class="card-stretched-link">` | Never wrap the whole card in an interactive element if it also contains a nested `<button>`/`<a>` — that produces invalid nested interactive content and breaks screen reader navigation. Use the **stretched-link pattern** instead: only the title link is a real `<a>`, expanded to cover the full card via `::after { inset: 0 }`; nested controls (e.g. header action button) get `position: relative; z-index: 2` to remain clickable above it. |

### ARIA Roles & Attributes

| Element | Attribute | Value |
|---------|-----------|-------|
| Interactive card (`<button>`) | `type` | `"button"` — always explicit |
| Interactive card | `aria-disabled` | `"true"` for temporarily unavailable cards — prefer over `disabled` when a tooltip explains why |
| Interactive card | `aria-pressed` | `"true"` / `"false"` when the card acts as a toggle (e.g. a selectable plan) |
| Interactive card | `aria-current` | `"true"` on the currently selected card in a selectable set |
| Header action icon-only button | `aria-label` | Required — a meaningful Arabic action phrase (e.g. `"خيارات إضافية"`) |
| Media image | `alt` | Descriptive alt text, or `alt=""` if the media is purely decorative and the title already conveys the content |
| Decorative overline / feature icon | `aria-hidden` | `"true"` |
| Skeleton card | `aria-hidden` | `"true"` on the whole `.card-skeleton`, plus `aria-busy="true"` on the containing list/grid |

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus to the interactive card (or its stretched link) |
| `Shift + Tab` | Move focus away (backwards) |
| `Enter` | Trigger the card's action (native `<a>`/`<button>` behavior) |
| `Space` | Trigger the action if the card is a `<button>` |

Within a card that has nested controls, `Tab` must visit the stretched link first (or last, per DOM order) and then each nested control individually — never skip nested controls, and never let the stretched overlay intercept their clicks (see `z-index: 2` in CSS Implementation).

### Color & Contrast

| Pair | Minimum Ratio | WCAG Level |
|------|--------------|------------|
| `text-color-primary` (title) vs. card background | 4.5:1 | AA — normal text |
| `text-color-secondary` (body) vs. card background | 4.5:1 | AA — normal text |
| `text-color-tertiary` (overline/meta) vs. card background | 4.5:1 | AA — normal text (verify against `bg-color-tertiary` specifically, the lowest-contrast surface) |
| `border-color-brand` (selected) vs. card background | 3:1 | AA — UI component |
| Focus ring vs. adjacent color | 3:1 | AA — UI component |
| Disabled text vs. disabled background | Not required — disabled states are exempt |

### Touch Targets

An interactive card's clickable surface is, by definition, far larger than 44×44px — no extra padding is required. The one exception is the header action icon-only button, which follows the Button component's icon-only touch target rule (extend with transparent padding to 44×44px if the visual icon is smaller).

---

## Figma Component Structure

### Component Variants

```
Card
├── Style:       Elevated / Outlined / Filled
├── Size:        Compact / Default / Large
├── Behavior:    Static / Interactive
├── State:       Default / Hover / Pressed / Disabled / Focus / Selected
├── Media:       None / Image
├── Header:      None / Overline / Title / Title + Action
├── Footer:      None / Actions / Actions + Meta
└── Loading:     Default / Skeleton
```

> Hover, Pressed, Focus, and Selected variants only exist when Behavior = Interactive.

### Figma Variable Bindings

| Layer | Variable |
|-------|----------|
| Container fill (Elevated) | `semantic/bg-color-secondary` |
| Container fill (Outlined) | `semantic/bg-color-primary` |
| Container fill (Filled) | `semantic/bg-color-tertiary` |
| Container fill (Hover — Filled) | `semantic/bg-color-brand-subtle` |
| Container fill (Selected — Outlined/Filled) | `semantic/bg-color-brand-subtle` |
| Container fill (Disabled) | `semantic/bg-color-disabled` |
| Container stroke (Outlined) | `semantic/border-color-primary` |
| Container stroke (Selected) | `semantic/border-color-brand` |
| Container stroke (Disabled — Outlined) | `semantic/border-color-disabled` |
| Container effect (Elevated / Default) | `semantic/elevation-card` |
| Container effect (Elevated / Hover) | `semantic/elevation-card-hover` |
| Title fill | `semantic/text-color-primary` |
| Body fill | `semantic/text-color-secondary` |
| Overline fill | `semantic/text-color-tertiary` |
| Footer meta fill | `semantic/text-color-tertiary` |
| Disabled text fill | `semantic/text-color-disabled` |
| Header action icon fill | `semantic/icon-color-secondary` |
| Corner radius (Compact) | `semantic/radius-lg` |
| Corner radius (Default) | `semantic/radius-xl` |
| Corner radius (Large) | `semantic/radius-2xl` |
| Padding (Compact) | `semantic/spacing-md` |
| Padding (Default) | `semantic/spacing-lg` |
| Padding (Large) | `semantic/spacing-xl` |
| Region gap (Compact) | `semantic/spacing-sm` |
| Region gap (Default) | `semantic/spacing-md` |
| Region gap (Large) | `semantic/spacing-lg` |
| Header action icon size | `semantic/icon-size-default` |
| Overline icon size | `semantic/icon-size-inline` |

---

## Content Patterns

Three composed patterns cover Acadimiat's most common catalog and commerce surfaces — **Course Card**, **Progress Card**, and **Cart Item Card**. Each is a standard `.card` (same container, Style, Size, and state machinery documented above) with a small set of additional sub-parts layered on top. Nothing here introduces a new tier — every sub-part still resolves color, spacing, radius, and typography from Semantic tokens only.

### Layout Axis: Vertical / Horizontal

A new axis, orthogonal to Style / Size / Behavior.

| Layout | Media Placement | Used By |
|--------|-----------------|---------|
| Vertical *(default)* | Edge-to-edge, block-start — see base Anatomy | Course Card, Progress Card |
| Horizontal | Fixed-size **Thumbnail**, inline-start | Cart Item Card |

> In RTL, `inline-start` resolves to the **right** edge — a Horizontal card's thumbnail sits on the right with text flowing to its left. This is automatic via logical properties; no direction-specific CSS is written.

### New Sub-Parts

| Part | Description | Used By |
|------|-------------|---------|
| Media Badge | A pill label pinned to the media's start corner — text-only or icon + text | Course Card |
| Media Meta Chip | A dark scrim chip pinned to the media's end corner — e.g. a duration stamp | Course Card |
| Meta Row | A row of icon + value **Stat** groups (e.g. learner count, rating) | Course Card |
| Price Row | Current price + optional struck-through original price | Course Card, Cart Item Card |
| Progress Track | A horizontal bar showing completion percentage, paired with a % label | Progress Card |
| Thumbnail | A small fixed-size square image replacing edge-to-edge media in Horizontal layout | Cart Item Card |
| Trailing Group | A column anchored at the row's end — price stacked above/beside a remove action | Cart Item Card |

---

### Media Badge & Media Meta Chip

```
┌───────────────────────────────┐
│ [●badge]                      │  ← inset-block-start / inset-inline-start
│                                │
│              media             │
│                                │
│                    [meta chip]│  ← inset-block-end / inset-inline-end
└───────────────────────────────┘
```

| State | Background | Text / Icon |
|-------|-----------|--------------|
| Badge — brand (default) | `bg-color-brand` | `text-color-on-brand` / `icon-color-on-brand` |
| Badge — promo/error | `bg-color-error` | `text-color-on-error` / `icon-color-on-error` |
| Meta chip | `bg-color-overlay` | `text-color-inverse` |

| Property | Token | Value |
|----------|-------|-------|
| Badge / chip offset from media edge | `spacing-sm` | 8px |
| Badge padding-inline / padding-block | `spacing-sm` / `spacing-xs` | 8px / 4px |
| Badge radius | `radius-full` | 9999px |
| Chip radius | `radius-sm` | 4px |
| Typography | `type-label-sm` | 14px, medium |
| Icon size (badge, if present) | `icon-size-inline` | 16px |

```css
.card-media-wrap { position: relative; }

.card-badge {
  position:         absolute;
  inset-block-start:  var(--spacing-sm);
  inset-inline-start: var(--spacing-sm);
  display:           inline-flex;
  align-items:       center;
  gap:               var(--spacing-xs);
  padding-inline:    var(--spacing-sm);
  padding-block:     var(--spacing-xs);
  border-radius:     var(--radius-full);
  font-family:       var(--type-label-sm-family);
  font-size:         var(--type-label-sm-size);
  font-weight:       var(--type-label-sm-weight);
  line-height:       var(--type-label-sm-line-height);
  background-color:  var(--bg-color-brand);
  color:             var(--text-color-on-brand);
}
.card-badge--promo { background-color: var(--bg-color-error); color: var(--text-color-on-error); }
.card-badge-icon   { width: var(--icon-size-inline); height: var(--icon-size-inline); flex-shrink: 0; }

.card-media-meta {
  position:          absolute;
  inset-block-end:   var(--spacing-sm);
  inset-inline-end:  var(--spacing-sm);
  padding-inline:    var(--spacing-sm);
  padding-block:     var(--spacing-xs);
  border-radius:     var(--radius-sm);
  font-family:       var(--type-label-sm-family);
  font-size:         var(--type-label-sm-size);
  font-weight:       var(--type-label-sm-weight);
  background-color:  var(--bg-color-overlay);
  color:             var(--text-color-inverse);
}
```

> Both are positioned with logical inset properties — they relocate automatically in RTL without a mirrored variant. Badge and chip backgrounds are non-directional; never mirror them.

---

### Meta Row (Stat Groups)

```html
<div class="card-meta-row">
  <span class="card-stat">
    <svg class="card-stat-icon" aria-hidden="true"><!-- users --></svg>
    176.7K
  </span>
  <span class="card-stat">
    <svg class="card-stat-icon" aria-hidden="true"><!-- thumbs-up --></svg>
    98% (4,077)
  </span>
</div>
```

| Element | Token |
|---------|-------|
| Icon color | `icon-color-secondary` (neutral stat) / `icon-color-warning` (rating star) |
| Icon size | `icon-size-inline` — 16px |
| Value text | `type-label-sm` / `text-color-secondary` |
| Gap (icon ↔ value) | `spacing-xs` — 4px |
| Gap (between stats) | `spacing-md` — 16px |

```css
.card-meta-row { display: flex; align-items: center; gap: var(--spacing-md); }
.card-stat     { display: inline-flex; align-items: center; gap: var(--spacing-xs);
                 font-family: var(--type-label-sm-family); font-size: var(--type-label-sm-size);
                 font-weight: var(--type-label-sm-weight); color: var(--text-color-secondary); }
.card-stat-icon { width: var(--icon-size-inline); height: var(--icon-size-inline); flex-shrink: 0; color: var(--icon-color-secondary); }
.card-stat-icon--rating { color: var(--icon-color-warning); }
```

Decorative icons (`users`, `thumbs-up`, `star`) are `aria-hidden="true"` — the adjacent text already carries the value; there is nothing non-visual to announce separately.

---

### Price Row

```html
<div class="card-price">
  <span class="card-price-current">١٩٩.٩٩ ج.م</span>
  <span class="card-price-original">٩٩٩.٩٩ ج.م</span>
</div>
```

| Element | Token |
|---------|-------|
| Current price | `type-label` / `text-color-primary` |
| Original price | `type-body-sm` / `text-color-tertiary`, `text-decoration: line-through` |
| Gap | `spacing-sm` — 8px |

```css
.card-price         { display: flex; align-items: baseline; gap: var(--spacing-sm); }
.card-price-current { font-family: var(--type-label-family); font-size: var(--type-label-size);
                       font-weight: var(--type-label-weight); color: var(--text-color-primary); }
.card-price-original{ font-family: var(--type-body-sm-family); font-size: var(--type-body-sm-size);
                       color: var(--text-color-tertiary); text-decoration: line-through; }
```

---

### Progress Track (Progress Card)

```html
<div class="card-progress-row">
  <div class="card-progress" role="progressbar" aria-valuenow="62" aria-valuemin="0" aria-valuemax="100" aria-label="نسبة إتمام الدورة">
    <div class="card-progress-fill" style="inline-size: 62%;"></div>
  </div>
  <span class="card-progress-label">62%</span>
</div>
```

| Property | Token / Value | Note |
|----------|----------------|------|
| Track height | `8px` | Fixed component height — same allowed exception class as Button heights (32/40/48/56px); see CLAUDE.md "Allowed px Exceptions" |
| Track background | `bg-color-tertiary` | — |
| Fill background | `bg-color-brand` | — |
| Radius (track + fill) | `radius-full` | 9999px |
| Label typography | `type-caption` / `text-color-secondary` | — |
| Gap (track ↔ label) | `spacing-sm` — 8px | — |

```css
.card-progress-row { display: flex; align-items: center; gap: var(--spacing-sm); }
.card-progress {
  flex: 1;
  block-size:       8px;
  border-radius:    var(--radius-full);
  background-color: var(--bg-color-tertiary);
  overflow:         hidden;
}
.card-progress-fill {
  block-size:       100%;
  border-radius:    var(--radius-full);
  background-color: var(--bg-color-brand);
  transition:       inline-size 300ms cubic-bezier(0, 0, 0.2, 1);
}
.card-progress-label {
  font-family: var(--type-caption-family);
  font-size:   var(--type-caption-size);
  color:       var(--text-color-secondary);
  flex-shrink: 0;
}
```

> The fill uses `inline-size`, not `width` — in RTL the track's own `direction` is inherited from `dir="rtl"`, so the fill correctly grows from the inline-start (right) edge without a mirrored variant.

The CTA below the track is a standard [Button](../Button/button.md) — `btn btn-primary btn-md`, stretched full-width via a footer-only modifier:

```css
.btn-full-width { inline-size: 100%; }
```

---

### Thumbnail & Trailing Group (Cart Item Card)

| Card Size | Thumbnail | Value | Justification |
|-----------|-----------|-------|----------------|
| Compact | 40px | fixed | Allowed px exception (fixed component height) |
| Default | 48px | fixed | Allowed px exception (fixed component height) |
| Large | 56px | fixed | Allowed px exception (fixed component height) |

```css
.card-layout-horizontal {
  flex-direction:  row;
  align-items:     center;
  gap:             var(--spacing-md);
  padding-inline:  var(--spacing-md);
  padding-block:   var(--spacing-sm);
}
.card-layout-horizontal .card-body-region {
  flex:            1;
  min-inline-size: 0; /* allows title/subtitle to truncate instead of overflowing */
  padding:         0;
  gap:             var(--spacing-xs);
}

.card-thumbnail {
  inline-size:   48px;   /* Default — see table above for Compact/Large */
  block-size:    48px;
  border-radius: var(--radius-md);
  object-fit:    cover;
  flex-shrink:   0;
}
.card-thumbnail--compact { inline-size: 40px; block-size: 40px; }
.card-thumbnail--lg      { inline-size: 56px; block-size: 56px; }

.card-title--truncate {
  overflow:      hidden;
  white-space:   nowrap;
  text-overflow: ellipsis;
}

.card-trailing {
  display:        flex;
  flex-direction: column;
  align-items:    center;
  gap:            var(--spacing-xs);
  flex-shrink:    0;
}
```

The remove action reuses [Button](../Button/button.md) icon-only Tertiary: `btn btn-tertiary btn-icon-only btn-sm`, with `icon-color-secondary` by default and `icon-color-error` on hover/focus to signal a destructive action:

```css
.card-remove-action .btn-icon { color: var(--icon-color-secondary); }
.card-remove-action:hover .btn-icon,
.card-remove-action:focus-visible .btn-icon { color: var(--icon-color-error); }
```

> `card-trailing` is populated in DOM order (price, then button) — flex-row reversal in RTL handles mirroring automatically. Do not use `float` or `order` to position it.

---

### Composed Examples

**Course Card** — Elevated, Default, Interactive, Vertical:

```html
<a class="card card-elevated card-default card-interactive" href="/courses/embroidery">
  <div class="card-media-wrap">
    <img class="card-media" src="embroidery.jpg" alt="تخصص في التطريز الإبداعي وأقمشة الأزياء">
    <span class="card-badge">مجانًا مع بلس</span>
    <span class="card-media-meta">12 س 2 د</span>
  </div>
  <div class="card-body-region">
    <h3 class="card-title">تخصص في التطريز الإبداعي وأقمشة الأزياء</h3>
    <p class="card-body">Domestika</p>
    <div class="card-meta-row">
      <span class="card-stat"><svg class="card-stat-icon" aria-hidden="true"></svg>176.7K</span>
      <span class="card-stat"><svg class="card-stat-icon card-stat-icon--rating" aria-hidden="true"></svg>98% (4,077)</span>
    </div>
    <hr class="card-divider">
    <div class="card-price">
      <span class="card-price-current">١٩٩.٩٩ ج.م</span>
      <span class="card-price-original">٩٩٩.٩٩ ج.م</span>
    </div>
  </div>
</a>
```

**Progress Card** — Outlined, Default, Static, Vertical:

```html
<article class="card card-outlined card-default">
  <div class="card-media-wrap">
    <img class="card-media" src="course-cover.jpg" alt="">
  </div>
  <div class="card-body-region">
    <h3 class="card-title">أساسيات تصميم واجهات المستخدم</h3>
    <div class="card-progress-row">
      <div class="card-progress" role="progressbar" aria-valuenow="62" aria-valuemin="0" aria-valuemax="100" aria-label="نسبة إتمام الدورة">
        <div class="card-progress-fill" style="inline-size: 62%;"></div>
      </div>
      <span class="card-progress-label">62%</span>
    </div>
    <button class="btn btn-primary btn-md btn-full-width" type="button">
      <span class="btn-label">متابعة التعلم</span>
    </button>
  </div>
</article>
```

**Cart Item Card** — Outlined, Compact, Static, Horizontal:

```html
<div class="card card-outlined card-compact card-layout-horizontal">
  <img class="card-thumbnail card-thumbnail--compact" src="product.jpg" alt="غطاء وسادة مطرز يدويًا">
  <div class="card-body-region">
    <h4 class="card-title card-title--truncate">غطاء وسادة مطرز يدويًا</h4>
    <p class="card-body card-title--truncate">مقاس 45×45 سم — قطن 100%</p>
  </div>
  <div class="card-trailing">
    <span class="card-price-current">٢٩٩.٩٩ ج.م</span>
    <button class="btn btn-tertiary btn-icon-only btn-sm card-remove-action" type="button" aria-label="إزالة من السلة">
      <svg class="btn-icon" aria-hidden="true"><!-- trash-2 --></svg>
    </button>
  </div>
</div>
```

---

### Accessibility — Content Patterns

| Element | Attribute | Value |
|---------|-----------|-------|
| Progress track | `role` | `"progressbar"` |
| Progress track | `aria-valuenow` / `aria-valuemin` / `aria-valuemax` | Current %, `0`, `100` |
| Progress track | `aria-label` | A meaningful Arabic phrase — e.g. `"نسبة إتمام الدورة"` |
| Meta row / rating icons | `aria-hidden` | `"true"` — the adjacent text is the accessible value |
| Media Badge / Meta Chip | *(none)* | Plain visible text — no ARIA needed, not interactive |
| Remove action (`btn-icon-only`) | `aria-label` | Required — e.g. `"إزالة من السلة"`, per Button's icon-only rules |
| Cart Item Card | Behavior | Always **Static** — it nests its own remove button, so the whole row must never be wrapped in a single interactive element (same rule as Card's Static-vs-Interactive guidance above) |
| Price strike-through (`card-price-original`) | `aria-hidden` | `"true"` optional — if the discount is announced elsewhere (e.g. an adjacent "خصم 80%" badge); otherwise leave it readable so screen reader users hear both prices |

### Figma — Content Pattern Properties

Added to the base Card component set (see **Figma Component Structure** above):

```
Card
├── … (all base properties)
├── Layout:          Vertical / Horizontal
├── Media Badge:     None / Text / Icon + Text
├── Media Meta Chip: None / Text
├── Meta Row:        None / 1 Stat / 2 Stats
├── Price Row:       None / Single / Discounted
├── Progress:        None / Value (number property, 0–100)
└── Trailing Group:  None / Price / Price + Remove Action
```

| Layer | Variable |
|-------|----------|
| Badge fill (brand) | `semantic/bg-color-brand` |
| Badge fill (promo) | `semantic/bg-color-error` |
| Badge text/icon | `semantic/text-color-on-brand`, `semantic/icon-color-on-brand` |
| Meta chip fill | `semantic/bg-color-overlay` |
| Meta chip text | `semantic/text-color-inverse` |
| Stat icon (neutral) | `semantic/icon-color-secondary` |
| Stat icon (rating) | `semantic/icon-color-warning` |
| Stat value text | `semantic/text-color-secondary` |
| Price — current | `semantic/text-color-primary` |
| Price — original | `semantic/text-color-tertiary` |
| Progress track fill | `semantic/bg-color-tertiary` |
| Progress bar fill | `semantic/bg-color-brand` |
| Progress label text | `semantic/text-color-secondary` |
| Thumbnail radius | `semantic/radius-md` |
| Remove action icon (default) | `semantic/icon-color-secondary` |
| Remove action icon (hover) | `semantic/icon-color-error` |
