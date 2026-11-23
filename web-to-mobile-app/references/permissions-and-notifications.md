# Permissions and notifications

Used at steps 4 and 5: when and how to ask for each permission, what happens on refusal, and how to design notifications. Which capabilities to add and their cost: [native-capabilities.md](native-capabilities.md). Push deep links: [deep-linking.md](deep-linking.md).

## Asking rules

| Rule | Detail |
|------|--------|
| In context | Ask when the user starts the action that needs it (tap "Scan", enable reminders), never at first launch |
| Pre-prompt | One app screen or sheet before the system prompt: what, why, benefit, "Continue" / "Not now". "Not now" does not trigger the system prompt, so the one chance is not spent |
| Smallest scope | Coarse before precise, when-in-use before always, selected photos before full library |
| Degraded mode | The feature still works partly without the permission when possible (manual address, photo picker) |
| Purpose text | iOS usage description strings are specific ("to scan receipts for your expenses"), not generic |

## Per permission

| Permission | When to ask | iOS | Android |
|------------|-------------|-----|---------|
| Notifications | After a first success that notifications extend (first order, first conversation), or when the user enables a reminder | One system prompt; provisional authorization delivers quietly without asking | Android 13+: `POST_NOTIFICATIONS` runtime prompt; before 13, on by default |
| Camera | Tap on a capture action | `NSCameraUsageDescription` | `CAMERA`; not needed when using the system camera app intent |
| Photos | Prefer the system picker (no permission) | PHPicker needs none; library access offers "limited" selection | Photo Picker needs none; Android 14+ partial access (`READ_MEDIA_VISUAL_USER_SELECTED`) |
| Location | Tap on "near me" or an address field; background only after foreground was useful | When-in-use first, "Always" later; precise location can be turned off by the user | Coarse / fine (user can choose approximate from Android 12); background requested separately and opens settings (Android 11+) |
| Contacts | Tap on "invite from contacts"; prefer the system contact picker | Full or limited access (iOS 18+) | `READ_CONTACTS` |
| Tracking (ATT) | Only if the app tracks users across other companies' apps or sites; before any tracking | `AppTrackingTransparency` prompt, required to access the IDFA; pre-prompt allowed but must not mislead | No equivalent prompt; Advertising ID can be reset or deleted by the user; `AD_ID` permission declared for apps targeting Android 13+ that use it |
| Microphone | Tap on record or call | `NSMicrophoneUsageDescription` | `RECORD_AUDIO` |

## Refusal and the way to settings

| | iOS | Android |
|---|---|---|
| After a refusal | The system prompt never shows again; only Settings can change it | The prompt can show again; after repeated denials (twice from Android 11) it stops showing |
| Detect when to explain | Check the authorization status (`denied`) | `shouldShowRequestPermissionRationale` returns true after one denial |
| Way to settings | Button opening the app's settings page (`openSettingsURLString`) | Button opening the app details settings screen |
| Screen behavior | Show the permission-denied state (see `states.md`): what is missing, why, button to settings, degraded mode | Same |
| Re-check | On app resume, re-read the status and update the screen | Same |

## Notification types

| Type | Examples | Default | Frequency |
|------|----------|---------|-----------|
| Transactional | Order shipped, payment failed, code to log in | On | As events happen |
| Social / activity | New message, mention, reply, invitation | On, adjustable per type | Grouped when bursts happen |
| Reminders | Due date, appointment, unfinished task | Set by the user | As set |
| Marketing | Promotions, new features, re-engagement | Off until the user opts in explicitly | Rare; capped |

App Store rules forbid using push for marketing without explicit opt-in and require a way to opt out in the app. Judgment: caps per day and quiet hours for non-transactional types.

## iOS categories and Android channels

| Need | iOS | Android |
|------|-----|---------|
| Per-type user control | In-app settings per type (the system only offers app-level control) | One notification channel per type; the user can disable each channel in system settings |
| Actions in the notification | Notification categories with actions (Reply, Mark as done) | Notification actions, direct reply |
| Urgency | Interruption levels: passive, active, time-sensitive, critical (entitlement required) | Channel importance; the app cannot raise it after the channel is created |
| Grouping | Thread identifier | Notification groups |

Define the channel / category list in the contract (section 4), one row per notification type.

## A good notification

| Element | Rule |
|---------|------|
| Title | Who or what ("Anna", "Order #1042") |
| Body | The actual content, readable without opening the app ("Anna: Can we move to 3 pm?"); no "You have a new notification" |
| Sensitive data | Hide content on the lock screen when private (health, finance, codes visible only when unlocked) |
| Tap | Deep link to the exact screen, handled from cold start |
| Actions | 1 to 2 quick actions when they avoid opening the app |
| Badge | Count of items that need action, kept in sync and cleared when read |
| Language | User's language, sent from the server with the user's locale |

## Silent notifications

| | iOS | Android |
|---|---|---|
| Mechanism | Background push (`content-available`) | FCM data message |
| Use for | Refresh data or invalidate a cache before the user opens the app | Same |
| Limits | Throttled, not guaranteed, not delivered when the user force-quit the app | Delivery may be delayed by Doze and app standby; high priority is limited |
| Never | Rely on it for anything the user must see; use a visible notification | Same |
