# Halftone

- **Look**: an image or gradient made of a regular grid of dots whose size encodes tone, like newspaper or screen print. Often one or two ink colors.
- **Fits**: editorial, music, culture, retro, posters, bold campaigns, anything with a printed feel.
- **Avoid when**: you need smooth photographic realism or the dots hurt text readability.

## Make it

Constant dots in CSS:

```css
.dots {
  background: radial-gradient(circle, var(--ink) 30%, transparent 31%) 0 0 / 10px 10px;
}
```

Varying dot size (the real halftone): canvas.

1. Draw the source image small on a hidden canvas and read its pixels.
2. For each cell of a grid (rotate the grid 15-45° for a print look), compute luminance.
3. Draw a circle with `radius = cellSize * 0.5 * sqrt(1 - luminance)` for dark-on-light.
4. For color, repeat per CMYK-like channel with different grid angles (0°, 15°, 45°, 75°) and `globalCompositeOperation = "multiply"`.

SVG alternative for gradients: a `<pattern>` of circles masked by a linear gradient.

## Legibility and cost

Dots at low contrast behind copy, or keep text outside the dotted area. Generate once, export as image/SVG for production.

## Pairs with

Blurred photos (halftone the blur), bold flat color, grain, mono-ink palettes, oversized type.

## Search keywords

`halftone effect canvas`, `CSS halftone gradient`, `CMYK halftone JavaScript`, `risograph halftone web`
