---
name: Accessibility
tier: Foundation
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Accessibility — Foundation

## Philosophy

Accessibility is not optional. Every Acadimiat product must meet **WCAG 2.1 AA** as a minimum standard. Accessible design is inclusive design — it improves the experience for all users, not just those with disabilities.

> **WCAG 2.1 AA is the non-negotiable baseline.**
> No component ships without passing accessibility requirements.

---

## Standard

| Property | Value |
|----------|-------|
| Standard | WCAG 2.1 |
| Level | AA (minimum) |
| Target | AAA where feasible |
| Languages | Arabic (RTL), English (LTR) |

---

## Color Contrast

All text and interactive elements must meet minimum contrast ratios against their background.

### Minimum Ratios (WCAG AA)

| Context | Min Contrast Ratio |
|---------|--------------------|
| Normal text (< 18px) | `4.5 : 1` |
| Large text (≥ 18px regular, ≥ 14px bold) | `3 : 1` |
| UI components & icons | `3 : 1` |
| Decorative elements | No requirement |

### Rules

- Never use raw hex colors for text — use Semantic Tokens only
- Semantic tokens are pre-validated for contrast compliance
- Never override token colors with lower-contrast alternatives
- Always test both Light and Dark themes

---

## Focus States

Focus states must be visible at all times. Removing the outline is strictly forbidden.

### Requirements

- Every interactive element must have a visible focus indicator
- Focus ring must meet `3:1` contrast ratio against adjacent colors
- Focus must be keyboard-triggerable

### Standard Focus Style

```css
:focus-visible {
  outline: 2px solid var(--app-primary);
  outline-offset: 2px;
  border-radius: var(--radius-4);
}
```

### Rules

- Never use `outline: none` or `outline: 0` without a custom visible replacement
- Use `:focus-visible` — not `:focus` — to avoid rings on mouse click
- Focus order must follow logical reading order (RTL-aware)

---

## Keyboard Navigation

All interactive elements must be fully operable via keyboard.

### Required Keys

| Key | Behavior |
|-----|----------|
| `Tab` | Move focus forward |
| `Shift + Tab` | Move focus backward |
| `Enter` | Activate button, link, submit form |
| `Space` | Activate button, toggle checkbox / switch |
| `Escape` | Close modal, drawer, dropdown, tooltip |
| `Arrow keys` | Navigate within components (tabs, select, menu, radio group) |
| `Home` / `End` | Jump to first / last item in a list |

### Rules

- Tab order must match visual reading order
- No keyboard traps — users must always be able to tab out
- Modals must trap focus within themselves while open
- On close, focus must return to the triggering element

---

## Touch Targets

| Property | Value | Token |
|----------|-------|-------|
| Minimum touch target | `40px × 40px` | `size-10` |
| Recommended touch target | `44px × 44px` | `size-11` |
| Minimum gap between targets | `8px` | `space-2` |

### Rules

- No interactive element may have a clickable area smaller than `40px`
- Use padding to extend small icons or labels to meet the minimum
- Spacing between adjacent touch targets must be at least `8px`

---

## Screen Readers & ARIA

### Semantic HTML First

Always prefer semantic HTML over ARIA. ARIA supplements native semantics — it never replaces them.

```html
<!-- Correct -->
<button>Save</button>

<!-- Wrong -->
<div role="button">Save</div>
```

### Required ARIA Patterns

| Scenario | Requirement |
|----------|-------------|
| Icon-only button | `aria-label="Action name"` |
| Decorative image / icon | `alt=""` / `aria-hidden="true"` |
| Meaningful image | `alt="Description"` |
| Loading state | `aria-busy="true"` on container |
| Error message | `aria-describedby` linking input to error |
| Required field | `aria-required="true"` |
| Expanded state | `aria-expanded="true/false"` on trigger |
| Modal / Dialog | `role="dialog"`, `aria-modal="true"`, `aria-labelledby` |
| Live region | `aria-live="polite"` for dynamic content updates |
| Progress bar | `role="progressbar"`, `aria-valuenow`, `aria-valuemin`, `aria-valuemax` |

### Angular Examples

```html
<!-- Icon-only button -->
<button aria-label="Delete course">
  <lucide-icon name="trash-2" [size]="20" aria-hidden="true" />
</button>

<!-- Input with error -->
<input
  id="email"
  type="email"
  aria-describedby="email-error"
  aria-required="true"
  aria-invalid="true"
/>
<span id="email-error" role="alert">Email is required</span>

<!-- Modal -->
<div role="dialog" aria-modal="true" aria-labelledby="modal-title">
  <h2 id="modal-title">Confirm Delete</h2>
</div>

<!-- Live region for toast -->
<div aria-live="polite" aria-atomic="true">
  Course saved successfully.
</div>
```

---

## Reduced Motion

All animated components must respect the user's motion preference.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

> State changes must always be communicated through color, text, or ARIA — never through animation alone.

---

## RTL Accessibility

| Requirement | Implementation |
|-------------|----------------|
| Reading order | Matches RTL visual layout |
| Focus order | Follows RTL direction |
| `lang` attribute | `<html lang="ar" dir="rtl">` |
| Directional icons | Flipped via `scaleX(-1)` |
| Mixed-language content | Set `lang` on inline spans |

```html
<!-- Mixed language -->
<p lang="ar">اسم المستخدم: <span lang="en">John Doe</span></p>
```

---

## Forms Accessibility

| Requirement | Rule |
|-------------|------|
| Labels | Every input must have a visible `<label>` |
| Error messages | Below the field, linked via `aria-describedby` |
| Required fields | Marked visually and with `aria-required="true"` |
| Autocomplete | Use `autocomplete` attribute on common fields |
| Error summary | On submit failure, show a summary at the top of the form |

---

## Component Checklist

Every component must pass before shipping:

- [ ] Color contrast meets WCAG AA (4.5:1 text, 3:1 UI)
- [ ] Focus state is visible and uses design tokens
- [ ] Fully keyboard navigable
- [ ] All interactive elements meet `40px` minimum touch target
- [ ] ARIA roles and attributes are correct
- [ ] Tested with screen reader (VoiceOver / NVDA)
- [ ] Tested in RTL layout
- [ ] Respects `prefers-reduced-motion`
- [ ] No meaning conveyed by color alone
- [ ] Error states have text descriptions, not just color change

---

## Rules

- WCAG 2.1 AA is mandatory — no exceptions
- Semantic HTML before ARIA — always
- Never remove focus outlines without a visible replacement
- Minimum touch target is `40px` enforced via `size-10` token
- Always add `aria-hidden="true"` to decorative icons
- State changes must be communicated to screen readers via `aria-live` or role updates
- Test with keyboard, screen reader, and high-contrast mode before marking done
