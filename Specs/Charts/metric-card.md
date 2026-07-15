---
name: Metric Card
tier: Component
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Metric Card — Component Spec

## Purpose

The Metric Card displays a **single KPI value** with its context — a label, a trend indicator, and optionally a sparkline. It is the primary component for dashboard overviews where multiple metrics need to be scanned quickly.

---

## When to Use

- Dashboard summary rows showing top-level KPIs
- Displaying a single value with its change vs. a previous period
- Quick scanning of multiple metrics side by side
- Highlighting positive, negative, or neutral performance at a glance

## When to Avoid

- Comparing two or more values with equal importance → use a chart
- Displaying more than one metric in the same card → use separate cards
- When the trend context is not available — show a plain stat instead

---

## Anatomy

| Part | Description | Token |
|------|-------------|-------|
| Card container | Outer surface | `bg-color-secondary`, `radius-xl`, `elevation-card` |
| Label | Metric name — "Total Revenue", "New Students" | `type-label`, `text-color-secondary` |
| Value | The primary KPI number | `type-heading-3`, `text-color-primary` |
| Trend badge | % change vs. previous period | See Trend Badge section |
| Trend icon | Arrow icon indicating direction | `icon-size-sm` (18px) |
| Period label | Context text — "vs. last month" | `type-caption`, `text-color-tertiary` |
| Sparkline *(optional)* | Mini line or bar chart showing recent trend | `chart-color-1`, `chart-grid-color` |
| Divider *(optional)* | Separator between value and sparkline | `border-color-primary` |

---

## Variants

### By Trend Direction

| Variant | Trend Color | Icon | Usage |
|---------|------------|------|-------|
| Positive | `text-color-success` / `bg-color-success` | `trending-up` | Value increased vs. previous period |
| Negative | `text-color-error` / `bg-color-error` | `trending-down` | Value decreased vs. previous period |
| Neutral | `text-color-secondary` / `bg-color-tertiary` | `minus` | No significant change |

### By Sparkline

| Variant | Description | When to Use |
|---------|-------------|-------------|
| No sparkline | Label + Value + Trend only | Compact dashboards, small grid cells |
| Sparkline line | Mini line chart below the value | When recent trend shape matters |
| Sparkline bar | Mini bar chart below the value | When period-by-period values matter |

### By Size

| Variant | Use Case |
|---------|----------|
| Default | Standard dashboard grid (4-column layout) |
| Compact | Dense grids, sidebar stats |
| Large | Hero KPI — single prominent metric |

---

## Trend Badge

The trend badge combines an icon + percentage value in a pill.

| Element | Token |
|---------|-------|
| Badge background (positive) | `--bg-color-success` |
| Badge background (negative) | `--bg-color-error` |
| Badge background (neutral) | `--bg-color-tertiary` |
| Badge text (positive) | `--text-color-success` |
| Badge text (negative) | `--text-color-error` |
| Badge text (neutral) | `--text-color-secondary` |
| Badge radius | `--radius-full` |
| Badge padding | `--spacing-xs` inline, `--spacing-xs` block |
| Badge typography | `type-label-sm` |
| Icon | `trending-up` / `trending-down` / `minus` |
| Icon size | `--icon-size-sm` (18px) |

---

## Design Tokens

### Colors

| Element | Token |
|---------|-------|
| Card background | `--bg-color-secondary` |
| Label | `--text-color-secondary` |
| Value | `--text-color-primary` |
| Period label | `--text-color-tertiary` |
| Card border | `--border-color-primary` |
| Sparkline line | `--chart-color-1` |
| Sparkline area | `--chart-color-1` @ 12% opacity |
| Sparkline grid | `--chart-grid-color` |

### Spacing

| Element | Token | Value |
|---------|-------|-------|
| Card padding | `--spacing-lg` | 24px |
| Gap: label → value | `--spacing-xs` | 4px |
| Gap: value → trend | `--spacing-xs` | 4px |
| Gap: trend → period | `--spacing-xs` | 4px |
| Gap: value → sparkline | `--spacing-md` | 16px |
| Gap between icon and % | `--spacing-xs` | 4px |

### Typography

| Element | Token |
|---------|-------|
| Label | `type-label` |
| Value (default) | `type-heading-3` |
| Value (compact) | `type-heading-5` |
| Value (large) | `type-heading-1` |
| Trend % | `type-label-sm` |
| Period label | `type-caption` |

### Elevation & Radius

| Element | Token |
|---------|-------|
| Card shadow | `--elevation-card` |
| Card shadow on hover | `--elevation-card-hover` |
| Card radius | `--radius-xl` |
| Trend badge radius | `--radius-full` |

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| xs — Mobile | Full width cards stacked vertically, sparkline hidden by default |
| md — Tablet | 2-column grid |
| xl — Desktop | 4-column grid, sparkline shown, full hover interactions |

