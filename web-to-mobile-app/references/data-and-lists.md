# Data and lists

Used at steps 1 and 2, when a web feature shows a table, a list, a dashboard or charts. The short adapt cases are in [feature-triage.md](feature-triage.md); this file gives the detail.

## Contents
- From table to list
- List, cards or grid
- Filters, sort and search
- Selection and bulk actions
- Swipe actions
- Loading more and scroll
- Charts

## From table to list

Map each column to one role; drop or move the rest to the detail screen.

| Role in the row | Takes | Example (invoices table) |
|-----------------|-------|--------------------------|
| Title | The column users scan for (name, subject) | Client name |
| Subtitle | The second most read column | Invoice number · due date |
| Trailing value | The one number that matters | Amount |
| Badge | A status with few values | Paid / Overdue (text plus color, never color alone) |
| Leading visual | Avatar, thumbnail, icon, if it helps recognition | Client logo |
| Detail screen | Every other column | Lines, taxes, history, notes |

Judgment: 3 to 4 visible values per row at most. Ask the user which column they look at first.

## List, cards or grid

| Layout | Use when |
|--------|----------|
| List | Text-first items scanned quickly (messages, invoices, tasks) |
| Cards | Items with an image plus several fields, or mixed content (feed) |
| Grid | Visual items where the image is the content (photos, products) |
| Grouped list | Sections by date, status or category, with sticky headers |

Tap on a row opens the detail screen (stack push); actions on the row go to swipe or long press.

## Filters, sort and search

| Element | Mobile pattern |
|---------|----------------|
| Filters | Button with active count → sheet with filter controls; active filters as removable chips above the list |
| Sort | Menu or option in the filter sheet; show the current sort |
| Quick filters | Segmented control or chips for 2 to 4 frequent views (All, Mine, Overdue) |
| Search | Search field in the navigation bar; results as you type when the server is fast, else on submit; recent searches |
| No results | "No results" state with the active filters and a "clear filters" action (see `states.md`) |

## Selection and bulk actions

| Rule | Detail |
|------|--------|
| Enter | "Select" button or long press on a row |
| Show | Checkmarks on rows, selected count in the title, "Select all" |
| Act | Bottom action bar with the bulk actions |
| Exit | "Done" / "Cancel", system back on Android |
| Destructive bulk | Confirmation with the count ("Delete 12 invoices?") |

## Swipe actions

| Rule | Detail |
|------|--------|
| Use for | 1 to 3 frequent row actions (archive, mark as read, delete) |
| Always also reachable | Through long press or the detail screen; swipe is a shortcut, not the only path |
| Destructive | Trailing side, red, with undo or confirmation |
| Android | Less standard: keep explicit actions; swipe to dismiss where users expect it |

## Loading more and scroll

| Rule | Detail |
|------|--------|
| Pagination | Cursor based, infinite scroll, load the next page before the end (see `api-for-mobile.md`) |
| Pull to refresh | On every list showing server data |
| Scroll position | Kept when coming back from the detail screen and across tab switches |
| Virtualization | Always for long lists (FlatList / FlashList, `ListView.builder`, `LazyColumn`, `List` / `UICollectionView`) |
| Stable keys | Item IDs as keys so updates do not jump the list |
| New items on top | "New items" pill instead of shifting the content under the finger |

## Charts

| Chart | On a phone |
|-------|-----------|
| Single key number with trend | Best: big number, delta, sparkline |
| Line chart, one or two series | Good, full width |
| Bar chart, few categories | Good; horizontal bars when labels are long |
| Donut / pie | Only 2 to 4 segments, with values in a legend |
| Stacked areas, many series, scatter | Poor: split into several charts or move to the detail screen |
| Data tables inside dashboards | Convert to a list (see above) |
| Multi-widget dashboard | Vertical feed of key metric cards, detail on tap |

| Interaction | Rule |
|-------------|------|
| Read a value | Tap or press-and-drag on the chart shows a tooltip with the value; never hover |
| Period | Segmented control (7D, 30D, 1Y) above the chart |
| Accessibility | Provide the values as text or an accessible summary |
