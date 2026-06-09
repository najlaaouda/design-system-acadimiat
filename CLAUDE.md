# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

> **READ THIS FIRST. Every session. No exceptions.**
> This file is enforcement, not documentation. Violations produce incorrect specs and break the token contract between design and code.

This product is built on the **Acadimiat Design System** — a three-tier token architecture (Primitives → Semantic → Components). Every spec in this repo feeds both Figma variables and CSS custom properties for all Acadimiat products: landing pages, dashboards, mobile apps. **Always resolve tokens downward. Never skip a tier.**

---

## Files at a Glance

```
Specs/
├── Foundations/          ← Primitive tokens — raw values, reference only, never apply directly
│   ├── Color.md          — palettes: purple, neutral, green, yellow, blue, red, alpha
│   ├── Typography.md     — font families, weights, sizes, line heights, paragraph spacing
│   ├── Spacing.md        — 4px-base scale (space-0 → space-24), inset/inline/stack patterns
│   ├── Border.md         — border width scale + border style tokens
│   ├── Radius.md         — border radius scale
│   ├── Elevation.md      — shadow/depth scale
│   ├── Motion.md         — duration and easing tokens
│   ├── Breakpoints.md    — responsive breakpoints
│   ├── Size.md           — fixed size scale (heights, icon sizes)
│   ├── Icon.md           — icon sizing primitives
│   └── Accessibilty.md   — contrast ratios and minimum touch target rules
│
├── Semantic/             ← Role-based aliases — these are what components use
│   ├── text-color.md     — --text-color-primary/secondary/brand/error/…
│   ├── background-color.md — --bg-color-brand/subtle/disabled/…
│   ├── border-color.md   — --border-color-brand/focus/disabled/…
│   ├── icon-color.md     — --icon-color-brand/on-brand/disabled/…
│   ├── icon-size.md      — --icon-size-inline/default/feature
│   ├── typography.md     — --type-label/type-label-lg/type-body/… composite tokens
│   ├── spacing.md        — --spacing-inset-*/spacing-inline-*/spacing-stack-*
│   ├── radius.md         — --radius-sm/md/lg/full
│   ├── elevation.md      — --elevation-* shadow tokens
│   └── chart-color.md    — --chart-color-* for data visualisation
│
├── Components/           ← Component specs — consume Semantic tokens only
│   └── Button/
│       └── button.md     — Primary/Secondary/Tertiary, sizes SM→XL, RTL, a11y, CSS
│
└── Charts/               ← Chart component specs
    ├── line-chart.md
    ├── bar-chart.md
    ├── area-chart.md
    ├── pie-chart.md
    └── metric-card.md
```

---

## When to Update Specs

- A new token is needed → add it to the correct Foundation file, then create or update its Semantic alias.
- A component is added → create `Specs/Components/<ComponentName>/<component-name>.md` following the Component rules below.
- A token value changes → update the Foundation file. Semantic files reference primitives by name — they update automatically.
- A theme variant is added → add a new `[data-theme="x"]` block to every affected Semantic file. Token names never change.

Never change a token **name** without updating every spec file that references it. Names are the contract.

---

## Token Rules — Non-Negotiable

1. **Components reference Semantic tokens only.** A component spec that shows `--purple-500` directly is wrong.
2. **Semantic tokens reference Primitive tokens only.** A Semantic file that hardcodes `#65398D` is wrong.
3. **Primitive tokens have no Figma scope.** They are reference tables, not applied variables.
4. **Tokens flow downward only.** Semantic → Primitive. Never Primitive → Semantic back-reference.
5. **Token names are stable.** Only values change across themes. Rename = breaking change.

---

## Primitive vs Semantic — How to Tell Them Apart

| | Primitive | Semantic |
|---|---|---|
| File location | `Specs/Foundations/` | `Specs/Semantic/` |
| Naming | `purple-500`, `space-4`, `radius-md` | `bg-color-brand`, `text-color-primary`, `spacing-inset-lg` |
| CSS location | `:root` (always) | `:root` + `[data-theme="dark"]` |
| Figma scope | None — reference only | Scoped to Fill / Stroke / Text / etc. |
| Used in components | Never | Always |

---

## Allowed `px` Exceptions

The system uses `rem` for type and spacing. Raw `px` is allowed **only** for:

- Focus ring: `outline: 2px`, `outline-offset: 2px`
- Border width on components: `1.5px` (Secondary button stroke)
- Fixed component heights in size tables: `32px`, `40px`, `48px`, `56px`
- Icon `width`/`height` when set by a size token (`--icon-size-default` resolves to `20px`)

Everything else must use a token.

---

## Pattern Rules

### Spec frontmatter — required on every file

```yaml
---
name: <Token or Component Name>
tier: Primitive | Semantic | Component
status: Active | Draft | Deprecated
last-updated: YYYY-MM-DD
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---
```

`tier` governs where the token sits in the hierarchy. Get it wrong and the architecture breaks.

### Primitive token file — required sections

