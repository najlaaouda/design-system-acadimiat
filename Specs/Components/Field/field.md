---
name: Text Input Field
tier: Component
status: Active
last-updated: 2026-07-07
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Text Input Field — Component Spec

## Philosophy

The Text Input Field is the primary control for collecting a single line of user-entered text — names, emails, search terms, form values. It communicates its current condition through state, not through color alone: a resting field, a focused field, a field holding a value, and a field in error must each be distinguishable without relying on color contrast as the only signal (a border-weight or icon change accompanies every color change). Every visual property — color, spacing, radius, typography, icon size — is resolved from semantic tokens, never from raw values.

> All spacing uses logical CSS properties (`padding-inline`, `padding-block`, `gap`).
> The field is RTL-first — label, placeholder, icon positions, and error text flip automatically via the document `dir` attribute.

---

## When to Use

- Collecting a single line of free-text input — names, emails, phone numbers, search queries, short answers
- Any form control that needs a label, helper text, or validation message attached

## When to Avoid

- Multi-line content — use a Textarea instead
- A closed set of choices — use Select, Radio, or Checkbox instead
- Binary on/off state — use a Toggle instead

---

## Anatomy

```
Label
┌─────────────────────────────────────────────┐
│  [leading icon]  Placeholder / Value  [trailing icon] │
└─────────────────────────────────────────────┘
Helper text / Error message
```

| Part | Description | Always Present |
|------|-------------|----------------|
| Label | Describes what the field collects | No |
| Container | The input surface — carries background, border, radius | Yes |
| Leading icon | Icon at the inline-start of the input (e.g. search, mail) | No |
| Input text | The typed value, or the placeholder when empty | Yes |
| Trailing icon | Icon at the inline-end (e.g. clear, password-toggle, error) | No |
| Helper text | Supporting instruction below the field | No |
| Error message | Replaces helper text when State = Error | No (only in Error state) |

> A field's Label sits outside the container, above it. Helper text and Error message sit outside the container, below it. Never place either inside the bordered container.

---

## Variants & States

Single visual style — no Elevated/Outlined/Filled split like Button or Card. State alone communicates condition.

| State | Background | Border | Text (value) | Helper/Error text |
|-------|-----------|--------|---------------|--------------------|
| Default | `bg-color-primary` | `border-color-primary` — 1px | `text-color-placeholder` (empty) | `text-color-tertiary` |
| Hover | `bg-color-primary` | `border-color-strong` — 1px | `text-color-placeholder` (empty) | `text-color-tertiary` |
| Pressed | `bg-color-primary` | `border-color-focus` — 2px | `text-color-placeholder` (empty) | `text-color-tertiary` |
| Filled | `bg-color-primary` | `border-color-primary` — 1px | `text-color-primary` (value) | `text-color-tertiary` |
| Focus | `bg-color-primary` | `border-color-focus` — 2px | `text-color-primary` (value) | `text-color-tertiary` |
| Error | `bg-color-primary` | `border-color-error` — 2px | `text-color-primary` (value) | `text-color-error` |
| Disabled | `bg-color-disabled` | `border-color-disabled` — 1px | `text-color-disabled` | `text-color-disabled` |

> Hover and Pressed are transient pointer states (Pressed = actively clicking into the field, the instant before Focus takes over) and are included because every component spec in this repo covers the mandatory five (Default/Hover/Pressed/Disabled/Focus) — see `CLAUDE.md`. Filled and Error extend that base set; they never replace one of the five.
> Pressed and Focus share the same 2px focus-colored border by design — Pressed is the mouse-down instant immediately before the field receives focus.
> Error takes visual precedence over Filled — a filled field that fails validation shows the Error border and Error helper text, not the Filled treatment.

---

## Focus State

| Property | Value | Token |
|----------|-------|-------|
| Border color | `border-color-focus` | `--border-color-focus` |
| Border width | 2px | — |
| Border style | solid | — |

```css
.field-input:focus-visible {
  border-color: var(--border-color-focus);
}
```

> Focus is expressed as a border-color and border-width change on the container itself (not a separate outline ring) — the field's own border doubling in weight is the focus indicator. This differs from Button/Card, which use a detached `outline`, because a field's border is already the primary affordance boundary; adding a second detached ring around a small, dense form control reads as visual noise.

---

## Sizes

| Size | Height | padding-inline | Icon Size | Typography (value) | Radius |
|------|--------|-----------------|-----------|----------------------|--------|
| Large | 48px | `spacing-md` — 16px | `icon-size-default` — 20px | `type-body-lg` | `radius-md` — 8px |
| Medium | 40px | `spacing-md` — 16px | `icon-size-default` — 20px | `type-body` | `radius-md` — 8px |
| Small | 32px | `spacing-sm` — 8px | `icon-size-inline` — 16px | `type-body-sm` | `radius-sm` — 4px |

