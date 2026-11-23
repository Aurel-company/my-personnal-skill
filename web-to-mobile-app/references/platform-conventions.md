# iOS and Android conventions

Used at step 4. Keep only what applies to the screens in the graph. Add missing conventions here (block plus one index line), from the official guidelines.

## Navigation and back
| Topic | iOS (HIG) | Android (Material 3) |
|-------|-----------|----------------------|
| Top-level | Tab bar at the bottom, labels always visible | Navigation bar at the bottom (3 to 5); navigation rail on large screens; drawer for many destinations |
| Back | Back button in the navigation bar, edge swipe from the left | System back gesture or button, plus up arrow in the top app bar; predictive back animation |
| Back on a root tab | Nothing; tapping the active tab scrolls to top / pops to root | System back exits the app or returns to the start tab |
| Titles | Large title on root screens collapsing on scroll, inline on pushed screens | Top app bar: small, center, medium or large; collapses on scroll |
| Modals | Sheets (page sheet, detents), close / cancel at top left, confirm at top right | Full-screen dialog with close at top left and action at top right; bottom sheets (modal or standard) |

## Controls
| Topic | iOS | Android |
|-------|-----|---------|
| Primary action | Button in the navigation bar or in content; no floating button by convention | Floating action button for the main create action, or a bottom app bar |
| Menus | Pull-down menus, context menus on long press, action sheets for choices | Menus, context menus, bottom sheets for choices |
| Toggles | Switch | Switch |
| Segments | Segmented control | Segmented buttons, tabs |
| Pickers | Wheel or compact date picker, menus | Material date and time pickers, exposed dropdown menus |
| Alerts | Alert with 1 to 2 buttons, destructive in red | Dialog with text buttons, actions at the bottom right |
| Feedback | Haptics (impact, notification), HUD or inline | Snackbar with optional action, haptics |
| Swipe on rows | Leading and trailing swipe actions, full swipe | Less standard; prefer explicit actions, swipe-to-dismiss where expected |

## Layout and touch
| Topic | iOS | Android |
|-------|-----|---------|
| Minimum target | 44 × 44 pt | 48 × 48 dp |
| Safe areas | Respect notch, Dynamic Island and home indicator | Edge-to-edge with system bar insets (enforced from Android 15 for apps targeting it) |
| Text size | Dynamic Type, text styles (Body 17 pt) | Font scale in sp, type scale (Body large 16 sp) |
| Typeface | SF Pro (system) | Roboto / system font, or brand via the type scale |
| Icons | SF Symbols | Material Symbols |
| Color | Semantic system colors, light and dark | Dynamic color (Material You) optional, light and dark |

## System integration
| Topic | iOS | Android |
|-------|-----|---------|
| Permissions | Purpose string required; ask in context; one chance before Settings | Runtime permissions; rationale after a denial; notification permission from Android 13 |
| Push | APNs; provisional authorization possible | FCM; notification channels per category |
| Auth | Face ID / Touch ID, passkeys, Sign in with Apple (required if other social logins are offered, with exceptions) | Biometric prompt, passkeys / Credential Manager, Google sign-in |
| Storage of secrets | Keychain | Keystore / encrypted storage |
| Links | Universal Links | App Links |
| Sharing | Share sheet, share extension | Sharesheet, intent filters |
| Widgets and shortcuts | WidgetKit, Home Screen quick actions, App Intents | App widgets, app shortcuts |
| In-app purchase | App Store payment rules for digital goods | Google Play billing rules for digital goods |

## What to share across platforms
Brand colors, illustrations, content, information architecture, screen list, iconography style, copy and states. Let back behavior, navigation chrome, pickers, alerts, sheets and typography defaults follow each platform.
