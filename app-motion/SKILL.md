---
name: app-motion
description: Design and review motion for app UI (transitions, micro-interactions, feedback, popovers, lists, toggles, success states, theme changes) so it maximizes UX. Combines concrete UI motion rules (easing, durations, scale values, stagger, origin-aware popovers, interruptibility), the Disney animation principles adapted to interfaces, and UX laws (Fitts, Hick, Miller, Doherty, Postel, Jakob, frequency of use). Use when adding, tuning or auditing animation in an app, or when motion feels slow, noisy, bouncy or generic.
---

# App motion

Motion in an app exists to serve the user, in this order: **feedback** (I was heard), **orientation** (where did that come from, where did it go), **continuity** (this is the same thing, changed), **attention** (look here), and only last **delight**.

**Everything below is a recommendation, not an obligation.** The numbers are starting points. Deviate when the product, brand or context calls for it, and when you do, say why in one line. Never apply a rule just to apply it; never add motion that does not serve one of the five purposes above.

The concrete material lives in `references/`, so it can be updated without touching this file. Start with [references/index.md](references/index.md); it lists every rule, principle, law and recipe. Read only what you need:
- [references/cheat-sheet.md](references/cheat-sheet.md): starting values by situation.
- [references/component-recipes.md](references/component-recipes.md): one recipe per component.
- [references/ui-motion-rules.md](references/ui-motion-rules.md): concrete rules with values, code and when to skip them.
- [references/disney-principles.md](references/disney-principles.md): the Disney animation principles translated to UI.
- [references/ux-laws.md](references/ux-laws.md): UX laws and what they mean for motion.

Related skills: `interface-craft` (details such as origin-aware, interruptible, stagger, shared element), `apple-design` (physical, fluid motion), `design-without-ai-tells` (generic fade-in-everything).

## Workflow

### 1. Ask how often it happens (frequency of use)

This single question sets the budget. The more often users see an interaction, the less and shorter its motion should be.

| Frequency | Examples | Motion budget |
|-----------|----------|---------------|
| Constant (many times a minute) | keyboard shortcuts, list row selection, tab switching, command palette | none or ≤100 ms, no flourish |
| Frequent (several times a session) | dropdowns, toggles, press feedback, popovers, row enter | fast and subtle, 100-250 ms, no bounce |
| Occasional | modals, sheets, page transitions, toasts | standard, 200-350 ms, orientation matters |
| Rare or first time | onboarding, empty states, success celebrations, upgrades | expressive allowed: arcs, exaggeration, a little overshoot |

### 2. Name the purpose

Feedback, orientation, continuity, attention, or delight. If you cannot name one, skip the animation.

### 3. Pick values from the cheat sheet

Open [references/cheat-sheet.md](references/cheat-sheet.md) for the starting value that matches the situation (entrance, exit, dropdown, popover, press, list stagger, toggle, success, drag, reveal, and so on). Use the matching rule in [references/ui-motion-rules.md](references/ui-motion-rules.md) for the reason, the code and when to skip it.

### 4. Check against the UX laws

- Does it respond within ~100 ms and finish within ~400 ms? (Doherty)
- Is the target still big, stable and reachable while it moves? (Fitts)
- Are we animating many options at once? Group and reveal progressively. (Hick, Miller)
- Does it follow platform conventions users already know? (Jakob)
- Does it tolerate rushed, imprecise or interrupted input? (Postel)

### 5. Implement

- Animate `transform`, `opacity` (and small `filter`). Avoid animating `width`, `height`, `top`, `left`, and never use `transition: all`.
- Drive animation from state (`data-state="open"`) so every state is a pose and the browser interpolates; make it **interruptible** (CSS transitions or springs, not locked keyframes).
- Keep values in tokens (`--dur-fast`, `--dur-base`, `--ease-out`, `--ease-in-out`, `--press-scale`) so the whole app shares one motion personality.
- Honour `prefers-reduced-motion`: replace movement with opacity or a color change, keep the feedback.
- Test on a mid-range phone, not only on a fast laptop.

## Component recipes

For a button, dropdown, popover, modal, toggle, list, toast, theme change, page transition or drag, start from [references/component-recipes.md](references/component-recipes.md).

## Review format

For an audit, report each finding as: **element → what it does now → recommendation (rule or principle) → why it helps UX**. Separate **must fix** (blocks input, slows response past ~400 ms, bounces on constant-use UI, ignores reduced motion) from **could improve**.

## Checks before delivering

- Does every animation serve feedback, orientation, continuity or attention?
- Is the motion budget matched to how often the interaction happens?
- Are entrances ease-out, moves ease-in-out, exits shorter, and nothing bouncy in everyday UI?
- Can every animation be interrupted, and does input stay responsive during it?
- Is there a reduced-motion path, and is the whole app using the same easings and durations?
