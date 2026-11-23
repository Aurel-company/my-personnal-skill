# Sources

| Source | Used for | Reliability |
|--------|----------|-------------|
| [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) | iOS navigation, controls, targets, typography, permissions | Official |
| [Material Design 3](https://m3.material.io/) | Android navigation, components, type scale, targets | Official |
| [Android developers: edge-to-edge, predictive back, permissions](https://developer.android.com/) | Insets, back behavior, runtime permissions | Official |
| [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/) | Sign in with Apple, payments, minimum functionality | Official, changes often |
| [Google Play policies](https://play.google.com/about/developer-content-policy/) | Billing, permissions policy | Official, changes often |
| [Apple: Supporting universal links](https://developer.apple.com/documentation/xcode/supporting-universal-links-in-your-app) | apple-app-site-association, associated domains | Official |
| [Android: App Links](https://developer.android.com/training/app-links) | assetlinks.json, verified intent filters | Official |
| [Android: Principles of navigation](https://developer.android.com/guide/navigation/principles) | Back stack after a deep link | Official |
| [Android: Build an offline-first app](https://developer.android.com/topic/architecture/data-layer/offline-first) | Offline levels, sync, conflict resolution | Official |
| [Apple: ActivityKit](https://developer.apple.com/documentation/activitykit) | Live Activities | Official |
| [Apple: WidgetKit](https://developer.apple.com/documentation/widgetkit) | Widgets, refresh budget | Official |
| [Android: App shortcuts](https://developer.android.com/develop/ui/views/launch/shortcuts) | Static and dynamic shortcuts | Official |
| [Android: Location permissions](https://developer.android.com/training/location/permissions) | Foreground and background location | Official |
| [Android: Photo picker](https://developer.android.com/training/data-storage/shared/photopicker) | Image selection without permission | Official |
| [Apple: VisionKit](https://developer.apple.com/documentation/visionkit) / [ML Kit Document Scanner](https://developers.google.com/ml-kit/vision/doc-scanner) | Document scanning | Official |
| [Apple: Passkeys](https://developer.apple.com/passkeys/) / [Android: Credential Manager](https://developer.android.com/identity/sign-in/credential-manager) | Passkeys, associated domains | Official |
| [Apple Pay HIG](https://developer.apple.com/design/human-interface-guidelines/apple-pay) / [Google Pay API](https://developers.google.com/pay/api) | Native payment | Official |
| Web frameworks: [Next.js](https://nextjs.org/docs), [React Router](https://reactrouter.com/), [Vue Router](https://router.vuejs.org/), [Nuxt](https://nuxt.com/docs), [Angular](https://angular.dev/), [SvelteKit](https://svelte.dev/docs/kit), [Rails](https://guides.rubyonrails.org/routing.html), [Laravel](https://laravel.com/docs), [Django](https://docs.djangoproject.com/) | Where routes, layouts and permissions live (web app discovery) | Official |
| [Expo docs](https://docs.expo.dev/) / [React Native docs](https://reactnative.dev/docs/getting-started) / [Flutter docs](https://docs.flutter.dev/) / [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html) | Stack choice, OTA updates, code sharing | Official, changes often |
| [Apple: textContentType](https://developer.apple.com/documentation/uikit/uitextinputtraits/textcontenttype) / [Android: Autofill](https://developer.android.com/guide/topics/text/autofill-optimize) / [MDN: autocomplete](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete) | Keyboards and autofill per field | Official |
| [Android: Request runtime permissions](https://developer.android.com/training/permissions/requesting) | Permission flow, rationale, repeated denial | Official |
| [Apple: App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) | ATT prompt | Official |
| [Apple: UserNotifications](https://developer.apple.com/documentation/usernotifications) / [Android: Notification channels](https://developer.android.com/develop/ui/views/notifications/channels) | Categories, interruption levels, channels, background push | Official |
| [Apple: Accessibility HIG](https://developer.apple.com/design/human-interface-guidelines/accessibility) / [Android: Accessibility](https://developer.android.com/guide/topics/ui/accessibility) / [WCAG 2.2](https://www.w3.org/TR/WCAG22/) | Text size, screen readers, contrast, motion | Official |
| [RFC 8252: OAuth 2.0 for Native Apps](https://www.rfc-editor.org/rfc/rfc8252) / [RFC 9700: OAuth 2.0 Security BCP](https://www.rfc-editor.org/rfc/rfc9700) | Mobile auth flow, refresh token rotation | Standard |

Judgment, not sourced: the triage verdicts, the web-to-native mapping, the graph notation, the wave split, the capability costs, the offline levels, the anti-pattern severities, the deep-link back stack choice, the stack comparison and decision tree, the form split threshold, the list and chart mappings, the notification frequency caps and the API priorities. Platform rules change every year: check the official pages before relying on a detail.
