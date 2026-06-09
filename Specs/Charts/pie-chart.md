---
name: Pie & Donut Chart
tier: Component
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Pie & Donut Chart — Component Spec

## Purpose

The Pie and Donut Charts visualize **part-to-whole relationships** — how individual segments contribute to a total of 100%. The Donut variant adds a center area that can display a key metric or total value.

---

## When to Use

- Showing percentage distribution across a small number of categories
- KPI breakdowns — how budget, traffic, or sales are split
- Proportional comparisons where the total = 100%

## When to Avoid

- More than 6 slices — small slices become unreadable → group into "Other"
- Time-series data → use Line or Area Chart
- Comparing values across multiple datasets → use Bar Chart
- When exact values matter more than proportions → use a Table
- Slices with very similar values (within 5%) — the difference is imperceptible

---

## Anatomy

| Part | Description | Token |
|------|-------------|-------|
| Chart container | Outer wrapper | `bg-color-secondary`, `radius-xl` |
| Title | Chart heading | `type-label-lg`, `text-color-primary` |
| Subtitle | Supporting label | `type-body-sm`, `text-color-secondary` |
| Slice | A pie segment representing one category | `chart-color-[n]` |
| Slice hover | Active slice — slightly pulled out | `chart-color-[n]` + 4px offset |
| Slice border | Gap between slices | `bg-color-secondary` — 2px |
| Center content *(Donut only)* | Value or label in the hollow center | `type-heading-3`, `text-color-primary` |
| Center label *(Donut only)* | Descriptor below the center value | `type-caption`, `text-color-secondary` |
| Tooltip | Percentage and value popup on hover | `chart-tooltip-background`, `chart-tooltip-text`, `chart-tooltip-border` |
| Legend | Category labels with color indicators | `chart-legend-text`, `type-label-sm` |

---

## Variants

### Pie vs. Donut

| Variant | Center | When to Use |
|---------|--------|-------------|
| Pie | Solid fill | Simple proportional view |
| Donut | Hollow — shows total or KPI | Dashboard widget, KPI breakdown |

### Donut Center Content

| Type | Example | Token |
|------|---------|-------|
| Total value | `1,240` | `type-heading-3`, `text-color-primary` |
| Percentage | `64%` | `type-heading-3`, `text-color-primary` |
| Metric label | Total Revenue | `type-caption`, `text-color-secondary` |
| Status | ↑ 12% | `type-label`, `text-color-success` / `text-color-error` |

---

## Slice Rules

| Rule | Value |
|------|-------|
| Maximum slices | 6 |
| Minimum slice angle | 5° — slices smaller than this are grouped into "Other" |
| Total must equal | 100% |
| Slice gap (stroke) | 2px in `bg-color-secondary` |
| Hover offset | 4px outward pull |

### "Other" Slice

When categories exceed 6 or slices are too small, group them into a single "Other" segment.

| Element | Token |
|---------|-------|
| Other slice color | `--chart-color-neutral` |
| Other slice label | "Other" — `type-label-sm` |

---

## Design Tokens

### Colors

| Element | Token |
|---------|-------|
| Slice 1 | `--chart-color-1` |
| Slice 2–6 | `--chart-color-2` → `--chart-color-6` |
| Other slice | `--chart-color-neutral` |
| Slice border (gap) | `--bg-color-secondary` |
| Tooltip background | `--chart-tooltip-background` |
| Tooltip text | `--chart-tooltip-text` |
| Tooltip border | `--chart-tooltip-border` |
| Legend text | `--chart-legend-text` |
| Center value | `--text-color-primary` |
| Center label | `--text-color-secondary` |

### Spacing

| Element | Token | Value |
|---------|-------|-------|
| Container padding | `--spacing-inset-xl` | 24px |
| Gap: title → chart | `--spacing-stack-md` | 16px |
| Gap: chart → legend | `--spacing-stack-md` | 16px |
| Legend item gap | `--spacing-inline-sm` | 8px |

### Typography

| Element | Token |
|---------|-------|
| Title | `type-label-lg` |
| Subtitle | `type-body-sm` |
| Center value *(Donut)* | `type-heading-3` |
| Center label *(Donut)* | `type-caption` |
| Tooltip value | `type-label` |
| Tooltip percentage | `type-caption` |
| Legend text | `type-label-sm` |

### Radius

| Element | Token |
|---------|-------|
| Container | `radius-xl` |
| Tooltip | `radius-md` |

### Dimensions

| Property | Value |
|----------|-------|
| Donut inner radius | 55% of outer radius |
| Pie / Donut outer radius | Fills available plot area |
| Min chart size | 160 × 160px |

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| xs — Mobile | Legend moves below chart, font sizes reduced, center content abbreviated |
| md — Tablet | Legend beside or below chart |
| xl — Desktop | Legend beside chart, full tooltips, hover slice offset |

