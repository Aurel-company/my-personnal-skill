# Motion

Default budget: **150–250 ms** for UI feedback, **250–400 ms** for large surfaces. Use `ease-out` for entering, `ease-in` for leaving, and custom curves over the browser defaults. Always honour `prefers-reduced-motion` (replace movement with a fade or nothing).

## Origin-aware animation
- **Rule**: an element should **grow from and shrink to the thing that caused it**. A popover from a button must not scale from its own centre.
- **Apply**: set `transform-origin` to the trigger point (`top left` for a menu opened from the top-left, or compute it from the trigger's position, or use the `anchor()` / popover APIs). Dropdowns scale + fade from the anchor edge; modals from the click point or from centre if triggered by a keyboard shortcut; toasts slide in from the edge they dock to.
- **Failure**: a tooltip that zooms from its centre while its arrow points elsewhere.

## Interruptible animation
- **Rule**: the user can change their mind mid-motion, and the animation must respond **immediately and continue from its current state**, not restart or finish first.
- **Apply**: prefer **CSS transitions** (they retarget from the current value) over keyframe animations for state changes that can toggle. Use springs (Motion, react-spring, `linear()` easing) for gestures and anything draggable: they carry velocity and are naturally interruptible. Never lock the UI during an animation; never block input with `pointer-events: none` for the duration. Open→close→open quickly must not jump.
- **Failure**: a drawer that completes its open animation before it will close; a double-clicked toggle that snaps.

## Stagger
- **Rule**: when several items enter together, offset them slightly so the eye follows a sequence instead of seeing one block pop in.
- **Apply**: **30–60 ms** between items (cap total stagger around 400 ms — show at most ~8 items staggered, then group the rest). Set the delay via a CSS variable (`animation-delay: calc(var(--i) * 40ms)`). Order by reading order or by proximity to the trigger. Trigger once, on entry, not on every re-render, and disable under reduced motion.
- **Failure**: a 20-item list taking 2 seconds to appear; stagger replaying on every data refresh.

## Shared element transition
- **Rule**: when the same thing exists in two views (a card → its detail page, a thumbnail → full image), **morph one into the other** so the user tracks identity across the change.
- **Apply**: the **View Transitions API** (`document.startViewTransition`, `view-transition-name` unique per element per page; cross-document with `@view-transition { navigation: auto }`), or Motion's `layoutId`. Match aspect ratio and radius, or animate them. Keep it under ~400 ms, make it reversible (back morphs back), and have a plain crossfade as fallback. Only the shared element morphs; the rest of the page fades.
- **Failure**: a card that cuts to a new page with no continuity; two elements sharing the same `view-transition-name`.

## Blurred icon swap
- **Rule**: when an icon changes in place (copy → check, play → pause, menu → close, theme toggle), neither hard-cut nor plain-crossfade it. **Scale, blur and fade** the outgoing and incoming icons so two different shapes read as one object changing state: the blur hides the moment where both glyphs overlap.
- **Apply**:
  - Stack both icons in the same fixed-size box (`display: grid` with both in `grid-area: 1 / 1`, or absolute positioning).
  - Exiting icon: opacity 1 → 0, scale 1 → ~0.25-0.6, blur 0 → 2-4px. Entering icon: the reverse.
  - Duration about **150-200 ms**, ease-in-out or a spring. One `transition` on `opacity, transform, filter`, never `transition: all`.
  - Swap with a changed `key` (React + Motion `AnimatePresence`) or a `data-state` attribute in CSS. Use transitions so rapid clicks retarget (see interruptible animation).
  - Reduced motion: opacity only, no scale or blur.
  - Keep blur small and on small elements: large blurred areas are GPU-costly on low-end phones.
  - The swap is visual only: update the accessible name or announce the state ("Copied") as well.
- **Failure**: an instant swap that flickers; a plain crossfade showing two half-visible glyphs; layout shift because the two icon boxes differ in size.
