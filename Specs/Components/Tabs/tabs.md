---
name: Tabs
tier: Component
status: Active
last-updated: 2026-07-06
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Tabs — Component Spec

## Philosophy

Tabs let a user switch between sibling views that share the same context without leaving the page — course content vs. reviews, this week vs. this month. Two visual weights cover the system's needs: **Underline** (default, for primary in-page navigation between views) and **Segmented** (an enclosed, toggle-like control for filtering or short binary/ternary choices). Every visual property — color, spacing, radius, typography, icon size — is resolved from semantic tokens, never from raw values.

> All spacing uses logical CSS properties (`padding-inline`, `gap`).
> Tabs are RTL-first — tab order follows DOM order, and arrow-key navigation direction is remapped under `dir="rtl"` (see RTL Behavior).
> A Tab list is not a Button group — tabs change *which content is visible*, they never trigger a standalone action (that's what Buttons are for).

---

## When to Use

- 2–6 sibling views of comparable importance that share the same page context
- The user needs to compare or repeatedly switch between the views (course "Content" / "Reviews" / "Q&A")
- Underline: primary navigation between full sections of a page
- Segmented: a compact filter or mode switch inside a card, table toolbar, or panel

## When to Avoid

- More than 6 fixed (non-scrollable) tabs — switch to Scrollable layout, or reconsider an overflow/dropdown pattern
- A single tab — there is nothing to switch between
- Using tabs to trigger a submit/navigate-away action — that changes context, which breaks the tab mental model; use a Button
- Mixing Underline and Segmented styles in the same tab list

---

## Anatomy

```
┌──────────────────────────────────────────────────────────┐
│  [icon] Content     Reviews (24)     Q&A          More ›  │  ← tab list
│  ▔▔▔▔▔▔▔▔▔▔▔▔                                              │  ← active indicator (Underline style)
├──────────────────────────────────────────────────────────┤
│                                                            │
│                     [ Tab panel content ]                 │
│                                                            │
└──────────────────────────────────────────────────────────┘
```

| Part | Description | Always Present |
|------|-------------|----------------|
| Tab list | The row of tabs — `role="tablist"` | Yes |
| Tab | One switchable trigger — icon + label + optional count badge | Yes (2+ per list) |
| Active indicator | Underline bar (Underline style) or filled pill (Segmented style) marking the selected tab | Yes |
| Baseline | Full-width hairline under the entire tab list (Underline style only) | No |
| Tab panel | The content region the selected tab controls — `role="tabpanel"` | Yes |
| Count badge | Small inline chip showing a number next to the label | No |

---

## Variants & States

### Style: Underline (default)

Flat tabs sitting on a full-width baseline. Use for primary page-level navigation.

| State | Text | Icon | Indicator | Baseline |
|-------|------|------|-----------|----------|
| Default | `text-color-secondary` | `icon-color-secondary` | none | `border-color-secondary` — 1px, full width |
| Hover | `text-color-primary` | `icon-color-primary` | none | unchanged |
| Pressed | `text-color-brand` | `icon-color-brand` | none | unchanged |
| Selected | `text-color-brand` | `icon-color-brand` | `border-color-brand` — 4px underline | unchanged |
| Disabled | `text-color-disabled` | `icon-color-disabled` | none | unchanged |
| Focus | inherits current state's color | inherits current state's color | Focus ring — see Focus section | unchanged |

### Style: Segmented

An enclosed track — tabs behave like a toggle group. Use for filters and mode switches.

| State | Track Background | Segment Background | Text |
|-------|-------------------|---------------------|------|
| Default | `bg-color-tertiary` | transparent | `text-color-secondary` |
| Hover | `bg-color-tertiary` | `bg-color-secondary` | `text-color-primary` |
| Pressed | `bg-color-tertiary` | `bg-color-secondary` | `text-color-primary` |
| Selected | `bg-color-tertiary` | `bg-color-primary` + `elevation-card` | `text-color-primary` |
| Disabled | `bg-color-tertiary` | transparent | `text-color-disabled` |
| Focus | `bg-color-tertiary` | inherits current state's background | Focus ring — see Focus section |

> Segmented tabs use `text-color-primary` (not brand) when selected — the pattern reads as a neutral toggle, not a navigation/brand action.

### Layout

| Layout | Behavior | When to Use |
|--------|----------|-------------|
| Fixed *(default)* | Tabs share equal width and fill the container (`flex: 1` each) | 2–4 tabs, all labels are short |
| Scrollable | Tabs size to their content and the list scrolls horizontally when it overflows | 5+ tabs, or labels of uneven/unpredictable length |

### Content

| Content Type | Composition |
|--------------|-------------|
| Label only | Text label, no icon |
| Icon + Label | Leading icon + text label |
| Icon only | Icon with no visible label — requires `aria-label` (see Accessibility) |
| Label + Count badge | Text label followed by an inline numeric chip |

### Count Badge Tone

| Tone | Background | Text | Usage |
|------|-----------|------|-------|
| Neutral *(default)* | `bg-color-tertiary` | `text-color-secondary` | General counts — "All (24)" |
| Alert | `bg-color-error` | `text-color-inverse` | Counts that need attention — "Unread (3)" |

---

## Focus State

| Property | Value | Token |
|----------|-------|-------|
| Outline color | `border-color-focus` | `--border-color-focus` |
| Outline width | 2px | — |
| Outline offset | 2px | — |
| Outline style | solid | — |

```css
.tab:focus-visible {
  outline: 2px solid var(--border-color-focus);
  outline-offset: 2px;
}
```

> Use `:focus-visible` — not `:focus`. Only one tab is ever keyboard-focusable at rest (roving `tabindex`) — see Accessibility.

---

## Sizes

| Size | Height | Icon Size | Typography | Icon ↔ Label Gap | Horizontal Padding |
|------|--------|-----------|------------|---------------------|---------------------|
| Medium *(default)* | 40px | `icon-size-inline` — 16px | `type-label-sm` | `spacing-xs` — 4px | `spacing-sm` — 8px |
| Large | 48px | `icon-size-default` — 20px | `type-label` | `spacing-sm` — 8px | `spacing-md` — 16px |

### Radius (Segmented style only)

| Element | Token | Value |
|---------|-------|-------|
| Track container | `radius-lg` | 12px |
| Active segment | `radius-md` | 8px |

> Underline style tabs use `radius-none` — they are flat list items, not enclosed surfaces.

---

## Design Tokens Reference

### Color Tokens

| Role | Default | Hover | Selected | Disabled |
|------|---------|-------|----------|----------|
| **Underline — text** | `--text-color-secondary` | `--text-color-primary` | `--text-color-brand` | `--text-color-disabled` |
| **Underline — icon** | `--icon-color-secondary` | `--icon-color-primary` | `--icon-color-brand` | `--icon-color-disabled` |
| **Underline — indicator** | — | — | `--border-color-brand` | — |
| **Underline — baseline** | `--border-color-secondary` | — | — | — |
| **Segmented — track bg** | `--bg-color-tertiary` | — | — | — |
| **Segmented — segment bg** | transparent | `--bg-color-secondary` | `--bg-color-primary` | transparent |
| **Segmented — text** | `--text-color-secondary` | `--text-color-primary` | `--text-color-primary` | `--text-color-disabled` |
| **Count badge (neutral)** | `--bg-color-tertiary` / `--text-color-secondary` | — | — | — |
| **Count badge (alert)** | `--bg-color-error` / `--text-color-inverse` | — | — | — |
| **Focus ring** | `--border-color-focus` | — | — | — |

### Spacing Tokens

| Property | Medium | Large |
|----------|--------|-------|
| `padding-inline` | `--spacing-sm` (8px) | `--spacing-md` (16px) |
| Icon ↔ label gap | `--spacing-xs` (4px) | `--spacing-sm` (8px) |
| Segmented track padding | `--spacing-xs` (4px) | `--spacing-xs` (4px) |

### Typography Tokens

| Size | Token |
|------|-------|
| Medium | `type-label-sm` |
| Large | `type-label` |

### Icon Size Tokens

| Size | Token | Value |
|------|-------|-------|
| Medium | `--icon-size-inline` | 16px |
| Large | `--icon-size-default` | 20px |

### Border Tokens

| Element | Width Token | Color Token |
|---------|-------------|-------------|
| Baseline (Underline style) | `--border-1` | `--border-color-secondary` |
| Active indicator (Underline style) | `--border-4` | `--border-color-brand` |

> The active indicator uses `--border-4`, the system's **Accent border** width — the same category used for highlighted-card accents. `--border-2` is reserved exclusively for focus rings and must never be repurposed here.

### Elevation Tokens

| Element | Token |
|---------|-------|
| Selected segment (Segmented style) | `--elevation-card` |

---

## RTL Behavior

| Property | Approach |
|----------|----------|
| Tab order | DOM order — reverses automatically under `dir="rtl"` |
| Underline indicator | `inset-inline` (not `left`/`right`) so it stays under the correct tab in both directions |
| Arrow-key direction | **Remapped, not automatic** — under `dir="rtl"`, `ArrowLeft` moves to the *next* tab and `ArrowRight` moves to the *previous* tab (the physical direction stays consistent with what the user sees, but the key-to-action mapping flips). Read `document.dir` (or the nearest ancestor's `dir`) at the moment of the keydown handler — never hardcode `ArrowRight = next` |
| Scrollable overflow | `overflow-x: auto` scrolls in the direction dictated by `dir` — no extra logic needed, browsers handle this natively |
| Edge fade mask | Apply on `inset-inline-start`/`inset-inline-end`, not `left`/`right` |
| Tab icons | Non-directional content icons are never mirrored; if a tab icon is directional (rare), mirror with `scaleX(-1)` per the system-wide rule |

---

## Motion & Animation

| Interaction | Property | Duration | Easing | Effect |
|------------|----------|----------|--------|--------|
| Tab select (Underline) | `transform` (indicator), `color` | 250ms | `cubic-bezier(0.4, 0, 0.2, 1)` — easing-in-out | Indicator grows from `scaleX(0)` to `scaleX(1)`, text/icon recolor |
| Tab deselect (Underline) | `color` | 250ms | `cubic-bezier(0.4, 0, 0.2, 1)` | Text/icon fade back to secondary color |
| Tab select (Segmented) | `background-color`, `box-shadow` | 250ms | `cubic-bezier(0.4, 0, 0.2, 1)` | Segment background and shadow fade in |
| Tab hover | `color` | 150ms | `cubic-bezier(0, 0, 0.2, 1)` — easing-out | Text/icon lighten toward primary |
| Panel switch | `opacity` | 150ms | `cubic-bezier(0, 0, 0.2, 1)` | Outgoing panel fades out, incoming panel fades in — never slide, to avoid implying a fixed left-to-right/right-to-left order |

> Duration and easing for the tab indicator match the system's documented Tab pattern (`duration-normal` / `easing-in-out`) in `Foundations/Motion.md`.
> `prefers-reduced-motion` removes the indicator grow animation and panel fade, swapping states instantly.

---

## CSS Implementation

```css
/* ── Tab List ─────────────────────────────────────────── */
.tab-list {
  display: flex;
  position: relative;
}

/* Underline style baseline */
.tab-list-underline {
  border-block-end: var(--border-1) var(--border-style-solid) var(--border-color-secondary);
}

/* Segmented style track */
.tab-list-segmented {
  background-color: var(--bg-color-tertiary);
  border-radius:    var(--radius-lg);
  padding:          var(--spacing-xs);
  gap:              var(--spacing-xs);
}

/* Layout: Fixed vs Scrollable */
.tab-list-fixed .tab {
  flex: 1;
}
.tab-list-scrollable {
  overflow-x:      auto;
  scroll-snap-type: x proximity;
  scrollbar-width: none;
}
.tab-list-scrollable::-webkit-scrollbar { display: none; }
.tab-list-scrollable .tab {
  flex-shrink: 0;
  scroll-snap-align: start;
}

/* ── Tab ──────────────────────────────────────────────── */
.tab {
  display:          inline-flex;
  align-items:      center;
  justify-content:  center;
  position:         relative;
  height:           var(--tab-height);
  padding-inline:   var(--tab-padding-inline);
  gap:              var(--tab-gap);
  background:       none;
  border:           none;
  cursor:           pointer;
  color:            var(--text-color-secondary);
  font-family:      var(--type-label-sm-family);
  font-size:        var(--type-label-sm-size);
  font-weight:      var(--type-label-sm-weight);
  line-height:      var(--type-label-sm-line-height);
  white-space:      nowrap;
  transition: color 150ms cubic-bezier(0, 0, 0.2, 1);
}

.tab-md {
  --tab-height:         40px;
  --tab-padding-inline: var(--spacing-sm);        /* 8px  */
  --tab-gap:            var(--spacing-xs);        /* 4px  */
}

.tab-lg {
  --tab-height:         48px;
  --tab-padding-inline: var(--spacing-md);        /* 16px */
  --tab-gap:            var(--spacing-sm);        /* 8px  */
  font-family:          var(--type-label-family);
  font-size:            var(--type-label-size);
  font-weight:          var(--type-label-weight);
  line-height:          var(--type-label-line-height);
}

.tab:hover {
  color: var(--text-color-primary);
}

.tab:active {
  color: var(--text-color-brand);
}

.tab:focus-visible {
  outline:        2px solid var(--border-color-focus);
  outline-offset: 2px;
}

.tab:disabled,
.tab[aria-disabled="true"] {
  color:          var(--text-color-disabled);
  cursor:         not-allowed;
  pointer-events: none;
}

.tab-icon {
  width:        var(--tab-icon-size, var(--icon-size-inline));
  height:       var(--tab-icon-size, var(--icon-size-inline));
  flex-shrink:  0;
  stroke-width: 2;
  color: currentColor;
}
.tab-lg .tab-icon {
  --tab-icon-size: var(--icon-size-default);
}

/* ── Underline Style ──────────────────────────────────── */
.tab-list-underline .tab[aria-selected="true"] {
  color: var(--text-color-brand);
}

.tab-list-underline .tab-indicator {
  position:          absolute;
  inset-inline:      0;
  inset-block-end:   0;
  height:            var(--border-4); /* 4px — accent-width, not focus-width */
  background-color:  var(--border-color-brand);
  border-radius:     var(--radius-full);
  transform:         scaleX(0);
  transform-origin:  center;
  transition:        transform 250ms cubic-bezier(0.4, 0, 0.2, 1);
}
.tab-list-underline .tab[aria-selected="true"] .tab-indicator {
  transform: scaleX(1);
}

/* ── Segmented Style ──────────────────────────────────── */
.tab-list-segmented .tab {
  border-radius: var(--radius-md);
  transition: background-color 250ms cubic-bezier(0.4, 0, 0.2, 1),
              box-shadow       250ms cubic-bezier(0.4, 0, 0.2, 1),
              color            150ms cubic-bezier(0, 0, 0.2, 1);
}
.tab-list-segmented .tab:hover {
  background-color: var(--bg-color-secondary);
}
.tab-list-segmented .tab[aria-selected="true"] {
  background-color: var(--bg-color-primary);
  box-shadow:       var(--elevation-card);
  color:            var(--text-color-primary);
}

/* ── Count Badge ──────────────────────────────────────── */
.tab-badge {
  display:          inline-flex;
  align-items:      center;
  justify-content:  center;
  min-width:        var(--icon-size-inline); /* 16px */
  height:           var(--icon-size-inline);
  padding-inline:   var(--spacing-xs);
  border-radius:    var(--radius-full);
  font-family:      var(--type-caption-family);
  font-size:        var(--type-caption-size);
  font-weight:      var(--type-caption-weight);
  line-height:      1;
}
.tab-badge-neutral {
  background-color: var(--bg-color-tertiary);
  color:            var(--text-color-secondary);
}
.tab-badge-alert {
  background-color: var(--bg-color-error);
  color:            var(--text-color-inverse);
}

/* ── Tab Panel ────────────────────────────────────────── */
.tab-panel {
  animation: tab-panel-fade-in 150ms cubic-bezier(0, 0, 0.2, 1);
}
@keyframes tab-panel-fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}
.tab-panel[hidden] {
  display: none;
}

/* ── Reduced Motion ───────────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  .tab,
  .tab-list-underline .tab-indicator,
  .tab-list-segmented .tab {
    transition: color 150ms ease;
  }
  .tab-list-underline .tab-indicator {
    transition: none;
  }
  .tab-panel {
    animation: none;
  }
}
```

---

## Accessibility

### Semantic Structure (WAI-ARIA Tabs Pattern)

```html
<div class="tab-list tab-list-underline tab-list-fixed" role="tablist" aria-label="أقسام الدورة">
  <button class="tab tab-md" role="tab" id="tab-content"
          aria-selected="true" aria-controls="panel-content" tabindex="0">
    <span>المحتوى</span>
    <span class="tab-indicator" aria-hidden="true"></span>
  </button>

  <button class="tab tab-md" role="tab" id="tab-reviews"
          aria-selected="false" aria-controls="panel-reviews" tabindex="-1">
    <span>التقييمات</span>
    <span class="tab-badge tab-badge-neutral" aria-hidden="true">24</span>
    <span class="tab-indicator" aria-hidden="true"></span>
  </button>

  <button class="tab tab-md" role="tab" id="tab-qa" aria-disabled="true"
          aria-selected="false" aria-controls="panel-qa" tabindex="-1">
    <span>أسئلة وأجوبة</span>
    <span class="tab-indicator" aria-hidden="true"></span>
  </button>
</div>

<div class="tab-panel" id="panel-content" role="tabpanel"
     aria-labelledby="tab-content" tabindex="0"></div>
<div class="tab-panel" id="panel-reviews" role="tabpanel"
     aria-labelledby="tab-reviews" tabindex="0" hidden></div>
<div class="tab-panel" id="panel-qa" role="tabpanel"
     aria-labelledby="tab-qa" tabindex="0" hidden></div>
```

### ARIA Roles & Attributes

| Element | Attribute | Value |
|---------|-----------|-------|
| Tab list container | `role` | `"tablist"` |
| Tab list container | `aria-label` | Required — describes the set, e.g. `"أقسام الدورة"` |
| Tab list container | `aria-orientation` | `"vertical"` only for a vertical tab list — omit for the default horizontal |
| Each tab | `role` | `"tab"` |
| Each tab | `aria-selected` | `"true"` on exactly one tab, `"false"` on the rest |
| Each tab | `aria-controls` | ID of the tab panel it governs |
| Each tab | `tabindex` | `"0"` on the selected tab only, `"-1"` on all others — **roving tabindex** |
| Each tab | `aria-disabled` | `"true"` for an unavailable tab — keep it in the DOM and in the tab order sequence conceptually, just not reachable/selectable |
| Icon-only tab | `aria-label` | Required — a meaningful Arabic phrase, since no visible label exists |
| Tab panel | `role` | `"tabpanel"` |
| Tab panel | `aria-labelledby` | ID of the tab that controls it |
| Tab panel | `tabindex` | `"0"` — lets keyboard users focus and scroll the panel if it has no other focusable content |
| Count badge | `aria-hidden` | `"true"` — the number must also be reachable in the tab's accessible name (visually-hidden text) if it changes the meaning, e.g. `"التقييمات، 24"` |

### Keyboard Navigation (Roving Tabindex)

| Key | Action |
|-----|--------|
| `Tab` | Move focus **into** the tab list (lands on the selected tab) or **out of** it to the tab panel — never between individual tabs |
| `Arrow Right` / `Arrow Left` | Move focus between tabs — direction is remapped under `dir="rtl"` (see RTL Behavior) |
| `Home` | Move focus to the first tab |
| `End` | Move focus to the last tab |
| `Enter` / `Space` | Activate the focused tab (required only in **Manual Activation** mode — see below) |

### Activation Mode

| Mode | Behavior | When to Use |
|------|----------|-------------|
| Automatic *(default)* | Moving focus with arrow keys immediately selects the tab and shows its panel | Panel content is cheap to render (static content, no network fetch) |
| Manual | Arrow keys only move focus; `Enter`/`Space` selects the focused tab | Selecting a tab triggers a data fetch or another expensive operation — avoids firing it on every arrow keypress |

### Color & Contrast

| Pair | Minimum Ratio | WCAG Level |
|------|--------------|------------|
| `text-color-brand` (selected, Underline) vs. background | 4.5:1 | AA |
| `text-color-secondary` (default) vs. background | 4.5:1 | AA |
| `border-color-brand` (indicator) vs. background | 3:1 | AA — UI component |
| `text-color-inverse` (alert badge) vs. `bg-color-error` | 4.5:1 | AA |
| Focus ring vs. background | 3:1 | AA — UI component |

### Touch Targets

Minimum tab height is 40px (Medium). Per the system's 44px touch target guideline, extend Medium tabs with the same transparent-padding technique used for small Buttons if the tab list is used in a touch-primary context:

```css
.tab-md {
  position: relative;
}
.tab-md::before {
  content: '';
  position: absolute;
  inset-block: -2px;
}
```

---

## Figma Component Structure

### Component Variants

```
Tabs
├── Style:      Underline / Segmented
├── Layout:     Fixed / Scrollable
├── Size:       Medium / Large
├── Content:    Label / Icon + Label / Icon Only / Label + Badge
└── Tab
    ├── State:  Default / Hover / Pressed / Selected / Disabled / Focus
    └── Badge:  None / Neutral / Alert
```

### Figma Variable Bindings

| Layer | Variable |
|-------|----------|
| Tab text (default) | `semantic/text-color-secondary` |
| Tab text (hover) | `semantic/text-color-primary` |
| Tab text (selected — Underline) | `semantic/text-color-brand` |
| Tab text (selected — Segmented) | `semantic/text-color-primary` |
| Tab text (disabled) | `semantic/text-color-disabled` |
| Tab icon | mirrors tab text variable per state |
| Baseline stroke | `semantic/border-color-secondary` |
| Active indicator fill | `semantic/border-color-brand` |
| Segmented track fill | `semantic/bg-color-tertiary` |
| Segmented segment fill (hover) | `semantic/bg-color-secondary` |
| Segmented segment fill (selected) | `semantic/bg-color-primary` |
| Segmented segment effect (selected) | `semantic/elevation-card` |
| Count badge fill (neutral) | `semantic/bg-color-tertiary` |
| Count badge fill (alert) | `semantic/bg-color-error` |
| Count badge text (alert) | `semantic/text-color-inverse` |
| Corner radius (Segmented track) | `semantic/radius-lg` |
| Corner radius (Segmented segment) | `semantic/radius-md` |
| Corner radius (badge) | `semantic/radius-full` |
| Icon size (Medium) | `semantic/icon-size-inline` |
| Icon size (Large) | `semantic/icon-size-default` |