---

## Design Tokens Reference

### Color Tokens

| Role | Default | Hover | Pressed | Filled | Focus | Error | Disabled |
|------|---------|-------|---------|--------|-------|-------|----------|
| Background | `--bg-color-primary` | `--bg-color-primary` | `--bg-color-primary` | `--bg-color-primary` | `--bg-color-primary` | `--bg-color-primary` | `--bg-color-disabled` |
| Border | `--border-color-primary` | `--border-color-strong` | `--border-color-focus` | `--border-color-primary` | `--border-color-focus` | `--border-color-error` | `--border-color-disabled` |
| Value text | `--text-color-placeholder` | `--text-color-placeholder` | `--text-color-placeholder` | `--text-color-primary` | `--text-color-primary` | `--text-color-primary` | `--text-color-disabled` |
| Label text | `--text-color-secondary` | `--text-color-secondary` | `--text-color-secondary` | `--text-color-secondary` | `--text-color-secondary` | `--text-color-error` | `--text-color-disabled` |
| Helper/Error text | `--text-color-tertiary` | `--text-color-tertiary` | `--text-color-tertiary` | `--text-color-tertiary` | `--text-color-tertiary` | `--text-color-error` | `--text-color-disabled` |
| Leading/Trailing icon | `--icon-color-secondary` | `--icon-color-secondary` | `--icon-color-secondary` | `--icon-color-secondary` | `--icon-color-secondary` | `--icon-color-error` | `--icon-color-disabled` |

### Spacing Tokens

| Property | Large | Medium | Small |
|----------|-------|--------|-------|
| `padding-inline` | `--spacing-md` (16px) | `--spacing-md` (16px) | `--spacing-sm` (8px) |
| Gap (icon ↔ text) | `--spacing-sm` (8px) | `--spacing-sm` (8px) | `--spacing-xs` (4px) |
| Label ↔ container gap | `--spacing-xs` (4px) | `--spacing-xs` (4px) | `--spacing-xs` (4px) |
| Container ↔ helper text gap | `--spacing-xs` (4px) | `--spacing-xs` (4px) | `--spacing-xs` (4px) |

### Typography Tokens

| Element | Large | Medium | Small |
|---------|-------|--------|-------|
| Label | `type-label-sm` | `type-label-sm` | `type-label-sm` |
| Value / Placeholder | `type-body-lg` | `type-body` | `type-body-sm` |
| Helper / Error text | `type-caption` | `type-caption` | `type-caption` |

### Icon Size Tokens

| Size | Token | Value |
|------|-------|-------|
| Large / Medium | `--icon-size-default` | 20px |
| Small | `--icon-size-inline` | 16px |

### Radius Tokens

| Size | Token | Value |
|------|-------|-------|
| Large / Medium | `--radius-md` | 8px |
| Small | `--radius-sm` | 4px |

---

## RTL Behavior

| Property | Approach |
|----------|----------|
| Text direction | Inherited from `dir="rtl"` on `<html>` — no override needed |
| Icon position | Controlled by DOM order, not CSS `order` or `float` |
| Horizontal padding | `padding-inline` — resolves to start/end, not left/right |
| Label / helper text alignment | `text-align: start` — resolves to right in RTL, left in LTR |
| Directional icons (e.g. calendar-arrow) | Mirror with `transform: scaleX(-1)` in RTL |
| Non-directional icons (search, mail, error, clear) | Never mirror |

---

## Motion & Animation

| Interaction | Property | Duration | Easing | Effect |
|------------|----------|----------|--------|--------|
| Hover enter/leave | `border-color` | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Border tints to `border-color-strong` |
| Focus enter/leave | `border-color`, `border-width` | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Border widens to 2px and shifts to `border-color-focus` |
| Error enter | `border-color`, `border-width` | 200ms | `cubic-bezier(0, 0, 0.2, 1)` | Border widens to 2px and shifts to `border-color-error`; helper text swaps to error message |

> `prefers-reduced-motion` removes the border-width transition, snapping directly between states.

---

## CSS Implementation

