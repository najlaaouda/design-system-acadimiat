---
name: Border Primitives
tier: Primitive
status: Active
last-updated: 2026-06-09
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Border System — Primitive Tokens

## Philosophy

Acadimiat's border system defines the structural properties of strokes: width and style. These are **Primitive Tokens** — raw values that Semantic Tokens reference. Border color is a separate concern handled in `Semantic/border-color.md`. Border radius is handled in `Foundations/Radius.md`.

> **Important — Do not use these tokens directly in components.**
> Always use Semantic Tokens in code and design.
> No Scope is applied to these variables in Figma — they serve as a reference only.

---

## Border Width

All border widths are derived from a sub-pixel–to–4px scale. Values above `border-4` are reserved for decorative use only.

| Token | Value | Usage |
|-------|-------|-------|
| `border-0` | `0px` | No border — removes an existing border |
| `border-1` | `1px` | Default border — cards, inputs, dividers |
| `border-1-5` | `1.5px` | Medium emphasis — secondary button stroke |
| `border-2` | `2px` | High emphasis — focus ring, selected state |
| `border-4` | `4px` | Accent — left-border highlight, progress indicator |

---

## Border Style

| Token | Value | Usage |
|-------|-------|-------|
| `border-style-solid` | `solid` | Default — all UI borders |
| `border-style-dashed` | `dashed` | Placeholder zones, dropzone targets |
| `border-style-dotted` | `dotted` | Informational or subtle separators |
| `border-style-none` | `none` | Explicit border removal |

---

## Border Shorthand Patterns

These are the combinations used across components. Always decompose into `border-width` + `border-style` + `border-color` token — never use raw shorthand values in components.

| Pattern | Width Token | Style Token | Color Token | Used In |
|---------|------------|-------------|-------------|---------|
| Default border | `border-1` | `border-style-solid` | `--border-color-primary` | Cards, inputs, dividers |
| Brand border | `border-1-5` | `border-style-solid` | `--border-color-brand` | Secondary button, selected input |
| Focus ring | `border-2` | `border-style-solid` | `--border-color-focus` | All interactive elements on `:focus-visible` |
| Disabled border | `border-1` | `border-style-solid` | `--border-color-disabled` | Disabled inputs, disabled secondary button |
| Error border | `border-1` | `border-style-solid` | `--border-color-error` | Invalid input state |
| Accent border | `border-4` | `border-style-solid` | `--border-color-brand` | Highlighted cards, info banners |
| Dropzone | `border-1-5` | `border-style-dashed` | `--border-color-primary` | File upload zones |

---

## CSS Custom Properties

```css
:root {
  /* Border Width */
  --border-0:   0px;
  --border-1:   1px;
  --border-1-5: 1.5px;
  --border-2:   2px;
  --border-4:   4px;

  /* Border Style */
  --border-style-solid:  solid;
  --border-style-dashed: dashed;
  --border-style-dotted: dotted;
  --border-style-none:   none;
}
```

---

## Rules

- Use `border-2` exclusively for focus rings — do not repurpose it for decorative borders
- The `border-1-5` value is the only sub-pixel border in the system — reserved for button strokes only
- Never write `border: 1px solid #65398D` in a component — decompose into `var(--border-1)`, `var(--border-style-solid)`, `var(--border-color-brand)`
- `border-0` exists to explicitly remove a border — use it instead of `border: none` for token consistency
- `border-4` is accent-only — never use it as a structural UI border

---

## Figma Variables

> **No Scope:** These variables have no scope applied in Figma. They are primitive references only and must not be applied directly to components.

| Collection | Variable | Value |
|------------|----------|-------|
| Primitives | `border/width/0` | `0px` |
| Primitives | `border/width/1` | `1px` |
| Primitives | `border/width/1-5` | `1.5px` |
| Primitives | `border/width/2` | `2px` |
| Primitives | `border/width/4` | `4px` |
| Primitives | `border/style/solid` | `solid` |
| Primitives | `border/style/dashed` | `dashed` |
| Primitives | `border/style/dotted` | `dotted` |
| Primitives | `border/style/none` | `none` |

---

## Related Files

| File | Relationship |
|------|-------------|
| `Foundations/Color.md` | Raw color values that border colors resolve to |
| `Foundations/Radius.md` | Border radius primitives |
| `Semantic/border-color.md` | Semantic color tokens — use these in components, not raw colors |
