# Geometry, icons and touch

## Optical centre
- **Rule**: mathematical centre is not perceived centre. Shapes with visual weight or asymmetry look off when centred by the box.
- **Apply**:
  - Play/forward triangles: shift **right** by roughly 6–10% of their width.
  - Icons inside circles or buttons: nudge the heavier side inward until it feels centred; judge with the eye, then store the offset in the icon token.
  - Text in buttons: align on the **x-height / cap-height centre**, not the line box. A slightly smaller top padding than bottom (e.g. 10px / 12px) often looks centred; `text-box-trim: trim-both` with `text-box-edge: cap alphabetic` does it properly where supported.
  - Content placed in a hero or modal: sit it slightly **above** geometric centre (about 45% from the top, not 50%).
- **Failure**: a play icon that looks pushed left; text that sits low in its button.

## Concentric radius
- **Rule**: when a rounded element sits inside another rounded element, their corners must share the same centre: **outer radius = inner radius + the distance between the two edges** (the padding, plus the border width if the parent has a border). Example: inner 8px + padding 12px → outer 20px.
- **Apply**: derive the inner radius, never type it twice.
  ```css
  .card { --r-outer: 20px; --pad: 12px;
          border-radius: var(--r-outer); padding: var(--pad); }
  .card > .inner { border-radius: max(0px, calc(var(--r-outer) - var(--pad))); }
  ```
  With a parent border: subtract `padding + border-width`. Use it for image in card, button in container, input groups, segmented controls, nested menus; chain it for three levels. The formula is not needed when a radius is 0 or fully round (pill, circle). If padding is larger than the outer radius, the inner radius clamps to 0 (square), which is correct. Sheets and cards near a device edge should follow the same logic against the screen corner.
- **Failure**: the same radius token on parent and child: the gap looks thick in the corners and thin on the sides, the inner shape looks pinched.

## Matched icon weight
- **Rule**: an icon's stroke must carry the **same visual weight as the text beside it**. Thin icons next to semibold text look faint; heavy icons next to light text look clunky. Font weight and stroke width are different systems: judge the apparent emphasis in the real component, not the numbers alone.
- **Apply**:
  - Starting points (verify against your font): **1.5px stroke beside regular text, 2px beside semibold**. At 16px a regular sans has stems of about 1.5px.
  - Use SVG icons with a controllable `stroke-width` (Lucide, Phosphor weights) or a variable icon font with a weight axis (Material Symbols). Classic icon fonts have one weight.
  - One stroke width for the whole set; never mix outline and solid icons in one row.
  - Scaling an SVG with `width/height` scales its stroke too (a 24px icon shown at 16px gets 1.33px). Set `stroke-width` per size, or use `vector-effect: non-scaling-stroke` / Lucide's `absoluteStrokeWidth`.
  - Size the icon to the text line (16px icon with 14px text, 20px with 16px) and centre it on the text's x-height / cap-height, not the line box (see optical centre).
  - Check at the real size on 1x and 2x screens, never zoomed in.
- **Failure**: 2px chunky icons beside a light 400 caption; icons that thin out when scaled down; a set that mixes strokes.

## Touch target
- **Rule**: interactive targets are at least **44×44 px** (Apple HIG) or **48×48 dp** (Material); WCAG 2.2 AA minimum is 24×24 CSS px with spacing. Pick 44px as the default.
- **Apply**: the *visible* element may be smaller; extend the **hit area** with padding, a transparent `::before { inset: -8px }`, or `min-width/min-height: 44px`. Leave at least 8px between adjacent targets. Make the whole row tappable in lists, not only the label. Never let two hit areas overlap.
- **Failure**: 16px icon buttons packed together; a checkbox you can only hit on the box itself.

## Safe area
- **Rule**: content and controls must not sit under notches, rounded corners, the home indicator, or browser chrome.
- **Apply**: `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">`, then pad with `env(safe-area-inset-top|right|bottom|left)`. Combine with your own spacing: `padding-bottom: max(16px, env(safe-area-inset-bottom))`. Fixed bottom bars, tab bars, sheets and sticky CTAs always need it. Backgrounds may extend edge to edge; interactive content stays inside. Use `dvh`, not `vh`, for full-height layouts on mobile.
- **Failure**: a bottom button under the home indicator; landscape content clipped by the notch.

## Dynamic viewport
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
