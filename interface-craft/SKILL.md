---
name: interface-craft
description: Apply fine-grained interface craft when building or reviewing UI: typography, geometry and touch, color and surfaces, motion, and interaction and state. Use when polishing a component, auditing UI details, or when something "feels off" but is hard to name.
---

# Interface craft

Polish is the sum of small decisions that nobody notices when they are right and everybody feels when they are wrong.

The concepts live in `references/`, not here, so they can grow without touching this file. Start with [references/index.md](references/index.md): it lists every concept, when to use it and its severity, and points to the category file with the detail. Categories: [typography](references/typography.md), [geometry, icons and touch](references/geometry-icons-touch.md), [color and surfaces](references/color-surfaces.md), [motion](references/motion.md), [interaction and state](references/interaction-state.md).

Each concept has: **what it is**, **the rule**, **how to apply it**, **the common failure**.

## Operating rules

1. Apply a concept only when the interface actually contains the situation (no stagger without a list, no combobox without a long option set).
2. Fix the floor first: contrast, focus states, `prefers-reduced-motion`, working mobile layout.
3. Read the concept's block in its category file before applying it; do not apply a rule from memory of its name.

## Workflow

### Building
1. **Direction first** (new screen or component, not a one-line fix): call the Skill tool with "design-without-ai-tells" if it is not already loaded in this conversation, and settle its direction step before applying any concept. If it is not available, continue without it.
2. List which situations appear in the screen (text, numbers, tap targets, lists, overlays, async actions, navigation between views).
3. Open the index, pick the matching concepts, apply them; skip the rest.
4. Encode values as **tokens** (type scale with tracking and leading, `--tap-min: 44px`, motion durations and easings, OKLCH palette) so the details are consistent rather than repeated.

### Reviewing
Go through the screen and report each issue as: **concept → location → what is wrong → concrete fix**. Order by the severity given in the index:

- **P0 (breaks use)**: the condition under which a concept rises to P0 is stated in the index (touch target, safe area, `100vh`, layout shift on a primary action, keyboard access, blocked input, destructive optimistic update).
- **P1 (felt by everyone)**: details every user feels without naming them.
- **P2 (felt by designers)**: fine craft details.

### Final check
- Last pass for AI tells: call the Skill tool with "design-without-ai-tells" if it is not already loaded (if it is not available, continue without it) and run its pre-ship questions on the result.
- Can every target be hit with a thumb, with space between neighbours?
- Does anything move that the user did not cause?
- Does every animation start from its cause and survive being interrupted?
- Do numbers stay still when they change?
- Is each paragraph readable at its width and leading, with no lone last word?
- Is everything essential visible, and everything else one clear step away?
- Do nested rounded shapes share a centre, and do icons match the weight of their text?
- Do borders, fades and gradients still look right on every background and in dark mode?
- Does the layout fit with the mobile toolbar both shown and hidden?

## Skill links

**Calls** (mandatory, at the steps named above):
- `design-without-ai-tells`: direction before building, tells check at the final check.

**Related** (only when the situation appears, no automatic call):
- `app-motion`: as soon as a concept from the Motion category applies, to set the motion budget by how often the interaction happens.
- `responsive-web-app`: when safe area, dynamic viewport or touch targets are part of a wider responsive question (breakpoints, tables, navigation).
