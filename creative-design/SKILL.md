---
name: creative-design
description: Push a design toward a more creative, specific and surprising direction by consulting a local library of creative ideas (starting with background treatments such as felt, fluted glass, halftone, grain, dithering, ASCII) and, when the library is not enough, by researching the web. Use when the user wants a more creative, distinctive or less generic look, asks for ideas or inspiration, needs a background or texture, or when a design feels flat, safe or template-like.
---

# Creative design

Creativity here is a **process, not a mood**: widen the options, pick with intent, combine, then execute with craft. The skill has a library of concrete ideas to start from and a research protocol for when the library runs out.

- Library index: [references/library-index.md](references/library-index.md)
- One file per idea: `references/backgrounds/<idea>.md`
- Web research protocol: [references/research-protocol.md](references/research-protocol.md)
- New finds waiting to be promoted: [references/inbox.md](references/inbox.md)

## Operating rules

1. **Diverge before you converge.** Never start from the first idea. Always lay out at least three directions before building one.
2. **Fit the product, not the trend.** A technique is only good if it says something true about the product or audience. Name that link in one sentence for every proposal.
3. **Legibility and performance are the floor.** Text on a textured background must keep AA contrast; heavy effects need a static or cheap fallback; honour `prefers-reduced-motion`.
4. **Take the principle, not the pixels.** Research gives you ideas and techniques. Never copy someone's artwork, code or assets without a license that allows it.
5. **Do not ask a long list of questions.** Infer from the brief, state assumptions, ask only for what changes the direction (audience, mood, brand constraints).
6. **Leave the library better.** Anything useful found during research goes back into the library (step 6).

## Workflow

### 1. Read the brief

In two or three lines, write: what the surface is (hero, app shell, card, poster, loader, empty state), who it is for, the feeling to produce, and the constraints (brand colors, performance budget, stack, dark/light). If the user gave a brand or existing design, start from it.

### 2. Consult the library

1. Read `references/library-index.md` (mood, technique, cost per idea).
2. Select **candidates**: 2 that fit the brief well, 1 **unexpected** one that would not be the obvious choice (the "stretch").
3. Open the matching `backgrounds/*.md` files for the details: look, how to build it, legibility and cost, pairings, search keywords.

### 3. Research when needed

Go to the web (see the protocol) when any of these is true: the user asks for fresh or current references; the library has nothing close; the technique needs a recent implementation (shader, new CSS feature); a candidate needs real assets (public-domain images, textures). Collect 3 to 5 references, extract the **technique and the reason it works**, and note the source and license.

### 4. Push the idea

Take the best candidate and push it with one or two of these moves, then keep what survives:

- **Combine**: two ideas, one dominant and one accent (e.g. grain on a single-hue landscape, halftone over a blurred photo).
- **Constrain**: one hue, two colors, one shape, one grid, one font. Constraints force identity.
- **Change the medium**: make a digital surface feel like paper, glass, print, a terminal, a map, a scientific plate.
- **Change the scale**: show the texture 10x bigger or 10x finer than expected.
- **Subtract**: remove the decoration until only the idea is left.
- **Make it react**: let the pointer, scroll or time change the surface, subtly.

### 5. Propose, then build

Present **three directions** in this format, then build the one the user picks (or the strongest one if the user said to go ahead):

```
Direction N: <name>
- Idea: <library idea(s) used, or the researched one>
- Why it fits: <one sentence tied to the product>
- How: <technique in one line: CSS / SVG filter / canvas / shader / asset>
- Cost and risk: <performance, legibility, browser support>
```

When building: tokens first (colors in OKLCH where possible, one grain/size variable), a static fallback, a reduced-motion path, contrast checked against the text that sits on top, and a sensible mobile version (smaller or simpler effect). Prefer CSS and SVG for light effects, canvas for generated patterns, WebGL for real-time distortion.

### 6. Feed the library

If research produced something reusable:

1. Add a short note to `references/inbox.md` (idea, source, technique, license, date).
2. If it is solid and tested, promote it to its own file in `backgrounds/` (or a new category folder) using the same structure as the existing files, and add one row to `references/library-index.md`.

## Checks before delivering

Call the Skill tool with "design-without-ai-tells" if it is not already loaded in this conversation (if it is not available, continue without it) and check that the result is not a second-order default (cream with terracotta, near-black with one acid accent, an accent word in the headline). An idea taken from this library is still a default if nobody chose it for the product.

- Is there a one-sentence reason this technique belongs to this product?
- Is the text readable at AA contrast on top of it, on desktop and phone?
- Does it have a cheap fallback and a reduced-motion version?
- Is any asset licensed for use, and is the source noted?
- Would a competitor's page look the same with the effect removed? If yes, push further.

## Skill links

**Calls** (mandatory, at the step named above):
- `design-without-ai-tells`: checks before delivering.

**Related** (only when the situation appears, no automatic call):
- `interface-craft`: OKLCH colors, text legibility on a texture, and the motion of the effect.
