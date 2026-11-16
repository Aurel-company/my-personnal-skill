---
name: interface-craft
description: Apply fine-grained interface craft when building or reviewing UI — typography (kerning, tracking, leading, x-height, line length, widows, tabular numbers), geometry (optical centre, concentric radius, matched icon weight, touch targets, safe areas, dynamic viewport), color and surfaces (OKLCH palettes and gradients, alpha borders, masked edges, dark mode depth), motion (origin-aware, staggered, interruptible, shared element and blurred icon swap transitions) and interaction (affordance, combobox, optimistic updates, progressive disclosure, layout shift). Use when polishing a component, auditing UI details, or when something "feels off" but is hard to name.
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

## 2. Geometry, icons and touch

### Optical centre
- **Rule**: mathematical centre is not perceived centre. Shapes with visual weight or asymmetry look off when centred by the box.
- **Apply**:
  - Play/forward triangles: shift **right** by roughly 6–10% of their width.
  - Icons inside circles or buttons: nudge the heavier side inward until it feels centred; judge with the eye, then store the offset in the icon token.
  - Text in buttons: align on the **x-height / cap-height centre**, not the line box. A slightly smaller top padding than bottom (e.g. 10px / 12px) often looks centred; `text-box-trim: trim-both` with `text-box-edge: cap alphabetic` does it properly where supported.
  - Content placed in a hero or modal: sit it slightly **above** geometric centre (about 45% from the top, not 50%).
- **Failure**: a play icon that looks pushed left; text that sits low in its button.

### Concentric radius
- **Rule**: when a rounded element sits inside another rounded element, their corners must share the same centre: **outer radius = inner radius + the distance between the two edges** (the padding, plus the border width if the parent has a border). Example: inner 8px + padding 12px → outer 20px.
- **Apply**: derive the inner radius, never type it twice.
  ```css
  .card { --r-outer: 20px; --pad: 12px;
          border-radius: var(--r-outer); padding: var(--pad); }
  .card > .inner { border-radius: max(0px, calc(var(--r-outer) - var(--pad))); }
  ```
  With a parent border: subtract `padding + border-width`. Use it for image in card, button in container, input groups, segmented controls, nested menus; chain it for three levels. The formula is not needed when a radius is 0 or fully round (pill, circle). If padding is larger than the outer radius, the inner radius clamps to 0 (square), which is correct. Sheets and cards near a device edge should follow the same logic against the screen corner.
- **Failure**: the same radius token on parent and child: the gap looks thick in the corners and thin on the sides, the inner shape looks pinched.

### Matched icon weight
- **Rule**: an icon's stroke must carry the **same visual weight as the text beside it**. Thin icons next to semibold text look faint; heavy icons next to light text look clunky. Font weight and stroke width are different systems: judge the apparent emphasis in the real component, not the numbers alone.
- **Apply**:
  - Starting points (verify against your font): **1.5px stroke beside regular text, 2px beside semibold**. At 16px a regular sans has stems of about 1.5px.
  - Use SVG icons with a controllable `stroke-width` (Lucide, Phosphor weights) or a variable icon font with a weight axis (Material Symbols). Classic icon fonts have one weight.
  - One stroke width for the whole set; never mix outline and solid icons in one row.
  - Scaling an SVG with `width/height` scales its stroke too (a 24px icon shown at 16px gets 1.33px). Set `stroke-width` per size, or use `vector-effect: non-scaling-stroke` / Lucide's `absoluteStrokeWidth`.
  - Size the icon to the text line (16px icon with 14px text, 20px with 16px) and centre it on the text's x-height / cap-height, not the line box (see optical centre).
  - Check at the real size on 1x and 2x screens, never zoomed in.
- **Failure**: 2px chunky icons beside a light 400 caption; icons that thin out when scaled down; a set that mixes strokes.

### Touch target
- **Rule**: interactive targets are at least **44×44 px** (Apple HIG) or **48×48 dp** (Material); WCAG 2.2 AA minimum is 24×24 CSS px with spacing. Pick 44px as the default.
- **Apply**: the *visible* element may be smaller; extend the **hit area** with padding, a transparent `::before { inset: -8px }`, or `min-width/min-height: 44px`. Leave at least 8px between adjacent targets. Make the whole row tappable in lists, not only the label. Never let two hit areas overlap.
- **Failure**: 16px icon buttons packed together; a checkbox you can only hit on the box itself.

### Safe area
- **Rule**: content and controls must not sit under notches, rounded corners, the home indicator, or browser chrome.
- **Apply**: `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">`, then pad with `env(safe-area-inset-top|right|bottom|left)`. Combine with your own spacing: `padding-bottom: max(16px, env(safe-area-inset-bottom))`. Fixed bottom bars, tab bars, sheets and sticky CTAs always need it. Backgrounds may extend edge to edge; interactive content stays inside. Use `dvh`, not `vh`, for full-height layouts on mobile.
- **Failure**: a bottom button under the home indicator; landscape content clipped by the notch.

