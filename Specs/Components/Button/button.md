---
name: Button
tier: Component
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat


# Button — Component Spec

## Philosophy

The Button is the primary interaction element in the Acadimiat design system. It communicates action intent through three visual weights — **Primary** (brand-filled, highest emphasis), **Secondary** (outlined, medium emphasis), and **Tertiary** (ghost, lowest emphasis). Every visual property — color, size, spacing, radius, icon size — is resolved from semantic tokens, never from raw values.

> All spacing uses logical CSS properties (`padding-inline`, `padding-block`, `gap`).
> The button is RTL-first — icon positions and text direction flip automatically via the document `dir` attribute.

---

## When to Use

- Primary: the single most important action on a page or modal (Submit, Save, Continue)
- Secondary: important but not primary (Cancel, Back, Edit)
- Tertiary: low-emphasis actions, inline links, or destructive secondary actions (Delete, Clear)

## When to Avoid

- More than one Primary button per view — creates hierarchy confusion
- Tertiary for a primary CTA — insufficient visual weight
- Icon-only button without a tooltip — not accessible

---

## Anatomy

```
┌─────────────────────────────────┐
│  [icon]  Label text  [icon]     │  ← Leading + Label + Trailing (RTL: reversed)
└─────────────────────────────────┘
     ↑           ↑         ↑
  leading      label    trailing
   icon        text       icon
```

| Part | Description | Always Present |
|------|-------------|----------------|
| Container | The clickable surface — carries background, border, radius | Yes |
| Label | Button text — describes the action | Yes (except icon-only) |
| Leading icon | Icon at the inline-start of the label | No |
| Trailing icon | Icon at the inline-end of the label | No |
| Focus ring | Visible outline on keyboard focus | Yes (on focus) |

> In RTL, inline-start = right. In LTR, inline-start = left. Use DOM order — not CSS transforms — to control icon position.

---

## Variants & States

### Primary

The filled brand button. Use for the main action on a page.

| State | Background | Text | Icon | Border |
|-------|-----------|------|------|--------|
| Default | `bg-color-brand` | `text-color-on-brand` | `icon-color-on-brand` | none |
| Hover | `bg-color-brand-hover` | `text-color-on-brand` | `icon-color-on-brand` | none |
| Pressed | `bg-color-brand-pressed` | `text-color-on-brand` | `icon-color-on-brand` | none |
| Disabled | `bg-color-disabled` | `text-color-disabled` | `icon-color-disabled` | none |
| Focus | `bg-color-brand` | `text-color-on-brand` | `icon-color-on-brand` | Focus ring — see Focus section |

### Secondary

An outlined button with a brand border. Use for supporting actions.

| State | Background | Text | Icon | Border |
|-------|-----------|------|------|--------|
| Default | transparent | `text-color-brand` | `icon-color-brand` | `border-color-brand` — 1.5px |
| Hover | `bg-color-brand-subtle` | `text-color-brand` | `icon-color-brand` | `border-color-brand` — 1.5px |
| Pressed | `bg-color-brand-hover` | `text-color-brand` | `icon-color-brand` | `border-color-brand` — 1.5px |
| Disabled | transparent | `text-color-disabled` | `icon-color-disabled` | `border-color-disabled` — 1.5px |
| Focus | transparent | `text-color-brand` | `icon-color-brand` | Focus ring — see Focus section |

### Tertiary

A ghost button with no background or border. Use for low-emphasis actions.

| State | Background | Text | Icon | Border |
|-------|-----------|------|------|--------|
| Default | transparent | `text-color-brand` | `icon-color-brand` | none |
| Hover | `bg-color-brand-subtle` | `text-color-brand` | `icon-color-brand` | none |
| Pressed | `bg-color-brand-hover` | `text-color-brand` | `icon-color-brand` | none |
| Disabled | transparent | `text-color-disabled` | `icon-color-disabled` | none |
| Focus | transparent | `text-color-brand` | `icon-color-brand` | Focus ring — see Focus section |

---

## Focus State

Focus applies to all three variants equally. Never suppress the focus ring.

| Property | Value | Token |
|----------|-------|-------|
| Outline color | `border-color-focus` | `--border-color-focus` |
| Outline width | 2px | — |
| Outline offset | 2px | — |
| Outline style | solid | — |

```css
.btn:focus-visible {
  outline: 2px solid var(--border-color-focus);
  outline-offset: 2px;
}
```

> Use `:focus-visible` — not `:focus` — so the ring appears on keyboard navigation but not on mouse click.

