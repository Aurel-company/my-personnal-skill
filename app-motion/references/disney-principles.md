# Animation principles for app UI

The classic principles of animation (Disney, 1930s) translated to interfaces. They are a lens, not a checklist: a calm productivity app uses few of them, a playful consumer app uses more. Match intensity to **frequency of use** and brand.

For each principle: **idea**, **in an app**, **use sparingly / skip when**.

## Squash and stretch
- **Idea**: deformable things compress and elongate, which conveys softness, speed and mass.
- **In an app**: press squash (scale 0.97), toggle knob stretching about 12% while it travels, a pull-to-refresh handle elongating as it is pulled. Keep apparent volume: if x grows, y shrinks slightly.
- **Skip when**: text, data, rigid-looking elements; frequent actions that need to feel crisp.

## Anticipation (wind-up)
- **Idea**: a small opposite movement before the main action tells the viewer what is about to happen.
- **In an app**: a button dips before it triggers, a card lifts slightly before a drag, a swipe row shows a bit of the action behind it, a pull-down gesture compresses before it refreshes. 50-100 ms, small.
- **Skip when**: the action is constant-use or time-critical: anticipation adds latency. Never delay the real response for the sake of a wind-up.

## Staging (focus)
- **Idea**: present one idea at a time so the eye knows where to look.
- **In an app**: dim or blur the backdrop behind a modal, animate only what changed, order entrances so the primary content arrives first, keep secondary motion quiet. One focal animation at a time.
- **Skip when**: nothing needs emphasis; then do not animate.

## Pose to pose
- **Idea**: define the key poses first (start, end), then fill in between.
- **In an app**: design the states first (closed, open, pressed, loading, success, error), then let transitions or springs interpolate between them. In code, drive visuals from state (`data-state`) rather than imperative step sequences. This also makes animations interruptible.
- **Skip when**: truly continuous, physics-driven motion (drag, scroll-linked), where you animate straight ahead from input.

## Follow through and overlapping action
- **Idea**: parts of a moving thing do not all stop at once; they settle after the main body.
- **In an app**: a sheet's content settles a beat after the sheet stops, a badge count ticks after the item lands in the cart, a drag release carries velocity into a soft settle. This is the basis of "stagger as details settle". Overshoot only where bounce is appropriate (rare, playful moments).
- **Skip when**: everyday UI where a settle would read as a bounce.

## Slow in and slow out
- **Idea**: things accelerate and decelerate; very few move at constant speed.
- **In an app**: ease-out for entrances, ease-in-out for moves, never default `linear` except for continuous motion (spinner, progress, marquee). Springs give this naturally.
- **Skip when**: continuous loops.

## Arcs
- **Idea**: living things and thrown objects move along curves, not straight lines.
- **In an app**: an item flying into a cart, a FAB changing position, a card moving between piles. Use `offset-path` or two axes with different easings.
- **Skip when**: axis-aligned UI motion (sliding panels, tab indicators).

## Secondary action
- **Idea**: a supporting motion that enriches the main one without stealing focus.
- **In an app**: the chevron rotates while the menu opens, the shadow deepens as a card lifts, a haptic tick accompanies a toggle, a checkmark draws after the pulse. Always subordinate: shorter, quieter and aligned with the main action.
- **Skip when**: it competes with the primary action or adds clutter.

## Timing (snappy)
- **Idea**: timing sets the feel and the weight of an action.
- **In an app**: UI should feel snappy: 100 ms for press, 150-250 ms for menus and popovers, 250-350 ms for large surfaces. Larger distance or area gets a slightly longer duration. Exits are about 20% shorter than entrances. Constant-use interactions get the shortest timing.
- **Skip when**: n/a, but always test: 50 ms too long is felt, 50 ms too short is missed.

## Exaggeration (exaggerated feedback)
- **Idea**: push a movement slightly beyond realism so it reads clearly.
- **In an app**: a gentle shake on a rejected input, a pulse that confirms success, the lift on a dragged card, a stronger response on destructive confirmations. Scale the exaggeration to the importance of the moment: subtle for common, bolder for rare or critical.
- **Skip when**: everyday interactions, where exaggeration becomes noise.

## Solid drawing (volume, depth)
- **Idea**: forms feel three-dimensional and consistent.
- **In an app**: one consistent light source and shadow logic (higher elevation = larger, softer shadow), coherent z-order (what is above stays above), scale and parallax that agree with depth, consistent perspective and transform-origin, objects that keep their volume while transforming. Elevation changes can be animated (lift on press or drag).
- **Skip when**: flat, graphic styles that deliberately avoid depth; then be consistent in that choice.

## Appeal
- **Idea**: the work has charisma and cohesion; it feels designed by one hand.
- **In an app**: a single motion personality: a small set of easings and durations used everywhere, shared tokens, consistent directions, polished edges, nothing arbitrary. Appeal comes from consistency and restraint more than from extra effects.
- **Skip when**: n/a. If you must choose, choose consistency over novelty.

## Quick mapping to the app rules

| Principle | Matching rule in `ui-motion-rules.md` |
|-----------|---------------------------------------|
| Squash and stretch | press 0.97, knob stretch 12% |
| Anticipation | short wind-up, never delaying the response |
| Staging | masks, overlap, one focal animation |
| Pose to pose | state-driven, interruptible transitions |
| Follow through | stagger as details settle |
| Slow in and slow out | ease-out entrances, ease-in-out moves |
| Arcs | arcs for object movement |
| Secondary action | subordinate supporting motion |
| Timing | 150-250 ms menus, exits 20% shorter |
| Exaggeration | pulse to confirm, reserved for important moments |
| Solid drawing | consistent elevation, depth and origin |
| Appeal | tokens and one motion personality |
