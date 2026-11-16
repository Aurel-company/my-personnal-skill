---
name: interface-craft
description: Apply fine-grained interface craft when building or reviewing UI — typography (kerning, tracking, leading, x-height, line length, widows, tabular numbers), geometry (optical centre, touch targets, safe areas), color (OKLCH), motion (origin-aware, staggered, interruptible, shared element transitions) and interaction (affordance, combobox, optimistic updates, progressive disclosure, layout shift). Use when polishing a component, auditing UI details, or when something "feels off" but is hard to name.
---

# Interface craft

Polish is the sum of small decisions that nobody notices when they are right and everybody feels when they are wrong. Each concept below has: **what it is**, **the rule**, **how to apply it**, **the common failure**.

Apply a concept only when the interface actually contains the situation (no stagger without a list, no combobox without a long option set). Fix the floor first: contrast, focus states, `prefers-reduced-motion`, working mobile layout.

---

## 1. Typography

### Line length (measure)
- **Rule**: body text lives between **45 and 75 characters per line** (66 is the classic target). Below 40 it chops; above 80 the eye loses the next line.
- **Apply**: cap with `max-width: 65ch` on the text container, not on the page. Set it in `ch`, never in px, so it follows the font.
- **Failure**: full-width paragraphs on a wide monitor; 25-character columns on mobile with huge type.

### Leading (line height)
- **Rule**: leading is inversely related to size and directly related to line length. Body: **1.5–1.65**. Headings: **1.05–1.25**. Long measure or small x-height needs more leading.
- **Apply**: unitless values (`line-height: 1.6`), never `px`, so nested sizes inherit correctly. Re-tune per size: a display heading at body leading looks broken. Multi-line buttons, labels and badges: 1.2–1.3.
- **Failure**: one global `line-height` for everything; headings that float apart.

### Tracking (letter-spacing)
- **Rule**: tracking is uniform spacing across a run of text. **Large type: tighten** (−0.01 to −0.03em). **Small text and ALL CAPS: loosen** (+0.04 to +0.12em). Never track lowercase body text.
- **Apply**: use `em` so it scales with size. Define it per type-scale step as a token, not ad hoc per component.
- **Failure**: crushed display type with touching letters; all-caps labels with default tracking.

### Kerning
- **Rule**: kerning is the adjustment of space between **specific letter pairs** (AV, To, 7.). It is a font feature, not a style you set manually.
- **Apply**: keep it on: `font-kerning: auto` (default) and `text-rendering: optimizeLegibility` on headings and logos. Check display sizes and wordmarks by eye for bad pairs; fix individual pairs in the logo asset, not with global tracking. Some browsers disable kerning or ligatures when `letter-spacing` is non-zero: verify after tracking changes.
- **Failure**: confusing kerning with tracking; hand-spacing a title that the font already kerns well.

### x-height
- **Rule**: x-height is the height of lowercase letters relative to capitals. A larger x-height reads bigger and clearer at the same `font-size`, and needs less size and less leading; a small x-height needs more of both.
- **Apply**: when pairing two typefaces, **match x-height, not font-size** (use `font-size-adjust: from-font` or an explicit value). Prefer large-x-height faces for dense UI and small text. Check fallback fonts: a fallback with a different x-height causes visible reflow when the web font loads.
- **Failure**: two fonts at "16px" where one looks 2px smaller; a fallback stack that jumps on load.

### Widows and orphans
- **Rule**: never end a paragraph or heading with a **single short word alone on the last line**.
- **Apply**: `text-wrap: balance` on headings, short blurbs and captions; `text-wrap: pretty` on body paragraphs. When the browser cannot help, bind the last two words with a non-breaking space (`&nbsp;`) in static copy.
- **Failure**: a heading that wraps to one orphan word; a card description ending in "of."

### Tabular numbers
- **Rule**: wherever digits change or align vertically (tables, prices, timers, counters, stats, dashboards, version numbers), use **tabular figures** so every digit has the same width.
- **Apply**: `font-variant-numeric: tabular-nums;` (add `slashed-zero` for codes and IDs, `lining-nums` for tables). Right-align numeric columns. Leave proportional figures in running prose.
- **Failure**: a live counter that jitters as digits change; a column of amounts that does not line up on the decimal.

---

## 2. Geometry and touch

### Optical centre
- **Rule**: mathematical centre is not perceived centre. Shapes with visual weight or asymmetry look off when centred by the box.
- **Apply**:
  - Play/forward triangles: shift **right** by roughly 6–10% of their width.
  - Icons inside circles or buttons: nudge the heavier side inward until it feels centred; judge with the eye, then store the offset in the icon token.
  - Text in buttons: align on the **x-height / cap-height centre**, not the line box. A slightly smaller top padding than bottom (e.g. 10px / 12px) often looks centred; `text-box-trim: trim-both` with `text-box-edge: cap alphabetic` does it properly where supported.
  - Content placed in a hero or modal: sit it slightly **above** geometric centre (about 45% from the top, not 50%).