1. Philosophy paragraph + "do not use directly" callout
2. Token table (Token | px or Hex | Usage)
3. CSS custom properties block under `:root`
4. Figma Variables table (Collection | Variable | Value | Scope = None)

### Semantic token file — required sections

1. Philosophy paragraph + "use these in components" callout
2. Token table (Token | Light value → primitive | Dark value → primitive | Usage)
3. CSS block for `[data-theme="light"]` and `[data-theme="dark"]`
4. Figma Variables table (Collection | Variable | Light Value | Dark Value | Scope)

### Component spec file — required sections

1. Philosophy paragraph
2. When to Use / When to Avoid
3. Anatomy diagram (ASCII)
4. Variants & States tables (all states: Default, Hover, Pressed, Disabled, Focus)
5. Focus State (always `:focus-visible`, never `:focus`)
6. Sizes table (height, padding-inline, icon size, gap, radius — all as token names + resolved px)
7. Design Tokens Reference (color, spacing, typography, icon size, radius — token name for every value)
8. RTL Behavior table
9. CSS Implementation (full class block)
10. Accessibility (ARIA attributes, keyboard nav, touch targets, contrast pairs)
11. Figma Component Structure (variant matrix + variable bindings table)

---

## Component Rules

- Every visual value in a component spec must show the **Semantic token name** (`--bg-color-brand`), never a raw value.
- Sizes are listed as both token name and resolved px — e.g. `--spacing-inset-xl` (24px).
- States covered: Default, Hover, Pressed, Disabled, Focus. No state may be omitted.
- Shape modifiers (rounded, pill) are a separate axis from size — documented in a dedicated Radius Shape Modifiers table.
- Icon-only variants require a separate size table (square dimensions).
- Loading state must be documented with full CSS (`.btn-loading`, `.btn-spinner`, `@keyframes`) if the component triggers async actions.
- Motion must be documented in a dedicated **Motion & Animation** table showing duration, easing, and visible effect per interaction.

---

## RTL and Arabic

- `dir="rtl"` on `<html>` is the default. Specs assume RTL unless noted.
- Use **logical CSS properties** everywhere: `padding-inline`, `margin-block`, `inset-inline-start`. Never `left` / `right`.
- Icon position = **DOM order**, not CSS `order` or `float`.
- **Directional icons** (arrow-right, arrow-left, chevron-right, chevron-left, send) → mirror with `transform: scaleX(-1)` in RTL. Class: `.btn-icon--directional`.
- **Non-directional icons** (plus, check, x, download, search, trash) → never mirror.
- No `letter-spacing` on Arabic text. Ever. Not even `0`.
- `font-family` for Arabic text always leads with `'IBM Plex Sans Arabic'`.
- On the landing page (`data-product="landing"`), display/heading-1/heading-2 use `'El Messiri'` at weight 480 — applied via the `[data-product="landing"]` CSS block in `Semantic/typography.md`, not inline.

---

## Accessibility — Block-Level Rules

These apply to every component spec written in this repo:

- Minimum contrast: **4.5:1** for normal text, **3:1** for UI components and large text (WCAG AA).
- Minimum touch target: **44 × 44px**. Components smaller than 44px must document the transparent padding workaround.
- Focus ring: `2px solid var(--border-color-focus)`, `outline-offset: 2px`, always on `:focus-visible`.
- Icon-only elements: `aria-label` required, must be a meaningful Arabic action phrase.
- Disabled state: prefer `aria-disabled="true"` + `pointer-events: none` over the `disabled` attribute when a tooltip is needed.
- Decorative icons: always `aria-hidden="true"`.

---

## Before Any Spec Change

1. Check the tier — are you editing the right file (Foundation vs Semantic)?
2. If renaming a token, grep all spec files for the old name first.
3. If a Semantic token value changes for dark theme, verify the primitive it references still exists in `Foundations/Color.md`.
4. If adding a new component, confirm every token it references already exists in `Specs/Semantic/`.

---

## Design Decisions — Quick Reference

| Decision | Value |
|----------|-------|
| Brand color | `#65398D` → `purple-500` |
| Primary font | `'IBM Plex Sans Arabic'` |
| Landing page headings | `'El Messiri'` — weight 480 (variable font), display + heading-1 + heading-2 only |
| Alt font | `'Readex Pro'` — dashboard-heavy interfaces only |
| Latin font | `'Inter'` — English content only |
| Icon library | Lucide Icons — `stroke-width: 2`, never filled |
| Spacing base | 4px unit, 8px grid |
| Theme control | `data-theme` on `<html>` (light/dark) + `data-product="landing"` for landing page font overrides |
| Focus ring | `2px solid --border-color-focus`, offset 2px, `:focus-visible` |
| Transition | `200ms cubic-bezier(0,0,0.2,1)` on color + box-shadow + transform; `150ms` on transform press |

---

## Final Reminder

> Primitives are a reference table. Semantics are the contract. Components are the implementation.
> If a component reaches past Semantics into Primitives, the theme system breaks.
> If a Semantic token hardcodes a hex value, the primitive layer is bypassed.
> Keep the tiers clean.
