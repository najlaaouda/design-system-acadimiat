---
name: Chart Color Semantic Tokens
tier: Semantic
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Chart Color — Semantic Tokens

## Philosophy

Chart color tokens are a dedicated semantic layer for data visualization. They are separate from UI color tokens because charts have unique requirements: series colors must be visually distinct from each other, remain accessible against both light and dark backgrounds, and carry meaning (positive, negative, neutral) without relying on color alone.

Three categories of tokens cover all chart coloring needs: **Series** (the data itself), **Status** (semantic data meaning), and **UI** (chart chrome — grid, axes, tooltips, legends).

> **Use these tokens in all chart components.**
> Never use general UI semantic tokens (text, bg, border) inside chart elements — always use chart-specific tokens.

---

## How to Read This File

### Naming Patterns

| Category | Pattern | Example |
|----------|---------|---------|
| Series | `chart-color-[number]` | `chart-color-1` |
| Status | `chart-color-[status]` | `chart-color-success` |
| UI elements | `chart-[element]-[property]` | `chart-grid-color`, `chart-tooltip-background` |

### Token Reference Format

`→ primitive-name` means the token resolves to that primitive at runtime.
Primitive values are defined in `Foundations/Color.md`.

### Theme Notes

- **Series colors** are lighter in Dark mode — saturated dark-mode backgrounds demand higher-value colors to stay legible.
- **Status colors** follow the same lightening pattern as UI status tokens.
- **UI colors** (grid, axis, tooltip) follow the same light/dark logic as other semantic color files.

---

## Series Colors

Used for chart data elements — lines, bars, areas, pie slices, and donut segments. Always assign series in order from `chart-color-1` to `chart-color-6`. Never skip a number.

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `chart-color-1` | → `purple-500` | → `purple-400` | Primary series — revenue, main KPI |
| `chart-color-2` | → `blue-500` | → `blue-400` | Secondary series — comparisons, last period |
| `chart-color-3` | → `green-500` | → `green-400` | Third series — targets, goals |
| `chart-color-4` | → `yellow-500` | → `yellow-400` | Fourth series — benchmarks, forecasts |
| `chart-color-5` | → `red-500` | → `red-400` | Fifth series — anomalies, limits |
| `chart-color-6` | → `purple-300` | → `purple-200` | Sixth series — additional segment |

> **Maximum 6 series per chart.** If more are needed, reconsider the chart type or split into multiple charts.

---

## Status Colors

Used when a data value carries a semantic meaning — growth, decline, or neutrality. Always pair with a label or icon; never use color as the sole indicator.

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `chart-color-success` | → `green-500` | → `green-400` | Positive trend — revenue increase, completed orders |
| `chart-color-warning` | → `yellow-500` | → `yellow-400` | Caution — near threshold, slowing growth |
| `chart-color-error` | → `red-500` | → `red-400` | Negative trend — revenue decrease, failed transactions |
| `chart-color-info` | → `blue-500` | → `blue-400` | Informational — in-progress, pending |
| `chart-color-neutral` | → `neutral-400` | → `white-alpha-40` | No change — forecasts, benchmarks |

---

## UI Colors

Used for chart structural elements — the non-data parts of a chart. These define the visual scaffolding that frames the data.

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `chart-grid-color` | → `neutral-200` | → `white-alpha-10` | Horizontal and vertical grid lines |
| `chart-axis-color` | → `neutral-300` | → `white-alpha-20` | X and Y axis lines |
| `chart-label-color` | → `neutral-400` | → `white-alpha-50` | Axis tick labels, value annotations |
| `chart-tooltip-background` | → `base-white` | → `neutral-800` | Tooltip container background |
| `chart-tooltip-text` | → `neutral-900` | → `base-white` | Tooltip primary text |
| `chart-tooltip-border` | → `neutral-200` | → `white-alpha-20` | Tooltip container border |
| `chart-legend-text` | → `neutral-500` | → `white-alpha-70` | Legend item labels |

---

## CSS Custom Properties

