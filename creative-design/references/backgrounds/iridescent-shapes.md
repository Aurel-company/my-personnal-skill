# Iridescent shapes

- **Look**: glossy blobs, spheres or ribbons with an oil-slick or holographic color shift across the surface, pastel to vivid rainbow edges.
- **Fits**: futuristic, creative, beauty, web3-free luxury, music, AI-adjacent products that want something tactile instead of a gradient blob.
- **Avoid when**: it is applied unchosen as the default "AI" look; keep one distinct shape language and restrained saturation.

## Make it

CSS conic gradient with hue rotation in OKLCH (the rainbow comes from a longer hue path):

```css
.iri {
  --a: 0deg;
  background:
    conic-gradient(from var(--a) at 40% 40%, in oklch longer hue,
      oklch(0.85 0.12 0), oklch(0.85 0.12 0));
  border-radius: 50%;
  filter: saturate(.9);
}
```

Add depth: a white radial highlight (`radial-gradient(circle at 30% 25%, #fff8, transparent 40%)`), a soft inner shadow, and a blurred copy underneath as a glow. Update `--a` from pointer position or device tilt (register `@property --a { syntax: "<angle>"; inherits: false; initial-value: 0deg }` to animate it).

3D route: Three.js with a `MeshPhysicalMaterial` using `iridescence: 1`, `iridescenceIOR`, and a thin environment map, or a thin-film shader. Export a still for non-WebGL fallback.

## Legibility and cost

CSS version is cheap. Keep shapes behind or beside copy, not under it. 3D needs a lazy load and a static poster image.

## Pairs with

Fluted glass (over the shapes), grainy gradients, dark backgrounds, blurred photos, clean sans-serif type.

## Search keywords

`iridescent gradient CSS conic oklch`, `holographic effect CSS`, `Three.js iridescence material`, `thin film interference shader`
