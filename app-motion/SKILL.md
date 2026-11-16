---
name: app-motion
description: Design and review motion for app UI (transitions, micro-interactions, feedback, popovers, lists, toggles, success states, theme changes) so it maximizes UX. Combines concrete UI motion rules (easing, durations, scale values, stagger, origin-aware popovers, interruptibility), the Disney animation principles adapted to interfaces, and UX laws (Fitts, Hick, Miller, Doherty, Postel, Jakob, frequency of use). Use when adding, tuning or auditing animation in an app, or when motion feels slow, noisy, bouncy or generic.
---

# App motion

Motion in an app exists to serve the user, in this order: **feedback** (I was heard), **orientation** (where did that come from, where did it go), **continuity** (this is the same thing, changed), **attention** (look here), and only last **delight**.

**Everything below is a recommendation, not an obligation.** The numbers are starting points. Deviate when the product, brand or context calls for it, and when you do, say why in one line. Never apply a rule just to apply it; never add motion that does not serve one of the five purposes above.

References (read the one you need):
- [references/ui-motion-rules.md](references/ui-motion-rules.md): 17 concrete rules with values and code.
- [references/disney-principles.md](references/disney-principles.md): 12 animation principles translated to UI.
- [references/ux-laws.md](references/ux-laws.md): 7 UX laws and what they mean for motion.

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

| Situation | Starting point |
|-----------|----------------|
| Entrance | ease-out (fast start, soft landing) |
| Move between positions on screen | ease-in-out |
| Exit | about **20% shorter** than the entrance; keep it quick |
| Dropdown, menu, select | **150-250 ms** |
| Popover | start at **scale 0.95** + opacity 0, **enter from the trigger**, **exit to the trigger** |
| Press | scale to **0.97**, ~100 ms in, spring back out |
| List rows entering | stagger **30 ms** per row (cap around 8 rows) |
| Moving toggle knob | stretch about **12%** while it travels |
| Details around a main change | stagger so they **settle after** the main element |
| Object moving across the screen | follow an **arc**, not a straight line |
| Success confirmation | one **pulse** (scale 1 → ~1.05 → 1 or a ring) |
| Everyday UI | **no bounce**; critically damped springs |
| Held or dragged element | **do not tween**: follow the pointer 1:1, animate on release |
| Old and new state | **overlap** them (crossfade), do not wait for one to finish |
| Reveal or color change | use a **mask** (clip-path / mask-image / view transition) |

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

| Component | Recipe |
|-----------|--------|
| Button | press scale 0.97 at ~100 ms; hit area unchanged by the scale (scale a child); success → one pulse |
| Dropdown / menu | opens from the trigger edge, 150-250 ms ease-out, items appear at once (or a very light stagger), closes ~20% faster toward the trigger |
| Popover / tooltip | scale 0.95 → 1 + fade from the trigger, tooltips instant after the first one is open |
| Modal / sheet | ease-out in 250-300 ms from its source (or from the bottom on mobile), exit ~20% shorter, backdrop fades with it |
| Toggle / switch | knob moves with ease-in-out and stretches ~12%, track color changes at the same time |
| List rows | stagger 30 ms on first load only, never on every re-render or on constant-use lists |
| Toast | slides from its docked edge, short exit, pulse or icon draw on success |
| Theme change | circular or linear mask reveal from the toggle |
| Page / route | continuity first: shared element or directional slide matching navigation (forward vs back), 250-350 ms |
| Drag | lift on grab (scale + shadow), 1:1 tracking while held, settle on release with the release velocity |

## Review format

For an audit, report each finding as: **element → what it does now → recommendation (rule or principle) → why it helps UX**. Separate **must fix** (blocks input, slows response past ~400 ms, bounces on constant-use UI, ignores reduced motion) from **could improve**.

## Checks before delivering

- Does every animation serve feedback, orientation, continuity or attention?
- Is the motion budget matched to how often the interaction happens?
- Are entrances ease-out, moves ease-in-out, exits shorter, and nothing bouncy in everyday UI?
- Can every animation be interrupted, and does input stay responsive during it?
- Is there a reduced-motion path, and is the whole app using the same easings and durations?
