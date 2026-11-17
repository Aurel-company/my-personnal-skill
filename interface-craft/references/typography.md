# Typography

## Line length (measure)
- **Rule**: body text lives between **45 and 75 characters per line** (66 is the classic target). Below 40 it chops; above 80 the eye loses the next line.
- **Apply**: cap with `max-width: 65ch` on the text container, not on the page. Set it in `ch`, never in px, so it follows the font.
- **Failure**: full-width paragraphs on a wide monitor; 25-character columns on mobile with huge type.

## Leading (line height)
- **Rule**: leading is inversely related to size and directly related to line length. Body: **1.5–1.65**. Headings: **1.05–1.25**. Long measure or small x-height needs more leading.
- **Apply**: unitless values (`line-height: 1.6`), never `px`, so nested sizes inherit correctly. Re-tune per size: a display heading at body leading looks broken. Multi-line buttons, labels and badges: 1.2–1.3.
- **Failure**: one global `line-height` for everything; headings that float apart.

## Tracking (letter-spacing)
- **Rule**: tracking is uniform spacing across a run of text. **Large type: tighten** (−0.01 to −0.03em). **Small text and ALL CAPS: loosen** (+0.04 to +0.12em). Never track lowercase body text.
- **Apply**: use `em` so it scales with size. Define it per type-scale step as a token, not ad hoc per component.
- **Failure**: crushed display type with touching letters; all-caps labels with default tracking.

## Kerning
- **Rule**: kerning is the adjustment of space between **specific letter pairs** (AV, To, 7.). It is a font feature, not a style you set manually.
- **Apply**: keep it on: `font-kerning: auto` (default) and `text-rendering: optimizeLegibility` on headings and logos. Check display sizes and wordmarks by eye for bad pairs; fix individual pairs in the logo asset, not with global tracking. Some browsers disable kerning or ligatures when `letter-spacing` is non-zero: verify after tracking changes.
- **Failure**: confusing kerning with tracking; hand-spacing a title that the font already kerns well.

## x-height
- **Rule**: x-height is the height of lowercase letters relative to capitals. A larger x-height reads bigger and clearer at the same `font-size`, and needs less size and less leading; a small x-height needs more of both.
- **Apply**: when pairing two typefaces, **match x-height, not font-size** (use `font-size-adjust: from-font` or an explicit value). Prefer large-x-height faces for dense UI and small text. Check fallback fonts: a fallback with a different x-height causes visible reflow when the web font loads.
- **Failure**: two fonts at "16px" where one looks 2px smaller; a fallback stack that jumps on load.

## Widows and orphans
- **Rule**: never end a paragraph or heading with a **single short word alone on the last line**.
- **Apply**: `text-wrap: balance` on headings, short blurbs and captions; `text-wrap: pretty` on body paragraphs. When the browser cannot help, bind the last two words with a non-breaking space (`&nbsp;`) in static copy.
- **Failure**: a heading that wraps to one orphan word; a card description ending in "of."

## Tabular numbers
- **Rule**: wherever digits change or align vertically (tables, prices, timers, counters, stats, dashboards, version numbers), use **tabular figures** so every digit has the same width.
- **Apply**: `font-variant-numeric: tabular-nums;` (add `slashed-zero` for codes and IDs, `lining-nums` for tables). Right-align numeric columns. Leave proportional figures in running prose.
- **Failure**: a live counter that jitters as digits change; a column of amounts that does not line up on the decimal.
