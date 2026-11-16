# ASCII and pixels

- **Look**: images, video or shapes drawn with text characters (` .:-=+*#%@`) or with chunky visible pixels in a tight palette.
- **Fits**: developer tools, terminals, games, hacker culture, retro-tech, creative coding, playful technical brands.
- **Avoid when**: the audience needs accessibility-first plain content, or the brand is soft and lifestyle.

## Make it

ASCII from an image (canvas): sample brightness per cell and map to a character ramp.

```js
const ramp = " .:-=+*#%@";                 // light to dark (invert for dark mode)
// per cell: lum = 0.2126*r + 0.7152*g + 0.0722*b  (0..255)
// char = ramp[Math.floor(lum / 256 * ramp.length)]
```

Render in a `<pre>` or on canvas with a **monospace** font, fixed `line-height` near 0.6-0.8 (to compensate for tall cells), and `letter-spacing` tuned so cells are roughly square. Animate by recomputing from video frames or from noise. Color it with a single ink plus one accent.

Pixels: draw at low resolution, then upscale with `image-rendering: pixelated` by whole-number factors; limit to 4-16 colors from the brand palette; keep outlines 1px at native size.

## Legibility and cost

Mark decorative ASCII as `aria-hidden="true"` and keep real copy as real text. Re-rendering large character grids every frame is expensive: use canvas, lower the grid size, or render once.

## Pairs with

Dithered images, square-dot grids, pixel mosaics, blueprint grids, monospace and bitmap-style type.

## Search keywords

`image to ASCII canvas JavaScript`, `ASCII video effect web`, `pixel art CSS image-rendering`, `character ramp luminance`
