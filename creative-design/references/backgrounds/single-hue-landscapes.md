# Single-hue landscapes

- **Look**: layered hills, dunes, mountains or waves drawn in one hue, separated only by lightness. Far layers pale and hazy, near layers dark and saturated.
- **Fits**: brands that need atmosphere with discipline, onboarding, empty states, hero sections, covers.
- **Avoid when**: you need many distinct category colors on the same screen.

## Make it

Layered SVG paths, colors from OKLCH with fixed H and C, stepped L.

```css
:root { --h: 255; }
.l1 { fill: oklch(0.88 0.04 var(--h)); }  /* far */
.l2 { fill: oklch(0.74 0.08 var(--h)); }
.l3 { fill: oklch(0.58 0.12 var(--h)); }
.l4 { fill: oklch(0.38 0.10 var(--h)); }  /* near */
```

Generate each ridge with a sum of sine waves or 1D noise at a different frequency per layer; far layers smoother and flatter. Add a vertical gradient (light at the horizon) for atmospheric perspective. Optional: a sun or moon disc in the lightest tone, and grain on top.

## Legibility and cost

Pure vector, tiny, scales perfectly. Put text in the sky region (the lightest, flattest area) with dark ink of the same hue.

## Pairs with

Grainy gradients, cloud sky, contour lines, parallax on scroll (move layers at different speeds, respect reduced motion).

## Search keywords

`layered mountains SVG monochrome`, `atmospheric perspective illustration`, `monochrome landscape vector`, `layered waves SVG generator`