---

## Sizes

Height is a fixed constraint. Icons and text are vertically centered inside the container using flexbox. Horizontal padding (`padding-inline`) is the only variable padding — block padding is derived automatically.

| Size | Height | padding-inline | Icon Size | Typography | Gap (icon ↔ text) | Radius |
|------|--------|----------------|-----------|------------|-------------------|--------|
| XLarge | 56px | `spacing-inset-xl` — 24px | `icon-size-feature` — 24px | `type-label-lg` | `spacing-inline-sm` — 8px | `radius-lg` — 12px |
| Large | 48px | `spacing-inset-xl` — 24px | `icon-size-default` — 20px | `type-label-lg` | `spacing-inline-sm` — 8px | `radius-lg` — 12px |
| Medium | 40px | `spacing-inset-lg` — 16px | `icon-size-default` — 20px | `type-label` | `spacing-inline-sm` — 8px | `radius-md` — 8px |
| Small | 32px | `spacing-inset-md` — 12px | `icon-size-inline` — 16px | `type-label-sm` | `spacing-inline-xs` — 4px | `radius-md` — 8px |

### Icon-Only Sizes

Icon-only buttons are perfectly square. No label is rendered.

| Size | Width | Height | Icon Size | Radius |
|------|-------|--------|-----------|--------|
| XLarge | 56px | 56px | `icon-size-feature` — 24px | `radius-lg` — 12px |
| Large | 48px | 48px | `icon-size-default` — 20px | `radius-lg` — 12px |
| Medium | 40px | 40px | `icon-size-default` — 20px | `radius-md` — 8px |
| Small | 32px | 32px | `icon-size-inline` — 16px | `radius-md` — 8px |

---

## Icon Positions

Acadimiat uses Lucide Icons exclusively — stroke-width: 2, never filled.

### Leading Icon

The icon appears at the **inline-start** of the label. In RTL (Arabic), this is the **right side**. In LTR, this is the left side.

**DOM order (RTL-first):**
```html
<button class="btn btn-primary btn-md">
  <svg class="btn-icon" aria-hidden="true"><!-- icon --></svg>
  <span class="btn-label">إرسال</span>
</button>
```

**Rendered — RTL:**
```
│  ← icon  │  إرسال  │
           start(right) → end(left)
```

**Rendered — LTR:**
```
│  icon →  │  Submit  │
  start(left) → end(right)
```

### Trailing Icon

The icon appears at the **inline-end** of the label. In RTL, this is the **left side**. In LTR, this is the right side.

**DOM order:**
```html
<button class="btn btn-primary btn-md">
  <span class="btn-label">التالي</span>
  <svg class="btn-icon" aria-hidden="true"><!-- arrow-right --></svg>
</button>
```

**Rendered — RTL:**
```
│  التالي  │  icon →  │
  start(right) ← end(left)
```

> For directional icons (arrows), **mirror** the icon horizontally in RTL:
> `transform: scaleX(-1)` on the icon element when `dir="rtl"`.
> Non-directional icons (check, x, plus) are **never** mirrored.

### Icon Only

No visible label. The accessible label is provided via `aria-label`.

```html
<button class="btn btn-primary btn-md btn-icon-only" aria-label="إرسال">
  <svg class="btn-icon" aria-hidden="true"><!-- send --></svg>
</button>
```

---

## Design Tokens Reference

### Color Tokens

| Role | Default | Hover | Pressed | Disabled |
|------|---------|-------|---------|----------|
| **Primary bg** | `--bg-color-brand` | `--bg-color-brand-hover` | `--bg-color-brand-pressed` | `--bg-color-disabled` |
| **Primary text** | `--text-color-on-brand` | `--text-color-on-brand` | `--text-color-on-brand` | `--text-color-disabled` |
| **Primary icon** | `--icon-color-on-brand` | `--icon-color-on-brand` | `--icon-color-on-brand` | `--icon-color-disabled` |
| **Secondary bg** | transparent | `--bg-color-brand-subtle` | `--bg-color-brand-hover` | transparent |
| **Secondary text** | `--text-color-brand` | `--text-color-brand` | `--text-color-brand` | `--text-color-disabled` |
| **Secondary icon** | `--icon-color-brand` | `--icon-color-brand` | `--icon-color-brand` | `--icon-color-disabled` |
| **Secondary border** | `--border-color-brand` | `--border-color-brand` | `--border-color-brand` | `--border-color-disabled` |
| **Tertiary bg** | transparent | `--bg-color-brand-subtle` | `--bg-color-brand-hover` | transparent |
| **Tertiary text** | `--text-color-brand` | `--text-color-brand` | `--text-color-brand` | `--text-color-disabled` |
| **Tertiary icon** | `--icon-color-brand` | `--icon-color-brand` | `--icon-color-brand` | `--icon-color-disabled` |
| **Focus ring** | `--border-color-focus` | — | — | — |

