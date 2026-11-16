# Catalogue des signes « fait par IA » (anglais, pour l'IA)

Chaque entrée : **tell** → why it reads as AI → what to do instead.
Severity: **P0** noticed by anyone, **P1** noticed by designers/developers, **P2** craft.
Sources numbered `[n]` are listed in [sources.md](sources.md). Rows tagged `[c]` come from established craft practice rather than the research sources; the `interface-craft` skill details their implementation.

## 1. Typography

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Inter everywhere, no pairing | Most frequent UI font in training data. The problem is the *unchosen* default, not Inter itself [1][2][4] | Choose a display face and a body face on purpose; if Inter stays, say why and pair it | P1 |
| The recurring "tasteful" fonts (Space Grotesk, Geist, Instrument Serif, Fraunces) | Second-order default: same few fonts across generated pages [1][3] | Pick from the product's world, not from "fonts AI likes" | P1 |
| Fonts declared in CSS but never loaded | Falls back to system sans without anyone noticing [3] | Load the faces and verify in the rendered page | P1 |
| One italic serif word in the headline | Stock "editorial" accent on an otherwise sans page [1][3][5] | Make the type system consistent, drop the accent | P1 |
| One colored word in a headline | Same reflex, color instead of italic [5] | Emphasis through structure or weight, or none | P1 |
| All-caps tracked micro-labels / eyebrow above headings | Template section labels [1][3][5] | Sentence case; delete the eyebrow if the heading works alone | P0 |
| Tiny numbered labels (01 / 02 / 03) | Decorative numbering [3][5] | Number only when order matters, and in a real layout | P1 |
| Oversized hero headline, crushed letter spacing | Fills space with size instead of content [5] | Size from content and hierarchy; normal tracking | P1 |
| Flat hierarchy (everything similar size/weight) | Nothing prioritised [5][6] | Clear 3-level hierarchy: one dominant element per view | P1 |
| Line length too long, tight line height, justified text | Unreviewed defaults [5] | 60–75 characters, 1.4–1.6 body leading, left-aligned | P2 |
| Headlines that break badly: one orphan word on the last line, ragged or accidental line breaks | Browser default wrapping never reviewed [c] | `text-wrap: balance` on headlines and short copy, `text-wrap: pretty` on paragraphs; never fix with manual `<br>` | P2 |
| Proportional digits in tables, prices, timers, counters and stats | Default figures make columns misalign and live numbers jitter [c] | `font-variant-numeric: tabular-nums`, right-align numeric columns | P2 |
| Monospace used as decoration (labels, headings, buttons, "technical" flavor) | Cheap shortcut to a "developer" look [3][c] | Mono only where it does work: code, IDs, keyboard shortcuts, data that must align. Everything else in the chosen text face | P1 |
| Redundant labels: a label repeating its placeholder or icon, an eyebrow repeating its heading, "Price: $9", a section named after its only content | Filler text added by reflex [c] | Keep a label only if it adds information the layout does not already give; delete the rest | P1 |

## 2. Color

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Purple / indigo-to-blue gradient | Tailwind indigo default plus training-data loop; the loudest tell [1][2][4][6] | Palette derived from something true about the product; flat color | P0 |
| Lavender-purple accent even without gradient | Same default, flat [1] | Choose an accent with a point of view | P0 |
| Gradient text, gradient buttons, gradient backgrounds | Gradients applied everywhere [1][3][5] | Flat color, or one deliberate gradient at one moment | P0 |
| Colored glows, colored box-shadows, radial halo behind hero | Visual noise standing in for depth [1][3][5] | Neutral, subtle shadow, or none | P0 |
| Permanent dark mode with grey text and all-caps labels | Default theme, not a decision [1] | Decide light or dark from context and audience | P1 |
| Low-contrast muted text | Fails WCAG AA, especially grey on dark or on color [1][3][5] | Test against AA (4.5:1 body); raise contrast | P0 (floor) |
| Pure `#000` and `#fff` | Raw defaults [6] | Off-black and warm/cool off-white tuned to the palette | P2 |
| Untouched shadcn / component-library palette | Fingerprint of the kit [1][3] | Customize tokens, radius, shadow depth, variants | P1 |
| One hue posing as two | Fake palette depth [3] | Real neutral family plus one or two functional accents | P1 |
| Colors named by look (`blue-500`) | No semantics [6] | Name by function: `action`, `warning`, `success` | P2 |

