# Library index

Creative ideas to start from. Pick by mood and cost, then open the file.

**Cost**: 1 = pure CSS, trivial. 2 = SVG filter or small canvas. 3 = canvas generation or WebGL, needs a fallback.

## Backgrounds

| Idea | File | Mood | Main technique | Cost |
|------|------|------|----------------|------|
| Felt texture | [felt-texture](backgrounds/felt-texture.md) | handmade, warm, soft | SVG noise + blend | 2 |
| Fluted glass | [fluted-glass](backgrounds/fluted-glass.md) | premium, calm, architectural | stripes + backdrop blur / shader | 2-3 |
| Water ripples | [water-ripples](backgrounds/water-ripples.md) | calm, fluid, playful | SVG displacement / shader | 3 |
| Speckled graphite | [speckled-graphite](backgrounds/speckled-graphite.md) | industrial, minimal, tactile | thresholded noise | 2 |
| Single-hue landscapes | [single-hue-landscapes](backgrounds/single-hue-landscapes.md) | atmospheric, poetic, focused | layered SVG, one hue, stepped lightness | 1-2 |
| Blueprint grids | [blueprint-grids](backgrounds/blueprint-grids.md) | technical, precise, engineering | CSS grid lines | 1 |
| Halftone | [halftone](backgrounds/halftone.md) | print, punchy, retro | dots by tone (canvas / SVG) | 2 |
| Grainy gradients | [grainy-gradients](backgrounds/grainy-gradients.md) | modern, warm, soft | gradient + noise overlay | 2 |
| Grass texture | [grass-texture](backgrounds/grass-texture.md) | natural, eco, sport | procedural blades / photo | 3 |
| Dithered images | [dithered-images](backgrounds/dithered-images.md) | retro-tech, graphic, lo-fi | ordered / error-diffusion dither | 2 |
| Paper texture | [paper-texture](backgrounds/paper-texture.md) | editorial, human, tactile | noise + lighting / scanned tile | 1-2 |
| Contour lines | [contour-lines](backgrounds/contour-lines.md) | cartographic, quiet, scientific | isolines from noise | 2-3 |
| Cloud sky | [cloud-sky](backgrounds/cloud-sky.md) | dreamy, optimistic, open | gradient + fractal noise / photo | 2 |
| Pixel mosaics | [pixel-mosaics](backgrounds/pixel-mosaics.md) | digital, playful, bold | downsampled grid of squares | 2 |
| Lens distortion | [lens-distortion](backgrounds/lens-distortion.md) | cinematic, experimental | barrel / chromatic shader | 3 |
| Stippled gradients | [stippled-gradients](backgrounds/stippled-gradients.md) | illustrative, crafted, ink | random dots by density | 2-3 |
| Square-dot grids | [square-dot-grids](backgrounds/square-dot-grids.md) | systematic, techy, clean | CSS gradients, optional wave | 1-2 |
| Blurred photos | [blurred-photos](backgrounds/blurred-photos.md) | ambient, emotional, soft | heavy blur / tiny upscaled image | 1 |
| Iridescent shapes | [iridescent-shapes](backgrounds/iridescent-shapes.md) | futuristic, luxurious, glossy | conic gradients in OKLCH | 1-3 |
| Impressionist paintings | [impressionist-paintings](backgrounds/impressionist-paintings.md) | cultural, romantic, painterly | public-domain art + crop | 1 |
| ASCII and pixels | [ascii-and-pixels](backgrounds/ascii-and-pixels.md) | hacker, retro, playful | luminance to characters / pixel art | 2 |

## Quick pick by feeling

- **Warm and human**: felt, paper, grainy gradients, impressionist, stippled.
- **Technical and precise**: blueprint grids, square-dot grids, contour lines, ASCII and pixels, speckled graphite.
- **Calm and atmospheric**: cloud sky, single-hue landscapes, blurred photos, water ripples, fluted glass.
- **Bold and graphic**: halftone, dithered images, pixel mosaics, iridescent shapes, lens distortion.

## Good combinations

- Single-hue landscape + grain.
- Halftone + blurred photo (halftone the blur, keep the color).
- Blueprint grid + contour lines.
- Fluted glass over iridescent shapes or a blurred photo.
- Dithered image + square-dot grid in the same two colors.
- Paper texture + stippled gradient for an editorial look.

## Adding an idea

Copy the structure of any file in `backgrounds/` (Look, Fits, Avoid when, Make it, Legibility and cost, Pairs with, Search keywords), then add one row above. New categories (typography, motion, color, layout) get their own folder next to `backgrounds/` and their own table here.
