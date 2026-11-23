# Accessibility on mobile

Used at steps 4 and 5: what each screen and state must support for VoiceOver, TalkBack, large text and reduced motion. Minimum touch target sizes: [platform-conventions.md](platform-conventions.md).

## Text size

| Rule | iOS | Android |
|------|-----|---------|
| Text scales with the system setting | Dynamic Type text styles, including accessibility sizes | `sp` units, respect font scale (up to 200 % from Android 14) |
| Layout survives the largest size | Rows wrap to several lines, horizontal stacks become vertical, nothing truncated that matters | Same; test at the largest font and display size |
| No text in images | Real text for labels and buttons | Same |
| Fixed-size exceptions | Tab bar labels and small chrome may cap their size; offer a large content viewer on long press for tab items | Keep caps rare |

## Screen readers

| Rule | Detail |
|------|--------|
| Label | Every interactive element has a short name ("Delete invoice", not "button" or the icon name) |
| Hint | Only when the result is not obvious ("Opens the invoice"); not repeated on every row |
| Traits / role | Button, link, header, selected, disabled, adjustable: set by the native component or added explicitly on custom views |
| Value and state | Toggles, sliders and progress expose their value ("Notifications, on") |
| Grouping | A list row reads as one element ("Anna, Can we move to 3 pm, 2 min ago"), not five fragments |
| Custom actions | Swipe and long-press actions are also exposed as accessibility actions (rotor actions / TalkBack actions) |
| Focus order | Follows the visual reading order; after navigation, focus goes to the screen title |
| Changes announced | Errors, toasts and loading completion are announced; new screens and sheets move focus |
| Modals and sheets | Content behind is hidden from the screen reader; a close action is reachable |
| Decorative images | Hidden from the screen reader |
| Headers | Section titles marked as headers for quick navigation |

## Visual

| Rule | Detail |
|------|--------|
| Contrast | At least 4.5:1 for body text, 3:1 for large text and essential icons and borders (WCAG); check in light and dark mode |
| Color never alone | Status, errors and chart series also carry text, an icon or a pattern |
| Bold text / increase contrast | Respect the system settings when the design uses thin weights or translucent surfaces |
| Focus visible | For hardware keyboards and switch access |

## Motion and media

| Rule | Detail |
|------|--------|
| Reduce motion | When the setting is on, replace large movements, parallax and zooms with fades or nothing |
| No autoplay of flashing content | Never more than 3 flashes per second |
| Video | Captions for speech; transcripts for audio-only content |
| Timers | No action that expires without a way to extend it |

## Touch

| Rule | Detail |
|------|--------|
| Target size | Platform minimums (see `platform-conventions.md`), larger hit area than the visual if needed |
| Gestures | Every gesture (swipe, long press, drag, pinch) has a visible alternative |
| Shake, tilt | Never the only way to do something |

## Device test checklist

Run on a real device for each core screen and its states.

| # | Check |
|---|-------|
| 1 | VoiceOver and TalkBack: reach and activate every element in order, with understandable labels |
| 2 | Each list row reads as one element; swipe actions available as custom actions |
| 3 | Largest text size: nothing important truncated or overlapping, every action reachable |
| 4 | Dark mode and increased contrast: text readable, states distinguishable |
| 5 | Reduce motion on: no large movement |
| 6 | Errors and toasts announced; focus lands on the new screen or sheet |
| 7 | Hardware keyboard (iPad, Chromebook): tab order and visible focus |
| 8 | Grayscale: statuses still distinguishable |