```css
/* ── Base ─────────────────────────────────────────────── */
.field {
  display:        flex;
  flex-direction: column;
  gap:             var(--spacing-xs);
}

.field-label {
  font-family: var(--type-label-sm-family);
  font-size:   var(--type-label-sm-size);
  font-weight: var(--type-label-sm-weight);
  color:       var(--text-color-secondary);
}

.field-input-wrapper {
  display:          inline-flex;
  align-items:      center;
  gap:              var(--field-gap);
  height:           var(--field-height);
  padding-inline:   var(--field-padding-inline);
  border-radius:    var(--field-radius);
  background-color: var(--bg-color-primary);
  border:           1px solid var(--border-color-primary);
  transition:
    border-color 200ms cubic-bezier(0, 0, 0.2, 1),
    border-width 200ms cubic-bezier(0, 0, 0.2, 1);
}

.field-input-wrapper:hover {
  border-color: var(--border-color-strong);
}

.field-input-wrapper:has(.field-input:focus-visible) {
  border-width: 2px;
  border-color: var(--border-color-focus);
}

.field-error .field-input-wrapper {
  border-width: 2px;
  border-color: var(--border-color-error);
}

.field-disabled .field-input-wrapper {
  background-color: var(--bg-color-disabled);
  border-color:     var(--border-color-disabled);
}

.field-input {
  flex: 1;
  border:  none;
  outline: none;
  background: transparent;
  font-family: var(--type-body-family);
  font-size:   var(--type-body-size);
  color:       var(--text-color-primary);
}

.field-input::placeholder {
  color: var(--text-color-placeholder);
}

.field-disabled .field-input {
  color: var(--text-color-disabled);
  cursor: not-allowed;
}

.field-icon {
  width:       var(--field-icon-size);
  height:      var(--field-icon-size);
  flex-shrink: 0;
  color:       var(--icon-color-secondary);
}

.field-error .field-icon {
  color: var(--icon-color-error);
}

.field-disabled .field-icon {
  color: var(--icon-color-disabled);
}

.field-helper-text {
  font-family: var(--type-caption-family);
  font-size:   var(--type-caption-size);
  color:       var(--text-color-tertiary);
}

.field-error .field-helper-text {
  color: var(--text-color-error);
}

.field-disabled .field-helper-text {
  color: var(--text-color-disabled);
}

/* ── Sizes ────────────────────────────────────────────── */
.field-lg {
  --field-height:         48px;
  --field-padding-inline: var(--spacing-md); /* 16px */
  --field-gap:            var(--spacing-sm); /* 8px */
  --field-radius:         var(--radius-md);  /* 8px */
  --field-icon-size:      var(--icon-size-default); /* 20px */
}

.field-md {
  --field-height:         40px;
  --field-padding-inline: var(--spacing-md); /* 16px */
  --field-gap:            var(--spacing-sm); /* 8px */
  --field-radius:         var(--radius-md);  /* 8px */
  --field-icon-size:      var(--icon-size-default); /* 20px */
}

.field-sm {
  --field-height:         32px;
  --field-padding-inline: var(--spacing-sm); /* 8px */
  --field-gap:            var(--spacing-xs); /* 4px */
  --field-radius:         var(--radius-sm);  /* 4px */
  --field-icon-size:      var(--icon-size-inline); /* 16px */
}

/* ── Reduced motion ───────────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  .field-input-wrapper {
    transition: border-color 150ms ease;
  }
}
```

---

## Accessibility

### ARIA Roles & Attributes

| Element | Attribute | Value |
|---------|-----------|-------|
| `<input>` | `id` | Unique, referenced by the `<label for>` |
| `<label>` | `for` | Matches the input's `id` — never rely on visual proximity alone |
| `<input>` | `aria-invalid` | `"true"` when State = Error |
| `<input>` | `aria-describedby` | Points to the helper/error text element's `id` |
| `<input>` | `aria-disabled` / `disabled` | Set when State = Disabled |
| `<input>` | `required` + `aria-required` | Set when the field is mandatory |
| Leading/trailing icon | `aria-hidden` | `"true"` — decorative; the label carries the accessible name |
| Error icon (if trailing) | `aria-hidden` | `"true"` — the error is announced via `aria-invalid` + `aria-describedby`, not the icon |

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus to the field |
| `Shift + Tab` | Move focus away (backwards) |
| Standard text-editing keys | Native `<input>` behavior — no custom handling |

### Color & Contrast

| Pair | Minimum Ratio | WCAG Level |
|------|--------------|------------|
| `text-color-primary` (value) vs. `bg-color-primary` | 4.5:1 | AA — normal text |
| `text-color-placeholder` vs. `bg-color-primary` | 4.5:1 | AA — normal text |
| `border-color-focus` / `border-color-error` vs. `bg-color-primary` | 3:1 | AA — UI component |
| Disabled text vs. disabled background | Not required — disabled states are exempt |

> Error is never signaled by border color alone — the border width also increases to 2px, and the helper text switches to the error message. This satisfies WCAG 1.4.1 (Use of Color) by pairing the color change with a shape/weight change and a textual message.

