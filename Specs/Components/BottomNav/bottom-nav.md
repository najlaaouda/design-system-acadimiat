---
name: Bottom Navigation
tier: Component
status: Active
last-updated: 2026-07-06
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Bottom Navigation — Component Spec

## Philosophy

Bottom Navigation is the primary wayfinding surface on mobile viewports — it stays fixed to the block-end of the screen and gives the user constant access to the app's top-level destinations (typically 3–5). It is a **mobile-only** pattern: on tablet and desktop the same destinations move into a side rail or top nav, which is a separate spec. Every visual property — color, spacing, radius, elevation, typography, icon size — is resolved from semantic tokens, never from raw values.

> The bar is fixed-position and RTL-first — item order follows DOM order and reverses automatically under `dir="rtl"`.
> Bottom Navigation is for **top-level destinations only** — never use it for contextual or in-page actions. That's what a Button or app bar action is for.

---

## When to Use

- 3–5 top-level, mutually exclusive destinations that persist across the whole app (Home, Courses, Notifications, Profile)
- The product is viewed primarily on mobile (`xs`–`sm`, below 768px)
- Every item is a real navigation target the user can deep-link to, not a modal trigger

## When to Avoid

- More than 5 destinations — group the extras behind a "المزيد" (More) item that opens a sheet, don't shrink items further
- Fewer than 3 destinations — use a simpler pattern (e.g. a single back button or top app bar)
- Above the `md` breakpoint (768px) — switch to a side rail or top nav; never show both simultaneously
- Transient or contextual actions (e.g. "Save", "Filter") — those belong in an app bar or as inline Buttons, not as nav items
- Nesting a Button or Card's stretched-link inside a nav item — nav items are the interactive element themselves

---

## Anatomy

```
                              ┌──────────┐
                              │    ➕    │  ← optional center action (elevated, overlaps bar)
                              └────┬─────┘
┌──────────────────────────────────┴──────────────────────────────────┐
│                                                                      │
│   🏠         📚            ⬤              🔔•              👤       │
│ الرئيسية    دوراتي       (center)      الإشعارات          حسابي     │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
  ↑ active item                              ↑ badge (dot or count)
  (pill indicator behind icon)
```

| Part | Description | Always Present |
|------|-------------|----------------|
| Bar container | Fixed-position surface anchored to block-end of viewport | Yes |
| Nav item | One destination — icon + optional label, the whole item is the tap target | Yes (3–5 per bar) |
| Active indicator | Pill background behind the active item's icon (or a minimal color-only state) | Yes (on the active item) |
| Badge | Dot or numeric count overlaid on an item's icon, top-end corner | No |
| Center action | An elevated circular action button that overlaps the bar's top edge | No — max one per bar |
| Safe-area inset | Extra block-end padding reserved for the device home indicator | Yes (iOS devices) |

---

## Variants & States

### Item States

| State | Icon | Label | Indicator |
|-------|------|-------|-----------|
| Default (inactive) | `icon-color-secondary` | `text-color-secondary` | none |
| Active | `icon-color-brand` | `text-color-brand` | Pill: `bg-color-brand-subtle` behind icon (Pill style) — or color-only (Minimal style) |
| Pressed | `icon-color-brand` | `text-color-brand` | `bg-color-brand-subtle` at full opacity, no scale change on the pill |
| Disabled | `icon-color-disabled` | `text-color-disabled` | none — item is present but not reachable (e.g. locked feature) |
| Focus | inherits current state's color | inherits current state's color | Focus ring — see Focus section |

### Indicator Style

| Style | Behavior |
|-------|----------|
| Pill *(default)* | Active item gets a `radius-full` pill of `bg-color-brand-subtle` behind its icon, sized to the icon plus `spacing-xs` padding |
| Minimal | No pill — only the icon/label color change signals the active item. Use when the bar already carries a center action and a pill would visually compete with it |

### Label Visibility (Density)

