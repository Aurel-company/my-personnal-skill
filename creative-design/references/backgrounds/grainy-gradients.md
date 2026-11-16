# Grainy gradients

- **Look**: soft color gradients with visible film-like noise, which kills banding and adds warmth and depth.
- **Fits**: almost anything modern: hero backgrounds, cards, covers, app icons, music and wellness brands.
- **Avoid when**: used as an unchosen default on every page; it is now a common look, so give it a distinct palette and shape.

## Make it

Gradient plus an inline SVG noise layer.

```css
.grainy {
  background:
    url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='200' height='200'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='3' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)' opacity='0.5'/></svg>"),
    radial-gradient(circle at 20% 20%, oklch(0.75 0.17 40), transparent 60%),
    radial-gradient(circle at 80% 60%, oklch(0.6 0.2 280), transparent 60%),
    oklch(0.25 0.05 270);
  background-blend-mode: overlay, normal, normal, normal;
}
```

The strong version: raise contrast on the combination so grain becomes crisp, speckled color transitions: wrap the gradient and noise in one element and apply `filter: contrast(150%) brightness(105%)`. Interpolate gradients in OKLCH (`in oklch`) so they stay vivid in the middle.

## Legibility and cost

Keep grain opacity moderate. A static tile is cheap; avoid animating the filter. Test on dark and light mode.

## Pairs with

Single-hue landscapes, blurred photos, iridescent shapes, big plain type.

## Search keywords

`grainy gradient CSS`, `noise gradient SVG filter`, `film grain overlay web`, `gradient banding dither`
