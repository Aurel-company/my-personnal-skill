# Blurred photos

- **Look**: a photo blurred until it becomes a field of soft color and light, giving mood without detail.
- **Fits**: music players, media, cards that adapt to their content, wellness, onboarding, hero backgrounds with a human feel.
- **Avoid when**: the image is generic stock; blur hides low quality but also hides meaning.

## Make it

The cheap trick: a tiny image scaled up is already blurred and costs almost nothing.

```css
.ambient {
  background: url("thumb-24px.jpg") center / cover;   /* 24-48px wide source */
  image-rendering: auto;
}
```

Or with a filter (hide the soft edges by oversizing):

```css
.ambient { position: relative; overflow: hidden; }
.ambient img { position: absolute; inset: -10%; width: 120%; height: 120%;
  object-fit: cover; filter: blur(60px) saturate(1.3); }
```

Make it content-aware: extract 2-3 dominant colors from the image (canvas or a palette library) and build a mesh of radial gradients instead of shipping the photo. Add a 20-40% dark or light overlay for text.

## Legibility and cost

Verify contrast on the lightest part of the blur. Large `filter: blur` is GPU-costly and bad when animated; prefer the tiny-image trick. Mind privacy: do not use identifiable user photos without consent.

## Pairs with

Halftone, grain, fluted glass over it, iridescent shapes, lens distortion.

## Search keywords

`blurred image background CSS`, `ambient color from image`, `dominant color extraction canvas`, `gradient mesh from photo`