### Dynamic viewport
- **Rule**: on mobile, `100vh` equals the **largest** viewport (browser toolbars retracted), so a full-height layout is cut off while the toolbar is visible. Choose the unit by intent: **`svh`** (small: toolbars shown, always fits), **`lvh`** (large: toolbars hidden, same as legacy `vh`), **`dvh`** (dynamic: follows the current state as toolbars show and hide). On desktop all three equal `vh`.
- **Apply**:
  - Hero or landing section that must not jump while scrolling → `min-height: 100svh`.
  - App shell, chat, full-screen sheet or modal that should fill exactly what is visible → `100dvh`.
  - A background that must always cover the screen → `lvh`.
  - Fallback for older browsers: `height: 100vh; height: 100dvh;`. Prefer `min-height` to `height` so content can grow.
  - `dvh` re-lays out while the toolbar animates: avoid it on heavy, animated or text-reflowing elements.
  - `dvh` does not react to the on-screen keyboard. Where supported use `interactive-widget=resizes-content` in the viewport meta, or the `visualViewport` API, for inputs pinned to the bottom.
  - Combine with safe-area padding; test on a real phone.
- **Failure**: a primary button hidden under the browser toolbar because of `100vh`; a hero that jumps on every scroll because `dvh` was used where `svh` was needed.

---

## 3. Color, surfaces and depth

### OKLCH palettes
- **Rule**: define color in **OKLCH** (`oklch(L C H)`), a perceptually uniform space: equal lightness steps look equal, and changing hue does not change perceived brightness the way it does in HSL.
- **Apply**:
  - Build scales by **stepping L** with C and H nearly constant, then lower C at the extremes (very light and very dark colors cannot hold high chroma).
  - Keep accessible contrast by controlling **L**: pair tokens with a known L gap, then still verify with a real contrast checker (APCA or WCAG).
  - Make a semantic palette (success, warning, danger, info) with the **same L and C** and different H, so they have equal visual weight.
  - Derive hover, active, disabled and dark mode by shifting L, not by guessing hex.
  - Tint neutrals with the brand hue at tiny chroma (C ≈ 0.005–0.02) so grays belong to the palette.
  - Provide a fallback when needed: `color: #3b82f6; color: oklch(62% 0.19 255);` and use `color-mix(in oklch, …)` for blends.
- **Failure**: HSL palettes where yellow looks bright and blue looks dark at the same "lightness"; a generated scale that looks accessible but was never contrast-checked; out-of-gamut colors that get clipped and flatten.

### OKLCH gradients
- **Rule**: always say which color space a gradient interpolates in. The default (sRGB) makes mixes between distant colors dull, gray or dark in the middle (blue to yellow is the classic). **`in oklch`** (or `in oklab`) keeps lightness and chroma steady, so transitions stay clean and vivid.
- **Apply**:
  ```css
  background: linear-gradient(in oklch, oklch(0.7 0.15 250), oklch(0.85 0.15 90));
  ```
  - Hue path in OKLCH: `shorter` is the default (blue to red goes through purple). Add `longer hue` for a rainbow or iridescent sweep; `increasing hue` / `decreasing hue` force the direction.
  - Use `in oklab` for a straight blend with no hue detour (neutral to color, or two close colors).
  - When one end is gray, OKLCH takes the hue from the other end, so there is no detour.
  - Fade to transparent with the same color at zero alpha (`oklch(0.7 0.15 250 / 0)`) so the fade does not drift in hue.
  - The same method works in `conic-gradient`, `radial-gradient` and `color-mix(in oklch, …)`.
  - Keep chroma inside the gamut you target; out-of-gamut stops are clipped and create flat bands. Large soft gradients can show banding: add a faint grain.
- **Failure**: a muddy gray band in the middle of a blue to yellow gradient; a brand gradient that turns purple on the way because of an unintended hue path.

### Alpha borders
- **Rule**: draw borders, dividers and outlines with a **semi-transparent** color (black or white at low alpha) instead of an opaque gray, so they adapt to whatever is under them: tinted cards, hover states, light and dark mode.
- **Apply**:
  - Light: `border: 1px solid oklch(0 0 0 / 0.08)`. Dark: `oklch(1 0 0 / 0.1)`. Tokens: `--border-subtle` 6-8%, `--border` 10-14%, `--border-strong` ~20%.
  - There is no `border-opacity` property, and `opacity` would fade the whole element: put the alpha in the color.
  - A background paints under the border by default, which makes a translucent border look solid. Use `background-clip: padding-box` when you need the true alpha (translucent or glass surfaces).
  - Images: add a hairline inset outline so their edge does not melt into a similar background: `outline: 1px solid oklch(0 0 0 / 0.1); outline-offset: -1px;`.
  - Adjacent translucent borders stack and look doubled: use one divider or a `gap` instead of two borders.
- **Failure**: opaque `#ddd` borders that look heavy on a tinted card and glow in dark mode; double-thick lines where translucent borders overlap.

