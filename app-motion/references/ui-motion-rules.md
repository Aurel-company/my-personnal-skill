# UI motion rules

Recommendations with starting values. Adjust for your product and test on real devices. Each rule: **what**, **why**, **how**, **skip when**.

Suggested tokens:

```css
:root {
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);       /* entrances, popovers */
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);   /* moves on screen */
  --ease-in: cubic-bezier(0.5, 0, 0.75, 0);        /* optional, exits that leave */
  --dur-press: 100ms;
  --dur-fast: 150ms;
  --dur-base: 200ms;
  --dur-slow: 300ms;
  --press-scale: 0.97;
}
@media (prefers-reduced-motion: reduce) {
  :root { --dur-fast: 0.01ms; --dur-base: 0.01ms; --dur-slow: 0.01ms; }
}
```

## 1. Ease-out for entrances
- **Why**: a fast start gives instant feedback, a soft landing feels natural. Ease-in on an entrance feels sluggish because the user waits for it to get going.
- **How**: `transition: opacity var(--dur-base) var(--ease-out), translate var(--dur-base) var(--ease-out)`.
- **Skip when**: continuous motion (spinner, progress, marquee) where `linear` is right.

## 2. Dropdowns at 150-250 ms
- **Why**: below 150 ms the change is hard to follow, above 250 ms the menu feels slow on a frequent action.
- **How**: open at 150-200 ms, closed slightly faster. Menus used constantly can be at the low end or instant.

## 3. Stagger list rows by 30 ms
- **Why**: a small offset guides the eye down the list instead of one block popping in.
- **How**: `animation-delay: calc(var(--i) * 30ms)`; cap at about 8 rows (~240 ms total), group the rest. Play it once on entry, not on every re-render.
- **Skip when**: lists used constantly (inbox, command palette), long lists, reduced motion.

## 4. Scale to 0.97 on press
- **Why**: a tiny squash confirms the press physically, within one frame of the touch.
- **How**:
  ```css
  .btn { transition: scale var(--dur-press) var(--ease-out); }
  .btn:active { scale: var(--press-scale); }
  ```
  Keep the hit area stable: put the scale on an inner element or accept it only on `:active`. Use 0.95-0.98; smaller targets can take a stronger squash, large cards a weaker one (0.99).
- **Skip when**: the control is tiny and the shrink makes it feel like it moves away from the finger.

## 5. Stretch moving knobs by 12%
- **Why**: a thumb that elongates in the direction of travel feels elastic and fast, and shows the intent of the move.
- **How**: scaleX to about 1.12 (origin on the trailing edge) during travel, back to 1 on arrival.
  ```css
  @keyframes knob-travel { 50% { scale: 1.12 1; } }
  .switch[data-state] .knob { transition: translate 200ms var(--ease-in-out);
                              animation: knob-travel 200ms var(--ease-in-out); }
  ```
  Keep the height or volume believable; do not stretch the knob's icon or text.
- **Skip when**: the control is very small or rigid-looking.

## 6. Stagger as details settle
- **Why**: when a container arrives and its secondary details (icon, label, badge, buttons) settle a beat later, the main change reads first and the screen feels crafted, not dumped.
- **How**: container at t=0, content at +30-60 ms, small accents at +60-90 ms, same easing. Total stays under about 300 ms.
- **Skip when**: the screen is used constantly or the delay would hide information the user needs now.

## 7. Arcs for object movement
- **Why**: natural motion curves; a straight line between two points looks mechanical.
- **How**: use for an object that travels across the screen (item flying to a cart, a FAB moving, a card dealt to a pile):
  ```css
  .fly { offset-path: path("M0,0 C 80,-120 220,-120 300,0");
         animation: fly 450ms var(--ease-in-out) forwards; }
  @keyframes fly { to { offset-distance: 100%; } }
  ```
  Or animate X and Y on nested elements with different easings.
- **Skip when**: motion is axis-aligned UI (a panel sliding in from an edge, a tab indicator).

