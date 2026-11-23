# Web to native patterns

Used at steps 1 and 2: the native equivalent of each web pattern.

| Web pattern | Native pattern | Notes |
|-------------|----------------|-------|
| Top nav / sidebar (top-level sections) | Tab bar (iOS) / navigation bar (Android), 3 to 5 destinations | More than 5: a "More" tab or a drawer on Android only if sections are many and rarely switched |
| Nested routes, breadcrumbs | Stack navigation with back | iOS edge swipe back, Android system back |
| Modal dialog with a form | Full-screen modal (create, edit) or bottom sheet (short task) | Sheets need a clear dismiss and must not lose input |
| Confirmation dialog | Alert (iOS) / dialog (Android); action sheet for destructive choices | Keep text short, destructive action clearly marked |
| Dropdown / select | Native picker, menu, or a selection screen for long lists | Long lists get search |
| Date input | Native date picker | Never a web-style calendar widget |
| Tabs inside a page | Segmented control (iOS) / tabs (Android) | 2 to 4 segments |
| Hover card, tooltip | Long press preview, info button, or visible text | |
| Right-click menu | Context menu on long press, swipe actions | |
| Pagination | Infinite scroll with pull to refresh | Keep scroll position on back |
| Search bar in header | Search in the navigation bar, or a search tab | |
| Toast / flash message | Snackbar (Android) / inline banner or HUD (iOS) | Plus haptic feedback for success or error |
| Email notification | Push notification with deep link to the screen | Ask permission at the moment of value |
| File upload | Photo library, camera, document scanner, Files picker | |
| Copy link | Share sheet | Also accept incoming shares if useful |
| Login with password | Biometrics after first login, passkeys, Sign in with Apple / Google | Store tokens in Keychain / Keystore |
| Settings page | Grouped list screen; system settings for permissions | |
| Footer links (legal, help) | Settings or profile screen | |
| Multi-step wizard on one page | One step per screen, progress, back keeps data | |

Detail: dropdowns, dates and wizards in [forms-and-input.md](forms-and-input.md); pagination, tables and search in [data-and-lists.md](data-and-lists.md); upload, share and login in [native-capabilities.md](native-capabilities.md); email to push in [permissions-and-notifications.md](permissions-and-notifications.md).