| Mode | Bar Height | Behavior |
|------|-----------|----------|
| Labeled *(default)* | 56px | Every item shows icon + label at all times |
| Active-label-only | 56px | Inactive items show icon only; the active item reveals its label |
| Icon-only | 48px | No labels ever — use only when icons are unambiguous and well-tested with users (rare; prefer Labeled for an educational product) |

### Badge

| Type | Appearance | Usage |
|------|-----------|-------|
| None | — | Default |
| Dot | 8px filled circle, `bg-color-error`, positioned top-end of the icon | Unread indicator with no count (e.g. "new content available") |
| Count | Pill, `bg-color-error` fill, `text-color-inverse` label, min 16px, positioned top-end of the icon | Numeric unread count (e.g. "3", "9+" — cap at 9+ to avoid pill growth) |

### Center Action (Optional)

A single elevated circular button that overlaps the bar's top edge, used for the app's single most important creation action (e.g. "Start a new course").

| State | Background | Icon | Shadow |
|-------|-----------|------|--------|
| Default | `bg-color-brand` | `icon-color-on-brand` | `elevation-brand` |
| Pressed | `bg-color-brand-pressed` | `icon-color-on-brand` | `elevation-brand-active` |
| Disabled | `bg-color-disabled` | `icon-color-disabled` | `elevation-flat` |
| Focus | `bg-color-brand` | `icon-color-on-brand` | Focus ring — see Focus section |

> At most one Center Action per bar, and it replaces the middle nav item slot — it is not a 6th item.

---

## Focus State

| Property | Value | Token |
|----------|-------|-------|
| Outline color | `border-color-focus` | `--border-color-focus` |
| Outline width | 2px | — |
| Outline offset | 2px | — |
| Outline style | solid | — |

```css
.nav-item:focus-visible,
.nav-center-action:focus-visible {
  outline: 2px solid var(--border-color-focus);
  outline-offset: 2px;
}
```

> Use `:focus-visible` — not `:focus`. On a touch-only device the ring will rarely appear, but it must exist for keyboard/switch-control users.

---

## Sizes

| Property | Labeled / Active-label-only | Icon-only |
|----------|------------------------------|-----------|
| Bar height (content, excl. safe area) | 56px | 48px |
| Icon size | `--icon-size-default` — 20px | `--icon-size-default` — 20px |
| Icon ↔ label gap | `--spacing-xs` — 4px | — |
| Item min touch target | `--size-11` — 44px × 44px (per Foundations/Size.md) | 44px × 44px |
| Bar horizontal padding | `--spacing-sm` — 8px | `--spacing-sm` — 8px |
| Label typography | `type-caption` | — |
| Center action diameter | 56px | 56px |
| Center action icon size | `--icon-size-default` — 20px | `--icon-size-default` — 20px |

> Bar heights of 56px/48px are fixed component heights — an allowed `px` exception per system rules, same category as Button's fixed heights.

---

## Design Tokens Reference

### Color Tokens

| Role | Default (inactive) | Active | Disabled |
|------|--------------------|--------|----------|
| **Icon** | `--icon-color-secondary` | `--icon-color-brand` | `--icon-color-disabled` |
| **Label** | `--text-color-secondary` | `--text-color-brand` | `--text-color-disabled` |
| **Active pill background** | — | `--bg-color-brand-subtle` | — |
| **Bar background** | `--bg-color-primary` | — | — |
| **Bar top border** | `--border-color-primary` — 1px | — | — |
| **Badge dot / count fill** | `--bg-color-error` | — | — |
| **Badge count text** | `--text-color-inverse` | — | — |
| **Center action background** | `--bg-color-brand` | — | `--bg-color-disabled` |
| **Center action icon** | `--icon-color-on-brand` | — | `--icon-color-disabled` |
| **Focus ring** | `--border-color-focus` | — | — |

### Spacing Tokens

| Property | Token |
|----------|-------|
| Bar horizontal padding | `--spacing-sm` (8px) |
| Icon ↔ label gap | `--spacing-xs` (4px) |
| Active pill padding | `--spacing-xs` (4px) |
| Gap between items | distributed via `justify-content: space-around` — no fixed gap token |