## 8. Pulse to confirm success
- **Why**: a single, short pulse tells the user the action worked without a modal or a message.
- **How**: once, 300-400 ms: `@keyframes pulse { 40% { scale: 1.06; } }` on the confirming element, or an expanding ring fading out. Pair with a color or icon change and an accessible announcement.
- **Skip when**: the action is constant-use (do not pulse every row save); never pulse an error.

## 9. Ease-in-out for moves
- **Why**: an element already on screen that changes place accelerates then decelerates, like a real object.
- **How**: `transition: translate var(--dur-base) var(--ease-in-out)` for repositioning, reorder, tab indicator, knob.

## 10. Start popovers at 0.95
- **Why**: scaling from 0.95 (not 0) plus fade feels like a small, quick growth rather than a zoom-in.
- **How**: closed state `opacity: 0; scale: 0.95`, open `opacity: 1; scale: 1`, `ease-out`, ~150 ms.

## 11. Enter from the trigger, exit to the trigger
- **Why**: it tells the user where the layer came from and where it went, which is orientation for free.
- **How**: set `transform-origin` to the trigger point (anchor side, or computed from the trigger rect). Modals launched by a click can originate at the click point; keyboard-launched ones from center.
  ```css
  .popover { transform-origin: var(--origin-x, 50%) var(--origin-y, 0%); }
  ```
- **Skip when**: there is no clear trigger (system toasts), then use the docked edge.

## 12. No bounce on everyday UI
- **Why**: bounce draws attention and costs time. Repeated dozens of times a day it becomes noise and feels toy-like.
- **How**: use critically damped springs (`bounce: 0`) or ease-out curves for frequent UI. Keep overshoot for rare, celebratory or playful moments, and keep it small.
  ```js
  transition={{ type: "spring", duration: 0.3, bounce: 0 }}
  ```

## 13. Do not tween while held
- **Why**: if an element eases toward the pointer while the user is holding or dragging it, it lags and feels disconnected. Direct manipulation must be 1:1.
- **How**: while pressed or dragging, set `transition: none` and write the position directly (pointer events, `transform`); on release, animate to the resting place using the release velocity (spring).
  ```css
  .card[data-dragging="true"] { transition: none; }
  ```

## 14. Make exits 20% shorter
- **Why**: users have decided to move on; a long exit makes the app feel like it is holding them back. Entrances need time to be understood, exits do not.
- **How**: if the entrance is 250 ms, the exit is about 200 ms. Exits can use ease-in or the same ease-out, but stay quick.

## 15. Overlap old and new states
- **Why**: waiting for the old state to leave before the new one enters adds dead time and a flash of empty space. Overlap feels continuous and faster.
- **How**: stack both in the same slot; the new one fades/moves in while the old one leaves, offset by 0-50 ms. In React with Motion: `AnimatePresence mode="popLayout"` rather than `mode="wait"`. For icon or text swaps, add a small blur to hide the overlap.
- **Skip when**: the two states must never be seen together (rare).

## 16. Masks for reveal and color
- **Why**: a mask reveals new content (or a new color) from a place, with a direction, instead of a flat fade. It carries meaning: "this came from here".
- **How**: `clip-path` or `mask-image` wipes for content reveals, progress fills and tab underlines; for a theme or color change, a circular reveal from the toggle with view transitions:
  ```js
  document.startViewTransition(() => setTheme(next));
  // CSS: ::view-transition-new(root) { animation: reveal 400ms var(--ease-in-out); }
  // @keyframes reveal { from { clip-path: circle(0 at var(--x) var(--y)); }
  //                     to   { clip-path: circle(150% at var(--x) var(--y)); } }
  ```
  Provide a plain crossfade fallback.
- **Skip when**: reduced motion (use an instant or crossfade change).

## 17. Interruptibility and reduced motion (always)
- Use transitions or springs so a reversed state continues from the current value; never block input during an animation.
- Under `prefers-reduced-motion`, drop translate, scale and blur; keep opacity and color changes so the feedback stays.
