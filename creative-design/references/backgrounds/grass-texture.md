# Grass texture

- **Look**: dense blades of grass seen from above or close up, with variation in height, angle and green, optionally swaying.
- **Fits**: outdoor, eco, gardening, sport, pets, family, sustainability, spring campaigns.
- **Avoid when**: the surface must stay quiet and neutral; many animated blades are heavy.

## Make it

Procedural, on canvas (preferred over thousands of DOM nodes).

1. Seeded RNG so the pattern is identical on every load.
2. For each blade: base x, height 20-80px, lean angle ±15°, draw a tapered quadratic curve, color from 3-4 greens with small random lightness shifts (OKLCH: H 125-145, L 0.45-0.7).
3. Draw back to front, darker blades first.
4. Optional wind: re-draw at low frame rate with a shared sine offset per x, or animate a few overlay strips with `transform: skewX()` and staggered delays.

Photo route: a macro grass photo, desaturated and tinted, blurred at the edges; or a seamless texture from a CC0 source (check license).

## Legibility and cost

Render once to an image for static use. Keep animation to a few layers and stop it under `prefers-reduced-motion`. Place text on a calm solid or blurred zone.

## Pairs with

Single-hue landscapes, cloud sky, paper cards, hand-drawn type.

## Search keywords

`procedural grass canvas`, `grass blades SVG pattern`, `animated grass CSS`, `seamless grass texture CC0`
