# Lens distortion

- **Look**: barrel or fisheye bulge, wavy glass, stretched edges, optional red/blue color fringes (chromatic aberration), like a cheap or experimental lens.
- **Fits**: cinematic, music, fashion, experimental portfolios, photography, "optical" product stories.
- **Avoid when**: content must stay straight and readable; strong distortion can also cause discomfort.

## Make it

WebGL fragment shader, barrel distortion plus chromatic split.

```glsl
vec2 c = uv - 0.5;
float r2 = dot(c, c);
vec2 d = c * (1.0 + k * r2);              // k ≈ 0.2..0.6 for barrel
float ca = 0.004 * r2;                    // chromatic offset
vec3 col = vec3(
  texture2D(tex, 0.5 + d * (1.0 + ca)).r,
  texture2D(tex, 0.5 + d).g,
  texture2D(tex, 0.5 + d * (1.0 - ca)).b);
```

Animate `k` or a bulge center with the pointer, eased and low amplitude. CSS-only approximation: an `<svg>` `feDisplacementMap` with a radial gradient as the map, or simple `transform: perspective() scale()` on a rounded "lens" element over a photo.

## Legibility and cost

Apply to photos or video only, not to text. Keep distortion below roughly 0.3 at screen edges. Offer a static image under reduced motion. Limit canvas size on mobile.

## Pairs with

Water ripples, blurred photos, grain, halftone, dark cinematic palettes.

## Search keywords

`barrel distortion shader`, `chromatic aberration WebGL`, `fisheye effect canvas`, `lens bulge hover effect`