### Spacing Tokens

| Property | XLarge | Large | Medium | Small |
|----------|--------|-------|--------|-------|
| `padding-inline` | `--spacing-inset-xl` (24px) | `--spacing-inset-xl` (24px) | `--spacing-inset-lg` (16px) | `--spacing-inset-md` (12px) |
| `gap` (icon ↔ text) | `--spacing-inline-sm` (8px) | `--spacing-inline-sm` (8px) | `--spacing-inline-sm` (8px) | `--spacing-inline-xs` (4px) |

### Typography Tokens

| Size | Token | Font | Size | Weight | Line-height |
|------|-------|------|------|--------|-------------|
| XLarge | `type-label-lg` | IBM Plex Sans Arabic | 16px | semibold (600) | normal |
| Large | `type-label-lg` | IBM Plex Sans Arabic | 16px | semibold (600) | normal |
| Medium | `type-label` | IBM Plex Sans Arabic | 14px | semibold (600) | normal |
| Small | `type-label-sm` | IBM Plex Sans Arabic | 12px | semibold (600) | normal |

### Icon Size Tokens

| Size | Token | Value |
|------|-------|-------|
| XLarge | `--icon-size-feature` | 24px |
| Large | `--icon-size-default` | 20px |
| Medium | `--icon-size-default` | 20px |
| Small | `--icon-size-inline` | 16px |

### Radius Tokens

| Size | Token | Value |
|------|-------|-------|
| XLarge | `--radius-lg` | 12px |
| Large | `--radius-lg` | 12px |
| Medium | `--radius-md` | 8px |
| Small | `--radius-md` | 8px |

---

## RTL Behavior

| Property | Approach |
|----------|----------|
| Text direction | Inherited from `dir="rtl"` on `<html>` — no override needed |
| Flex direction | `row` — items reverse automatically in RTL |
| Icon position | Controlled by **DOM order**, not CSS `order` or `float` |
| Horizontal padding | `padding-inline` — resolves to start/end, not left/right |
| Icon gap | `gap` on flex container — direction-agnostic |
| Directional icons | Mirror with `transform: scaleX(-1)` in RTL contexts |
| Non-directional icons | Never mirror |

### Directional vs Non-Directional Icons

| Category | Examples | Mirror in RTL? |
|----------|---------|----------------|
| Directional | `arrow-right`, `arrow-left`, `chevron-right`, `chevron-left`, `send` | Yes — `scaleX(-1)` |
| Non-directional | `plus`, `check`, `x`, `download`, `search`, `trash` | No |

---

## CSS Implementation

