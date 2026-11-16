# Paper texture

- **Look**: subtle fibers and grain, slight unevenness, maybe a soft fold, deckled edge or a bit of translucency. The page feels printed.
- **Fits**: editorial, journals, stationery, books, craft, legal-with-warmth, heritage brands.
- **Avoid when**: it reads as a skeuomorphic gimmick on a data-heavy product.

## Make it

Lighting filter for emboss: noise becomes bumps lit from a corner.

```html
<filter id="paper">
  <feTurbulence type="fractalNoise" baseFrequency="0.04" numOctaves="5" result="noise"/>
  <feDiffuseLighting in="noise" lighting-color="#fff" surfaceScale="1.2">
    <feDistantLight azimuth="45" elevation="60"/>
  </feDiffuseLighting>
</filter>
```

```css
.paper { background: #f4efe6; position: relative; }
.paper::before { content: ""; position: absolute; inset: 0; filter: url(#paper);
  mix-blend-mode: multiply; opacity: .35; pointer-events: none; }
```

Scanned route: use a seamless CC0 paper tile (Poly Haven, Openverse; check license) with `mix-blend-mode: multiply` at 10-25% opacity over your color. For a torn edge, mask with an irregular SVG path.

## Legibility and cost

Keep contrast of the texture very low. Lighting filters are costly over large areas: use a tile for full-page backgrounds.

## Pairs with

Serif type, stippled gradients, ink-only palettes, felt (as a contrast of materials), subtle shadows.

## Search keywords

`paper texture CSS SVG`, `feDiffuseLighting paper`, `seamless paper texture CC0`, `torn paper edge CSS mask`