---

## States

### Loading State

| Element | Value |
|---------|-------|
| Value | Skeleton line — 60% width, `type-heading-3` height |
| Label | Skeleton line — 40% width |
| Trend badge | Skeleton pill |
| Sparkline | Skeleton rectangle |

### Error State

When the metric fails to load, display within the card area.

| Element | Value |
|---------|-------|
| Icon | `alert-circle` — `icon-color-error` — `icon-size-default` |
| Message | Unable to load — `type-body-sm`, `text-color-secondary` |
| Action | Retry link |

### No Change State

When the value is identical to the previous period.

| Element | Value |
|---------|-------|
| Trend badge | Neutral variant |
| Icon | `minus` |
| Text | `0%` |

---

## Accessibility

### ARIA Markup

| Element | Attribute | Value |
|---------|-----------|-------|
| Card container (static) | `role` | `"region"` |
| Card container (static) | `aria-label` | Full readable sentence — see pattern below |
| Card container (interactive / link) | `role` | `"link"` or wrap in `<a>` |
| Card container (interactive) | `aria-label` | Same full sentence + `", view details"` |
| Trend icon | `aria-hidden` | `"true"` — direction conveyed by text, not icon |
| Trend badge | `aria-label` | `"up 12%"` / `"down 3%"` / `"no change"` |
| Sparkline SVG | `aria-hidden` | `"true"` — decorative; hidden data table below provides the data |
| Sparkline data table | `class` | `"sr-only"` |
| Loading skeleton | `aria-busy` | `"true"` on the card container while loading |
| Loading skeleton | `aria-label` | `"Loading [metric label]"` |

### Card `aria-label` Pattern

The card's `aria-label` (or `aria-labelledby` pointing to a visually hidden `<span>`) must be a complete, readable sentence:

```
"[Label]: [Value], [trend direction] [percentage] compared to [period]"
```

Examples:
```
"Total Revenue: 124,500 SAR, up 12% compared to last month"
"New Students: 1,240, up 8% compared to last week"
"Conversion Rate: 4.2%, no change compared to last month"
"Course Completions: 847, down 3% compared to last month"
```

This ensures screen reader users hear a meaningful summary in one pass without navigating into the card.

### Sparkline Hidden Data Table

The sparkline is `aria-hidden`. Provide a visually hidden table for the last N data points:

```html
<table class="sr-only" aria-label="Total Revenue — last 6 months">
  <thead><tr><th>Month</th><th>Revenue (SAR)</th></tr></thead>
  <tbody>
    <tr><td>Jan</td><td>98,000</td></tr>
    <tr><td>Feb</td><td>104,500</td></tr>
    <!-- ... -->
  </tbody>
</table>
```

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus to the card (if interactive) |
| `Enter` / `Space` | Navigate to detail view (if the card is a link) |

Cards that are purely display (non-interactive) must NOT receive keyboard focus — they should not be in the tab order.

### Color & Visual

- Trend direction must NEVER be communicated by color alone. Always combine:
  - The trend icon (`trending-up`, `trending-down`, `minus`)
  - Text (`+12%`, `-3%`, `0%`) with an explicit sign or word ("up", "down")
  - The `aria-label` on the badge
- Minimum contrast ratios:
  - Trend badge text vs. badge background: **4.5:1** (WCAG AA normal text)
  - Metric value vs. card background: **4.5:1**
  - Label vs. card background: **4.5:1**
  - Period label (`text-color-tertiary`) vs. card background: **4.5:1** — verify in both light and dark themes

### Color Blindness

The positive (green) and negative (red) trend colors are indistinguishable for users with deuteranopia or protanopia. The icon (`trending-up` / `trending-down`) and the `+` / `-` prefix on the percentage are the primary accessible differentiators — not the badge color.

### Motion

The sparkline draw animation and value count-up animation must be disabled:

```css
@media (prefers-reduced-motion: reduce) {
  .sparkline-path,
  .metric-value-countup {
    transition: none;
    animation: none;
  }
}
```

### Touch & Mobile

- If the card is interactive (links to a detail view), the entire card surface is the touch target — minimum **44px** tall.
- Do not place interactive elements inside an interactive card (nested click targets conflict on touch devices). If a card needs both a primary link and a secondary action, use a non-interactive card with explicit buttons instead.

---

## Acadimiat Examples

| Label | Value | Trend | Period |
|-------|-------|-------|--------|
| Total Revenue | 124,500 SAR | ↑ 12% | vs. last month |
| New Students | 1,240 | ↑ 8% | vs. last week |
| Course Completions | 847 | ↓ 3% | vs. last month |
| Conversion Rate | 4.2% | → 0% | vs. last month |
| Active Courses | 38 | ↑ 5 | vs. last quarter |
| Avg. Session Duration | 14m 32s | ↑ 6% | vs. last month |