```css
/* ── Base ─────────────────────────────────────────────── */
.btn {
  display:         inline-flex;
  align-items:     center;
  justify-content: center;
  gap:             var(--btn-gap);
  height:          var(--btn-height);
  padding-inline:  var(--btn-padding-inline);
  border-radius:   var(--btn-radius);
  font-family:     var(--type-label-family);
  font-size:       var(--type-label-size);
  font-weight:     var(--type-label-weight);
  line-height:     1;
  white-space:     nowrap;
  cursor:          pointer;
  border:          none;
  text-decoration: none;
  transition:      background-color 150ms ease, border-color 150ms ease, color 150ms ease;
}

.btn:focus-visible {
  outline:        2px solid var(--border-color-focus);
  outline-offset: 2px;
}

.btn:disabled,
.btn[aria-disabled="true"] {
  cursor:         not-allowed;
  pointer-events: none;
}

/* ── Sizes ────────────────────────────────────────────── */
.btn-xl {
  --btn-height:         56px;
  --btn-padding-inline: var(--spacing-inset-xl);   /* 24px */
  --btn-gap:            var(--spacing-inline-sm);  /* 8px  */
  --btn-radius:         var(--radius-lg);          /* 12px */
  --btn-icon-size:      var(--icon-size-feature);  /* 24px */
  font-size:            var(--type-label-lg-size);
  font-weight:          var(--type-label-lg-weight);
}

.btn-lg {
  --btn-height:         48px;
  --btn-padding-inline: var(--spacing-inset-xl);   /* 24px */
  --btn-gap:            var(--spacing-inline-sm);  /* 8px  */
  --btn-radius:         var(--radius-lg);          /* 12px */
  --btn-icon-size:      var(--icon-size-default);  /* 20px */
  font-size:            var(--type-label-lg-size);
  font-weight:          var(--type-label-lg-weight);
}

.btn-md {
  --btn-height:         40px;
  --btn-padding-inline: var(--spacing-inset-lg);   /* 16px */
  --btn-gap:            var(--spacing-inline-sm);  /* 8px  */
  --btn-radius:         var(--radius-md);          /* 8px  */
  --btn-icon-size:      var(--icon-size-default);  /* 20px */
  font-size:            var(--type-label-size);
  font-weight:          var(--type-label-weight);
}

.btn-sm {
  --btn-height:         32px;
  --btn-padding-inline: var(--spacing-inset-md);   /* 12px */
  --btn-gap:            var(--spacing-inline-xs);  /* 4px  */
  --btn-radius:         var(--radius-md);          /* 8px  */
  --btn-icon-size:      var(--icon-size-inline);   /* 16px */
  font-size:            var(--type-label-sm-size);
  font-weight:          var(--type-label-sm-weight);
}

/* ── Variants ─────────────────────────────────────────── */

/* Primary */
.btn-primary {
  background-color: var(--bg-color-brand);
  color:            var(--text-color-on-brand);
  border:           none;
}
.btn-primary:hover  { background-color: var(--bg-color-brand-hover);    }
.btn-primary:active { background-color: var(--bg-color-brand-pressed);  }
.btn-primary:disabled,
.btn-primary[aria-disabled="true"] {
  background-color: var(--bg-color-disabled);
  color:            var(--text-color-disabled);
}

/* Secondary */
.btn-secondary {
  background-color: transparent;
  color:            var(--text-color-brand);
  border:           1.5px solid var(--border-color-brand);
}
.btn-secondary:hover  { background-color: var(--bg-color-brand-subtle); }
.btn-secondary:active { background-color: var(--bg-color-brand-hover);  }
.btn-secondary:disabled,
.btn-secondary[aria-disabled="true"] {
  color:            var(--text-color-disabled);
  border-color:     var(--border-color-disabled);
}

/* Tertiary */
.btn-tertiary {
  background-color: transparent;
  color:            var(--text-color-brand);
  border:           none;
}
.btn-tertiary:hover  { background-color: var(--bg-color-brand-subtle); }
.btn-tertiary:active { background-color: var(--bg-color-brand-hover);  }
.btn-tertiary:disabled,
.btn-tertiary[aria-disabled="true"] {
  color: var(--text-color-disabled);
}

/* ── Icon ─────────────────────────────────────────────── */
.btn-icon {
  width:       var(--btn-icon-size);
  height:      var(--btn-icon-size);
  flex-shrink: 0;
  stroke-width: 2;
}

/* Mirror directional icons in RTL */
[dir="rtl"] .btn-icon--directional {
  transform: scaleX(-1);
}

/* ── Icon Only ────────────────────────────────────────── */
.btn-icon-only {
  width:          var(--btn-height);
  padding-inline: 0;
}

/* ── Reduced motion ───────────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  .btn { transition: none; }
}
```

---

## Accessibility

### ARIA Roles & Attributes

| Element | Attribute | Value |
|---------|-----------|-------|
| `<button>` | `type` | `"button"` — always explicit (prevents accidental form submit) |
| `<button>` | `disabled` | Boolean — use with `aria-disabled="true"` for focusable-but-disabled state |
| `<button>` | `aria-label` | Required on icon-only buttons — describes the action in Arabic |
| `<button>` | `aria-pressed` | `"true"` / `"false"` for toggle buttons |
| `<button>` | `aria-busy` | `"true"` while a loading action is in progress |
| `<button>` | `aria-describedby` | Points to a tooltip ID when tooltip is present |
| Leading / trailing icon | `aria-hidden` | `"true"` — icons are decorative; the label carries the accessible name |
| Icon-only icon | `aria-hidden` | `"true"` — `aria-label` on the `<button>` provides the name |

### Disabled vs. Aria-Disabled

| Approach | Keyboard Focusable | Reads in Screen Reader | Tooltip Possible |
|----------|-------------------|----------------------|-----------------|
| `disabled` attribute | No | Announced as "dimmed" or skipped | No |
| `aria-disabled="true"` + `pointer-events: none` | **Yes** | Announced as "unavailable" | **Yes** |

