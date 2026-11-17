# AI tells: resource index

Everything that lists tells lives here and in the catalog, so it can be updated without touching `SKILL.md`.

**To add a tell**: add a row to the matching section of [ai-tells-catalog.md](ai-tells-catalog.md) (tell, why it reads as AI, do instead, severity). If it is among the most noticed ones, add it to the lists below. `SKILL.md` does not change.

| File | What it holds |
|---|---|
| [ai-tells-catalog.md](ai-tells-catalog.md) | Full catalog by category: tell, why it reads as AI, what to do instead, severity. The `Sev` column is the source of truth |
| [sources.md](sources.md) | Research sources, dates, limits |

## Catalog sections

1. Typography
2. Color
3. Layout and structure
4. Components and surfaces
5. Motion
6. Icons and imagery
7. Copy
8. States and behavior
9. Code and metadata
10. Second-order defaults (the trap)
11. Floor (never ship without)

## Highest-signal tells (in the order laypeople notice them)

Keep this list open while building.

- **Gradients and glow**: purple/indigo-to-blue gradients, gradient text, colored glows or shadows, radial halos behind the hero.
- **Type**: unchosen Inter, an all-caps tracked eyebrow above headings, one italic serif accent word, crushed letter spacing.
- **Hero**: centered stack of badge, giant headline, gray subhead, two buttons, then a stat row or logo strip.
- **Cards**: three equal cards with a top icon, colored left or top border stripes, cards nested in cards, everything the same radius, padding and height.
- **Decoration**: glassmorphism everywhere, fake window dots, pulsing status dots, blinking cursors, marquee logos, "New ✨" badges, emoji as icons.
- **Motion**: the same fade-up on every section, bounce easing, count-up stats, motion that responds to nothing.
- **Copy**: buzzwords ("seamless", "robust", "supercharge"), em-dash in every sentence, "Build faster. Ship smarter.", hedging, aphorism cadence, stock openers.
- **Imagery**: plastic AI illustrations, stock team photos, placeholder avatars, shape-assembled illustrations.
- **Hierarchy and grouping**: competing buttons of equal weight, groups split by lines instead of spacing, decorative badges and filter chips, redundant labels, a main feature that is no larger than the rest.
- **Craft details**: mono used as decoration, proportional digits in tables and counters, headlines with orphan words, the same radius on nested shapes, centering by box instead of by eye.
- **Missing reality**: only the happy path designed, no empty, loading or error states, every function visible at once.

## Fix order (audit)

Fix in this order, P0 first. The severity of each individual tell is in the catalog.

- **P0, noticed by anyone**: gradient and glow, centered generic hero, identical card row, buzzword copy, AI imagery, builder badges ("Built with…"), emoji icons.
- **P1, noticed by designers and developers**: unchosen fonts, untouched shadcn tokens, uniform spacing and radius, stock section order, same animation everywhere, missing states, design drift between pages, competing CTAs, decorative badges and chips, redundant labels, groups separated by lines instead of spacing, mono as decoration.
- **P2, craft**: tracking and line-height, optical alignment (align by eye), icon weight consistency, concentric radii (inner = outer − padding), tabular numbers, headline wrapping, meta and alt text, OG image.