### Typography Tokens

| Element | Token |
|---------|-------|
| Item label | `type-caption` |
| Badge count | `type-caption` |

### Icon Size Tokens

| Context | Token | Value |
|---------|-------|-------|
| Nav item icon | `--icon-size-default` | 20px |
| Center action icon | `--icon-size-default` | 20px |

### Radius Tokens

| Element | Token | Value |
|---------|-------|-------|
| Active pill | `--radius-full` | 9999px |
| Badge (dot & count) | `--radius-full` | 9999px |
| Center action | `--radius-full` | 9999px |
| Bar top corners *(optional, if the bar floats above the edge instead of sitting flush)* | `--radius-xl` | 16px |

### Elevation Tokens

| Element | Token |
|---------|-------|
| Bar | `--elevation-sticky` |
| Center action (default) | `--elevation-brand` |
| Center action (pressed) | `--elevation-brand-active` |

---

## RTL Behavior

| Property | Approach |
|----------|----------|
| Item order | DOM order — reverses automatically under `dir="rtl"`, no CSS `order` needed |
| Bar layout | `display: flex` row — items distribute evenly regardless of direction |
| Badge position | `inset-inline-end` / `inset-block-start` on the icon wrapper — never `right`/`top` |
| Safe-area padding | `padding-block-end: env(safe-area-inset-bottom)` — block-direction, unaffected by RTL |
| Icons | Bottom nav icons (home, book, bell, user, plus) are non-directional — never mirrored |
| Center action position | Horizontally centered via `inset-inline-start: 50%` + `transform: translateX(-50%)` — direction-agnostic |

---

## Motion & Animation

| Interaction | Property | Duration | Easing | Effect |
|------------|----------|----------|--------|--------|
| Item activate | `color`, `background-color` (pill) | 200ms | `cubic-bezier(0, 0, 0.2, 1)` — easing-out | Icon/label recolor, pill fades in |
| Item deactivate | same | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Pill fades out, color returns to inactive |
| Item press | `transform` on icon only | 150ms | `cubic-bezier(0, 0, 0.2, 1)` | Icon scales to `0.9` and back — confirms the tap |
| Badge appear | `transform`, `opacity` | 150ms | `cubic-bezier(0, 0, 0.2, 1)` | Scales in from `0` to `1` — draws attention to new content |
| Center action press | `transform`, `box-shadow` | 150ms | `cubic-bezier(0, 0, 0.2, 1)` | Sinks `scale(0.96)`, shadow reduces to `elevation-brand-active` |

> Never animate the bar's own position (e.g. slide out on scroll) without also providing a way back — if the bar auto-hides on scroll, it must reappear on scroll-up, never require a page reload.
> `prefers-reduced-motion` removes the icon/badge scale transforms and keeps only the color-fade transitions.

---

## CSS Implementation

