---
name: Line Chart
tier: Component
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Line Chart — Component Spec

## Purpose

The Line Chart visualizes data points connected by lines to show **trends over time** or continuous change. It is the primary chart type for monitoring progress, growth, and performance over a time axis.

---

## When to Use

- Trends over time (daily, weekly, monthly, yearly)
- Growth analysis — user registrations, revenue growth
- Performance monitoring — course completion rates, conversion rates
- Comparing multiple metrics over the same time period (multi-line)

## When to Avoid

- Comparing unrelated categories with no time relationship → use Bar Chart
- Showing part-to-whole relationships → use Pie or Donut Chart
- Fewer than 3 data points — a single number or metric card is clearer
- More than 6 series on one chart — split into separate charts

---

## Anatomy

| Part | Description | Token |
|------|-------------|-------|
| Chart container | Outer wrapper with background and border radius | `bg-color-secondary`, `radius-xl` |
| Title | Chart heading above the plot area | `type-label-lg`, `text-color-primary` |
| Subtitle / Period | Supporting label below the title | `type-body-sm`, `text-color-secondary` |
| Plot area | The inner area where data is drawn | — |
| X axis | Horizontal axis — typically time | `chart-axis-color` |
| Y axis | Vertical axis — typically values | `chart-axis-color` |
| Axis labels | Tick labels on X and Y axes | `chart-label-color`, `type-caption` |
| Grid lines | Horizontal reference lines across the plot | `chart-grid-color` |
| Line path | The data line connecting points | `chart-color-[n]` |
| Data point | Optional dot at each data value | `chart-color-[n]` |
| Area fill | Optional semi-transparent fill below the line | `chart-color-[n]` @ 12% opacity |
| Tooltip | Value popup on hover / focus | `chart-tooltip-background`, `chart-tooltip-text`, `chart-tooltip-border` |
| Legend | Series labels below or beside the chart | `chart-legend-text`, `type-label-sm` |

---

## Variants

### By Number of Series

| Variant | Series Count | Token Assignment |
|---------|-------------|-----------------|
| Single line | 1 | `chart-color-1` |
| Multi-line | 2–6 | `chart-color-1` → `chart-color-6` in order |

### By Line Style

| Variant | Description | When to Use |
|---------|-------------|-------------|
| Straight | Sharp corners between data points | Dense datasets, precise values |
| Smooth (curve) | Bezier curve between points | Sparse datasets, visual polish |

### By Fill

| Variant | Description | When to Use |
|---------|-------------|-------------|
| Line only | No area fill | Multiple series, clean comparison |
| Line + area | Semi-transparent fill below the line | Single series, emphasize volume |

---

## Design Tokens

### Colors

| Element | Token |
|---------|-------|
| Line (series 1) | `--chart-color-1` |
| Line (series 2–6) | `--chart-color-2` → `--chart-color-6` |
| Area fill | `--chart-color-[n]` @ 12% opacity |
| Grid lines | `--chart-grid-color` |
| Axis lines | `--chart-axis-color` |
| Axis labels | `--chart-label-color` |
| Tooltip background | `--chart-tooltip-background` |
| Tooltip text | `--chart-tooltip-text` |
| Tooltip border | `--chart-tooltip-border` |
| Legend text | `--chart-legend-text` |

### Spacing

| Element | Token | Value |
|---------|-------|-------|
| Container padding | `--spacing-lg` | 24px |
| Gap: title → chart | `--spacing-md` | 16px |
| Gap: chart → legend | `--spacing-sm` | 8px |

### Typography

| Element | Token |
|---------|-------|
| Title | `type-label-lg` |
| Subtitle / Period | `type-body-sm` |
| Axis labels | `type-caption` |
| Tooltip value | `type-label` |
| Tooltip label | `type-caption` |
| Legend text | `type-label-sm` |

### Radius

| Element | Token |
|---------|-------|
| Container | `radius-xl` |
| Tooltip | `radius-md` |
| Data point dot | `radius-full` |

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| xs — Mobile | Simplified X-axis labels (show every nth label), hide legend, enable horizontal scroll for dense data |
| md — Tablet | Condensed axis labels, compact legend below chart |
| xl — Desktop | Full axis labels, full legend, hover tooltips |

---

## States

### Empty State

Displayed when no data is available for the selected period.

| Element | Value |
|---------|-------|
| Illustration | Empty chart skeleton (dashed axes, no line) |
| Title | No data available |
| Description | Data will appear once records are available. |
| Action | Refresh or adjust filters |

### Loading State

Use skeleton placeholders that match the chart's dimensions. Never render an empty chart while data is loading.

| Element | Value |
|---------|-------|
| Plot area | Animated skeleton bar |
| Title | Skeleton line — 40% width |
| Legend | Skeleton pills |

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
| Chart container | `aria-labelledby` | ID of the chart title element |
| Chart container | `aria-describedby` | ID of the hidden data summary |
| Chart title | `id` | e.g. `"revenue-chart-title"` |
| Tooltip | `role` | `"tooltip"` |
| Tooltip | `aria-live` | `"polite"` |
| Legend items | `role` | `"list"` / `"listitem"` |
| Data table (hidden) | `class` | `"sr-only"` — visually hidden, available to screen readers |

### Hidden Data Table

Every line chart must include a visually hidden `<table>` beneath the SVG that screen readers can announce. The table mirrors the chart data exactly.

```html
<table class="sr-only" aria-label="Revenue Trend data table">
  <thead>
    <tr><th>Month</th><th>Revenue (SAR)</th></tr>
  </thead>
  <tbody>
    <tr><td>Jan</td><td>98,000</td></tr>
    <!-- ... -->
  </tbody>
</table>
```

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus into and out of the chart |
| `Arrow Right / Left` | Move between data points along the X axis |
| `Arrow Up / Down` | Switch between series (multi-line) |
| `Enter` / `Space` | Open tooltip for focused data point |
| `Escape` | Close tooltip |
| `Home` / `End` | Jump to first / last data point |

### Color & Visual

- Never rely on color alone to distinguish series. Combine:
  - Different line styles: solid, dashed (`- - -`), dotted (`· · ·`)
  - Different point shapes: circle, square, diamond, triangle
  - Direct line labels at the end of each line (preferred over legend-only)
- Minimum contrast ratio:
  - Axis labels vs. chart background: **4.5:1** (WCAG AA, normal text)
  - Line color vs. chart background: **3:1** (WCAG AA, UI component)
  - Tooltip text vs. tooltip background: **4.5:1**

### Color Blindness

The 6 chart-color series are chosen to be distinguishable for the most common types of color blindness (deuteranopia, protanopia). Always pair color with a secondary differentiator (line pattern or point shape) — color alone is never sufficient.

### Motion

Respect the user's motion preference. Disable entry animations and tooltip transitions when:

```css
@media (prefers-reduced-motion: reduce) {
  .chart-line, .chart-area, .chart-tooltip {
    transition: none;
    animation: none;
  }
}
```

### Touch & Mobile

- Minimum touch target for data points: **44 × 44px** (WCAG 2.5.5)
- On touch devices, replace hover tooltip with tap-to-show tooltip that persists until tapped elsewhere.

---

## Acadimiat Examples

| Chart Title | X Axis | Y Axis | Series |
|-------------|--------|--------|--------|
| Revenue Trend | Month | Revenue (SAR) | 1 — `chart-color-1` |
| Course Enrollments | Week | New Students | 1 — `chart-color-1` |
| Traffic Sources | Day | Visits | Multi — up to 4 |
| Conversion Rate | Month | Rate (%) | 2 — current vs. target |
