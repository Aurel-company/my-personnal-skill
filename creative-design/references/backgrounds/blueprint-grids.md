# Blueprint grids

- **Look**: deep blue field with thin pale lines, a fine grid and a heavier major grid, plus dimension marks, crosshairs and technical annotations.
- **Fits**: developer tools, engineering, architecture, hardware, APIs, "how it works" sections, specs.
- **Avoid when**: the brand is emotional or consumer-soft; the grid becomes visual noise if overdone.

## Make it

Two stacked grids in pure CSS.

```css
.blueprint {
  --line: rgb(255 255 255 / .12);
  --major: rgb(255 255 255 / .28);
  background-color: oklch(0.36 0.12 255);
  background-image:
    linear-gradient(var(--major) 1px, transparent 1px),
    linear-gradient(90deg, var(--major) 1px, transparent 1px),
    linear-gradient(var(--line) 1px, transparent 1px),
    linear-gradient(90deg, var(--line) 1px, transparent 1px);
  background-size: 80px 80px, 80px 80px, 16px 16px, 16px 16px;
}
```

Make it feel real: corner marks and registration crosses, dimension lines with arrowheads and numbers, a title block (name, scale, rev), monospace or drafting-style type, all in the same line color. Annotations should say true things about the product.

## Legibility and cost

Free to render. Keep line alpha low under text; put copy on a slightly darker panel if needed.

## Pairs with

Contour lines, square-dot grids, speckled graphite, monospace type, ASCII.

## Search keywords

`blueprint background CSS grid`, `technical drawing website`, `engineering schematic UI`, `drafting title block design`
