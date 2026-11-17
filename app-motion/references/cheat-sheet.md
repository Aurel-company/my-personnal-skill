# Cheat sheet: starting values

Starting points, not obligations. Deviate when the product or brand calls for it, and say why in one line. Detail, code and the cases to skip each rule: [ui-motion-rules.md](ui-motion-rules.md).

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
