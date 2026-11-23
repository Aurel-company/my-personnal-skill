# Release and stores

Used at step 7, wave 3: from a working app to a published one, then keeping it healthy. Store rules, limits and review guidelines change often: every number and rule here must be checked on the official pages (see `sources.md`) before relying on it.

## Before submission

| Item | iOS | Android |
|------|-----|---------|
| Developer account | Apple Developer Program, organization account for a company (needs a D-U-N-S number) | Google Play Console, organization account for a company; new personal accounts have extra testing requirements (see Testing tracks) |
| App identifier | Bundle ID (`com.company.app`), final once published | Application ID (`com.company.app`), final once published |
| Signing | Certificates and provisioning profiles, managed by Xcode or the build service | Upload key plus Play App Signing; keep the upload key safe; add the Play signing fingerprint to `assetlinks.json` (see `deep-linking.md`) |
| Environments | Dev, staging, prod as separate schemes or configurations; ideally separate bundle IDs so all three install side by side | Product flavors or build variants with application ID suffixes |
| Per-environment config | API URL, push environment (APNs sandbox vs production), analytics keys, associated domains | API URL, FCM project, analytics keys, App Links domains |
| Build pipeline | CI or a build service (Xcode Cloud, EAS Build, Fastlane, Codemagic…) producing signed builds | Same, producing signed App Bundles (AAB) |

## Testing tracks

| Track | iOS: TestFlight | Android: Google Play |
|-------|-----------------|----------------------|
| Team | Internal testers (App Store Connect users), no review | Internal testing, small group, available in minutes |
| Invited users | External testers by email or public link, after a Beta App Review | Closed testing, by email lists or Google Groups |
| Public beta | Public TestFlight link | Open testing, listed on the store |
| Build lifetime | Builds expire after a set period (90 days) | No expiry |
| Before production | — | New personal developer accounts must run a closed test with a minimum number of testers for a minimum period before production access (check the current numbers) |

Give testers the test accounts, the build's environment and what to test.

## Frequent review rejections

| Reason | Rule (store) | How to avoid it |
|--------|--------------|-----------------|
| App looks like a website | Minimum functionality (App Store 4.2) | Native navigation and screens for core features; no app that is only a webview of the site (see `mobile-anti-patterns.md`) |
| Minimal features | Minimum functionality (4.2), spam (4.3) | A clear mobile use case at launch; not a shell for a login form |
| Reviewer cannot log in | App completeness (2.1) | Working demo account with data, or a demo mode, in the review notes; backend reachable from the review |
| Crashes, placeholders, broken links | App completeness (2.1) | Test the release build on real devices; no "coming soon" screens |
| No account deletion | Account deletion (5.1.1(v)); Play account deletion policy | In-app deletion if accounts can be created in the app; Play also needs a web deletion link |
| Digital goods paid outside the store | In-app purchase (3.1.1); Play billing policy | Store billing for digital content and features; external payment only where the current rules and region allow it |
| Login without a privacy-focused option | Login services (4.8) | When third-party or social login is offered, also offer an equivalent privacy-focused login (Sign in with Apple qualifies) |
| Vague permission texts | Data collection and storage (5.1.1) | Specific purpose strings; ask in context (see `permissions-and-notifications.md`) |
| Privacy declarations wrong | App privacy details (App Store), Data safety form (Play), privacy manifest for listed APIs (iOS) | Inventory every SDK's data collection; keep declarations in sync with each release; privacy policy URL in the store and the app |
| Background location or sensitive permissions unjustified | 5.1.1, Play permissions declarations | Visible feature that needs it, explained in the review notes; Play declaration form |
| Metadata mismatch | Accurate metadata (2.3) | Screenshots show the real app; no other platforms' names or prices in the text |

Write the review notes: test account, how to reach each core feature, hardware or location needs.

## Store assets

| Asset | App Store | Google Play |
|-------|-----------|-------------|
| Icon | 1024 × 1024 px, no transparency | 512 × 512 px, plus the adaptive icon in the app |
| Screenshots | Per device size class required by App Store Connect (largest iPhone size; iPad if supported) | Phone screenshots required; tablet and other form factors if supported; feature graphic 1024 × 500 px |
| Name and subtitle | Name and subtitle, 30 characters each | Title, 30 characters; short description, 80 characters |
| Description | Up to 4000 characters; promotional text editable without release | Full description up to 4000 characters |
| Keywords | Keywords field, 100 characters | No field: keywords come from title and descriptions |
| Other | Privacy policy URL, support URL, age rating, category | Privacy policy, content rating questionnaire, target audience, category |

Judgment: screenshots show the core tasks in order, with a short caption each, in light mode, in every supported language.

## After release

| Topic | Rule |
|-------|------|
| OTA updates | JS / Dart code and assets can be updated without review (e.g. EAS Update); native code cannot. App Store: downloaded code must not change the app's primary purpose or add features outside review. Google Play: no downloaded executable native code; interpreted code is allowed within the policies |
| Feature flags | Ship dark, enable remotely; also a kill switch for a broken feature (see `api-for-mobile.md`) |
| Phased rollout | App Store phased release over 7 days, pausable; Play staged rollout by percentage, haltable |
| Crash reporting | Crash and ANR reporting (Crashlytics, Sentry…) with symbol files uploaded per build; alert on new crashes after each release |
| Analytics | One screen-view event per graph screen id, plus core task completion events; respect consent and ATT |
| Versioning | Semantic marketing version (`2.4.0`) plus an increasing build number; one changelog per release |
| Forced update | Raise the minimum version only after checking active users on old versions (see `api-for-mobile.md`) |
| Store reviews | Ask for a rating with the system prompt (SKStoreReviewController / In-App Review API) after a success, never after an error; the system limits how often it shows |
