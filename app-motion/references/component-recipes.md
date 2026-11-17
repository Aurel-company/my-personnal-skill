# Component recipes

One starting recipe per common component. Adjust the numbers for the product, and keep the motion budget matched to how often the interaction happens (see the frequency table in `SKILL.md`).

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
