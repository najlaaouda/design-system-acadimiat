---
name: Area Chart
tier: Component
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Area Chart — Component Spec

## Purpose

The Area Chart is a Line Chart with the region between the line and the axis filled with a semi-transparent color. It emphasizes **volume and magnitude over time** — not just direction of change, but how large the values are relative to the baseline.

---

## When to Use

- Visualizing volume that accumulates over time (traffic, revenue, signups)
- Showing the magnitude of change — not just the trend direction
- Stacked area to show how multiple series contribute to a total
- Single-metric dashboards where volume needs emphasis

## When to Avoid

- Multiple overlapping series (3+) — fills obscure each other → use Line Chart instead
- Precise value comparison between categories → use Bar Chart
- Part-to-whole without time dimension → use Pie or Donut Chart
- When the area fill adds no meaning — if it's just decoration, use Line Chart

---

## Anatomy

| Part | Description | Token |
|------|-------------|-------|
| Chart container | Outer wrapper | `bg-color-secondary`, `radius-xl` |
| Title | Chart heading | `type-label-lg`, `text-color-primary` |
| Subtitle / Period | Supporting label | `type-body-sm`, `text-color-secondary` |
| Plot area | Inner drawing area | — |
| X axis | Horizontal time axis | `chart-axis-color` |
| Y axis | Vertical value axis | `chart-axis-color` |
| Axis labels | Tick labels | `chart-label-color`, `type-caption` |
| Grid lines | Horizontal reference lines | `chart-grid-color` |
| Line path | The data line at the top of the area | `chart-color-[n]` |
| Area fill | Filled region between line and baseline | `chart-color-[n]` @ 12% opacity |
| Data point | Optional dot on hover | `chart-color-[n]` |
| Tooltip | Value popup on hover / focus | `chart-tooltip-background`, `chart-tooltip-text`, `chart-tooltip-border` |
| Legend | Series labels (stacked variant only) | `chart-legend-text`, `type-label-sm` |

---

## Variants

### By Fill Type

| Variant | Description | When to Use |
|---------|-------------|-------------|
| Standard area | Single fill from line to zero baseline | Single metric, emphasize volume |
| Stacked area | Series stack on top of each other | Show how parts add up to a total |
| Stacked 100% area | Normalized to 100% — shows proportions over time | Show proportion shifts, not absolute volume |

### By Line Style

| Variant | Fill Opacity | When to Use |
|---------|-------------|-------------|
| Solid line + fill | 12% opacity | Default — clean and readable |
| Gradient fill | 20% at line → 0% at baseline | Single series hero sections |

---

## Design Tokens

### Colors

| Element | Token |
|---------|-------|
| Line (series 1) | `--chart-color-1` |
| Line (series 2–3) | `--chart-color-2`, `--chart-color-3` |
| Area fill (series 1) | `--chart-color-1` @ 12% opacity |
| Area fill (series 2–3) | `--chart-color-2/3` @ 12% opacity |
| Grid lines | `--chart-grid-color` |
| Axis lines | `--chart-axis-color` |
| Axis labels | `--chart-label-color` |
| Tooltip background | `--chart-tooltip-background` |
| Tooltip text | `--chart-tooltip-text` |
| Tooltip border | `--chart-tooltip-border` |
| Legend text | `--chart-legend-text` |

> **Series limit for area charts:** Maximum 3 series. Beyond 3, overlapping fills become unreadable — switch to Line Chart.

### Spacing

| Element | Token | Value |
|---------|-------|-------|
| Container padding | `--spacing-inset-xl` | 24px |
| Gap: title → chart | `--spacing-stack-md` | 16px |
| Gap: chart → legend | `--spacing-stack-sm` | 8px |

### Typography

| Element | Token |
|---------|-------|
| Title | `type-label-lg` |
| Subtitle | `type-body-sm` |
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
| xs — Mobile | Simplified X-axis labels, hide legend, gradient fill removed (solid fill only), horizontal scroll for dense data |
| md — Tablet | Condensed axis labels, compact legend below chart |
| xl — Desktop | Full labels, full legend, hover tooltips, gradient fills enabled |

---

## States

### Empty State

| Element | Value |
|---------|-------|
| Illustration | Flat baseline with dashed axes |
| Title | No data available |
| Description | Data will appear once records are available. |
| Action | Refresh or adjust filters |

### Loading State

| Element | Value |
|---------|-------|
| Plot area | Animated skeleton gradient fill |
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
| Chart container | `aria-labelledby` | ID of the chart title |
| Chart container | `aria-describedby` | ID of the hidden data summary |
| Area fill path | `aria-hidden` | `"true"` — fill is decorative; the line carries the data |
| Line path | `role` | `"graphics-symbol"` |
| Line path | `aria-label` | Series name e.g. `"Revenue series"` |
| Tooltip | `role` | `"tooltip"` |
| Tooltip | `aria-live` | `"polite"` |
| Data table (hidden) | `class` | `"sr-only"` |

### Hidden Data Table

The area fill conveys no information to screen readers — the hidden table is the sole accessible data representation.

```html
<table class="sr-only" aria-label="Traffic Growth data table">
  <thead>
    <tr><th>Day</th><th>Page Views</th></tr>
  </thead>
  <tbody>
    <tr><td>Mon</td><td>4,200</td></tr>
    <!-- ... -->
  </tbody>
</table>
```

For **stacked area**, include one column per series and a Total column.

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Move focus into and out of the chart |
| `Arrow Right / Left` | Move between data points along the X axis |
| `Arrow Up / Down` | Switch between stacked series |
| `Enter` / `Space` | Open tooltip for focused point |
| `Escape` | Close tooltip |
| `Home` / `End` | Jump to first / last data point |

### Color & Visual

- The area **fill is purely decorative** — never assign semantic meaning to fill alone.
- The **line** at the top of each area must:
  - Maintain **3:1** contrast vs. the chart background (WCAG AA, UI component)
  - Be accompanied by a unique line style (solid, dashed, dotted) in multi-series charts
- In **stacked** variants, directly label each area band at the right edge of the chart in addition to the legend.
- Minimum contrast for axis labels vs. background: **4.5:1**

### Color Blindness

The area fill at 12% opacity makes fills nearly identical for colorblind users — they must never be the primary differentiator. Always rely on:
- The line stroke (unique style per series)
- Direct text labels at the end of each area band
- The legend with both color and text

### Motion

Gradient fills and entry animations must be disabled under reduced-motion preference:

```css
@media (prefers-reduced-motion: reduce) {
  .chart-area,
  .chart-line,
  .chart-tooltip {
    transition: none;
    animation: none;
  }
  /* Gradient fills revert to flat color at low opacity */
  .chart-area-fill {
    fill-opacity: 0.08;
  }
}
```

### Touch & Mobile

- Data points must have a minimum touch target of **44 × 44px**.
- On mobile, hide the gradient fill (flat opacity only) to reduce visual noise and improve readability on smaller screens.
- Tap-to-show tooltip that closes on tap outside.

---

## Acadimiat Examples

| Chart Title | X Axis | Y Axis | Variant |
|-------------|--------|--------|---------|
| Traffic Growth | Day | Page Views | Standard area, 1 series |
| Revenue Accumulation | Month | SAR | Standard area, 1 series |
| Enrollment vs. Completion | Week | Students | Stacked, 2 series |