### Masked edges
- **Rule**: to soften where content is clipped or continues, **mask the content's alpha** with a gradient instead of laying a colored gradient on top. A mask removes pixels, so it works on any background, image, theme or hover state; an overlay must match the background color exactly.
- **Apply**:
  ```css
  .fade {
    -webkit-mask-image: linear-gradient(to bottom, transparent, #000 24px, #000 calc(100% - 24px), transparent);
            mask-image: linear-gradient(to bottom, transparent, #000 24px, #000 calc(100% - 24px), transparent);
  }
  ```
  - Use for scroll lists, tab rows, marquees, carousels, clamped text, image bottoms. Fade length 16-32px. Safari needs the `-webkit-` prefix.
  - Fade an edge only when more content lies beyond it, so the first and last items are fully visible at the ends of the scroll. Scroll-driven animation (`animation-timeline: scroll(self y)`) can animate the mask size; keep a static fade as fallback.
  - A mask on the scroll container fades its scrollbar too: hide the scrollbar or put the mask on an inner wrapper.
  - Never let a fade hide content the user cannot otherwise reach or read.
- **Failure**: a white gradient overlay that shows as a band on a tinted card or in dark mode; a list cut hard at the edge with no hint that it scrolls.

### Dark mode depth
- **Rule**: in dark mode shadows barely show against a dark surface, so **elevation is expressed by lightness**: the closer a surface is to the user, the lighter it is. Keep real shadows only as a supplement for floating layers (popovers, modals).
- **Apply**:
  - Define surface tokens by elevation, one step of about **4-6% lightness** (OKLCH: ΔL ≈ 0.03-0.05): `--bg: oklch(0.16 0.01 260)`, `--surface-1: oklch(0.20 0.01 260)`, `--surface-2: oklch(0.24 0.01 260)`, `--surface-3: oklch(0.28 0.01 260)`. Keep the same elevation order as light mode (modal is highest).
  - Avoid pure `#000` backgrounds and pure `#fff` text (use text around L 0.92-0.95): harsh contrast and halation.
  - Separate layers with alpha borders (white 8-12%) and, optionally, a 1px top highlight: `box-shadow: inset 0 1px 0 oklch(1 0 0 / 0.06)`.
  - Lower chroma on large colored areas and raise lightness on accent text so it keeps its contrast.
  - Do not invert the light palette: re-derive dark tokens. Do not fake elevation with light glows.
- **Failure**: the light-mode box-shadow reused unchanged so every card looks flat; all surfaces the same black; a neon-saturated palette copied from light mode.

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

### Blurred icon swap
- **Rule**: when an icon changes in place (copy → check, play → pause, menu → close, theme toggle), neither hard-cut nor plain-crossfade it. **Scale, blur and fade** the outgoing and incoming icons so two different shapes read as one object changing state: the blur hides the moment where both glyphs overlap.
- **Apply**:
  - Stack both icons in the same fixed-size box (`display: grid` with both in `grid-area: 1 / 1`, or absolute positioning).
  - Exiting icon: opacity 1 → 0, scale 1 → ~0.25-0.6, blur 0 → 2-4px. Entering icon: the reverse.
  - Duration about **150-200 ms**, ease-in-out or a spring. One `transition` on `opacity, transform, filter`, never `transition: all`.
  - Swap with a changed `key` (React + Motion `AnimatePresence`) or a `data-state` attribute in CSS. Use transitions so rapid clicks retarget (see interruptible animation).
  - Reduced motion: opacity only, no scale or blur.
  - Keep blur small and on small elements: large blurred areas are GPU-costly on low-end phones.
  - The swap is visual only: update the accessible name or announce the state ("Copied") as well.
- **Failure**: an instant swap that flickers; a plain crossfade showing two half-visible glyphs; layout shift because the two icon boxes differ in size.

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

- **P0 (breaks use)**: touch target < 24px, content under the safe area, primary action hidden by `100vh` under the mobile toolbar, layout shift on a primary action, combobox/menu unusable by keyboard, animation that blocks input, destructive optimistic update.
- **P1 (felt by everyone)**: line length > 80ch, jittering numbers, orphan words in headings, non-interruptible transitions, missing affordance or states, wrong transform-origin, dark mode with flat identical surfaces, gradients with a gray middle, colored overlays instead of masks over variable backgrounds.
- **P2 (felt by designers)**: kerning on display type, optical centre of icons, x-height matching, stagger timing, OKLCH scale tuning, concentric radii, icon stroke vs text weight, alpha border levels, blurred icon swaps.

### Final check
- Can every target be hit with a thumb, with space between neighbours?
- Does anything move that the user did not cause?
- Does every animation start from its cause and survive being interrupted?
- Do numbers stay still when they change?
- Is each paragraph readable at its width and leading, with no lone last word?
- Is everything essential visible, and everything else one clear step away?
- Do nested rounded shapes share a centre, and do icons match the weight of their text?
- Do borders, fades and gradients still look right on every background and in dark mode?
- Does the layout fit with the mobile toolbar both shown and hidden?