- **Failure**: a play icon that looks pushed left; text that sits low in its button.

### Touch target
- **Rule**: interactive targets are at least **44×44 px** (Apple HIG) or **48×48 dp** (Material); WCAG 2.2 AA minimum is 24×24 CSS px with spacing. Pick 44px as the default.
- **Apply**: the *visible* element may be smaller; extend the **hit area** with padding, a transparent `::before { inset: -8px }`, or `min-width/min-height: 44px`. Leave at least 8px between adjacent targets. Make the whole row tappable in lists, not only the label. Never let two hit areas overlap.
- **Failure**: 16px icon buttons packed together; a checkbox you can only hit on the box itself.

### Safe area
- **Rule**: content and controls must not sit under notches, rounded corners, the home indicator, or browser chrome.
- **Apply**: `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">`, then pad with `env(safe-area-inset-top|right|bottom|left)`. Combine with your own spacing: `padding-bottom: max(16px, env(safe-area-inset-bottom))`. Fixed bottom bars, tab bars, sheets and sticky CTAs always need it. Backgrounds may extend edge to edge; interactive content stays inside. Use `dvh`, not `vh`, for full-height layouts on mobile.
- **Failure**: a bottom button under the home indicator; landscape content clipped by the notch.

---

## 3. Color

### OKLCH
- **Rule**: define color in **OKLCH** (`oklch(L C H)`), a perceptually uniform space: equal lightness steps look equal, and changing hue does not change perceived brightness the way it does in HSL.
- **Apply**:
  - Build scales by **stepping L** with C and H nearly constant, then lower C at the extremes (very light and very dark colors cannot hold high chroma).
  - Keep accessible contrast by controlling **L**: pair tokens with a known L gap, then still verify with a real contrast checker (APCA or WCAG).
  - Make a semantic palette (success, warning, danger, info) with the **same L and C** and different H, so they have equal visual weight.
  - Derive hover, active, disabled and dark mode by shifting L, not by guessing hex.
  - Tint neutrals with the brand hue at tiny chroma (C ≈ 0.005–0.02) so grays belong to the palette.
  - Provide a fallback when needed: `color: #3b82f6; color: oklch(62% 0.19 255);` and use `color-mix(in oklch, …)` for blends.
- **Failure**: HSL palettes where yellow looks bright and blue looks dark at the same "lightness"; gradients that turn gray in the middle (interpolate with `in oklch`).

---

## 4. Motion

Default budget: **150–250 ms** for UI feedback, **250–400 ms** for large surfaces. Use `ease-out` for entering, `ease-in` for leaving, and custom curves over the browser defaults. Always honour `prefers-reduced-motion` (replace movement with a fade or nothing).

