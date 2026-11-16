# Water ripples

- **Look**: concentric rings spreading on a surface, bending the image underneath. Caustic light patterns on a pool floor.
- **Fits**: wellness, travel, water or drink brands, interactive heroes, playful loaders, "touch" feedback.
- **Avoid when**: users are motion-sensitive and there is no static fallback; content is text-heavy.

## Make it

Static: SVG turbulence that warps an image.

```html
<filter id="water">
  <feTurbulence type="turbulence" baseFrequency="0.01 0.04" numOctaves="2" result="t"/>
  <feDisplacementMap in="SourceGraphic" in2="t" scale="24"/>
</filter>
```

Animate by changing `baseFrequency` slowly (SMIL `<animate>` or JS), keep it under about 0.02 change per second.

Interactive: WebGL ripple. On pointer move, add a drop to a height-field texture (two ping-pong buffers, simple wave equation: next = (avg of 4 neighbours) * 2 - previous, times damping 0.98); then offset the image UV by the height gradient. Libraries: `ripples` style jQuery plugins, OGL, Three.js, or a 60-line raw shader.

Caustics (no interaction): animated layered voronoi/noise in a fragment shader, thresholded and tinted aqua.

## Legibility and cost

Lower distortion strength under text. Provide a still image when `prefers-reduced-motion` is set. Cap canvas resolution on mobile.

## Pairs with

Blurred photos, single-hue (blue/teal) palettes, lens distortion, fluted glass.

## Search keywords

`water ripple effect WebGL`, `feDisplacementMap water`, `caustics shader`, `pointer ripple canvas`
