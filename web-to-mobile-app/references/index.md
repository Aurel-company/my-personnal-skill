# Web to mobile app: resource index

Everything concrete lives here so it can be updated without touching `SKILL.md`.

**To add a resource**: add the block to the matching file (or a new file), then add one row below, with a precise **Read when**. `SKILL.md` does not change.

| File | Step | Read when | What it holds |
|------|------|-----------|---------------|
| [web-app-discovery.md](web-app-discovery.md) | 0 | Step 0, when the web app's code is available, to draft the inventory | Where routes, layouts, API calls and permissions live per web stack; hidden features; draft table format |
| [stack-choice.md](stack-choice.md) | 0 | Step 0, only when the mobile stack is not already decided | React Native + Expo vs Flutter vs native, what can be shared with the web, decision tree |
| [contract-template.md](contract-template.md) | 0, all | Step 0, once, when creating the contract | Template of the running contract file |
| [feature-triage.md](feature-triage.md) | 1 | Step 1, when a feature's verdict or priority is not obvious | Verdicts (keep, adapt, replace, drop, add), decision questions, common adapt cases, priority |
| [native-capabilities.md](native-capabilities.md) | 1 | Step 1, when a feature could use a native capability (Add or Replace verdict) | Per capability: user value, when to add, cost, permission, pitfalls |
| [forms-and-input.md](forms-and-input.md) | 1, 4 | Step 1 or 4, when a feature includes a form longer than 3 fields or a field needing a specific keyboard (email, phone, code, amount, address) | Keyboard and autofill per field, keyboard avoidance, validation, splitting, pickers, drafts, sheet vs full screen, web form to mobile |
| [data-and-lists.md](data-and-lists.md) | 1, 2 | Step 1 or 2, when a feature shows a table, a long list, a dashboard or charts | Table to list mapping, list vs cards vs grid, filters, bulk actions, swipe, pagination and scroll, charts |
| [web-to-native-patterns.md](web-to-native-patterns.md) | 1, 2 | Steps 1 and 2, when a web pattern has no obvious native equivalent | Native equivalent of each web pattern |
| [navigation-graph.md](navigation-graph.md) | 2 | Step 2, when drawing the graph | Mermaid notation for node types and edges, rules, example, legend |
| [deep-linking.md](deep-linking.md) | 2 | Step 2, when web URLs are shared (email, push, share) or the app receives push notifications | Route mapping table, Universal Links and App Links, push routing, edge cases, graph notation |
| [design-grilling.md](design-grilling.md) | 3 | Step 3, only if the user wants a design artifact | Question bank for the design grilling |
| [platform-conventions.md](platform-conventions.md) | 4 | Step 4, only the sections matching the screens in the graph | iOS vs Android: navigation, controls, layout, system integration, what to share |
| [states.md](states.md) | 5 | Step 5, when a state's content or action is not obvious | Per-screen and app-wide states |
| [permissions-and-notifications.md](permissions-and-notifications.md) | 4, 5 | Step 4 or 5, when a screen needs a runtime permission or the app sends notifications | When to ask each permission, pre-prompt, refusal and settings, notification types, iOS categories and Android channels, silent push |
| [accessibility-mobile.md](accessibility-mobile.md) | 4, 5 | Step 4 or 5, for every core screen and its states; and before validating a wave | Text size, screen readers, contrast, motion, touch, device test checklist |
| [offline-and-sync.md](offline-and-sync.md) | 5 | Step 5, only when a feature must work with a weak or absent network | Offline levels, cache strategies, optimistic updates, action queue, conflicts, never offline, contract column |
| [mobile-anti-patterns.md](mobile-anti-patterns.md) | 6, review | Step 6, and when reviewing an existing mobile plan or app | Signs the app feels like a website: symptom, why, fix, severity |
| [implementation-waves.md](implementation-waves.md) | 7 | Step 7, when planning the waves | Wave split and rules for agents |
| [api-for-mobile.md](api-for-mobile.md) | 7 | Step 7, when planning wave 0, if the team can change the backend | Mobile need → API change → priority; versioning and forced update, auth, structured errors |
| [agent-brief-template.md](agent-brief-template.md) | 7 | Step 7, when launching an agent of a wave | Copyable brief: scope, reuse, states, conventions, done criteria, forbidden, reporting |
| [sources.md](sources.md) | — | When a platform rule must be checked against the official page | Sources and reliability |