```css
/* ── Bar Container ────────────────────────────────────── */
.bottom-nav {
  position:        fixed;
  inset-inline:     0;
  inset-block-end:  0;
  z-index:          300; /* matches elevation-sticky layer per Semantic/elevation.md */
  display:          flex;
  align-items:      stretch;
  justify-content:  space-around;
  height:           56px;
  padding-inline:   var(--spacing-sm);
  padding-block-end: env(safe-area-inset-bottom); /* device home-indicator clearance, not a design token */
  background-color: var(--bg-color-primary);
  border-block-start: var(--border-1) var(--border-style-solid) var(--border-color-primary);
  box-shadow:       var(--elevation-sticky);
}

/* Mobile-only — hide at tablet and above, side/top nav takes over */
@media (min-width: 768px) {
  .bottom-nav { display: none; }
}

/* Icon-only density */
.bottom-nav.bottom-nav-icon-only {
  height: 48px;
}

/* ── Nav Item ──────────────────────────────────────────── */
.nav-item {
  display:         flex;
  flex:             1;
  flex-direction:  column;
  align-items:     center;
  justify-content: center;
  gap:             var(--spacing-xs);
  min-width:       var(--size-11); /* 44px min touch target */
  color:           var(--icon-color-secondary);
  text-decoration: none;
  background:      none;
  border:          none;
  font:            inherit;
  cursor:          pointer;
  transition:
    color 200ms cubic-bezier(0, 0, 0.2, 1);
}

.nav-item-icon-wrap {
  display:         inline-flex;
  align-items:     center;
  justify-content: center;
  position:        relative;
  border-radius:   var(--radius-full);
  padding-inline:  var(--spacing-xs);
  transition:      background-color 200ms cubic-bezier(0, 0, 0.2, 1);
}

.nav-item-icon {
  width:        var(--icon-size-default);
  height:       var(--icon-size-default);
  flex-shrink:  0;
  stroke-width: 2;
  color:        var(--icon-color-secondary);
  transition:   color 200ms cubic-bezier(0, 0, 0.2, 1), transform 150ms cubic-bezier(0, 0, 0.2, 1);
}

.nav-item-label {
  font-family: var(--type-caption-family);
  font-size:   var(--type-caption-size);
  font-weight: var(--type-caption-weight);
  line-height: var(--type-caption-line-height);
  color:       var(--text-color-secondary);
  transition:  color 200ms cubic-bezier(0, 0, 0.2, 1);
}

.nav-item:active .nav-item-icon {
  transform: scale(0.9);
}

/* Active state — Pill indicator (default) */
.nav-item[aria-current="page"] .nav-item-icon-wrap {
  background-color: var(--bg-color-brand-subtle);
}
.nav-item[aria-current="page"] .nav-item-icon {
  color: var(--icon-color-brand);
}
.nav-item[aria-current="page"] .nav-item-label {
  color: var(--text-color-brand);
}

/* Active state — Minimal indicator (opt-in) */
.bottom-nav-minimal .nav-item[aria-current="page"] .nav-item-icon-wrap {
  background-color: transparent;
}

.nav-item:focus-visible {
  outline:        2px solid var(--border-color-focus);
  outline-offset: 2px;
}

.nav-item:disabled,
.nav-item[aria-disabled="true"] {
  cursor:         not-allowed;
  pointer-events: none;
}
.nav-item:disabled .nav-item-icon,
.nav-item[aria-disabled="true"] .nav-item-icon {
  color: var(--icon-color-disabled);
}
.nav-item:disabled .nav-item-label,
.nav-item[aria-disabled="true"] .nav-item-label {
  color: var(--text-color-disabled);
}

/* Active-label-only density: hide label unless active */
.bottom-nav-active-label-only .nav-item:not([aria-current="page"]) .nav-item-label {
  display: none;
}

/* Icon-only density: never show labels */
.bottom-nav-icon-only .nav-item-label {
  display: none;
}

/* ── Badge ─────────────────────────────────────────────── */
.nav-item-badge {
  position:   absolute;
  inset-block-start: 0;
  inset-inline-end:  0;
  transform:  translate(30%, -30%) scale(1);
  background-color: var(--bg-color-error);
  border-radius:    var(--radius-full);
  transition: transform 150ms cubic-bezier(0, 0, 0.2, 1), opacity 150ms cubic-bezier(0, 0, 0.2, 1);
}

.nav-item-badge--dot {
  width:  calc(var(--icon-size-inline) / 2); /* 8px, derived from a semantic token */
  height: calc(var(--icon-size-inline) / 2);
}

.nav-item-badge--count {
  min-width:      var(--icon-size-inline); /* 16px */
  height:         var(--icon-size-inline);
  padding-inline: var(--spacing-xs);
  display:        flex;
  align-items:    center;
  justify-content: center;
  color:          var(--text-color-inverse);
  font-family:    var(--type-caption-family);
  font-size:      var(--type-caption-size);
  font-weight:    var(--type-caption-weight);
  line-height:    1;
}

/* ── Center Action ─────────────────────────────────────── */
.nav-center-action {
  position:         absolute;
  inset-inline-start: 50%;
  inset-block-start:  0;
  transform:        translate(-50%, -40%);
  width:            56px;
  height:           56px;
  display:          flex;
  align-items:      center;
  justify-content:  center;
  border-radius:    var(--radius-full);
  background-color: var(--bg-color-brand);
  box-shadow:       var(--elevation-brand);
  border:           none;
  cursor:           pointer;
  transition:
    background-color 200ms cubic-bezier(0, 0, 0.2, 1),
    box-shadow       200ms cubic-bezier(0, 0, 0.2, 1),
    transform        150ms cubic-bezier(0, 0, 0.2, 1);
}
.nav-center-action:active {
  background-color: var(--bg-color-brand-pressed);
  box-shadow:       var(--elevation-brand-active);
  transform:        translate(-50%, -40%) scale(0.96);
}
.nav-center-action:focus-visible {
  outline:        2px solid var(--border-color-focus);
  outline-offset: 2px;
}
.nav-center-action:disabled {
  background-color: var(--bg-color-disabled);
  box-shadow:       var(--elevation-flat);
  cursor:           not-allowed;
}
.nav-center-action-icon {
  width:        var(--icon-size-default);
  height:       var(--icon-size-default);
  color:        var(--icon-color-on-brand);
  stroke-width: 2;
}

/* ── Reduced Motion ───────────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  .nav-item,
  .nav-item-icon,
  .nav-item-icon-wrap,
  .nav-item-label,
  .nav-center-action,
  .nav-item-badge {
    transition: color 150ms ease, background-color 150ms ease;
  }
  .nav-item:active .nav-item-icon,
  .nav-center-action:active {
    transform: none;
  }
}
```

