# Contract template

Copy this to `docs/mobile-transposition/CONTRACT.md` at step 0. It is a temporary working file: it lives until the implementation is done, then it can be archived or turned into product docs.

Every decision carries a status: `proposed`, `validated`, `changed (date, reason)`. Re-read this file at the start of every step.

```md
# Mobile transposition contract: <app name>

## Summary
<!-- Filled at step 6: the app in one sentence, kept / changed / new, open decisions. -->

## Status
| Step | State | Last update |
|------|-------|-------------|
| 0. Framing | in progress | |
| 1. Feature triage | todo | |
| 2. Navigation | todo | |
| 3. Design | todo / skipped | |
| 4. Platform conventions | todo | |
| 5. States | todo | |
| 6. Review | todo | |
| 7. Waves | todo | |

## 0. Framing
- Web app: <repo, stack, main routes>
- Platforms: iOS / Android / both
- Mobile stack: React Native / Flutter / Swift + Kotlin
- Users and context of use:
- Out of scope:

## 1. Features
| # | Feature | What it does | Web location | Verdict | Mobile problem | Solution | Priority | Status |
|---|---------|--------------|--------------|---------|----------------|----------|----------|--------|

## 2. Navigation
<!-- Mermaid graph + legend + screen list (id, type, features, entry points) -->

## 3. Design
<!-- Decisions from the grilling, link to the artifact, or "skipped". -->

## 4. Platform conventions
| Screen / component | Shared | iOS | Android |
|--------------------|--------|-----|---------|

## 5. States
| Screen | Loading | Empty | Error | Offline | Permission | Session expired |
|--------|---------|-------|-------|---------|------------|-----------------|
App-wide: first launch / onboarding, forced update, maintenance.

## 6. Open decisions
- [ ] ...

## 7. Waves
| Wave | Scope (screens) | Depends on | Agent(s) | Done |
|------|-----------------|------------|----------|------|

## Change log
- <date> — <what changed> — <steps affected>
```
