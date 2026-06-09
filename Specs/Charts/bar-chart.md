---
name: Bar Chart
tier: Component
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Bar Chart — Component Spec

## Purpose

The Bar Chart compares **discrete categories** using rectangular bars whose lengths are proportional to the values they represent. It is the primary chart type for rankings, comparisons, and periodic breakdowns.

---

## When to Use

- Comparing values across categories (products, courses, months)
- Rankings — top N items by value
- Performance comparison between periods or groups
- Showing distribution across categories

## When to Avoid

- Trends over continuous time with many points → use Line Chart
- Part-to-whole relationships → use Pie or Donut Chart
- More than 12 categories — consider a table with filters instead
- Negative + positive values on the same axis without clear zero reference

---

## Anatomy

| Part | Description | Token |
|------|-------------|-------|
| Chart container | Outer wrapper | `bg-color-secondary`, `radius-xl` |
| Title | Chart heading | `type-label-lg`, `text-color-primary` |
| Subtitle / Period | Supporting label | `type-body-sm`, `text-color-secondary` |
| Plot area | Inner area where bars are drawn | — |
| X axis | Category axis (vertical bar) or Value axis (horizontal bar) | `chart-axis-color` |
| Y axis | Value axis (vertical bar) or Category axis (horizontal bar) | `chart-axis-color` |
| Axis labels | Tick labels on both axes | `chart-label-color`, `type-caption` |
| Grid lines | Reference lines parallel to value axis | `chart-grid-color` |
| Bar | The rectangular data element | `chart-color-[n]` |
| Bar hover state | Highlight on hover | `chart-color-[n]` @ 80% opacity |
| Value label | Optional value displayed on or above the bar | `type-caption`, `chart-label-color` |
| Tooltip | Value popup on hover / focus | `chart-tooltip-background`, `chart-tooltip-text`, `chart-tooltip-border` |
| Legend | Series labels (Grouped and Stacked variants only) | `chart-legend-text`, `type-label-sm` |

---

## Variants

### By Orientation

| Variant | Description | When to Use |
|---------|-------------|-------------|
| Vertical bar | Bars grow upward — default | Time-based categories, most comparisons |
| Horizontal bar | Bars grow right | Long category names, rankings, many categories |

### By Series

| Variant | Description | Token Assignment |
|---------|-------------|-----------------|
| Single series | One bar per category | `chart-color-1` |
| Grouped | Multiple bars side-by-side per category | `chart-color-1` → `chart-color-[n]` |
| Stacked | Multiple series stacked in one bar | `chart-color-1` → `chart-color-[n]` |
| Stacked 100% | Stacked bars normalized to 100% | `chart-color-1` → `chart-color-[n]` |

---

## Design Tokens

### Colors

| Element | Token |
|---------|-------|
| Bar (series 1) | `--chart-color-1` |
| Bar (series 2–6) | `--chart-color-2` → `--chart-color-6` |
| Bar hover | `--chart-color-[n]` @ 80% opacity |
| Grid lines | `--chart-grid-color` |
| Axis lines | `--chart-axis-color` |
| Axis labels | `--chart-label-color` |
| Value labels | `--chart-label-color` |
| Tooltip background | `--chart-tooltip-background` |
| Tooltip text | `--chart-tooltip-text` |
| Tooltip border | `--chart-tooltip-border` |
| Legend text | `--chart-legend-text` |

### Status Bar Colors

When a bar represents a semantic state (positive/negative performance):

| State | Token |
|-------|-------|
| Positive / above target | `--chart-color-success` |
| Warning / near threshold | `--chart-color-warning` |
| Negative / below target | `--chart-color-error` |
| Neutral / forecast | `--chart-color-neutral` |

### Spacing

| Element | Token | Value |
|---------|-------|-------|
| Container padding | `--spacing-inset-xl` | 24px |
| Gap between bars (grouped) | 4px (fixed) | — |
| Gap between bar groups | 12px (fixed) | — |
| Gap: title → chart | `--spacing-stack-md` | 16px |
| Gap: chart → legend | `--spacing-stack-sm` | 8px |

### Typography