```css
/* ─── Light Theme ────────────────────────────────────────── */
:root,
[data-theme="light"] {

  /* Series */
  --chart-color-1: var(--purple-500);
  --chart-color-2: var(--blue-500);
  --chart-color-3: var(--green-500);
  --chart-color-4: var(--yellow-500);
  --chart-color-5: var(--red-500);
  --chart-color-6: var(--purple-300);

  /* Status */
  --chart-color-success: var(--green-500);
  --chart-color-warning: var(--yellow-500);
  --chart-color-error:   var(--red-500);
  --chart-color-info:    var(--blue-500);
  --chart-color-neutral: var(--neutral-400);

  /* UI */
  --chart-grid-color:          var(--neutral-200);
  --chart-axis-color:          var(--neutral-300);
  --chart-label-color:         var(--neutral-400);
  --chart-tooltip-background:  var(--base-white);
  --chart-tooltip-text:        var(--neutral-900);
  --chart-tooltip-border:      var(--neutral-200);
  --chart-legend-text:         var(--neutral-500);
}

/* ─── Dark Theme ─────────────────────────────────────────── */
[data-theme="dark"] {

  /* Series — lighter values for visibility on dark backgrounds */
  --chart-color-1: var(--purple-400);
  --chart-color-2: var(--blue-400);
  --chart-color-3: var(--green-400);
  --chart-color-4: var(--yellow-400);
  --chart-color-5: var(--red-400);
  --chart-color-6: var(--purple-200);

  /* Status */
  --chart-color-success: var(--green-400);
  --chart-color-warning: var(--yellow-400);
  --chart-color-error:   var(--red-400);
  --chart-color-info:    var(--blue-400);
  --chart-color-neutral: var(--white-alpha-40);

  /* UI */
  --chart-grid-color:          var(--white-alpha-10);
  --chart-axis-color:          var(--white-alpha-20);
  --chart-label-color:         var(--white-alpha-50);
  --chart-tooltip-background:  var(--neutral-800);
  --chart-tooltip-text:        var(--base-white);
  --chart-tooltip-border:      var(--white-alpha-20);
  --chart-legend-text:         var(--white-alpha-70);
}
```

---

## Figma Variables

> **Collection:** `Semantic/Chart Color`

### Series

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `chart/color/1` | `primitive/purple-500` | `primitive/purple-400` | Fill color |
| `chart/color/2` | `primitive/blue-500` | `primitive/blue-400` | Fill color |
| `chart/color/3` | `primitive/green-500` | `primitive/green-400` | Fill color |
| `chart/color/4` | `primitive/yellow-500` | `primitive/yellow-400` | Fill color |
| `chart/color/5` | `primitive/red-500` | `primitive/red-400` | Fill color |
| `chart/color/6` | `primitive/purple-300` | `primitive/purple-200` | Fill color |

### Status

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `chart/color/success` | `primitive/green-500` | `primitive/green-400` | Fill color |
| `chart/color/warning` | `primitive/yellow-500` | `primitive/yellow-400` | Fill color |
| `chart/color/error` | `primitive/red-500` | `primitive/red-400` | Fill color |
| `chart/color/info` | `primitive/blue-500` | `primitive/blue-400` | Fill color |
| `chart/color/neutral` | `primitive/neutral-400` | `primitive/white-alpha-40` | Fill color |

### UI Elements

| Variable | Light Value | Dark Value | Scope |
|----------|-------------|------------|-------|
| `chart/grid-color` | `primitive/neutral-200` | `primitive/white-alpha-10` | Stroke color |
| `chart/axis-color` | `primitive/neutral-300` | `primitive/white-alpha-20` | Stroke color |
| `chart/label-color` | `primitive/neutral-400` | `primitive/white-alpha-50` | Text color |
| `chart/tooltip-background` | `primitive/base-white` | `primitive/neutral-800` | Fill color |
| `chart/tooltip-text` | `primitive/neutral-900` | `primitive/base-white` | Text color |
| `chart/tooltip-border` | `primitive/neutral-200` | `primitive/white-alpha-20` | Stroke color |
| `chart/legend-text` | `primitive/neutral-500` | `primitive/white-alpha-70` | Text color |