### Touch Targets

| Size | Height | Minimum tap target |
|------|--------|--------------------|
| Large | 48px | ✅ Passes 44px |
| Medium | 40px | ⚠️ Below 44px — extend with transparent padding via a wrapping `min-height: 44px` |
| Small | 32px | ⚠️ Below 44px — extend with transparent padding via a wrapping `min-height: 44px` |

---

## Figma Component Structure

### Component Variants

```
Field (component set)
├── Size:  Large / Medium / Small
├── State: Default / Hover / Pressed / Filled / Focus / Error / Disabled
├── Show Label:        boolean component property
├── Label Text:        text component property
├── Show Leading Icon: boolean component property
├── Leading Icon:      instance-swap component property
├── Show Trailing Icon: boolean component property
├── Trailing Icon:     instance-swap component property
├── Value Text:        text component property
├── Placeholder Text:  text component property
├── Show Helper Text:  boolean component property
└── Helper Text:       text component property
```

> Icons and text content are modeled as component properties (boolean visibility + text/instance-swap), not variant values — this keeps the variant matrix to Size×State (21 variants) instead of multiplying by every content combination.

> Container background/border/text/icon colors, sizing (Height, Padding Inline, Gap, Icon Size, Radius), Label Gap, and Border Width are all centralized in a dedicated `Field` Figma variable collection — the same pattern as the `Button` collection. Components bind to `Field/*` variables, each of which aliases the corresponding Semantic token (color/spacing/radius tokens) or holds a flat raw value (font sizes, border widths — sized properties with no existing Semantic token). `Field/Placeholder Font Size` and `Field/Label Font Size` are flat 16px/14px shared across all sizes — value/placeholder/label text does not scale with Size the way Button's label does; only the container dimensions do.

### Figma Variable Bindings

| Layer | Variable |
|-------|----------|
| Container fill (Default/Hover/Pressed/Filled/Focus/Error) | `Field/Background Default` → `semantic/bg-color-primary` |
| Container fill (Disabled) | `Field/Background Disabled` → `semantic/bg-color-disabled` |
| Container stroke (Default, Filled) | `Field/Border Default` → `semantic/border-color-primary` |
| Container stroke (Hover) | `Field/Border Hover` → `semantic/border-color-strong` |
| Container stroke (Pressed, Focus) | `Field/Border Focus` → `semantic/border-color-focus` |
| Container stroke (Error) | `Field/Border Error` → `semantic/border-color-error` |
| Container stroke (Disabled) | `Field/Border Disabled` → `semantic/border-color-disabled` |
| Border width (Default, Filled, Hover, Disabled) | `Field/Border Width` — flat 1px |
| Border width (Pressed, Focus, Error) | `Field/Border Width Active` — flat 2px |
| Value text (Default, Hover, Pressed — empty) | `Field/Text Placeholder` → `semantic/text-color-placeholder` |
| Value text (Filled, Focus, Error) | `Field/Text Value` → `semantic/text-color-primary` |
| Value text (Disabled) | `Field/Text Disabled` → `semantic/text-color-disabled` |
| Value/Placeholder font size (all sizes) | `Field/Placeholder Font Size` — flat 16px |
| Label text | `Field/Text Label` → `semantic/text-color-secondary` |
| Label text (Error) | `Field/Text Label Error` → `semantic/text-color-error` |
| Label font size (all sizes) | `Field/Label Font Size` — flat 14px |
| Label ↔ container gap | `Field/Label Gap` → `semantic/spacing-xs` |
| Helper text | `Field/Text Helper` → `semantic/text-color-tertiary` |
| Helper text (Error) | `Field/Text Helper Error` → `semantic/text-color-error` |
| Icon fill | `Field/Icon Default` → `semantic/icon-color-secondary` |
| Icon fill (Error) | `Field/Icon Error` → `semantic/icon-color-error` |
| Icon fill (Disabled) | `Field/Icon Disabled` → `semantic/icon-color-disabled` |
| Corner radius (Large / Medium) | `Field/Radius` → `semantic/radius-md` |
| Corner radius (Small) | `Field/Radius` → `semantic/radius-sm` |
| Padding inline (Large / Medium) | `Field/Padding Inline` → `semantic/spacing-md` |
| Padding inline (Small) | `Field/Padding Inline` → `semantic/spacing-sm` |
| Icon size (Large / Medium) | `Field/Icon Size` → `semantic/icon-size-default` |
| Icon size (Small) | `Field/Icon Size` → `semantic/icon-size-inline` |
| Container height | `Field/Height` — raw px per size (48/40/32) |
