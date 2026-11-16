---
name: responsive-web-app
description: Build, review or fix the responsive behavior of a web app (dashboards, forms, tables, navigation), from 320px phones to desktop. Use when the user mentions responsive, mobile layout, breakpoints, container queries, fluid type, horizontal scroll, 100vh, safe areas, virtual keyboard, touch targets, tablet or desktop adaptation, or WCAG reflow.
---

# Responsive web app

Responsive means the interface works for every viewport, input method and user setting, not only for a few device widths. Start from content and intrinsic CSS, add queries only where layout must change structurally, then verify on real constraints (320px, 400% zoom, long text, real phones).

Full checklist with code: [references/responsive-checklist.md](references/responsive-checklist.md). Sources and their reliability: [references/sources.md](references/sources.md).

## Operating rules

1. **Mobile-first, content-driven.** Base styles are the small-screen styles; enhance with `min-width` queries. Place breakpoints where the content breaks, not at device models. Keep them few.
2. **Intrinsic first, queries second.** Prefer flex, grid, `minmax()`, `clamp()`, `min()`, `auto-fit`. Use media queries for viewport-level layout changes and user preferences; use container queries for components that live in different contexts.
3. **Never block the user's controls.** No `user-scalable=no`, no `maximum-scale=1`, no orientation lock, no fixed heights that clip text.
4. **Relative units for text and spacing** (`rem`, `em`, `ch`, `fr`, `%`). Pixels only for borders and hairlines.
5. **Diagnose overflow, do not hide it.** Never put `overflow-x: hidden` on `body` to mask a horizontal scrollbar. Find the element that overflows and fix its cause.
6. **Say what is sourced and what is judgment.** Rules from W3C, web.dev and Chrome docs are firm. Navigation and form patterns come from practitioner blogs: apply them as defaults, adapt to the product.
7. **Test, do not assume.** DevTools emulation does not reproduce browser bars, safe areas or iOS Safari quirks.

## Workflow

### 1. Decide the constraints (before code)

Write these down, in a short note or in the reply:

- **Target range**: smallest width supported (default 320px), largest content width, landscape yes/no.
- **Input modes**: touch, mouse, keyboard, hybrid. What depends on hover?
- **Content stress cases**: longest label, long translation, empty state, 200 rows, long unbroken string.
- **Structure per size**: navigation (phone, tablet, desktop), where the main action lives, what collapses, what scrolls and what stays fixed.
- **Containers**: which components appear in more than one context (card, list item, widget) and so need container queries.

### 2. Build

Apply the checklist sections in this order:

1. **Foundations**: viewport meta, box-sizing, fluid media, no fixed widths.
2. **Layout**: intrinsic grid/flex, `min-width: 0` on shrinking flex children, `minmax(0, 1fr)` tracks, container queries for components.
3. **Type and spacing**: `clamp()` with `rem` bounds, `ch` line length, spacing tied to type.
4. **Viewport behavior on mobile**: `svh`/`dvh` instead of `100vh`, safe-area insets, keyboard behavior for fixed bars.
5. **Input and touch**: 24px minimum targets (aim for 44px), `@media (hover: hover)` for hover styles, 16px minimum on inputs, correct `inputmode`, `autocomplete`.
6. **Components**: navigation, tables, forms, modals, images (see checklist).
7. **Accessibility tied to responsive**: reflow at 320px, text-spacing overrides, zoom at 200%/400%, reduced motion.

### 3. Verify

Run all of these and report what you checked:

- 320px wide, then 400% zoom on a 1280px window: no two-dimensional scroll (data tables, maps, diagrams excepted).
- Horizontal overflow scan: no element wider than the viewport, no stray horizontal scrollbar at 320, 375, 768, 1024, 1440.
- Stress content: longest label, long translation, empty state, many rows, long unbroken string.
- Text-spacing override (line-height 1.5, paragraph 2x, letter 0.12em, word 0.16em): nothing clipped.
- Touch: targets reach 24px minimum, primary ones about 44px; no hover-only function; no sticky hover.
- Mobile viewport: bottom bars not hidden by browser bar or home indicator; keyboard does not cover the focused field or the primary action.
- Keyboard-only navigation and visible focus at each size; both themes if both exist; landscape.
- On at least one real iOS and one real Android device when the project allows it. If not tested, say so.

## When reviewing existing work

Report findings as: element or rule, viewport or condition where it fails, cause, concrete fix. Order by severity: loss of content or function (P0), user setting ignored such as zoom or text spacing (P1), friction (P2). Do not rewrite what was not asked.

## Pairing

Pair with a product-design pass for flows and states, and with an accessibility check for anything beyond the responsive criteria. It does not decide visual style.
