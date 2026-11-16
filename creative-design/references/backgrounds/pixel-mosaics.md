# Pixel mosaics

- **Look**: an image rebuilt from a coarse grid of colored squares, sometimes with small gaps, sometimes revealing detail on hover.
- **Fits**: digital culture, games, creative tools, privacy-themed or "anonymized" moments, bold covers, data portraits.
- **Avoid when**: faces or recognizable people are used without consent; the mosaic reads as a censoring effect.

## Make it

Canvas downsample then redraw as squares.

```js
const cell = 16;
ctx.imageSmoothingEnabled = false;
small.getContext("2d").drawImage(img, 0, 0, w / cell, h / cell); // tiny copy
const px = small.getContext("2d").getImageData(0, 0, w / cell, h / cell).data;
// for each pixel: fillStyle = rgb; fillRect(x*cell+gap, y*cell+gap, cell-gap*2, cell-gap*2)
```

Variations: restrict to a palette or to one hue with varying lightness; let squares animate (scale or color swap) in waves; reduce the cell size on hover so the image resolves around the pointer; use CSS grid with `background-color` per cell for small mosaics. Use `image-rendering: pixelated` for plain upscales.

## Legibility and cost

Mosaics are noisy: keep copy on a separate solid area. Render once to canvas, redraw only on resize.

## Pairs with

Dithered images, square-dot grids, ASCII and pixels, blurred photos (mosaic of a blur is smoother).

## Search keywords

`pixelate image canvas`, `mosaic effect JavaScript`, `pixel grid hover reveal`, `CSS grid pixel art`
