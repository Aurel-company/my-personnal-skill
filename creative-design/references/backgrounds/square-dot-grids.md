# Square-dot grids

- **Look**: a regular lattice of small squares (or pixels) as a calm texture, optionally with size or opacity rippling across it.
- **Fits**: product and dev tools, dashboards, docs, tech landing pages, retro-digital aesthetics.
- **Avoid when**: it is the only idea and nothing else is specific to the product; it is a very common technical default.

## Make it

Static squares in pure CSS (a 3px square in each 12px cell):

```css
.sq {
  --cell: 12px; --dot: 3px;
  background-color: var(--ink);
  background-image:
    linear-gradient(to right, var(--bg) calc(var(--cell) - var(--dot)), transparent 0),
    linear-gradient(to bottom, var(--bg) calc(var(--cell) - var(--dot)), transparent 0);
  background-size: var(--cell) var(--cell);
}
```

Fade it out toward an edge with `mask-image: radial-gradient(circle at 50% 0, #000, transparent 70%)`.

Animated wave: canvas or WebGL. For each cell, `size = base * (0.5 + 0.5 * sin(distance * freq - time))`, with `distance` from the pointer or a corner. Drive with `requestAnimationFrame`, pause off-screen.

## Legibility and cost

CSS version is free. Keep dots low contrast (ink at 8-15% of the background) behind copy. Canvas wave: cap to a modest cell count and stop under reduced motion.

## Pairs with

Dithered images (same two colors), pixel mosaics, blueprint grids, monospace type, a single accent.

## Search keywords

`dot grid background CSS`, `pixel grid wave canvas`, `square dot pattern mask`, `interactive dot grid hero`
