# Contour lines

- **Look**: thin concentric isolines like a topographic map, flowing and organic, usually one color on a plain field.
- **Fits**: outdoor, maps, science, data, wellness, mountain and travel brands, calm technical heroes.
- **Avoid when**: lines would cross important content with no way to dim them.

## Make it

Generate from a noise field with marching squares.

1. Build a 2D scalar field: simplex/Perlin noise sampled on a grid (e.g. 120x80).
2. Extract isolines at evenly spaced levels (every 0.05). In JS: `d3-contour` returns SVG paths directly.
3. Draw with `stroke-width: 1`, `fill: none`, opacity 0.2-0.5. Make every 5th line heavier (an index contour) like a real map.

Shader route (no library): `float v = noise(uv*3.0 + t); float line = smoothstep(0.02, 0.0, abs(fract(v*20.0) - 0.5) - 0.48);` Animate `t` very slowly for a living terrain.

Static fallback: export the SVG once. Use a seeded noise so the pattern is stable.

## Legibility and cost

Static SVG is light. Animated shader should be paused when off-screen and under reduced motion.

## Pairs with

Blueprint grids, single-hue landscapes, speckled graphite, monospace labels with coordinates and elevations.

## Search keywords

`topographic contour lines SVG generator`, `d3-contour noise`, `marching squares tutorial`, `contour lines shader`
