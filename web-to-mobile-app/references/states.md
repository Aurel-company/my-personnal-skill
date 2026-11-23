# State screens

Used at step 5. For every screen, decide which states apply, what they show, and what action they offer.

## Per-screen states
| State | What to show | Action offered | Notes |
|-------|--------------|----------------|-------|
| Loading | Skeleton matching the layout; spinner only for short blocking actions | None, or cancel | Show cached data first when it exists |
| Empty (first use) | Why it is empty and what it will hold | The action that fills it | Different from "no results" |
| Empty (no results) | What was searched or filtered | Clear filters, change search | |
| Error | Plain-language cause | Retry; contact support if persistent | Never a raw error code alone |
| Partial error | Content plus an inline banner | Retry the failed part | Do not blank the whole screen |
| Offline | Cached content plus a discreet banner | Queue actions, sync later | Say which actions will wait |
| Permission denied | What the feature needs and why | Open system settings | Degraded mode when possible |
| Session expired | Short message | Log in again, then return to the same screen | Keep unsaved input |
| Pull to refresh | System refresh control | | |

## App-wide states
| State | What to show |
|-------|--------------|
| First launch / onboarding | Value in 1 to 3 screens at most, skippable; ask permissions later, in context |
| Forced update | Blocking screen with a store link when the API version is no longer supported |
| Soft update | Dismissible banner |
| Maintenance / server down | Message, expected return, cached content if possible |
| Interrupted and restored | Return to the same screen, scroll position and draft input after the OS kills the app |
| No network at cold start | Cached shell and content, or a clear offline screen |