| Element | Token |
|---------|-------|
| Title | `type-label-lg` |
| Subtitle | `type-body-sm` |
| Axis labels | `type-caption` |
| Value labels | `type-caption` |
| Tooltip value | `type-label` |
| Tooltip label | `type-caption` |
| Legend text | `type-label-sm` |

### Radius

| Element | Token | Value |
|---------|-------|-------|
| Container | `radius-xl` | 16px |
| Bar top corners | `radius-sm` | 4px |
| Tooltip | `radius-md` | 8px |

---

## Responsive Behavior

| Breakpoint | Behavior |
|------------|----------|
| xs — Mobile | Reduce visible bars (show top 6), hide value labels, stacked layout preferred over grouped, horizontal scroll if needed |
| md — Tablet | Condensed axis labels, compact legend below chart |
| xl — Desktop | Full labels, full legend, hover tooltips, grouped bars fully visible |

---

## States

### Empty State

| Element | Value |
|---------|-------|
| Illustration | Empty chart skeleton (dashed axes, no bars) |
| Title | No data available |
| Description | Data will appear once records are available. |
| Action | Refresh or adjust filters |

### Loading State

| Element | Value |
|---------|-------|
| Bars | Animated skeleton rectangles at varying heights |
| Title | Skeleton line — 40% width |

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
| Each bar | `role` | `"graphics-symbol"` |
| Each bar | `aria-label` | `"[Category]: [Value]"` e.g. `"January: 12,400 SAR"` |
| Tooltip | `role` | `"tooltip"` |
| Tooltip | `aria-live` | `"polite"` |
| Legend | `role` | `"list"` / `"listitem"` |
| Data table (hidden) | `class` | `"sr-only"` |

### Hidden Data Table

A visually hidden `<table>` must accompany every bar chart so screen readers can read the data directly.

```html
<table class="sr-only" aria-label="Students by Course data table">
  <thead>
    <tr><th>Course</th><th>Enrolled Students</th></tr>
  </thead>
  <tbody>
    <tr><td>Web Design</td><td>340</td></tr>
    <!-- ... -->
  </tbody>
</table>
```

For **Grouped** and **Stacked** variants, add a column per series:

```html
<thead>
  <tr><th>Month</th><th>Revenue</th><th>Target</th></tr>
</thead>
```

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus into and out of the chart |
| `Arrow Right / Left` | Move between bars (vertical orientation) |
| `Arrow Up / Down` | Move between bars (horizontal orientation) |
| `Arrow Up / Down` | Move between series in grouped/stacked charts |
| `Enter` / `Space` | Open tooltip for focused bar |
| `Escape` | Close tooltip |
| `Home` / `End` | Jump to first / last bar |

### Color & Visual

- For **Grouped** and **Stacked** variants, never rely on color alone to distinguish series. Combine color with:
  - SVG fill patterns: diagonal lines, dots, crosshatch
  - Direct labels above each bar group
- For **status bars** (success/warning/error), add an icon or prefix label alongside color.
- Minimum contrast ratios:
  - Bar fill vs. chart background: **3:1** (WCAG AA, UI component)
  - Value labels vs. bar fill: **4.5:1** (normal text)
  - Axis labels vs. chart background: **4.5:1**

### Color Blindness

The status colors (success = green, warning = yellow, error = red) are not distinguishable by all users with color blindness. Always accompany them with:
- An icon (`check`, `alert-triangle`, `x-circle`)
- A text label or value annotation

### Motion

```css
@media (prefers-reduced-motion: reduce) {
  .chart-bar {
    transition: none;
    animation: none;
  }
}
```

### Touch & Mobile

- Minimum touch target per bar: **44px** on the interaction axis (width for vertical bars, height for horizontal bars).
- On mobile, show a persistent tap tooltip — do not use hover-only states.

---

## Acadimiat Examples

| Chart Title | Category Axis | Value Axis | Variant |
|-------------|--------------|------------|---------|
| Sales by Product | Product Name | Revenue (SAR) | Horizontal, single |
| Students by Course | Course | Enrolled Students | Vertical, single |
| Orders by Month | Month | Order Count | Vertical, single |
| Revenue vs. Target | Month | SAR | Grouped (2 series) |
| Course Completion by Type | Course Type | % Completion | Stacked 100% |
