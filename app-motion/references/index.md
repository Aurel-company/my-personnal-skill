# App motion: resource index

Everything concrete lives here so it can be updated without touching `SKILL.md`.

**To add a resource**: add the block to the matching file (or a new file), then add one row below. `SKILL.md` does not change.

| File | What it holds |
|---|---|
| [cheat-sheet.md](cheat-sheet.md) | Starting values by situation: entrance, move, exit, dropdown, popover, press, list stagger, toggle, details, arcs, success, everyday UI, held element, overlap, masks |
| [component-recipes.md](component-recipes.md) | One recipe per component: button, dropdown/menu, popover/tooltip, modal/sheet, toggle, list rows, toast, theme change, page/route, drag |
| [ui-motion-rules.md](ui-motion-rules.md) | Concrete UI motion rules with suggested tokens, values, code and when to skip |
| [disney-principles.md](disney-principles.md) | The Disney animation principles translated to UI, plus a mapping to the app rules |
| [ux-laws.md](ux-laws.md) | UX laws and what each means for motion, plus how to use them together |

## ui-motion-rules.md

1. Ease-out for entrances
2. Dropdowns at 150-250 ms
3. Stagger list rows by 30 ms
4. Scale to 0.97 on press
5. Stretch moving knobs by 12%
6. Stagger as details settle
7. Arcs for object movement
8. Pulse to confirm success
9. Ease-in-out for moves
10. Start popovers at 0.95
11. Enter from the trigger, exit to the trigger
12. No bounce on everyday UI
13. Do not tween while held
14. Make exits 20% shorter
15. Overlap old and new states
16. Masks for reveal and color
17. Interruptibility and reduced motion (always)

## disney-principles.md

Squash and stretch · Anticipation · Staging · Pose to pose · Follow through and overlapping action · Slow in and slow out · Arcs · Secondary action · Timing · Exaggeration · Solid drawing · Appeal

## ux-laws.md

Fitts · Hick · Miller · Doherty · Postel · Jakob · Frequency of use
