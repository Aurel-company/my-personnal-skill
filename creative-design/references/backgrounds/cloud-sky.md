# Cloud sky

- **Look**: soft gradient sky with billowy clouds, dawn, midday or dusk palettes. Open, light, a bit dreamy.
- **Fits**: weather, travel, meditation, cloud and infrastructure brands, creative tools, optimistic launches.
- **Avoid when**: clouds are clip-art and cliche; push with an unusual palette or crop.

## Make it

CSS gradient sky plus fractal-noise clouds.

```html
<filter id="cloud">
  <feTurbulence type="fractalNoise" baseFrequency="0.006 0.012" numOctaves="4" seed="2"/>
  <feColorMatrix type="matrix"
    values="0 0 0 0 1  0 0 0 0 1  0 0 0 0 1  0 0 0 1.6 -0.55"/>
  <feGaussianBlur stdDeviation="2"/>
</filter>
```

Place the filtered element over a gradient (`linear-gradient(oklch(0.7 0.12 240), oklch(0.93 0.04 70))`). Stack 2-3 layers with different `baseFrequency` and offsets; slow horizontal drift with `transform: translateX()` over 60-120s.

Photo route: a real sky photo (check license), color-graded toward one hue. Sunset palettes: peach to magenta to deep blue; keep chroma controlled.

## Legibility and cost

Place text on the calmest part of the gradient. SVG filter on a large area is costly: render a PNG for production. Respect reduced motion.

## Pairs with

Single-hue landscapes, grainy gradients, grass texture, iridescent shapes (as sky objects).

## Search keywords

`CSS clouds feTurbulence`, `procedural clouds shader`, `sky gradient palette sunset`, `cloud background hero`
