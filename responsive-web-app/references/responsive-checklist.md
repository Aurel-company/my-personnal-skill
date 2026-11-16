# Responsive checklist (English, for the AI)

Sources are numbered `[n]` and listed in [sources.md](sources.md). Items without a source are **judgment** (practitioner convention or general knowledge): apply as defaults, adapt to the product.

## 1. Foundations

- Viewport meta: `<meta name="viewport" content="width=device-width, initial-scale=1">`. Never `user-scalable=no` or `maximum-scale=1`.
- Mobile-first: base styles for small screens, enhance with `@media (min-width: …)`.
- `*, *::before, *::after { box-sizing: border-box; }`.
- Media never overflows: `img, video, svg { max-width: 100%; height: auto; }`.
- Breakpoints few and content-driven (where the layout breaks). Express in `em`/`rem` when possible so they follow user font size. (judgment)
- Relative units for text and spacing; pixels for borders only.

## 2. Layout

### Intrinsic first
```css
.grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(min(18rem, 100%), 1fr));
}
```
The `min(18rem, 100%)` keeps a track from forcing overflow on a narrow container.

### Media queries or container queries [3]
- **Media query**: layout follows the viewport (cart moves above the list or into a sidebar).
- **Container query**: a component adapts to the space it has, because it appears in several places.
- Most apps use both.

```css
.card-wrapper { container-type: inline-size; }
@container (min-width: 30rem) {
  .card { display: grid; grid-template-columns: 1fr 2fr; }
}
```
Pitfalls [3]:
- An element cannot measure its own container: `25cqi` on a container resolves against the nearest ancestor container.
- A grid cell cannot be the container; use an inner element.
- Custom elements default to `display: inline`: set a `display`.
- Without a defined container, `cqi` falls back to the small viewport.

### Preventing horizontal overflow [4][5][6]
| Cause | Fix |
|---|---|
| `width: 100vw` (includes the classic scrollbar width; `100dvw`/`100svw` do not subtract it either) | Use `width: 100%`, or remove the declaration. `width: stretch` exists but has limited support |
| Flex child will not shrink below its minimum content | `min-width: 0` (or `overflow` other than `visible`) on the child, then choose wrap, clip or scroll |
| Grid track will not shrink | `minmax(0, 1fr)` instead of `1fr` |
| Truncated text does not truncate | `min-width: 0; overflow: hidden; text-overflow: ellipsis; white-space: nowrap` |
| Wide table pushes the page | Wrap in an `overflow-x: auto` element |
| Long unbroken strings, `white-space: nowrap`, fixed widths | `overflow-wrap: anywhere` (or `word-break`), avoid fixed widths |

Diagnose before fixing: find the element whose right edge exceeds the viewport width, fix its cause. Do not add `overflow-x: hidden` on `body` to hide it. (judgment)

## 3. Type and spacing

- Fluid type with `clamp()` and font-relative bounds [1][2]:
  ```css
  h1 { font-size: clamp(2rem, 1rem + 5vw, 4rem); }
  ```
- **Never `vw` alone** for font size [1].
- **Max no more than 2.5x min**, so 200% browser zoom still works (WCAG 1.4.4) [1].
- Keep the `rem` part near 1 and the viewport part low so zoom keeps working [2].
- Line length around 60-75 characters (`max-inline-size: 70ch`). (judgment)
- `text-wrap: balance` for short blocks (headings, captions); browsers may ignore it on long blocks [9].
- Spacing relative to line height with `lh`/`rlh`, or to the container with `cqi`, when it should adapt [2].

## 4. Mobile viewport behavior

- **Not `100vh`** for full-height areas: it ignores the collapsing browser bar [1][7].
  - `100svh` = stable (bar shown), `100dvh` = follows the bar, `100lvh` = bar hidden.
  - `dvh` can resize during scroll; prefer `svh` when stability matters [1][7].
