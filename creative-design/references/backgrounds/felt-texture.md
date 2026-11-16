# Felt texture

- **Look**: soft matte wool surface, tiny fibers, slightly uneven density. Flat saturated color that feels touchable.
- **Fits**: handmade goods, kids, craft, food, wellness, anything that should feel warm and human.
- **Avoid when**: the product must feel precise, cold or high-tech (fintech dashboards, dev tools).

## Make it

SVG noise multiplied over a flat color, plus a few fiber strokes.

```html
<svg width="0" height="0"><filter id="felt">
  <feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="3" seed="4" result="n"/>
  <feColorMatrix in="n" type="saturate" values="0"/>
  <feComponentTransfer><feFuncA type="linear" slope="0.35"/></feComponentTransfer>
</filter></svg>
```

```css
.felt { background: oklch(0.62 0.14 30); position: relative; }
.felt::after { content: ""; position: absolute; inset: 0; filter: url(#felt);
  mix-blend-mode: multiply; pointer-events: none; }
```

For fibers: canvas, draw 2,000+ short curved 1px strokes in slightly lighter and darker tints of the base, random angle, 4-12px long, low alpha. Render once, reuse as a background image.

## Legibility and cost

Keep noise amplitude low (alpha 0.2-0.4) so text stays readable. Filter is repainted on resize: render to a PNG tile for large surfaces. Static, no animation needed.

## Pairs with

Paper texture (as a card on felt), stitched borders, rounded chunky type, single saturated hue.

## Search keywords

`felt texture CSS`, `wool fiber canvas`, `feTurbulence fabric`, `handmade website design`