## 3. Layout and structure

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Centered hero: badge, headline, gray subhead, two buttons | The default hero [1][2][4][7] | Vary alignment; lead with the real product or a specific claim | P0 |
| Badge / pill chip above the H1 | "New ✨", "Now in beta" [1][3] | Remove, or move it where it informs | P0 |
| Three equal cards with a top icon | Tailwind tutorial grid learned as "features" [1][2][4][7] | Asymmetry, different weights, one distinctive primitive, or prose | P0 |
| Stock section order: hero, logos, features, stats, pricing, CTA | Template page [3] | Order by the user's decision path for this product | P1 |
| Three-tier pricing and four-column footer by reflex | Template [3] | Only if the business really has them | P1 |
| Stat banner row as social proof | Big numbers without a claim [1][3] | Show a figure only with the claim it supports | P0 |
| Numbered 1-2-3 "how it works" | Generic process [1][3] | Prose, a real diagram, or a screenshot sequence | P1 |
| Uniform spacing, radius, padding, card height | Flattens hierarchy [2][5][6] | Intentional variation: primary larger, closer, heavier | P1 |
| Everything visible at once | No progressive disclosure [6] | Reveal by step according to user journey | P1 |
| Email sign-up at the end of every page | Reflex CTA [5] | Only where it serves the page's goal | P1 |
| Hero that does not fit its screen, empty frames, one column stretching the first viewport | Unreviewed layout [3][5] | Check at real viewport sizes with real content | P1 |
| Related items split by lines and boxes while unrelated items sit at the same gap | Containers used instead of proximity; flat rhythm [5][c] | Group with spacing: tight inside a group, clearly larger between groups; add a divider or box only if space is not enough | P1 |
| Competing buttons of equal weight, or the main CTA lost among cards and links | Every action styled the same, no priority [5][6][c] | One primary action per view: largest, highest contrast, in the accent color; secondary as outline or text link; repeat the same primary label, do not multiply CTAs | P1 |

## 4. Components and surfaces

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Colored left/top border stripe on cards | One of the most reliable tells [1][3][5][6] | One card treatment; keep a colored border only if it encodes meaning | P0 |
| Cards nested inside cards | Container habit [5] | Flatten; use space and dividers | P1 |
| Heavy radius and shadow on everything | Soft-UI default [3][7] | One radius rule, one shadow rule | P1 |
| Glassmorphism, frosted blur by reflex | Glass everywhere [1][3][7] | Use only where layering has a function | P0 |
| Icon in a rounded square above a heading | Icon-tile reflex [3][5] | Drop the tile; icon inline or nothing | P1 |
| 1px gray borders on everything | Border default [7] | Separate with space, tone, or a single consistent rule | P1 |
| Fake window dots, pulsing status dot, blinking cursor | Decorative "tech" cues [3][5] | Remove unless they carry real status | P0 |
| Stock effect libraries (Aceternity, Magic UI) dropped in | Recognisable motion/FX [3] | Build the one effect the design needs | P1 |
| Missing focus states, tiny hit areas | Floor failure [3][8] | Visible focus, 44px targets | P0 (floor) |
| Decorative badges, pills and filter chips scattered on cards and headers ("New", "Popular", category chips with no function) | Garnish that adds noise, not information [1][3][c] | Delete them. Keep a chip only if it filters, toggles or encodes a real status, and then style it as a control | P1 |
| Nested rounded elements with the same radius on parent and child | One radius token reused at every level, corners look thick and pinched [c] | Inner radius = outer radius − padding (− border width if any), clamped at 0; derive it with `calc()` | P2 |
| Elements centered mathematically but off to the eye: play triangle, icon in a button, text in a pill, mixed baselines | Alignment by box, not by perception [c] | Align by eye: shift asymmetric shapes, centre text on x-height/cap-height, align baselines across mixed icon and text rows | P2 |

