---
name: Icon System
tier: Primitive
status: Active
last-updated: 2026-06-08
maintainer: n.ouda@eltgcc.com
owner: acadimiat
---

# Icon System

## Philosophy

Acadimiat uses **Lucide Icons** exclusively — a clean, stroke-based icon library with consistent geometry and visual weight. Icons communicate meaning without decoration. Mixing icon libraries is strictly forbidden.

> **Lucide Icons only — no exceptions.**
> No filled icons, no other libraries, no custom SVGs unless approved.

---

## Library

| Property | Value |
|----------|-------|
| Library | [Lucide Icons](https://lucide.dev) |
| Style | Stroke-based (outline) |
| Stroke width | `2` (default) |
| Package (Angular) | `lucide-angular` |
| License | ISC |

---

## Icon Sizes

| Token | px | Usage |
|-------|----|-------|
| `icon-sm` → `size-4` | `16px` | Inline text, badges, compact UI |
| `icon-md` → `size-5` | `20px` | Buttons, inputs, nav items (default) |
| `icon-lg` → `size-6` | `24px` | Section headers, empty states, large actions |

> Default icon size is `20px`. Use `16px` only when space is critically constrained. Use `24px` for prominent standalone icons.

---

## Stroke Width

| Context | Stroke Width |
|---------|-------------|
| All sizes (default) | `2` |
| Do not change | — |

> Never change the stroke width. Lucide's visual consistency depends on a uniform stroke of `2`.

---

## Color

Icons inherit color from `currentColor` — they always match the text color of their parent element unless explicitly overridden via a Semantic Token.

| Context | Color Token |
|---------|-------------|
| Default icon | `--app-text-secondary` |
| Active / selected icon | `--app-primary` |
| Disabled icon | `--app-text-disabled` |
| Danger icon | `--app-error` |
| Success icon | `--app-success` |
| Warning icon | `--app-warning` |
| Info icon | `--app-info` |

---

## Angular Implementation

### Installation

```bash
npm install lucide-angular
```

### Module Setup

```typescript
import { LucideAngularModule, icons } from 'lucide-angular';

@NgModule({
  imports: [
    LucideAngularModule.pick(icons) // tree-shake — pick only used icons
  ]
})
```

### Usage in Template

```html
<!-- Default size (20px) -->
<lucide-icon name="check" [size]="20" />

<!-- Small (16px) -->
<lucide-icon name="chevron-right" [size]="16" />

<!-- Large (24px) -->
<lucide-icon name="layout-dashboard" [size]="24" />

<!-- With color token -->
<lucide-icon name="alert-circle" [size]="20" class="icon-warning" />
```

```css
.icon-warning {
  color: var(--app-warning);
}
```

---

## Icon Categories for Acadimiat

Common icons organized by product context. All names are Lucide icon names.

### Navigation

| Icon Name | Usage |
|-----------|-------|
| `layout-dashboard` | Dashboard home |
| `book-open` | Courses |
| `users` | Students / CRM |
| `shopping-cart` | Checkout / Sales |
| `bar-chart-2` | Analytics |
| `zap` | Automations |
| `settings` | Settings |
| `bell` | Notifications |
| `search` | Search |
| `menu` | Mobile hamburger |
| `x` | Close / dismiss |
| `chevron-right` | Navigation arrow (RTL: chevron-left) |
| `chevron-down` | Expand |

### Actions

| Icon Name | Usage |
|-----------|-------|
| `plus` | Add / create |
| `pencil` | Edit |
| `trash-2` | Delete |
| `copy` | Duplicate |
| `upload` | Upload |
| `download` | Download |
| `share-2` | Share |
| `eye` | Preview / view |
| `eye-off` | Hide |
| `filter` | Filter |
| `sort-asc` / `sort-desc` | Sort |
| `more-horizontal` | More options |
| `more-vertical` | More options (vertical) |

### Status & Feedback

| Icon Name | Usage |
|-----------|-------|
| `check` | Success inline |
| `check-circle` | Success state |
| `x-circle` | Error state |
| `alert-triangle` | Warning state |
| `info` | Info state |
| `loader-2` | Loading / spinner |
| `clock` | Pending / time |
| `lock` | Locked |
| `unlock` | Unlocked |

### Course & Content

| Icon Name | Usage |
|-----------|-------|
| `play-circle` | Start lesson / video |
| `pause-circle` | Pause |
| `file-text` | Article / document |
| `video` | Video lesson |
| `headphones` | Audio |
| `award` | Certificate |
| `graduation-cap` | Course / student |
| `clipboard-list` | Quiz / assignment |
| `bookmark` | Save / bookmark |
| `star` | Rating |

### Community & CRM

| Icon Name | Usage |
|-----------|-------|
| `message-circle` | Comment / message |
| `heart` | Like |
| `user` | Student profile |
| `user-plus` | Add student |
| `mail` | Email |
| `phone` | Phone |
| `tag` | Label / tag |

---

## RTL Notes

Some directional icons must be flipped for RTL layouts.

| Icon | RTL Behavior |
|------|-------------|
| `chevron-right` | Use `chevron-left` in RTL |
| `chevron-left` | Use `chevron-right` in RTL |
| `arrow-right` | Flip horizontally in RTL |
| `arrow-left` | Flip horizontally in RTL |
| `log-in` | Flip horizontally in RTL |
| `log-out` | Flip horizontally in RTL |

```css
[dir="rtl"] .icon-directional {
  transform: scaleX(-1);
}
```

---

## Rules

- Lucide Icons only — no other libraries, no mixing styles
- Stroke width must remain `2` at all times
- Always use `currentColor` — never hardcode icon colors
- Icon sizes are limited to `16px`, `20px`, and `24px`
- Directional icons must be flipped in RTL
- Tree-shake imports — never import the full icon set in production
- Never use icons to convey meaning without an accessible label (`aria-label` or visible text)