---

## Accessibility

### Semantic Structure

```html
<nav class="bottom-nav" aria-label="التنقل الرئيسي">
  <a class="nav-item" href="/home" aria-current="page">
    <span class="nav-item-icon-wrap">
      <svg class="nav-item-icon" aria-hidden="true"><!-- home --></svg>
    </span>
    <span class="nav-item-label">الرئيسية</span>
  </a>

  <a class="nav-item" href="/courses">
    <span class="nav-item-icon-wrap">
      <svg class="nav-item-icon" aria-hidden="true"><!-- book --></svg>
    </span>
    <span class="nav-item-label">دوراتي</span>
  </a>

  <button class="nav-center-action" aria-label="إنشاء دورة جديدة">
    <svg class="nav-center-action-icon" aria-hidden="true"><!-- plus --></svg>
  </button>

  <a class="nav-item" href="/notifications">
    <span class="nav-item-icon-wrap">
      <svg class="nav-item-icon" aria-hidden="true"><!-- bell --></svg>
      <span class="nav-item-badge nav-item-badge--count" aria-hidden="true">3</span>
    </span>
    <span class="nav-item-label">الإشعارات</span>
    <span class="visually-hidden">، 3 إشعارات غير مقروءة</span>
  </a>

  <a class="nav-item" href="/profile">
    <span class="nav-item-icon-wrap">
      <svg class="nav-item-icon" aria-hidden="true"><!-- user --></svg>
    </span>
    <span class="nav-item-label">حسابي</span>
  </a>
</nav>
```

### ARIA Roles & Attributes

| Element | Attribute | Value |
|---------|-----------|-------|
| `<nav>` | `aria-label` | A meaningful Arabic phrase, e.g. `"التنقل الرئيسي"` — required since there may be more than one `<nav>` on the page |
| Nav item (link to current page) | `aria-current` | `"page"` — the single source of truth for which item is active; drive all active styling off this attribute, not a class alone |
| Nav item (disabled/locked) | `aria-disabled` | `"true"` |
| Nav item icon | `aria-hidden` | `"true"` — decorative, the visible label carries the name |
| Center action | `aria-label` | Required, describes the action (e.g. `"إنشاء دورة جديدة"`) — it has no visible label |
| Badge | `aria-hidden` | `"true"` on the visual badge — the count must also be exposed as text (see below) |
| Unread count | Visually-hidden text | Append `"، N إشعارات غير مقروءة"` inside the item so screen readers announce the count as part of the link's accessible name, not just a decorative digit |

