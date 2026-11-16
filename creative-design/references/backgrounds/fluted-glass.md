# Fluted glass

- **Look**: vertical ribbed glass that refracts what is behind it into soft repeated slices. Blurred color shapes seen through reeded panels.
- **Fits**: premium brands, architecture, hospitality, audio, calm SaaS hero, login screens.
- **Avoid when**: the area holds dense text or data; the refraction fights legibility.

## Make it

Cheap version: ribs as a gradient, blur behind.

```css
.fluted {
  background: repeating-linear-gradient(90deg,
    rgb(255 255 255 / .22) 0 2px, rgb(255 255 255 / .02) 2px 14px);
  backdrop-filter: blur(8px) saturate(1.2);
}
```

Better version: slice the scene. Draw the same colorful shapes in N vertical strips (N ≈ 20-40), each strip shifted and slightly scaled horizontally by an amount that grows toward its edge, so each rib shows a compressed, mirrored piece. In WebGL: `uv.x = floor(uv.x*N)/N + fract(uv.x*N) * 0.5 + 0.25*(something)`; or use an SVG `feDisplacementMap` with a stripe-gradient map.

## Legibility and cost

Put text on an un-fluted plain area, or on a solid panel above. `backdrop-filter` is costly on large areas and animated content: limit its size, avoid stacking several.

## Pairs with

Iridescent shapes or blurred photo behind it, single-hue gradients, thin sans-serif type, generous space.

## Search keywords

`fluted glass CSS`, `reeded glass effect shader`, `glass ribbed refraction WebGL`, `frosted glass hero`
