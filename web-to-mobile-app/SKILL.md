---
name: web-to-mobile-app
description: Turn an existing web app into a real native mobile app (iOS and/or Android, React Native, Flutter, Swift, Kotlin), not a responsive website. Runs a gated workflow: feature inventory and triage (keep, adapt, replace, drop, add native), a running contract file in the project, a full navigation graph typed by component (tab, stack screen, modal, bottom sheet, drawer), an optional design grilling and artifact, iOS and Android conventions, state screens, a contract review, then implementation in waves of agents. Use whenever the user wants to port, transpose, adapt or rebuild a web app as a mobile app, plan a mobile version of a web product, or asks how a web feature should work on iOS or Android, even if they do not say "skill" or "workflow".
---

# Web to mobile app

A mobile app is a different product, not a shrunken website. Sessions are short, one-handed and interrupted; the network is unreliable; the platform has its own conventions and native capabilities. The job is to decide, feature by feature and screen by screen, what the mobile product should be, and to write every decision down so nothing is lost.

If the user only wants the web app to work on phones, this is the wrong skill: see `responsive-web-app`.

Everything concrete (patterns, conventions, question banks, templates) lives in `references/`. Start with [references/index.md](references/index.md).

## Operating rules

- **One step at a time, gated.** Every step produces a deliverable, shows it, and waits for explicit validation before moving on. Iteration within a step is normal; offer it.
- **The contract is the source of truth.** Every validated decision is written to the contract file. Re-read the contract at the start of every step and before answering any question about earlier decisions. Never rely on conversation memory alone.
- **Changes propagate.** When the user revises an earlier decision, update the contract, then list the later steps it affects and revisit only those.
- **Read the code, not just the user.** When the web app's code is available, the inventory comes from routes, pages, components and API calls; the user corrects it, they do not have to dictate it.
- **Justify every "adapt" and "replace".** Name the precise mobile problem (hover, density, wide table, keyboard shortcut, long form, multi-window) and propose a concrete solution from [references/web-to-native-patterns.md](references/web-to-native-patterns.md).
- **Platform-correct, not platform-identical.** Share logic and design language; let navigation, back behavior, sheets, pickers and typography follow each platform.

## Workflow

### 0. Framing

Read the web app (routes, pages, components, API). Ask what is not in the code: target platforms (iOS, Android, both), mobile stack (React Native, Flutter, native), who uses the mobile app and in what situation. Create the contract from [references/contract-template.md](references/contract-template.md) at `docs/mobile-transposition/CONTRACT.md` (or where the user prefers) and fill in the framing section.

### 1. Feature inventory and triage

Produce one table, every feature on its own row: name, what it does, where it lives in the web app, verdict, mobile problem, proposed solution, priority (core or secondary). Verdicts and how to decide them: [references/feature-triage.md](references/feature-triage.md). Also propose features to **add** that only make sense on mobile (push, biometrics, camera, share sheet, widgets, offline).

Gate: the user validates or edits row by row, as many rounds as needed. Write the validated table to the contract.

### 2. Navigation architecture

Produce the complete navigation graph as a Mermaid diagram, following [references/navigation-graph.md](references/navigation-graph.md): every screen is a node typed by its component (tab, stack screen, modal, bottom sheet, drawer, dialog, external), every edge is labelled with the interaction that triggers it (tap, swipe, long press, back, deep link, push notification). Add a legend. Check that every kept, adapted, replaced or added feature appears on at least one screen.

Gate: validate, then write the graph and the screen list to the contract.

### 3. Design grilling and artifact (optional)

Ask one question: do we produce a design artifact? If no, record it in the contract and go to step 4.

If yes: if the `grilling` skill is not already loaded in this conversation, call it with the Skill tool; if it is not available, continue without it. Grill the design using the question bank in [references/design-grilling.md](references/design-grilling.md): ask as many questions as needed, one branch at a time, until the direction is unambiguous. Then build the artifact (key screens first). Before delivering it, if the `design-without-ai-tells` skill is not already loaded in this conversation, call it with the Skill tool; if it is not available, continue without it.

Gate: validate, then write the design decisions to the contract.

### 4. iOS and Android conventions

Read [references/platform-conventions.md](references/platform-conventions.md) and keep only what applies to the screens in the graph. For each concerned screen or component, state what is shared and what diverges between iOS and Android. If a needed convention is missing from the references, research it from the official guidelines, use it, and add it to the references (new block plus one line in the index) without editing this file.

Gate: validate, then write the conventions to the contract.

### 5. State screens

For every screen, decide which states apply and what each one shows and offers: loading, empty, error, offline, permission denied, session expired. Then the app-wide states: first launch and onboarding, forced update, maintenance. Use [references/states.md](references/states.md).

Gate: validate, then write the states to the contract.

### 6. Contract review and summary

Re-read the whole contract and check its consistency with the checks below. Report every gap and fix it with the user. Then write a short, plain summary at the top of the contract: the app in one sentence, what is kept, what changes, what is new, and the open decisions.

### 7. Implementation in waves

Propose an implementation split into ordered waves, following [references/implementation-waves.md](references/implementation-waves.md): wave 0 foundations, then core features, then secondary features, then native extras and polish. Within a wave, each agent takes independent screens, reads the contract as its only spec and ticks off what it delivers. Offer to launch the agents wave by wave; launch the next wave only after the previous one is validated.

## Review format

When reviewing an existing mobile plan or app against this skill, report each finding as **screen or feature → problem → rule or pattern → fix**, with a severity: **P0** breaks a task or a platform rule users rely on (no back path, unreachable feature, hover-only action, data loss on interruption), **P1** works but feels like a website (web navigation, tiny targets, web pickers, missing states), **P2** polish.

## Checks before delivering

- Every web feature has a verdict, and every "adapt" or "replace" names its mobile problem and its solution.
- Every feature kept, adapted, replaced or added appears on a screen in the graph, and every screen is reachable and has a way back.
- Every node has a component type and every edge an interaction.
- Every screen has its states; app-wide states are defined.
- iOS and Android divergences are explicit where they matter.
- The contract is up to date, has a summary, and lists open decisions.

## Skill links

**Calls** (mandatory, at the steps named above):
- `grilling`: step 3, to grill the design before building the artifact.
- `design-without-ai-tells`: step 3, before delivering the design artifact.

**Related** (only when the situation appears, no automatic call):
- `responsive-web-app`: when the user actually wants the web app to work on phones, not a native app.
- `interface-craft`: fine detail of touch targets, typography and surfaces on a screen.
- `app-motion`: navigation transitions, sheets and feedback motion.
- `apple-design`: gestures, sheets, springs and fluid physical motion on iOS.