## 5. Motion

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Same fade-up on every section | Uniform decorative motion [2][3][6][7] | Motion tied to interaction feedback or directing attention | P0 |
| Bounce / elastic easing | Playful default [3][5] | Ease-out for entering, ease-in for leaving, short durations | P1 |
| Count-up stat animation | Gimmick [3] | Static figure | P1 |
| Auto-scrolling marquee of logos | Filler proof [5] | Static list of real customers, or remove | P1 |
| Animation ignores `prefers-reduced-motion` | Floor failure [3][8] | Honor the media query | P0 (floor) |
| Animating layout properties | Jank [5] | Animate `transform` and `opacity` | P2 |
| Nothing moves at all on interactive elements | No feedback [6] | Press, hover and focus feedback on primary controls | P1 |

## 6. Icons and imagery

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Emoji as icons (nav, bullets, features) | Quick stand-in [1][3][7] | One real icon set at one weight and size, or plain text | P0 |
| The same thin-line generic icon set (default Lucide look) and sparkle icon for "AI" | Interchangeable [3][4] | Pick a set deliberately; avoid sparkles as the AI symbol | P1 |
| Plastic AI illustrations, melted text or hands in generated photos | Synthetic look [2][9] | Real photography, custom illustration, real 3D | P0 |
| Shape-assembled illustrations from circles and rectangles | Placeholder art [5] | Commission or draw; or use real screenshots | P1 |
| Stock team photos, placeholder avatars, no product screenshots | No real proof [2][3] | Real people, real screenshots, named customers | P0 |
| Broken or placeholder images | Unreviewed [5] | Check every image loads | P0 (floor) |

## 7. Copy

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| "Build the future of work", "Build faster. Ship smarter." | Could describe any company [2][4][6] | Name the customer, the problem and the outcome | P0 |
| Buzzwords: seamless, robust, supercharge, unlock, elevate | Empty superlatives [2][3][5] | A number, a capability, or a before/after | P0 |
| Em-dash in nearly every sentence | Stylistic tic [2][5] | Use sparingly; rewrite with periods or commas | P0 |
| Stock openers: "In today's fast-paced world" | Boilerplate [2] | Start with the point | P0 |
| Aphorism cadence ("Not X. Just Y.") | Rhythm tic [5] | Plain statements | P1 |
| Hedging, emoji bullets, no stance | Noncommittal [2] | State who it is for and who it is not for | P1 |
| Generic buttons ("Get Started", "Learn more") and arrows attached to every CTA | Reflex labels [3] | Verb plus object specific to the action | P1 |
| Form says "thanks" without sending anything | Fake behavior [8] | Wire it up or do not show it | P0 |
| Invented facts, numbers, testimonials | Fabrication [8] | Use only real, verifiable content | P0 (floor) |

## 8. States and behavior

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| Only the happy path designed | No empty/loading/error [6] | Design each state; empty states prompt action; errors in plain language | P1 |
| Everything exposed at once | No hierarchy of tasks [6] | Progressive disclosure along the journey | P1 |
| Design drift between pages (font, radius, nav, footer change) | Pages generated independently [3] | Shared tokens in `DESIGN.md`; check all pages together | P1 |

## 9. Code and metadata

| Tell | Why it reads as AI | Do instead | Sev |
|---|---|---|---|
| "Built with v0 / Edit with Lovable / Made with Bolt" badges | Builder stamps [9] | Remove; check footer and corners | P0 |
| Duplicated meta descriptions, default/missing OG image, alt text "image" | Boilerplate [2] | Unique meta, custom OG image, descriptive alt | P2 |
| Repeated component structure, dead utility classes, accessibility gaps | Templated code [2] | Review for structure, performance and accessibility | P2 |
| Upload paths of the builder left in image URLs | Giveaway in source [9] | Rehost assets | P2 |

## 10. Second-order defaults (the trap)

Removing the tells above often leads the model to the *next* default. Treat these as tells too:

- Cream/beige background with a terracotta or clay accent [3][5]
- Near-black with a single acid-green (or electric) signal color [3]
- Monospace + all-caps template labels [3]
- One accented headline word (italic serif or colored) [1][3]
- Decorative 01/02/03 numbering [1][3]
- Emerald as the fallback "brand" color [3]
- A single "editorial serif + grotesk" pairing used with no reason [1][3]

The cure is the same as for the first-order tells: derive each choice from the product, and be able to say why.

## 11. Floor (never ship without)

Contrast at AA, visible focus, `prefers-reduced-motion`, no invented facts, a working phone layout, working forms, images that load. [3][8]
