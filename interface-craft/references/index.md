# Interface craft: concept index

Each concept has: **what it is**, **the rule**, **how to apply it**, **the common failure**. The detail lives in the category file; this index only routes and ranks.

**To add a concept**: add a `## <Concept>` block (Rule / Apply / Failure) to the matching category file, then add one row here. `SKILL.md` does not change.

Severity is the review order used by the workflow. The condition after the letter says when a concept rises to that level. `—` means the concept had no severity assigned: treat it as P2.

- **P0** breaks use
- **P1** felt by everyone
- **P2** felt by designers

## Typography: [typography.md](typography.md)

| Concept | Use when | Severity |
|---|---|---|
| Line length (measure) | any block of body text | P1 when > 80ch |
| Leading (line height) | any text, per size | — |
| Tracking (letter-spacing) | display type, small text, ALL CAPS | — |
| Kerning | display type, wordmarks | P2 |
| x-height | pairing fonts, fallback stacks | P2 |
| Widows and orphans | headings, captions, paragraphs | P1 |
| Tabular numbers | tables, prices, timers, counters | P1 when digits jitter |

## Geometry, icons and touch: [geometry-icons-touch.md](geometry-icons-touch.md)

| Concept | Use when | Severity |
|---|---|---|
| Optical centre | play icons, icons in buttons, text in buttons, hero content | P2 |
| Concentric radius | rounded element inside a rounded element | P2 |
| Matched icon weight | icons beside text | P2 |
| Touch target | any tappable element | P0 when < 24px |
| Safe area | fixed bars, sheets, sticky CTAs | P0 when content sits under the notch or home indicator |
| Dynamic viewport | full-height layouts on mobile | P0 when the primary action is hidden by `100vh` under the toolbar |

## Color, surfaces and depth: [color-surfaces.md](color-surfaces.md)

| Concept | Use when | Severity |
|---|---|---|
| OKLCH palettes | defining a color scale or semantic palette | P2 |
| OKLCH gradients | any gradient between distant colors | P1 when the middle turns gray |
| Alpha borders | borders and dividers on varied backgrounds | P2 |
| Masked edges | scroll lists, carousels, clamped text | P1 when a colored overlay is used over variable backgrounds |
| Dark mode depth | dark surfaces and elevation | P1 when all surfaces are flat and identical |

## Motion: [motion.md](motion.md)

| Concept | Use when | Severity |
|---|---|---|
| Origin-aware animation | popovers, menus, modals, toasts | P1 when the transform-origin is wrong |
| Interruptible animation | any state that can toggle or be dragged | P0 when it blocks input; P1 when it is not interruptible |
| Stagger | several items entering together | P2 |
| Shared element transition | same object in two views | — |
| Blurred icon swap | an icon that changes in place | P2 |

## Interaction and state: [interaction-state.md](interaction-state.md)

| Concept | Use when | Severity |
|---|---|---|
| Affordance | any interactive element | P1 when states or affordance are missing |
| Combobox | more than ~7-10 options | P0 when unusable by keyboard |
| Optimistic update | actions that almost always succeed | P0 when used on a destructive action |
| Progressive disclosure | dense settings, advanced options | — |
| Layout shift | images, async content, banners, fonts | P0 when it hits a primary action |
