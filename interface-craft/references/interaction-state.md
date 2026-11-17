# Interaction and state

## Affordance
- **Rule**: an element should **look like what it does**. Clickable things look clickable; editable things look editable; draggable things show a grip.
- **Apply**: buttons have shape, contrast and a pressed state; links are distinguishable beyond color; inputs have visible borders or fills; `cursor: pointer` on desktop targets; every interactive element has hover, focus-visible, active and disabled states. Do not use the same style for a button and a label. Icons alone get a label or tooltip unless universal (close, search). Hidden gestures (swipe, long-press) need a visible alternative.
- **Failure**: flat text that is secretly a button; a "disabled" look on an active control.

## Combobox
- **Rule**: use a **combobox** (input + filterable list) instead of a plain select when there are **more than ~7–10 options** or users know what they want and can type it.
- **Apply**: follow the ARIA APG pattern: `role="combobox"` on the input, `aria-expanded`, `aria-controls`, `aria-activedescendant`, `role="listbox"` / `role="option"`. Keyboard: ↓/↑ move, Enter selects, Esc closes (and clears on second press), Home/End, typing filters. Highlight the matched substring, show an empty state ("No results for …"), keep focus in the input, and debounce async search (150–250 ms) with a loading state. Distinguish *select-only* (must pick from list) from *editable* (free text allowed). Use a library (Radix, Headless UI, React Aria, Base UI) rather than hand-rolling.
- **Failure**: a native `<select>` with 200 countries and no search; a list that cannot be used with the keyboard.

## Optimistic update
- **Rule**: for actions that **almost always succeed** (like, toggle, reorder, add to list, rename), update the UI **immediately** and reconcile with the server afterwards.
- **Apply**: apply the change locally → send the request → on success keep (swap in server data/IDs) → on failure **roll back to the previous state and tell the user** (toast with retry). Keep a snapshot for rollback, guard against out-of-order responses, and make the request idempotent. Show a subtle pending state only for slow cases. **Do not** use it for payments, deletions that cannot be undone, or when the outcome depends on server validation.
- **Failure**: a spinner on a "like" button; a silent rollback that leaves the user confused.

## Progressive disclosure
- **Rule**: show only what is needed **now**; reveal the rest on demand, in a way that is easy to find.
- **Apply**: primary action and the common 80% case up front; advanced options behind "More options", an accordion, a drawer, or a second step. Label the disclosure clearly ("Advanced settings"), keep it keyboard accessible (`<details>`, `aria-expanded`), preserve state if the user collapses and reopens, and never hide something essential to completing the task. Wizards for long forms; defaults for the rest. Limit depth to about two levels.
- **Failure**: a settings page showing 40 controls at once; critical options buried three levels deep.

## Layout shift
- **Rule**: **nothing already on screen should move** because something else loaded or changed. Target **CLS < 0.1**.
- **Apply**:
  - Reserve space: `width`/`height` or `aspect-ratio` on images, video, embeds, ads, avatars.
  - Skeletons with the **same dimensions** as the final content.
  - Reserve room for error messages, banners and validation text (or overlay them).
  - Load web fonts with `font-display: swap` plus a fallback with matched metrics (`size-adjust`, `ascent-override`) — links to x-height above.
  - Use tabular numbers so counters do not resize.
  - Add content **below** the viewport or in response to a user action, never above what the user is reading; use `overflow-anchor` / scroll anchoring for prepended items.
  - Animate `transform` and `opacity`, not `width`, `height`, `top`, `left`.
  - Show a scrollbar gutter: `scrollbar-gutter: stable`.
- **Failure**: the button you were about to tap jumps down because an image loaded; a banner pushing the page after first paint.