---

## States

### Empty State

| Element | Value |
|---------|-------|
| Illustration | Single neutral-colored circle, no slices |
| Title | No data available |
| Description | Data will appear once records are available. |
| Action | Refresh or adjust filters |

### Loading State

| Element | Value |
|---------|-------|
| Pie / Donut | Animated neutral skeleton circle |
| Title | Skeleton line — 40% width |
| Legend | 3 skeleton pills |

### Error State

| Element | Value |
|---------|-------|
| Icon | `alert-triangle` — `icon-color-error` |
| Title | Unable to load chart |
| Description | Please try again later. |
| Action | Retry button |

---

## Accessibility

### ARIA Markup

| Element | Attribute | Value |
|---------|-----------|-------|
| Chart container | `role` | `"img"` |
| Chart container | `aria-labelledby` | ID of the chart title |
| Chart container | `aria-describedby` | ID of the hidden summary paragraph |
| Each slice | `role` | `"graphics-symbol"` |
| Each slice | `aria-label` | `"[Category]: [Value] ([Percentage]%)"` e.g. `"Organic: 4,200 visits (34%)"` |
| Donut center value | `aria-hidden` | `"true"` — announced via the container label, not separately |
| Tooltip | `role` | `"tooltip"` |
| Tooltip | `aria-live` | `"polite"` |
| Legend | `role` | `"list"` / `"listitem"` |
| Data table (hidden) | `class` | `"sr-only"` |

### Hidden Summary & Data Table

Provide both a short summary sentence and a full data table for screen readers:

```html
<!-- Summary -->
<p id="pie-summary" class="sr-only">
  Traffic Sources: Total 12,400 visits. Organic 34% (4,216), Paid 28% (3,472),
  Social 18% (2,232), Direct 12% (1,488), Referral 8% (992).
</p>

<!-- Data table -->
<table class="sr-only" aria-label="Traffic Sources data table">
  <thead>
    <tr><th>Source</th><th>Visits</th><th>Percentage</th></tr>
  </thead>
  <tbody>
    <tr><td>Organic</td><td>4,216</td><td>34%</td></tr>
    <!-- ... -->
    <tr><th>Total</th><td>12,400</td><td>100%</td></tr>
  </tbody>
</table>
```

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus into and out of the chart |
| `Arrow Right / Left` | Move clockwise / counter-clockwise between slices |
| `Enter` / `Space` | Open tooltip for focused slice |
| `Escape` | Close tooltip |
| `Home` / `End` | Jump to largest / smallest slice |

### Color & Visual

- Never rely on color alone to identify slices. Combine color with:
  - Percentage labels directly on or adjacent to each slice (if ≥ 5% angle)
  - SVG hatch or dot fill patterns per slice
  - A legend that lists both color swatch and category name
- Minimum contrast ratios:
  - Slice label text vs. slice fill: **4.5:1** (normal text)
  - Slice label text vs. chart background (if outside the slice): **4.5:1**
  - Donut center text vs. background: **4.5:1**
- Minimum readable slice: if a slice is < 5°, it must be grouped into "Other" — a label at that size is unreadable even visually.

### Color Blindness

The 6 series colors include hues that are difficult to distinguish for deuteranopes and protanopes. For Pie/Donut charts, always add:
- SVG pattern fills (diagonal lines, dots, crosshatch) — one pattern per slice
- Text percentage labels on each slice or directly in the legend

### "Other" Slice Accessibility

- The "Other" slice must have an `aria-label` listing how many categories it contains: `"Other: 3 categories, 8% (992 visits)"`.
- Provide a way to access the grouped data — either an expandable legend row or a link to a full data table.

### Motion

Slice entry animation (pie "grow" or rotate-in) must be disabled:

```css
@media (prefers-reduced-motion: reduce) {
  .chart-slice,
  .chart-tooltip {
    transition: none;
    animation: none;
  }
  /* Disable hover offset animation */
  .chart-slice:focus,
  .chart-slice:hover {
    transform: none;
  }
}
```

### Touch & Mobile

- Each slice must subtend enough arc to be tappable — enforce the 6-slice maximum.
- Minimum tap target: **44 × 44px** bounding box per slice.
- On touch, tapping a slice shows a persistent tooltip; tapping the same slice again dismisses it.

---

## Acadimiat Examples

| Chart Title | Slices | Center Content |
|-------------|--------|----------------|
| Revenue by Product | Product categories | Total revenue |
| Traffic Sources | Organic, Paid, Social, Direct, Referral | Total visits |
| Course Completion | Completed, In Progress, Not Started | % Completed |
| Sales by Region | Top 5 regions + Other | Total orders |
