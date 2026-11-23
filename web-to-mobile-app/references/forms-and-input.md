# Forms and input

Used at steps 1 and 4: how a web form becomes a mobile form. Native pickers per platform: [platform-conventions.md](platform-conventions.md). Keyboard covering inputs as an anti-pattern: [mobile-anti-patterns.md](mobile-anti-patterns.md).

## Contents
- Keyboard and autofill per field type
- Keyboard avoidance
- Field order and return key
- Validation
- Splitting a long form
- Pickers
- Drafts and interruption
- Sheet or full screen
- Web form to mobile form

## Keyboard and autofill per field type

| Field | iOS keyboard / `textContentType` | Android `inputType` / autofill hint | Web equivalent (`type`, `inputmode`, `autocomplete`) |
|-------|----------------------------------|-------------------------------------|------------------------------------------------------|
| Email | `.emailAddress` / `.emailAddress` (`.username` on login) | `textEmailAddress` / `emailAddress` | `type=email`, `autocomplete=email` |
| Password (login) | default / `.password` | `textPassword` / `password` | `autocomplete=current-password` |
| Password (sign-up) | default / `.newPassword` (strong password suggestion) | `textPassword` / `newPassword` | `autocomplete=new-password` |
| One-time code | `.numberPad` / `.oneTimeCode` | `number` / `smsOTPCode` (or SMS User Consent API) | `inputmode=numeric`, `autocomplete=one-time-code` |
| Phone | `.phonePad` / `.telephoneNumber` | `phone` / `phoneNumber` | `type=tel`, `autocomplete=tel` |
| Integer | `.numberPad` | `number` | `inputmode=numeric` |
| Decimal, amount | `.decimalPad` | `numberDecimal` | `inputmode=decimal` |
| URL | `.URL` / `.URL` | `textUri` | `type=url` |
| Name | default, capitalize words / `.name`, `.givenName`, `.familyName` | `textPersonName` / `personName`, `personGivenName` | `autocomplete=name`, `given-name` |
| Address | default / `.fullStreetAddress`, `.postalCode`, `.addressCity` | `textPostalAddress` / `postalAddress`, `postalCode` | `autocomplete=street-address`, `postal-code` |
| Card number | `.numberPad` / `.creditCardNumber` | `number` / `creditCardNumber` | `autocomplete=cc-number` |
| Search | `returnKeyType = .search` | `imeOptions=actionSearch` | `type=search`, `enterkeyhint=search` |
| Long text | default, sentence capitalization | `textMultiLine \| textCapSentences` | `<textarea>` |

Disable autocorrect and autocapitalization on emails, usernames, codes and URLs. For card payment, prefer the payment provider's native sheet or Apple Pay / Google Pay over raw card fields.

## Keyboard avoidance

| Rule | iOS | Android | Cross-platform |
|------|-----|---------|----------------|
| Focused field stays visible | Keyboard layout guide, scroll view insets | Edge-to-edge: handle the IME inset (`WindowInsets.ime`), or `adjustResize` | RN: `KeyboardAvoidingView` or a keyboard controller library; Flutter: `resizeToAvoidBottomInset` |
| Primary button stays reachable | Pinned above the keyboard, or in the navigation bar | Pinned above the keyboard, or in the top app bar | Same |
| Dismiss | Scroll or tap outside dismisses the keyboard | Same; system back closes the keyboard first | Same |

## Field order and return key

| Rule | Detail |
|------|--------|
| Return key | `Next` on every field but the last, `Done` / `Go` / `Send` on the last (iOS `returnKeyType`, Android `imeOptions`) |
| Order | Focus moves in visual order; skip fields filled by a picker |
| Fewer fields | Remove optional fields, derive what can be derived (city from postal code, country from locale) |
| One column | Never side-by-side fields except very short pairs (expiry month / year) |

## Validation

| When | What | Where |
|------|------|-------|
| On blur | Format errors (email, phone) | Inline under the field, in plain language |
| While typing | Only positive or progressive feedback (password strength, remaining characters) | Under the field |
| On submit | All required fields, then server errors | Scroll to and focus the first error; screen reader announces it |
| Server error on a field | Mapped to that field, not a generic alert | Inline |

Never disable the submit button without saying what is missing.

## Splitting a long form

Judgment: more than one screen of fields, or more than about 6 fields, is a candidate for steps.

| Rule | Detail |
|------|--------|
| One topic per step | Identity, address, payment… |
| Progress | Step count or progress bar |
| Back keeps data | Going back never clears a step |
| Prefill | From account, previous orders, device (autofill, contacts, location) |
| Review step | Summary with edit links before an irreversible submit |

## Pickers

| Web input | Mobile |
|-----------|--------|
| `<select>` with few options | Menu (iOS pull-down, Android exposed dropdown) or segmented control (2 to 4) |
| `<select>` with many options | Selection screen with search |
| Date, time | Native date / time picker |
| Multi-select | Selection screen with checkmarks, or chips |
| File input | Camera, photo picker, document scanner, Files (see `native-capabilities.md`) |
| Range | Slider with visible value, or stepper for small integers |

## Drafts and interruption

| Rule | Detail |
|------|--------|
| Save draft | Locally, on each change (debounced) and on backgrounding |
| Restore | After the app is killed, reopen on the form with the draft |
| Discard | Closing a dirty form asks to keep or discard |
| Server drafts | For long content (posts, listings) used across devices |

## Sheet or full screen

| Use a sheet | Use full screen (modal or pushed) |
|-------------|-----------------------------------|
| 1 to 3 fields, quick action (rename, add a note, filter) | Long or multi-step forms, rich text, attachments |
| Context behind must stay visible | Keyboard would cover most of the sheet |
| Swipe down to dismiss is safe | Losing input would hurt: disable swipe dismiss or confirm |

## Web form to mobile form

| Web form | Mobile version |
|----------|----------------|
| Sign-up | Email or social / Sign in with Apple, passkey creation, minimal fields; profile completed later |
| Checkout | Apple Pay / Google Pay first; saved address; steps: cart → delivery → payment → review |
| Advanced search | Search field plus filters in a sheet; saved searches; recent searches |
| Settings page | Grouped list; each setting is a toggle, a picker row or a pushed screen; saved instantly |
| Content creation (post, listing, ticket) | Full-screen modal; camera and photos first; steps for long content; server draft |
| Contact / support form | Prefilled user and device info, category picker, attachment from screenshot |