- **Safe areas** [7]:
  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
  ```
  ```css
  .bottom-nav { padding-bottom: env(safe-area-inset-bottom); }
  ```
  Without `viewport-fit=cover`, `env()` returns 0.
- **Virtual keyboard** [8]: add `interactive-widget=resizes-content` to the viewport meta to keep a fixed bottom bar above the keyboard. Default is `resizes-visual` (fixed elements can be covered). Supported in Chrome 108+ and Firefox 132+; Safari support not verified. Test on every target browser.
- `scrollbar-gutter: stable` on scroll containers to avoid layout shift when a scrollbar appears [9].
- Modals: `overscroll-behavior: contain` on the scrollable body so scroll does not leak to the page [7].

## 5. Input and touch

- **Target size**: WCAG 2.2 AA 2.5.8 requires at least **24x24 CSS px** [10]. Exceptions: spacing (a 24px circle centered on the target does not touch another target), equivalent control, inline link in text, user-agent control left unmodified, essential size. Aim for **44x44 px** on primary controls (2.5.5, AAA, recommended) [10][7].
- Grow the hit area with `padding`, not margin [7].
- **Hover** [11]:
  ```css
  @media (hover: hover) { .row:hover { background: var(--hover); } }
  ```
  `pointer: coarse` is for enlarging targets, not for hover decisions. Hybrid laptops can switch modes: use `any-hover` / `any-pointer` for defensive checks. Never put a function behind hover only.
- **Inputs at 16px minimum** or iOS Safari zooms on focus; do not disable zoom instead [7].
- Right keyboard per field: a suitable `type`, plus `inputmode`, `autocomplete`, `enterkeyhint` [7][13]:
  ```html
  <input type="email" inputmode="email" autocomplete="email" enterkeyhint="done">
  ```
  Use `inputmode="numeric"` for digits only, `"decimal"` for amounts. Avoid `type="text"` for everything.
- `touch-action: manipulation` on controls removes double-tap zoom and the tap delay while keeping pan and pinch [9].

## 6. Components

### Navigation [12]
- **Phone**: bottom tab bar, 3 to 5 primary destinations of equal weight, icon plus label, 44px targets, clear active state. Bottom edge is the easiest thumb zone.
- **Tablet**: sidebar collapsed to an icon rail, or fewer items.
- **Desktop**: full sidebar with visible labels.
- **Hamburger or drawer**: secondary items only, or when a tab bar is impossible. It lowers discoverability.
- Never just hide navigation on small screens: give an alternative (full menu, bottom bar for key destinations, search).
- Use familiar patterns; innovate on content, not wayfinding.
- Breakpoint numbers (for example 1024 and 768) are a suggestion from one source, not a standard: derive them from the layout.

### Data tables [14]
Choose by use case:
- **Comparison-heavy / dense**: keep the table in a horizontal scroll container (`overflow-x: auto`), keep the key column visible (sticky first column).
- **Content-like rows with no cross-row comparison**: stack each row as a card, with label and value pairs.
- **Many columns**: priority columns (hide the rest behind a toggle) or tap to expand the row.
- Large sets: pagination, sort, filter, search; persist the state.
- Keep heavy collapsible sections closed by default on mobile (scroll and memory cost on mid-tier phones).
- Keep real table semantics for accessibility; if the layout is converted to cards, keep the header association.
- WCAG reflow exempts data tables as a whole, but not their individual cells [10].

### Forms [13]
- **One column**, labels above fields. Side-by-side fields give cramped labels and awkward focus when the keyboard opens.
- No placeholder as label: it disappears on input and usually fails contrast.
- Long forms: split into steps of about 2 to 4 related fields, large targets, clear progress.
- Validation next to the field, in plain language; keep the focused field visible above the keyboard.
- Several statistics in the sources come from form-builder vendors: not verified.

### Modals vs full-screen (judgment, no source)
- A long or form-heavy modal on a phone usually works better as a full-screen page or a bottom sheet; short confirmations stay modals.
- If it stays modal: `overscroll-behavior: contain`, trapped and restored focus, a close control within thumb reach, safe-area padding.

### Images [15]
- `srcset` + `sizes` to switch resolution; `<picture>` only for art direction (different crops).
- A `sizes` value too large downloads too much; too small blurs. Keep an `<img>` fallback.
- Reserve space with `aspect-ratio` or `width`/`height` to prevent layout shift [1]:
  ```css
  img, video { aspect-ratio: 16 / 9; width: 100%; height: auto; }
  ```

## 7. Accessibility tied to responsive

- **Reflow (1.4.10 AA)** [10]: content works without loss of information or function and without two-dimensional scrolling at **320 CSS px** wide (equivalent to 1280px at 400% zoom) for vertical-scrolling content, and at 256px high for horizontal-scrolling content. Exceptions: parts that need two-dimensional layout (maps, diagrams, video, games, presentations, data tables as a whole, toolbars that must stay in view).
- **Text spacing (1.4.12 AA)** [16]: still usable with line-height 1.5x, paragraph spacing 2x, letter spacing 0.12x, word spacing 0.16x of font size. Avoid fixed heights that clip.
- **Orientation (1.3.4 AA)** [16]: do not lock portrait or landscape unless essential.
- **Resize text (1.4.4)** to 200% [1].
- Honor `prefers-reduced-motion` for animations.
- Visible focus at every size.

Items [16] come from secondary summaries; confirm thresholds against the WCAG 2.2 Understanding documents before a conformance claim.

## 8. Testing

- 320px wide; 400% zoom at 1280px; landscape; widths 375, 768, 1024, 1440.
- Stress content: longest label, long translation, empty, many rows, long unbroken string.
- Text-spacing override bookmarklet or user stylesheet.
- Keyboard only; both themes; reduced motion.
- **Real devices**: DevTools emulation does not simulate browser address-bar behavior, safe-area insets or iOS Safari CSS quirks [7].
- If something was not tested, say it.
