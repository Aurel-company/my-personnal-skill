# Feature triage

Used at step 1. Every web feature gets exactly one verdict.

## Verdicts

| Verdict | Meaning | When |
|---------|---------|------|
| **Keep** | Same behavior, mobile UI | The task already fits a short, one-handed session (view, approve, reply, search, toggle). |
| **Adapt** | Same goal, different interaction | The goal matters on mobile but the web interaction does not work there (hover, dense table, multi-column, drag-and-drop on a large canvas, keyboard shortcuts, long form). |
| **Replace** | Same need, different feature | A native capability serves the need better (file upload → camera / document scanner, copy link → share sheet, email digest → push, password → biometrics). |
| **Drop** | Not in the mobile app | Rare, heavy, admin or desktop-bound tasks (bulk editing, complex configuration, exports, back-office). Keep a "continue on desktop" path if users may need it. |
| **Add** | Mobile-only | Push notifications, biometrics, camera, location, share sheet in and out, widgets, offline, quick actions, deep links. |

## Questions to decide

1. Would a user do this on a phone, standing, in under two minutes? If not, adapt it or drop it.
2. Does it depend on hover, right click, a keyboard, a wide screen or precise pointing? Then it must be adapted.
3. Does it need more than one screen of input? Split it into steps, prefill, or move part of it to a native capability.
4. Is there a native capability that does it better? Then replace.
5. How often is it used, and by whom? Rare plus admin usually means drop.

## Common adapt cases

| Web problem | Mobile problem | Typical solution |
|-------------|----------------|------------------|
| Wide data table | Unreadable, horizontal scroll | List of cards with 2 to 3 key fields, detail screen, filters in a sheet |
| Sidebar plus content | No room for both | Tabs for top level, stack navigation for depth |
| Hover tooltips and previews | No hover | Visible label, long press, or a detail screen |
| Right-click menu | No right click | Long press context menu, swipe actions, overflow menu |
| Keyboard shortcuts | No keyboard | Primary actions in reach, quick actions, search |
| Long form on one page | Fatigue, keyboard covers fields | Steps, prefill, autofill, native pickers, save draft |
| Drag-and-drop board | Small targets, scroll conflicts | Move via action sheet, or long-press drag with handle |
| Dashboard with many widgets | Too dense | One key metric per card, vertical feed, detail on tap |
| Multi-select bulk actions | Fiddly | Edit mode with selection, bottom action bar |
| Modals stacked on modals | Lost context | Push a screen, or a single sheet |

## Priority

- **Core**: the reasons a user opens the app; they go into wave 1.
- **Secondary**: useful but not daily; wave 2.