### Origin-aware animation
- **Rule**: an element should **grow from and shrink to the thing that caused it**. A popover from a button must not scale from its own centre.
- **Apply**: set `transform-origin` to the trigger point (`top left` for a menu opened from the top-left, or compute it from the trigger's position, or use the `anchor()` / popover APIs). Dropdowns scale + fade from the anchor edge; modals from the click point or from centre if triggered by a keyboard shortcut; toasts slide in from the edge they dock to.
- **Failure**: a tooltip that zooms from its centre while its arrow points elsewhere.

### Interruptible animation
- **Rule**: the user can change their mind mid-motion, and the animation must respond **immediately and continue from its current state**, not restart or finish first.
- **Apply**: prefer **CSS transitions** (they retarget from the current value) over keyframe animations for state changes that can toggle. Use springs (Motion, react-spring, `linear()` easing) for gestures and anything draggable: they carry velocity and are naturally interruptible. Never lock the UI during an animation; never block input with `pointer-events: none` for the duration. Open→close→open quickly must not jump.
- **Failure**: a drawer that completes its open animation before it will close; a double-clicked toggle that snaps.

### Stagger
- **Rule**: when several items enter together, offset them slightly so the eye follows a sequence instead of seeing one block pop in.
- **Apply**: **30–60 ms** between items (cap total stagger around 400 ms — show at most ~8 items staggered, then group the rest). Set the delay via a CSS variable (`animation-delay: calc(var(--i) * 40ms)`). Order by reading order or by proximity to the trigger. Trigger once, on entry, not on every re-render, and disable under reduced motion.
- **Failure**: a 20-item list taking 2 seconds to appear; stagger replaying on every data refresh.

### Shared element transition
- **Rule**: when the same thing exists in two views (a card → its detail page, a thumbnail → full image), **morph one into the other** so the user tracks identity across the change.
- **Apply**: the **View Transitions API** (`document.startViewTransition`, `view-transition-name` unique per element per page; cross-document with `@view-transition { navigation: auto }`), or Motion's `layoutId`. Match aspect ratio and radius, or animate them. Keep it under ~400 ms, make it reversible (back morphs back), and have a plain crossfade as fallback. Only the shared element morphs; the rest of the page fades.
- **Failure**: a card that cuts to a new page with no continuity; two elements sharing the same `view-transition-name`.

---

## 5. Interaction and state

### Affordance
- **Rule**: an element should **look like what it does**. Clickable things look clickable; editable things look editable; draggable things show a grip.
- **Apply**: buttons have shape, contrast and a pressed state; links are distinguishable beyond color; inputs have visible borders or fills; `cursor: pointer` on desktop targets; every interactive element has hover, focus-visible, active and disabled states. Do not use the same style for a button and a label. Icons alone get a label or tooltip unless universal (close, search). Hidden gestures (swipe, long-press) need a visible alternative.
- **Failure**: flat text that is secretly a button; a "disabled" look on an active control.

### Combobox
- **Rule**: use a **combobox** (input + filterable list) instead of a plain select when there are **more than ~7–10 options** or users know what they want and can type it.
- **Apply**: follow the ARIA APG pattern: `role="combobox"` on the input, `aria-expanded`, `aria-controls`, `aria-activedescendant`, `role="listbox"` / `role="option"`. Keyboard: ↓/↑ move, Enter selects, Esc closes (and clears on second press), Home/End, typing filters. Highlight the matched substring, show an empty state ("No results for …"), keep focus in the input, and debounce async search (150–250 ms) with a loading state. Distinguish *select-only* (must pick from list) from *editable* (free text allowed). Use a library (Radix, Headless UI, React Aria, Base UI) rather than hand-rolling.
- **Failure**: a native `<select>` with 200 countries and no search; a list that cannot be used with the keyboard.

### Optimistic update
- **Rule**: for actions that **almost always succeed** (like, toggle, reorder, add to list, rename), update the UI **immediately** and reconcile with the server afterwards.
- **Apply**: apply the change locally → send the request → on success keep (swap in server data/IDs) → on failure **roll back to the previous state and tell the user** (toast with retry). Keep a snapshot for rollback, guard against out-of-order responses, and make the request idempotent. Show a subtle pending state only for slow cases. **Do not** use it for payments, deletions that cannot be undone, or when the outcome depends on server validation.
- **Failure**: a spinner on a "like" button; a silent rollback that leaves the user confused.

### Progressive disclosure
- **Rule**: show only what is needed **now**; reveal the rest on demand, in a way that is easy to find.
- **Apply**: primary action and the common 80% case up front; advanced options behind "More options", an accordion, a drawer, or a second step. Label the disclosure clearly ("Advanced settings"), keep it keyboard accessible (`<details>`, `aria-expanded`), preserve state if the user collapses and reopens, and never hide something essential to completing the task. Wizards for long forms; defaults for the rest. Limit depth to about two levels.
- **Failure**: a settings page showing 40 controls at once; critical options buried three levels deep.

### Layout shift
- **Rule**: **nothing already on screen should move** because something else loaded or changed. Target **CLS < 0.1**.
- **Apply**:
  - Reserve space: `width`/`height` or `aspect-ratio` on images, video, embeds, ads, avatars.
  - Skeletons with the **same dimensions** as the final content.
  - Reserve room for error messages, banners and validation text (or overlay them).
  - Load web fonts with `font-display: swap` plus a fallback with matched metrics (`size-adjust`, `ascent-override`) — links to x-height above.
  - Use tabular numbers so counters do not resize.
  - Add content **below** the viewport or in response to a user action, never above what the user is reading; use `overflow-anchor` / scroll anchoring for prepended items.
  - Animate `transform` and `opacity`, not `width`, `height`, `top`, `left`.
  - Show a scrollbar gutter: `scrollbar-gutter: stable`.
- **Failure**: the button you were about to tap jumps down because an image loaded; a banner pushing the page after first paint.

---

## Workflow

### Building
1. List which situations appear in the screen (text, numbers, tap targets, lists, overlays, async actions, navigation between views).
2. Apply the matching rules above; skip the rest.
3. Encode values as **tokens** (type scale with tracking and leading, `--tap-min: 44px`, motion durations and easings, OKLCH palette) so the details are consistent rather than repeated.

### Reviewing
Go through the screen and report each issue as: **concept → location → what is wrong → concrete fix**. Order by severity:

- **P0 (breaks use)**: touch target < 24px, content under the safe area, layout shift on a primary action, combobox/menu unusable by keyboard, animation that blocks input, destructive optimistic update.
- **P1 (felt by everyone)**: line length > 80ch, jittering numbers, orphan words in headings, non-interruptible transitions, missing affordance or states, wrong transform-origin.
- **P2 (felt by designers)**: kerning on display type, optical centre of icons, x-height matching, stagger timing, OKLCH scale tuning.

### Final check
- Can every target be hit with a thumb, with space between neighbours?
- Does anything move that the user did not cause?
- Does every animation start from its cause and survive being interrupted?
- Do numbers stay still when they change?
- Is each paragraph readable at its width and leading, with no lone last word?
- Is everything essential visible, and everything else one clear step away?
