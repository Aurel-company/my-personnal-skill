# Offline and sync

Used at step 5, after the per-screen states of [states.md](states.md), when the app must work with a weak or absent network. This file decides the data strategy; `states.md` decides what the screen shows.

## Contents
- Offline levels
- Choosing per feature
- Cache strategies
- Optimistic updates
- Action queue
- Conflict resolution
- Never offline
- Contract column

## Offline levels

| Level | What works offline | Cost | Typical features |
|-------|--------------------|------|------------------|
| 0. None | Nothing; offline state with retry | None | Live data, payments, search on the server |
| 1. Cached read | Last loaded content, read-only, with its age | S | Lists, details, profiles, documents |
| 2. Queued write | Read from cache, writes queued and sent later | M | Comments, check-ins, form submissions, status changes |
| 3. Offline-first | Local database is the source of truth, sync in background | L | Field work, notes, inventory, anything used where there is no signal |

Judgment: most apps need level 1 everywhere and level 2 on a few core writes. Level 3 is a product decision, not a default.

## Choosing per feature

1. Is the feature used where the network is bad (transport, field, basement, abroad)? If not, level 0 or 1.
2. Does losing the input cost the user real effort? Then at least level 2.
3. Can two people edit the same data? Then define conflict resolution before choosing level 2 or 3.
4. Is the action irreversible or financial? Then level 0 for that action (see "Never offline").

## Cache strategies

| Strategy | Behavior | Use for |
|----------|----------|---------|
| Stale-while-revalidate | Show cache immediately, refetch, update in place | Default for lists and details |
| TTL | Cache valid for a fixed time, then refetch before showing | Reference data (categories, settings) |
| Cache then network on demand | Cache shown, refresh on pull to refresh or focus | Feeds the user refreshes themselves |
| Network only | Never cached | Balances, stock, prices, anything wrong if stale |
| Invalidation by mutation | A write invalidates the queries it affects | Every write; list them per mutation |
| Invalidation by push | A silent push or socket event marks data stale | Shared data changed by others |

Show the age of cached data when it matters ("Updated 2 h ago"). Clear the cache on logout.

## Optimistic updates

| Rule | Detail |
|------|--------|
| When | The action almost always succeeds and is reversible (like, toggle, reorder, mark as read) |
| Apply | Update the UI immediately, keep the previous value |
| Fail | Roll back, show a snackbar / banner with retry; never fail silently |
| Avoid | Creations with server-generated data the UI needs right away, or anything with side effects outside the app |

## Action queue

| Rule | Detail |
|------|--------|
| Persist | Store queued actions on disk; they survive the app being killed |
| Idempotency | Each action carries a client-generated ID so a retry does not duplicate it |
| Order | Send in order per resource; a failed action blocks the ones that depend on it |
| Retry | On reconnect and on app resume, with backoff |
| Visibility | Mark pending items ("Waiting to send"), show a count somewhere reachable |
| Permanent failure | Validation or permission error → keep the user's input, let them edit or discard |
| Auth | Session expired while queued → re-login, then resume the queue |

## Conflict resolution

| Strategy | How | Use when |
|----------|-----|----------|
| Last write wins | Latest timestamp overwrites | Single user per record, low stakes |
| Server wins | Local change discarded, user told | Server-controlled data (status set by a workflow) |
| Field-level merge | Merge fields changed on each side; conflict only on the same field | Forms and records edited by several people |
| Ask the user | Show both versions, user picks | Rare, high-value conflicts (documents, notes) |
| CRDT / operational merge | Automatic merge of concurrent edits | Collaborative editing; needs a dedicated library and backend |

Requires a version or `updated_at` on each record, sent with every write.

## Never offline

| Action | Why |
|--------|-----|
| Payments, purchases, transfers | Price, stock and fraud checks must be live; a queued payment surprises the user |
| Irreversible actions (delete account, cancel order, send a signed document) | The user must see the result before leaving |
| Auth and security changes (password, 2FA, sessions) | Must be confirmed by the server |
| Actions depending on live availability (booking a slot, claiming an item) | The slot may be gone; queueing creates false confirmations |

Disable these offline with a short explanation, rather than hiding them.

## Contract column

Fill the **Offline** column of the contract's features table: `0`, `1`, `2` or `3`, plus the cache strategy and conflict rule when level ≥ 2 (e.g. `2, SWR, field merge`).