Use `aria-disabled="true"` when the button needs a tooltip explaining **why** it is disabled.

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus to the button |
| `Shift + Tab` | Move focus away (backwards) |
| `Enter` | Trigger the button action |
| `Space` | Trigger the button action |

### Icon-Only Buttons

- `aria-label` must be a meaningful Arabic action phrase, not the icon name.
- Provide a visible tooltip that appears on focus and hover — not just hover.
- Minimum touch/click target: **44 × 44px** (WCAG 2.5.5).
  If the button is smaller than 44px (e.g., Small = 32px), add `padding: 6px` to extend the clickable area transparently, or use a wrapper with `min-width: 44px; min-height: 44px`.

### Color & Contrast

| Pair | Minimum Ratio | WCAG Level |
|------|--------------|------------|
| `text-color-on-brand` vs. `bg-color-brand` | 4.5:1 | AA — normal text |
| `text-color-brand` vs. transparent (white bg) | 4.5:1 | AA |
| Disabled text vs. disabled background | Not required — disabled states are exempt from contrast requirements |
| Focus ring vs. adjacent color | 3:1 | AA — UI component |

### Touch Targets

| Size | Button | Minimum tap target |
|------|--------|--------------------|
| XLarge | 56px | ✅ Passes 44px |
| Large | 48px | ✅ Passes 44px |
| Medium | 40px | ⚠️ Below 44px — extend with transparent padding |
| Small | 32px | ⚠️ Below 44px — extend with transparent padding |

```css
/* Extend tap target for Small and Medium without changing visual size */
.btn-sm,
.btn-md {
  position: relative;
}
.btn-sm::after,
.btn-md::after {
  content: '';
  position: absolute;
  inset: -6px; /* extends tap area to at least 44px */
}
```

### Loading State

When a button triggers an async action:

```html
<button class="btn btn-primary btn-md" aria-busy="true" aria-label="جارٍ الإرسال…">
  <svg class="btn-icon btn-spinner" aria-hidden="true"><!-- spinner --></svg>
  <span class="btn-label">جارٍ الإرسال…</span>
</button>
```

- Replace the leading/trailing icon with a spinner icon
- Keep the button **disabled** during loading (`aria-disabled="true"`)
- Update the `aria-label` to reflect the in-progress state

---

## Figma Component Structure

### Component Variants

```
Button
├── Variant: Primary / Secondary / Tertiary
├── Size:    XLarge / Large / Medium / Small
├── State:   Default / Hover / Pressed / Disabled / Focus
└── Icon:    None / Leading / Trailing / Icon Only
```

### Figma Variable Bindings

| Layer | Variable |
|-------|----------|
| Container fill (Primary / Default) | `semantic/bg-color-brand` |
| Container fill (Primary / Hover) | `semantic/bg-color-brand-hover` |
| Container fill (Primary / Pressed) | `semantic/bg-color-brand-pressed` |
| Container fill (Disabled) | `semantic/bg-color-disabled` |
| Container fill (Secondary / Hover) | `semantic/bg-color-brand-subtle` |
| Container stroke (Secondary) | `semantic/border-color-brand` |
| Container stroke (Secondary / Disabled) | `semantic/border-color-disabled` |
| Label fill (Primary) | `semantic/text-color-on-brand` |
| Label fill (Secondary / Tertiary) | `semantic/text-color-brand` |
| Label fill (Disabled) | `semantic/text-color-disabled` |
| Icon fill (Primary) | `semantic/icon-color-on-brand` |
| Icon fill (Secondary / Tertiary) | `semantic/icon-color-brand` |
| Icon fill (Disabled) | `semantic/icon-color-disabled` |
| Corner radius (XL / LG) | `semantic/radius-lg` |
| Corner radius (MD / SM) | `semantic/radius-md` |
| Padding inline (XL / LG) | `semantic/spacing-inset-xl` |
| Padding inline (MD) | `semantic/spacing-inset-lg` |
| Padding inline (SM) | `semantic/spacing-inset-md` |
| Gap (XL / LG / MD) | `semantic/spacing-inline-sm` |
| Gap (SM) | `semantic/spacing-inline-xs` |
| Icon size (XL) | `semantic/icon-size-feature` |
| Icon size (LG / MD) | `semantic/icon-size-default` |
| Icon size (SM) | `semantic/icon-size-inline` |
