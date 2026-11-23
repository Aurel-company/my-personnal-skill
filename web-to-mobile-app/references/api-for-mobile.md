# API for mobile

Used at step 7, wave 0: backend changes the mobile app needs, to plan before the screens are built. Unlike a website, old app versions stay installed for months and the network is slow and unreliable. Priorities are judgment: **must** before the first release, **should** before scale, **could** when a problem shows.

## Changes table

| Mobile need | API change | Priority |
|-------------|------------|----------|
| Old app versions keep working | Versioned API (URL or header); additive changes only within a version; deprecation window | must |
| Block versions that no longer work | Minimum version endpoint or config (see below), checked at launch and on resume | must |
| Know which client calls | Send app version, platform and build in a header on every request | must |
| Infinite scroll | Cursor-based pagination (`after`, `limit`, `next_cursor`), stable under inserts | must |
| Slow networks | Light payloads: list endpoints return only list fields; selectable fields or sparse fieldsets for the rest | should |
| Avoid request cascades | Aggregated endpoints per screen when a screen needs several resources (or GraphQL / BFF) | should |
| Images | Resized variants or an image CDN with size parameters; never the original upload in a list | must |
| Mobile auth | Access and refresh tokens, rotation, revocation (see Auth) | must |
| Push | Endpoint to register and remove a device token (token, platform, app version, locale), linked to user and device; cleanup of invalid tokens returned by APNs / FCM | must if push |
| Notification preferences | Per-type preferences stored server side, matching the iOS categories / Android channels | should if push |
| Replayed actions from the offline queue | Idempotency key header on every write; same key returns the first result (see [offline-and-sync.md](offline-and-sync.md)) | must if offline level ≥ 2 |
| Conflict detection | `version` or `updated_at` on records; writes rejected with a conflict error when stale | must if offline level ≥ 2 |
| Delta sync | `updated_since` filter and tombstones for deleted records | could; must if offline level 3 |
| Deep links | Every shared URL maps to an API resource fetchable by ID (see [deep-linking.md](deep-linking.md)) | must |
| Abuse and retries | Rate limiting per user and device, `429` with `Retry-After`; clients back off | should |
| Account deletion | Endpoint to delete the account from the app (App Store requirement when accounts can be created in the app) | must |
| Uploads | Direct or resumable uploads (pre-signed URLs) for photos and files | should if uploads |

## Versioning and forced update

| Element | Detail |
|---------|--------|
| Config endpoint | Returns per platform: `min_supported_version`, `latest_version`, `store_url`, optional `maintenance` message |
| Forced update | App version < minimum → blocking screen with the store link (see `states.md`) |
| Soft update | App version < latest → dismissible banner |
| Kill switch | Remote flags to disable a broken feature without a release |
| Policy | Judgment: support at least the last few months of versions; never raise the minimum without checking the share of active users on older versions |

## Auth

| Element | Rule |
|---------|------|
| Flow | OAuth 2.0 / OIDC with PKCE through the system browser (`ASWebAuthenticationSession`, Custom Tabs), or first-party endpoints for email / passkeys |
| Access token | Short-lived; sent in the `Authorization` header; never in URLs |
| Refresh token | Long-lived, rotated on each use; reuse of an old refresh token revokes the session |
| Storage | Keychain (iOS), Keystore-backed encrypted storage (Android); never in plain preferences or JS storage |
| Refresh | One refresh at a time; queued requests retry after refresh; refresh failure → session-expired state |
| Revocation | Logout revokes the refresh token server side; list of sessions / devices in account settings |
| Biometrics | Unlocks the stored refresh token locally; not a server auth method |
| Cookies | Avoid cookie sessions for the mobile API; tokens are explicit and easier to rotate and revoke |

## Errors

Structured, stable, readable by the app, so screens can show the right state.

```json
{
  "error": {
    "code": "invoice_not_found",
    "message": "This invoice no longer exists.",
    "field": null,
    "retryable": false,
    "request_id": "req_8f2c"
  }
}
```

| Rule | Detail |
|------|--------|
| HTTP status | Correct class (`400` validation, `401` expired token, `403` forbidden, `404` not found, `409` conflict, `422` field errors, `429` rate limit, `5xx` server) |
| `code` | Stable machine code the app maps to a state or message; never parse `message` |
| `field` | Set for validation errors, so the form shows it inline |
| `message` | Localized from the request's `Accept-Language`, safe to show |
| `retryable` | Tells the app and the offline queue whether to retry |
| `request_id` | Shown in "contact support" to trace the error |
