# Design artifact guide

Used at step 3, after the grilling, when the user wants a design artifact. Questions to ask first: [design-grilling.md](design-grilling.md). Platform rules to follow: [platform-conventions.md](platform-conventions.md). This file only says what to produce and how.

## Screens to design first

| Order | Screen | Why |
|-------|--------|-----|
| 1 | Root of each core tab | Sets navigation, density and hierarchy |
| 2 | One detail screen | Sets typography, content layout and actions |
| 3 | One form (create or edit) | Sets inputs, keyboard and primary action placement (see `forms-and-input.md`) |
| 4 | One empty state | Sets tone and illustration style |
| 5 | One error or offline state | Sets feedback and recovery |
| 6 | One sheet or dialog | Sets the modal surfaces |

Judgment: validate these six before designing the rest; most other screens follow from them.

## Reference sizes

Judgment: one small and one large phone per platform covers most layout problems. Models are examples; use current equivalents.

| Platform | Small | Large |
|----------|-------|-------|
| iOS | 375 × 667 pt (iPhone SE size) | 440 × 956 pt (largest current iPhone) |
| Android | 360 dp wide (compact phone) | 412 dp wide (large phone) |

Add tablet frames only if tablets are in scope (see `tablets-and-foldables.md`).

## Presenting iOS and Android

| Rule | Detail |
|------|--------|
| Side by side | Same screen, iOS left, Android right, same content |
| Mark divergences | Annotate each difference (back, title bar, pickers, sheets, alerts, primary action) with a short label referring to the contract's conventions table |
| Shared first | When one shared design is chosen, still show the platform chrome that differs |
| Variants | Each key screen in light and dark, and at the largest text size |

## Format

| Format | Use when | Output |
|--------|----------|--------|
| Static mockups | Direction and visual choices are the open question | Frames per screen and state, annotated |
| Clickable prototype | Navigation and flows are the open question, or stakeholders must try it | Linked frames following the navigation graph |
| Screens in the target stack | The team wants to validate real feel (gestures, motion, text scaling), or there is no designer | Running screens with mock data, reused in wave 0 |

Judgment: for a small team without a designer, screens in the target stack avoid a translation step and feed wave 0 directly.

## Back to the contract

After validation, write to the contract's design section:

| Item | Content |
|------|---------|
| Link | Where the artifact lives, with the validated version or date |
| Tokens | Colors (light and dark), type scale, spacing, radii, elevation, motion durations |
| Decisions | Each grilling decision in one line (brand vs platform, density, primary action placement, haptics, motion personality) |
| Validated screens | List of screen ids from the graph that are designed and validated |
| Divergences | iOS / Android differences shown in the artifact, mirrored in the conventions section |
| Open points | What the artifact does not decide yet |
