# Color, surfaces and depth

## OKLCH palettes
- **Rule**: define color in **OKLCH** (`oklch(L C H)`), a perceptually uniform space: equal lightness steps look equal, and changing hue does not change perceived brightness the way it does in HSL.
- **Apply**:
  - Build scales by **stepping L** with C and H nearly constant, then lower C at the extremes (very light and very dark colors cannot hold high chroma).
  - Keep accessible contrast by controlling **L**: pair tokens with a known L gap, then still verify with a real contrast checker (APCA or WCAG).
  - Make a semantic palette (success, warning, danger, info) with the **same L and C** and different H, so they have equal visual weight.
  - Derive hover, active, disabled and dark mode by shifting L, not by guessing hex.
  - Tint neutrals with the brand hue at tiny chroma (C ≈ 0.005–0.02) so grays belong to the palette.
  - Provide a fallback when needed: `color: #3b82f6; color: oklch(62% 0.19 255);` and use `color-mix(in oklch, …)` for blends.
- **Failure**: HSL palettes where yellow looks bright and blue looks dark at the same "lightness"; a generated scale that looks accessible but was never contrast-checked; out-of-gamut colors that get clipped and flatten.

## OKLCH gradients
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

## Alpha borders
- **Rule**: draw borders, dividers and outlines with a **semi-transparent** color (black or white at low alpha) instead of an opaque gray, so they adapt to whatever is under them: tinted cards, hover states, light and dark mode.
- **Apply**:
  - Light: `border: 1px solid oklch(0 0 0 / 0.08)`. Dark: `oklch(1 0 0 / 0.1)`. Tokens: `--border-subtle` 6-8%, `--border` 10-14%, `--border-strong` ~20%.
  - There is no `border-opacity` property, and `opacity` would fade the whole element: put the alpha in the color.
  - A background paints under the border by default, which makes a translucent border look solid. Use `background-clip: padding-box` when you need the true alpha (translucent or glass surfaces).
  - Images: add a hairline inset outline so their edge does not melt into a similar background: `outline: 1px solid oklch(0 0 0 / 0.1); outline-offset: -1px;`.
  - Adjacent translucent borders stack and look doubled: use one divider or a `gap` instead of two borders.
- **Failure**: opaque `#ddd` borders that look heavy on a tinted card and glow in dark mode; double-thick lines where translucent borders overlap.

## Masked edges
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

## Dark mode depth
- **Rule**: in dark mode shadows barely show against a dark surface, so **elevation is expressed by lightness**: the closer a surface is to the user, the lighter it is. Keep real shadows only as a supplement for floating layers (popovers, modals).
- **Apply**:
  - Define surface tokens by elevation, one step of about **4-6% lightness** (OKLCH: ΔL ≈ 0.03-0.05): `--bg: oklch(0.16 0.01 260)`, `--surface-1: oklch(0.20 0.01 260)`, `--surface-2: oklch(0.24 0.01 260)`, `--surface-3: oklch(0.28 0.01 260)`. Keep the same elevation order as light mode (modal is highest).
  - Avoid pure `#000` backgrounds and pure `#fff` text (use text around L 0.92-0.95): harsh contrast and halation.
  - Separate layers with alpha borders (white 8-12%) and, optionally, a 1px top highlight: `box-shadow: inset 0 1px 0 oklch(1 0 0 / 0.06)`.
  - Lower chroma on large colored areas and raise lightness on accent text so it keeps its contrast.
  - Do not invert the light palette: re-derive dark tokens. Do not fake elevation with light glows.
- **Failure**: the light-mode box-shadow reused unchanged so every card looks flat; all surfaces the same black; a neon-saturated palette copied from light mode.
