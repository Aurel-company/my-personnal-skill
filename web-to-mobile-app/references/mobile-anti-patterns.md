# Mobile anti-patterns

Used at step 6 (contract review) and when reviewing an existing mobile plan or app: signs that the app "feels like a website". Severities follow the Review format in `SKILL.md`: **P0** breaks a task or a platform rule users rely on, **P1** works but feels like a website, **P2** polish. Severities are judgment; raise one when the pattern hits a core task.

| # | Anti-pattern | Symptom | Why it hurts | Fix | Severity |
|---|--------------|---------|--------------|-----|----------|
| 1 | Hamburger for all navigation | Every destination behind a ☰ menu | Hidden destinations are used less; two taps for everything | Tab bar / navigation bar with 3 to 5 top-level destinations; drawer only for many rare sections (Android) | P1 |
| 2 | Modal on modal | A dialog opens another dialog or sheet | User loses context and the way back | Push a screen inside the modal flow, or a single sheet | P1 |
| 3 | Web pickers and dates | HTML-style dropdowns, calendar widgets, custom selects | Small targets, wrong keyboard, unfamiliar | Native date / time pickers, menus, selection screen with search for long lists (see `web-to-native-patterns.md`) | P1 |
| 4 | Hover-only action | Actions appear on hover (row buttons, tooltips, previews) | No hover on touch: the action is unreachable | Visible button, swipe actions, long-press context menu | P0 |
| 5 | Screen without a way back | No back button, system back ignored or exits unexpectedly | User is stuck or loses the app | Back in the navigation bar, edge swipe (iOS), system back handled (Android) | P0 |
| 6 | Input lost on interruption | Call, app switch or OS kill wipes a form | Users are interrupted constantly on mobile | Persist drafts, restore state after process death | P0 |
| 7 | Targets too small | Links and icons under 44 pt / 48 dp, close together | Mis-taps, frustration, accessibility failure | Minimum target size, spacing, larger hit areas than visuals | P1 |
| 8 | Text that does not scale | Fixed font sizes, layout breaks at large text | Fails users who need larger text | Dynamic Type / sp, layouts that wrap and scroll | P1 |
| 9 | Full-screen spinner on every navigation | Blank screen with a spinner before each page | Feels slow, hides content already known | Skeletons, cached data first, prefetch, optimistic updates | P1 |
| 10 | Numbered pagination | "Page 1 2 3 … Next" at the bottom of lists | Tiny targets, loses scroll position | Infinite scroll with pull to refresh, position kept on back | P1 |
| 11 | Webview for key screens | Core screens are the website in a webview | Web navigation, no native states, slow, risk of store rejection for minimum functionality | Native screens for core features; webview only for rare content (legal, help) | P1, P0 if the app is mostly webviews |
| 12 | Links that open the browser | Tapping in-app content leaves for Safari / Chrome | User leaves the app, loses context and login | Route through the mapping in `deep-linking.md`; in-app browser (SFSafariViewController / Custom Tabs) only for external sites | P1 |
| 13 | Permission at first launch | Notification, location or camera prompt before any value | Users refuse; on iOS a refusal is hard to undo | Ask in context, at the moment of value, with a pre-prompt explaining why | P1 |
| 14 | Table with horizontal scroll | Wide data table squeezed into the screen | Unreadable, scroll conflicts | Cards with 2 to 3 key fields, detail screen, filters in a sheet (see `feature-triage.md`) | P1 |
| 15 | Website footer | Legal, social and sitemap links at the bottom of screens | Wastes space, web pattern | Move to settings or profile | P2 |
| 16 | Same chrome on both platforms | iOS back arrow on Android, Material FAB copied on iOS | Feels foreign on one platform | Shared design language, platform navigation chrome (see `platform-conventions.md`) | P2 |
| 17 | Login wall before any value | App opens on a login form with no context | Drop-off at first launch | Value screens first or guest mode when possible; biometrics or passkeys after first login | P1 |
| 18 | Toast as the only feedback for errors | Error flashes and disappears | Missed, especially with screen readers | Inline error near the cause, snackbar with retry, haptic | P1 |
| 19 | Keyboard covers inputs | Focused field or submit button hidden by the keyboard | Users cannot see what they type or submit | Scroll to focused field, keyboard-aware layout, correct keyboard type and return key | P1 |
| 20 | No pull to refresh on feeds | List only refreshes by leaving and coming back | Expected gesture missing | System refresh control | P2 |

Report each finding in the Review format: **screen or feature → problem → anti-pattern # → fix**, with its severity.