### Why `<a>`, not `<button>` + `router.navigate()`

Each nav item is a real, deep-linkable destination — use a native `<a href>` (or your framework's link component that renders one) so users can open items in a new tab, and so browser history/back behaves correctly. The Center Action is the one exception — if it opens a creation flow rather than navigating to a URL, it is correctly a `<button>`.

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus through nav items and the center action in DOM order |
| `Shift + Tab` | Move focus backward |
| `Enter` | Activate the focused item (native link/button behavior) |
| `Space` | Activate the focused item only if it is the `<button>` center action |

### Touch Targets

| Element | Size | Passes 44px? |
|---------|------|--------------|
| Nav item | `flex: 1` of bar width × 44px min-height | ✅ |
| Center action | 56px × 56px | ✅ |
| Badge | Decorative overlay, not independently tappable | N/A |

### Color & Contrast

| Pair | Minimum Ratio | WCAG Level |
|------|--------------|------------|
| `icon-color-brand` / `text-color-brand` (active) vs. `bg-color-primary` | 3:1 (icon), 4.5:1 (label text) | AA |
| `icon-color-secondary` / `text-color-secondary` (inactive) vs. `bg-color-primary` | 3:1 (icon), 4.5:1 (label text) | AA |
| `text-color-inverse` (badge count) vs. `bg-color-error` | 4.5:1 | AA |
| Focus ring vs. `bg-color-primary` | 3:1 | AA — UI component |

### Screen Reader Behavior Checklist

- [ ] Only one item ever carries `aria-current="page"` at a time
- [ ] Badge counts are announced as text, never conveyed by color/shape alone
- [ ] The bar does not trap focus — `Tab` must be able to leave it in both directions
- [ ] If the bar auto-hides on scroll, it must not remove focused items from the accessibility tree while they hold focus

---

## Figma Component Structure

### Component Variants

```
Bottom Nav
├── Density:        Labeled / Active-label-only / Icon-only
├── Indicator:       Pill / Minimal
├── Item Count:      3 / 4 / 5
├── Center Action:   None / Present
└── Item
    ├── State:  Default / Active / Pressed / Disabled / Focus
    └── Badge:  None / Dot / Count
```

### Figma Variable Bindings

| Layer | Variable |
|-------|----------|
| Bar fill | `semantic/bg-color-primary` |
| Bar top stroke | `semantic/border-color-primary` |
| Bar effect | `semantic/elevation-sticky` |
| Item icon (default) | `semantic/icon-color-secondary` |
| Item icon (active) | `semantic/icon-color-brand` |
| Item icon (disabled) | `semantic/icon-color-disabled` |
| Item label (default) | `semantic/text-color-secondary` |
| Item label (active) | `semantic/text-color-brand` |
| Item label (disabled) | `semantic/text-color-disabled` |
| Active pill fill | `semantic/bg-color-brand-subtle` |
| Badge fill | `semantic/bg-color-error` |
| Badge count text | `semantic/text-color-inverse` |
| Center action fill (default) | `semantic/bg-color-brand` |
| Center action fill (pressed) | `semantic/bg-color-brand-pressed` |
| Center action fill (disabled) | `semantic/bg-color-disabled` |
| Center action icon | `semantic/icon-color-on-brand` |
| Center action effect (default) | `semantic/elevation-brand` |
| Center action effect (pressed) | `semantic/elevation-brand-active` |
| Corner radius (pill, badge, center action) | `semantic/radius-full` |
| Icon size | `semantic/icon-size-default` |
| Bar horizontal padding | `semantic/spacing-sm` |
| Icon ↔ label gap | `semantic/spacing-xs` |
