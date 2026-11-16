# Stippled gradients

- **Look**: a gradient built from many tiny dots of the same size, dense where dark and sparse where light, placed irregularly like pen-and-ink stippling.
- **Fits**: illustration-led brands, editorial, science, books, crafted and analog feelings.
- **Avoid when**: you want the regular, mechanical look of halftone: that is a different idea.

Difference from halftone: halftone uses a regular grid and varies dot **size**; stipple uses random positions and varies dot **density**.

## Make it

Canvas, seeded random points accepted by density.

```js
const rnd = mulberry32(42);                 // seeded RNG
for (let i = 0; i < 40000; i++) {
  const x = rnd() * w, y = rnd() * h;
  const density = 1 - y / h;               // dark at top, sparse at bottom
  if (rnd() < density ** 1.5) { ctx.beginPath(); ctx.arc(x, y, 0.8, 0, 6.283); ctx.fill(); }
}
```

For shapes, use the shape's lightness or distance field as `density`. For nicer spacing, use Poisson-disk or weighted Voronoi relaxation instead of pure random. Export to SVG for crisp scaling.

## Legibility and cost

Thousands of SVG circles are heavy: draw once to canvas and export an image. Keep dot contrast low behind text. Seeded RNG keeps server and client output identical.

## Pairs with

Paper texture, single-ink palettes, serif type, contour lines, speckled graphite.

## Search keywords

`stippling algorithm canvas`, `Poisson disk sampling JavaScript`, `weighted voronoi stippling`, `stipple gradient SVG`
