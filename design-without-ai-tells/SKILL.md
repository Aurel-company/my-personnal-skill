---
name: design-without-ai-tells
description: Design or review a UI, landing page or brand surface so it does not look AI-generated. Use when building or auditing frontend work and the result must feel authored, specific and human, or when the user mentions AI slop, "looks like AI", generic design, vibe-coded look, purple gradients, or template-looking pages.
---

# Design without AI tells

An interface looks AI-made when **defaults were never replaced by decisions**. Every tell below is a default the model reached for because nobody chose otherwise. The fix is never "add more decoration": it is to make a real, product-specific decision wherever a default would appear.

The tells, their fixes and their severities live in `references/`, not here, so they can grow without touching this file. Start with [references/index.md](references/index.md). Full catalog with fixes: [references/ai-tells-catalog.md](references/ai-tells-catalog.md). Sources: [references/sources.md](references/sources.md).

## Operating rules

1. **Decide before you generate.** No UI code until the direction is written down (step 1 below).
2. **Replacing a tell with the next default is still a tell.** Cream plus terracotta, near-black plus one acid-green accent, mono uppercase labels, one italic serif word, 01/02/03 numbering: these are the "tasteful" defaults and read as AI just as much. Pick from the product, not from a style.
3. **A tell is a signal, not proof.** Never remove something that is doing real work (a colored border that encodes status, Inter chosen on purpose). Ask "did we choose this?" not "is this banned?".
4. **Fix the floor first.** Contrast, focus states, reduced motion, real content, working phone layout. Polish before a floor failure is wasted.

## Workflow

### 1. Write the direction (before any code)

Answer in a short `DESIGN.md` or in the reply:

- **Who and what**: the specific audience, their problem, the outcome. Not "teams" or "the future of work".
- **One point of view**: a single sentence on the feel (e.g. "dense and calm like a lab notebook", "loud and printed like a gig poster"). It must be something a competitor would not say.
- **Type**: one display face and one body face, chosen on purpose, both actually loaded. Say why.
- **Color**: tokens named by function (`action`, `warning`, `surface`), a palette derived from something true about the product, one neutral family. Light or dark decided, not defaulted.
- **Shape and depth**: one radius rule, one shadow rule, one border rule.
- **Layout idea**: the structural principle (asymmetry, a strong grid, an unusual section rhythm). Say what will NOT be a row of equal cards.
- **Voice**: how the product talks, with two sample lines in that voice.

If the user gave a brand, use it. If not, ask for the missing facts rather than inventing them. Never invent logos, customers, numbers, testimonials or team photos.

### 2. Build against the catalog

While building, keep the catalog open: [references/index.md](references/index.md) lists the highest-signal tells in the order people notice them, and [references/ai-tells-catalog.md](references/ai-tells-catalog.md) has the full list by category with the fix for each.

### 3. Audit before you ship

Run the pre-ship questions, then fix in the order given in [references/index.md](references/index.md) (P0 first). The severity of each tell is in the catalog.

Pre-ship questions:

1. Could this page belong to a competitor with only the logo swapped? If yes, the direction is too generic.
2. For each section: which default did I replace, and with what decision?
3. Is there anything on the page I cannot justify by the product, the content or a function?
4. Does hierarchy come from real priority (size, weight, space), or is everything the same weight? Is there one clearly primary action and one clearly main feature per view?
5. Are the unhappy paths (empty, loading, error, long text, no data) designed?
6. Does it still work with keyboard only, at phone width, with reduced motion, and in both themes if both exist?

## When reviewing existing work

Report findings as: tell, where it is, why it reads as AI, concrete replacement. Group by P0/P1/P2. Do not rewrite what the user did not ask to change, and do not strip intentional choices: ask when unsure.

## Pairing

This skill is about what to **avoid** and how to **decide**. It does not replace a full design process: pair it with a product-design pass for flows and states, and with a detector (a linter or a rendered-page scan) when one is available. For how to implement the craft fixes (concentric radius, tabular numbers, headline wrapping, optical alignment, OKLCH, alpha borders), use the `interface-craft` skill; for motion that gives useful feedback, use `app-motion`.
