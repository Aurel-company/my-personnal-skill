# Dithered images

- **Look**: photos reduced to a few colors (often 1-bit) where tones are rendered by dot patterns, like early Mac, newspaper or e-ink.
- **Fits**: retro-tech, indie, music, games, developer brands, art direction that wants a graphic, lo-fi photographic voice.
- **Avoid when**: product photography must be faithful (e-commerce) or the audience reads it as low quality.

## Make it

Pre-process offline when possible.

```bash
# ImageMagick: 1-bit ordered dither (Bayer 8x8)
magick in.jpg -colorspace Gray -ordered-dither o8x8 out.png
# Two-color brand palette: map to your colors after dithering
```

In the browser (canvas): read pixels, convert to luminance, then either
- **Ordered (Bayer)**: compare luminance to a threshold matrix value per pixel. Crisp, regular, fast.
- **Floyd-Steinberg / Atkinson**: push the error to neighbours. Organic, grainy, slower (fine for one-time render). Atkinson gives the classic soft Mac look.

Display with `image-rendering: pixelated` and scale by whole numbers (2x, 3x) so dots stay crisp. Map black and white to two brand colors for identity.

## Legibility and cost

A dithered image is high-frequency: do not put text over the busy area; use it as a framed image or a masked section. Keep file small by exporting as indexed PNG or SVG.

## Pairs with

Square-dot grids in the same two colors, ASCII and pixels, halftone, monospace type.

## Search keywords

`dithering JavaScript Bayer`, `Atkinson dither canvas`, `1-bit image effect web`, `ordered dither shader`
