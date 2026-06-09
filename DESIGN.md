---
project: Acadimiat Landing Page
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
ds: Acadimiat Design System
version: v1.0.0
acadimiat-theme: light | dark
---

# DESIGN.md — Acadimiat Design System

> **This document explains the system, not how to use it.**
> For enforcement rules, see `CLAUDE.md`. For spec details, see `Specs/`.

---

## Project DS — Built on Acadimiat v1

This repository is **Acadimiat Design System v1** — a custom, Arabic-first design system built from the ground up for the Acadimiat EdTech platform. It is not a fork or a theme of any existing system. Every token, component, and pattern was designed specifically for Arabic UI, RTL layout, and the Acadimiat product family.

The system feeds two consumers simultaneously:
- **Figma** — via Variables (Primitives as reference, Semantics as scoped variables)
- **Code** — via CSS custom properties following the same token names

When a token value changes in one place, it must change in both.

---

## Project Context

| Property | Value |
|----------|-------|
| Platform | Acadimiat — Arabic EdTech (courses, dashboards, assessments) |
| Products | Landing pages, user dashboards, mobile apps |
| Primary language | Arabic (RTL) |
| Secondary language | English (LTR, optional) |
| Design tool | Figma |
| CSS strategy | Custom properties (CSS variables), logical properties |
| Theming | Light and Dark via `data-theme` attribute on `<html>` |
| Responsive base | Mobile-first, base desktop at 1440px |
| Breakpoints | Tailwind v3 defaults (640 / 768 / 1024 / 1280 / 1536px) |
| Maintainer | n.ouda@eltgcc.com |

---

## Design Principles

These are not aspirational values — they are constraints that shaped every token and component decision.

### 1. Arabic First
The system is designed for Arabic text and RTL layout. English support is additive, not the baseline. Every spacing, sizing, and typographic decision was validated against Arabic script before Latin.

### 2. Token Discipline
No component ever hardcodes a value. Every color, size, radius, shadow, and spacing value is expressed as a token. This is what makes theming, dark mode, and multi-product deployment possible without touching component code.

### 3. Semantic Over Primitive
Designers and developers never ask "which shade of purple goes here?" — they ask "is this the primary action?" The semantic layer answers that question and insulates components from raw value changes.

### 4. Restraint in Motion
No animation exceeds 350ms. Transitions exist to confirm interactions and guide attention — not to impress. All motion respects `prefers-reduced-motion`.

### 5. Accessibility as Architecture
WCAG 2.1 AA is the floor, not a checklist item. Semantic tokens are pre-validated for contrast. Touch targets, focus rings, and ARIA patterns are specified at the system level — not left to individual implementations.

---

## Foundations — Primitive Token System

Foundations are the raw values the entire system is built on. They are **never applied directly to components**.

| Foundation | File | What It Defines |
|------------|------|-----------------|
| Color | `Specs/Foundations/Color.md` | 6 palettes × 10 steps: purple, neutral, green, yellow, blue, red. Plus base-white and white-alpha scale. |
| Typography | `Specs/Foundations/Typography.md` | Font families, weights (400–700), size scale (12px–72px), line heights, paragraph spacing. |
| Spacing | `Specs/Foundations/Spacing.md` | 4px-base scale from `space-0` to `space-24`. Inset, inline, stack, and layout patterns. |
| Border | `Specs/Foundations/Border.md` | Border width scale (0–4px) and border style tokens (solid, dashed, dotted). |
| Radius | `Specs/Foundations/Radius.md` | Border radius scale from `radius-none` to `radius-full`. |
| Elevation | `Specs/Foundations/Elevation.md` | 6 neutral shadow levels + brand (purple-tinted) shadow scale. |
| Motion | `Specs/Foundations/Motion.md` | 3 durations (150ms / 250ms / 350ms) + 4 easing curves. Max: 350ms. |
| Breakpoints | `Specs/Foundations/Breakpoints.md` | Tailwind v3 defaults. Mobile-first. Base desktop: 1440px. |
| Size | `Specs/Foundations/Size.md` | Fixed component heights and icon dimensions. |
| Icon | `Specs/Foundations/Icon.md` | Icon sizing primitives. Library: Lucide, stroke-width: 2. |
| Accessibility | `Specs/Foundations/Accessibilty.md` | WCAG 2.1 AA baseline, contrast ratios, touch target minimums. |

### Color Architecture

The color system uses a **10-step scale per palette** (50–900). Each step has a defined role:

| Range | Role |
|-------|------|
| 50–100 | Subtle backgrounds, tints |
| 200–400 | Borders, decorative fills, hover tints |
| 500 | Primary brand value — the canonical color |
| 600–700 | Hover and pressed states |
| 800–900 | Dark mode surfaces, deep backgrounds |

