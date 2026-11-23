# Agent brief template

Used at step 7: the brief given to each agent of a wave. Fill one per agent from the contract; the agent gets nothing else. Wave split and agent rules: [implementation-waves.md](implementation-waves.md).

```md
# Brief: wave <n>, agent <name>

## Read first
- Contract: docs/mobile-transposition/CONTRACT.md (the only spec)
- Sections for you: 1 (features #<ids>), 2 (screens <ids>), 4 (conventions rows <…>), 5 (states rows <…>)

## Scope
| Screen (graph id) | Type | Features (#) | Entry points | Exits |
|-------------------|------|--------------|--------------|-------|
| <id> | stack screen | #3, #7 | tap card on home, deep link /items/:id | back, share sheet |

Out of scope: every other screen, even if you see a bug there. Note it in the change log.

## Reuse (from wave 0, do not modify)
- Navigation: <file> (routes and params already declared)
- Components: <list with paths: list row, empty state, error state, skeleton, sheet…>
- API client: <path>, endpoints: <list>
- Tokens and theme: <path>

## States to implement
| Screen | Loading | Empty | Error | Offline | Permission | Session expired |
|--------|---------|-------|-------|---------|------------|-----------------|
| <copied from contract section 5> |

## Platform conventions
<copied rows from contract section 4: shared / iOS / Android>

## Done when (each item verifiable)
- [ ] Every screen in scope reachable from its entry points, including deep links, on iOS and Android
- [ ] Every exit works (back gesture, system back, close)
- [ ] Every state above renders (force each one: no data, network off, API error, permission denied)
- [ ] Input survives backgrounding and rotation
- [ ] Touch targets ≥ 44 pt / 48 dp; layout holds at the largest text size
- [ ] Typecheck, lint and existing tests pass; new logic has tests
- [ ] Contract ticked and change log updated

## Forbidden
- Inventing a feature, screen, state or copy that is not in the contract: add it to "Open decisions" instead
- Modifying wave 0 foundations (navigation shell, shared components, API client, tokens): request the change
- Working outside the scope above
- Adding a dependency without noting it in the change log

## Reporting
1. In the contract's waves table, tick your rows in "Done".
2. Any deviation (missing endpoint, convention not applicable, state impossible): one line in the change log:
   `<date> — wave <n> / <agent> — <what deviated and why> — <steps affected>`
3. End with a short report: what is done, what is not, open decisions raised.
```
