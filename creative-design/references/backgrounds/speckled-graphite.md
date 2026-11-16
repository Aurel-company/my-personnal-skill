# Speckled graphite

- **Look**: dark or mid-grey surface with fine light and dark flecks, like granite, terrazzo, a pencil-grey stone or a sprinkled ceramic glaze.
- **Fits**: industrial design, hardware, tools, architecture, minimal portfolios, "material" product pages.
- **Avoid when**: the brand is soft, colorful or playful.

## Make it

Threshold high-frequency noise into discrete speckles.

```html
<filter id="speckle">
  <feTurbulence type="fractalNoise" baseFrequency="0.6" numOctaves="2" seed="9"/>
  <feColorMatrix type="matrix"
    values="0 0 0 0 1  0 0 0 0 1  0 0 0 0 1  0 0 0 -9 5.2"/>
</filter>
```

The alpha row (`-9 5.2`) acts as a threshold: increase the second number for more flecks, lower it for fewer. Layer two filters (white flecks, black flecks) at different `baseFrequency` for depth. Put them over `background: oklch(0.32 0.01 260)`.

Alternative: pre-render a 512px seamless tile and use it as `background-image`. Cheaper and identical every load.

## Legibility and cost

Fleck contrast must stay low (alpha under 0.35) under body text. Prefer a tile on mobile.

## Pairs with

Blueprint or contour lines in white, monospace type, single accent color, paper texture cards.

## Search keywords

`granite texture CSS`, `terrazzo SVG`, `speckle noise threshold`, `feColorMatrix threshold`
