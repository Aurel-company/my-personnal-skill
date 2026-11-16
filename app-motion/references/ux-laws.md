# UX laws applied to motion

Laws of UX describe how people perceive and decide. Use them to test a motion idea, not to justify one. They are heuristics, not guarantees: validate with real users when it matters.

## Fitts's law: bigger hit areas
- **Idea**: the time to reach a target depends on its distance and size. Bigger and closer is faster.
- **Motion implications**:
  - Interactive targets at least 44×44 px (see `interface-craft`); extend the hit area with padding or a pseudo-element, not by enlarging the visible shape.
  - Do not move a target while the user is aiming at it: let entrance animations finish (or make the target interactive from its final position) before it can be pressed.
  - Press scale must not shrink the hit area: scale an inner element.
  - Place primary actions near the thumb zone or screen edges on mobile.
  - Sticky or docked controls (bottom bar) stay stable during transitions.

## Hick's law: fewer choices, faster decisions
- **Idea**: decision time grows with the number and complexity of choices.
- **Motion implications**:
  - Do not animate many options in at once for attention; reveal progressively (progressive disclosure) so the user sees few choices at a time.
  - Use motion to highlight the recommended or next step, not to give every option the same weight.
  - Group options and animate the group, not each item.
  - Transitions between steps (wizards) should clarify "one decision per step".

## Miller's law: chunking (about 7 ± 2 items)
- **Idea**: people hold a limited number of items in working memory, so chunking helps.
- **Motion implications**:
  - Stagger by group, and cap staggered items around 7-8; reveal the rest together.
  - Do not run more than a handful of simultaneous moving elements; extra motion competes for attention.
  - Use motion to show structure (a group expanding as a unit) rather than to decorate items.

## Doherty threshold: respond fast to keep flow
- **Idea**: when the system responds within about 400 ms, users stay in flow. Feedback under about 100 ms feels instant.
- **Motion implications**:
  - Give feedback (press state, spinner, optimistic change) within ~100 ms.
  - A transition should complete in under ~400 ms; otherwise it feels like waiting.
  - Animation must not delay the real result: never block the next action until an animation ends.
  - If work takes longer than ~400 ms, show progress: a skeleton, a progress indicator, a subtle shimmer. Animations can make waiting feel shorter, but do not use them to hide slowness for long.
  - Animate the response, not a fake delay.

## Postel's law: be liberal in what you accept, conservative in what you send
- **Idea**: tolerate imperfect input, produce clear and consistent output.
- **Motion implications**:
  - Accept rushed and imprecise input: generous hit areas, forgiving swipe thresholds, rapid repeated taps, input during an animation (interruptible).
  - Handle reversal gracefully: a user who changes their mind mid-transition continues from the current state.
  - Output a small, predictable set of motions (consistent easings, durations, directions).
  - Degrade well: `prefers-reduced-motion`, slow devices, missing View Transitions support, all give a clean fallback.

## Jakob's law: users expect your app to work like the ones they already know
- **Idea**: people spend most of their time in other products, and carry those expectations over.
- **Motion implications**:
  - Follow platform conventions: sheets rise from the bottom, forward navigation moves in the reading direction and back reverses it, swipe-back where the platform has it, pull-to-refresh at the top of a list.
  - Familiar easing and timing per platform feel native; custom physics should still respect the gesture's expected result.
  - Do not reinvent common gestures and transitions to be different; be distinctive in the details (tokens, icon swaps, success pulse), not in the basics.
  - Mirror directions for right-to-left languages.

## Frequency of use (the rule behind all the others)
- **Idea**: not a named law, but the strongest practical driver: the more often an interaction happens, the less motion it should have and the faster it should be.
- **Motion implications**:
  - Constant-use actions (shortcuts, list selection, tab switching): no animation or ≤100 ms.
  - Frequent actions (dropdowns, toggles, press): short, subtle, no bounce.
  - Occasional (modals, page changes): standard, for orientation.
  - Rare moments (onboarding, success, empty states): the place to be expressive.
  - Rule of thumb: if the user sees it dozens of times a day, delete a bit of motion; if they see it once, you can add some.

## Using the laws together

| Question | Laws to check |
|----------|---------------|
| Is it fast enough? | Doherty, frequency of use |
| Can the user hit it and recover from a mistake? | Fitts, Postel |
| Is it clear what to do next? | Hick, Miller |
| Does it behave as expected? | Jakob |