`purple-500` (#65398D) is the brand anchor. All brand-role Semantic tokens trace back to this value in Light theme.

---

## Semantic Token System

Semantic tokens are role-based aliases that sit between Primitives and Components. They are what components use. They are what changes between Light and Dark themes — never the token names, only the values.

### Naming Pattern

```
[category]-[type]-[role]
```

Examples: `text-color-primary`, `bg-color-brand`, `spacing-inset-lg`, `border-color-focus`

### Semantic Layers

| Layer | File | Token Pattern |
|-------|------|---------------|
| Text color | `Specs/Semantic/text-color.md` | `--text-color-*` |
| Background color | `Specs/Semantic/background-color.md` | `--bg-color-*` |
| Border color | `Specs/Semantic/border-color.md` | `--border-color-*` |
| Icon color | `Specs/Semantic/icon-color.md` | `--icon-color-*` |
| Icon size | `Specs/Semantic/icon-size.md` | `--icon-size-*` |
| Typography | `Specs/Semantic/typography.md` | `--type-label-*`, `--type-body-*`, `--type-heading-*` |
| Spacing | `Specs/Semantic/spacing.md` | `--spacing-inset-*`, `--spacing-stack-*`, `--spacing-inline-*`, `--spacing-layout-*` |
| Radius | `Specs/Semantic/radius.md` | `--radius-*` |
| Elevation | `Specs/Semantic/elevation.md` | `--elevation-*` |
| Chart color | `Specs/Semantic/chart-color.md` | `--chart-color-*` |

### Theming Model

Themes are additive CSS blocks. Token names never change between themes — only their resolved values.

```css
:root, [data-theme="light"] {
  --text-color-primary: var(--neutral-900);
  --bg-color-brand:     var(--purple-500);
}

[data-theme="dark"] {
  --text-color-primary: var(--base-white);
  --bg-color-brand:     var(--purple-400);
}
```

Adding a new theme (`[data-theme="high-contrast"]`, `[data-theme="brand-dark"]`) requires only a new CSS block — no component code changes.

---

## Components

Components are the top tier. Every visual value is expressed as a Semantic token — no exceptions.

### Component Spec Structure

Every component file follows this exact structure:

1. Philosophy
2. When to Use / When to Avoid
3. Anatomy (ASCII diagram)
4. Variants & States (all 5: Default, Hover, Pressed, Disabled, Focus)
5. Focus State spec
6. Sizes (token name + resolved px for every dimension)
7. Design Tokens Reference (color, spacing, typography, icon size, radius — full table)
8. RTL Behavior table
9. CSS Implementation (full, copy-pasteable)
10. Accessibility (ARIA, keyboard, touch targets, contrast)
11. Figma Component Structure (variant matrix + variable bindings)

### Current Components

| Component | File | Status |
|-----------|------|--------|
| Button | `Specs/Components/Button/button.md` | Active |

### Current Charts

| Chart | File | Status |
|-------|------|--------|
| Line Chart | `Specs/Charts/line-chart.md` | Active |
| Bar Chart | `Specs/Charts/bar-chart.md` | Active |
| Area Chart | `Specs/Charts/area-chart.md` | Active |
| Pie Chart | `Specs/Charts/pie-chart.md` | Active |
| Metric Card | `Specs/Charts/metric-card.md` | Active |

---

## Patterns

### RTL Layout Pattern

```
HTML root:  dir="rtl"  (default — Arabic)
Logical CSS: padding-inline, margin-block, inset-inline-start
Icon position: DOM order (not CSS order/float)
Directional icons: scaleX(-1) in RTL via [dir="rtl"] .icon--directional
Non-directional icons: never mirrored
Letter-spacing: never on Arabic text
```

### Spacing Pattern

Spacing is described by **role**, not by raw value.

| Role | When to use |
|------|-------------|
| `inset` | Padding inside a component boundary |
| `stack` | Vertical gap between stacked elements |
| `inline` | Horizontal gap between side-by-side elements |
| `layout` | Section and page-level spacing |

### Focus Pattern

Every interactive element uses the same focus ring — defined once at system level:

```css
:focus-visible {
  outline: 2px solid var(--border-color-focus);
  outline-offset: 2px;
}
```

`:focus-visible` always. `:focus` never. This prevents the focus ring appearing on mouse clicks while keeping it visible for keyboard navigation.

### Motion Pattern

| Interaction type | Duration token | Easing token |
|-----------------|----------------|--------------|
| Hover / toggle / button press | `duration-fast` (150ms) | `easing-out` |
| Dropdown / tooltip / tab | `duration-normal` (250ms) | `easing-out` |
| Modal / drawer / page transition | `duration-slow` (350ms) | `easing-in-out` |
| Spinner / progress bar | — | `easing-linear` |

Always wrap transitions in `@media (prefers-reduced-motion: reduce) { transition: none; }`.

---

## Enforcement

The design system enforces correctness at the spec level. These rules are stated explicitly in every Foundation file and carry over to every component built from this system.

**Tier contract:**
- Primitives → never reference other tiers
- Semantics → only reference Primitives
- Components → only reference Semantics

**Violation examples that must be caught in review:**

| What was written | Why it's wrong | Fix |
|-----------------|----------------|-----|
| `color: #65398D` in a component | Hardcoded hex bypasses theming | Use `var(--text-color-brand)` |
| `color: var(--purple-500)` in a component | Primitive in component skips Semantic tier | Use `var(--text-color-brand)` |
| `padding-left: 16px` | Direction-specific property breaks RTL | Use `padding-inline-start: var(--spacing-inset-lg)` |
| `letter-spacing: 0.05em` on Arabic text | Arabic script must never have letter-spacing | Remove it entirely |
| `transition: all 0.3s` | Targets too many properties, too slow | Use `transition: background-color 150ms ease` |

---

## Drift Detection

Drift = component code that no longer matches the spec. Drift accumulates when:

- A token is renamed in the spec but not updated in code
- A developer hardcodes a value because the token wasn't found
- A Figma value is updated without a corresponding spec update
- A component is built without consulting the spec

**How to detect it:**

1. Grep for raw hex values in component CSS → any `#` not inside a `:root` block is a violation
2. Grep for direction-specific properties → `padding-left`, `margin-right`, `right:`, `left:` in non-layout code
3. Grep for primitive token names in component files → `--purple-`, `--neutral-`, `--space-` inside component blocks
4. Check `last-updated` in frontmatter against git log — if the file hasn't changed but code has, the spec is stale

**When drift is found:**
- If code is wrong → fix code to match spec
- If spec is wrong → update spec first, then update code, then update Figma

The spec is the source of truth. Code and Figma follow.

---

## Versioning & Updates

The system follows **semantic versioning** at the spec level.

| Change type | Version bump | Examples |
|------------|--------------|---------|
| New token or component | Minor — `v1.1.0` | Adding a new Semantic token, new component spec |
| Token value change (non-breaking) | Patch — `v1.0.1` | Adjusting a shadow value, tweaking a spacing step |
| Token rename or removal | Major — `v2.0.0` | Renaming `bg-color-brand` → `bg-color-primary`, removing a primitive |
| New theme | Minor — `v1.1.0` | Adding `[data-theme="high-contrast"]` |

Token renames are **breaking changes**. Every consuming product must update. This is why names are stable and only values change across themes.

---

## When to Update Specs

| Trigger | Action |
|---------|--------|
| A new color is needed | Add to `Foundations/Color.md` → add Semantic alias in relevant Semantic file |
| A new component is designed | Create `Specs/Components/<Name>/<name>.md` with all 11 required sections |
| Dark mode value needs adjustment | Update the `[data-theme="dark"]` block in the affected Semantic file |
| A new product theme is introduced | Add new `[data-theme="x"]` CSS block to every Semantic file |
| A spacing value feels wrong in production | Validate against the 8px grid in `Foundations/Spacing.md` before changing |
| A new icon size is needed | Add to `Foundations/Icon.md` → add Semantic alias in `Semantic/icon-size.md` |
| Accessibility audit fails a component | Update `Foundations/Accessibilty.md` if it's a system-level gap, then fix the component spec |

**Never update a spec to match broken code.** Fix the code first.

---

## Why We Picked Acadimiat (Custom DS)

Existing design systems (Carbon, Material, Radix, Chakra) were evaluated and rejected for the following reasons:

| Criterion | Carbon / Material / others | Acadimiat DS |
|-----------|---------------------------|--------------|
| RTL support | Partial or bolted on | Native — every token and component is RTL-first |
| Arabic typography | Not designed for Arabic script | IBM Plex Sans Arabic, Readex Pro — Arabic-specific choices |
| Token naming | LTR-biased (`padding-left`, directional names) | Logical properties throughout |
| Brand fit | Generic neutral palettes | Built on `purple-500` (#65398D) — Acadimiat's exact brand |
| Scope | General-purpose, large bundle | Scoped to Acadimiat products — no unused components |
| Figma integration | Requires adapting their library | Token names match Figma variables 1:1 |
| Letter-spacing on Arabic | Frameworks often apply it globally | Explicitly prohibited at system level |
| Theme model | Often component-level theming | Single `data-theme` attribute, all tokens adapt |

A custom system costs more upfront. It pays back in every component that doesn't need an RTL workaround, every dark mode value that doesn't need a manual override, and every Arabic string that renders correctly without fighting a LTR-biased baseline.
