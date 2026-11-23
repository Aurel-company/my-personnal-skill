# Stack choice

Used at step 0, when the mobile stack is not already decided. This whole file is judgment: the ecosystems change every year, so check current versions and the team's real experience before deciding. Native capabilities and their cost: [native-capabilities.md](native-capabilities.md).

## Comparison

| Criterion | React Native + Expo | Flutter | Native (Swift + Kotlin) |
|-----------|---------------------|---------|-------------------------|
| Fits a web stack in | React, TypeScript | Any; no reuse of web UI code | Any; no reuse of web UI code |
| Team skills needed | React and TypeScript; some Swift / Kotlin for custom native modules | Dart (new for most web teams) | Two platform specialties |
| Native capabilities | Most covered by Expo modules or community libraries; custom native modules or config plugins for the rest | Most covered by plugins; platform channels for the rest | Everything, first, including new OS features on release day |
| Extensions (widgets, Live Activities, share extension) | Possible, written in Swift / Kotlin as separate targets | Same: native targets | Native by definition |
| Performance and animation | Native views; smooth for typical apps with Reanimated and a virtualized list | Own rendering engine; very consistent animations across platforms | Best ceiling, platform tools for profiling |
| Platform look | Native components by default | Material and Cupertino widgets; platform fidelity is a deliberate effort | Native by definition |
| Team size | One team, both platforms | One team, both platforms | Two codebases, roughly double effort for UI |
| Over-the-air updates | Expo Updates (EAS Update) for JS and assets | Third-party (e.g. Shorebird) | None; store releases only |
| Ecosystem maturity | Large npm ecosystem, uneven library quality | Large pub.dev ecosystem, strong official packages | Most mature, official SDKs first |
| Main risk | Native dependency upgrades; library abandonment | Dart-only knowledge; non-native feel if not handled | Cost and keeping two apps in sync |

OTA updates may change JS / Dart code and assets, not native code, and must not change the app's purpose (App Store Review Guidelines). Native changes still need a store release.

## What can be shared with the web

| Shared item | React Native + Expo | Flutter | Native |
|-------------|---------------------|---------|--------|
| Types and models | Same TypeScript package | Generated from the API schema (OpenAPI, GraphQL) | Generated from the API schema |
| API client | Same package (fetch client, tRPC, GraphQL client, generated OpenAPI client) | Generated Dart client | Generated Swift and Kotlin clients |
| Validation | Same schemas (e.g. Zod) | Rewritten, or server is the source of truth | Rewritten, or server is the source of truth |
| Business logic | Same TS package, if it has no DOM dependency | Not shared with the web | Shared between iOS and Android with Kotlin Multiplatform, not with the web |
| Design tokens | Same token source, exported per platform (e.g. Style Dictionary) | Same token source, exported to Dart | Same token source, exported to Swift and Kotlin |
| UI components | Not shared in practice (web DOM vs native views); share the design, not the code | No | No |
| Repo | Monorepo with workspaces (pnpm, Turborepo, Nx): `apps/web`, `apps/mobile`, `packages/*` | Separate app, shared schema and tokens | Separate apps, shared schema and tokens |

## Decision tree

1. Does the core value depend on platform features that cross-platform frameworks support poorly (heavy AR, custom camera pipeline, deep system integration), or does the team already have iOS and Android developers? → **Native**.
2. Is the web app React + TypeScript, and does the team want to share types, client and logic? → **React Native + Expo**.
3. Is the design a highly custom, animation-heavy brand UI identical on both platforms, and is the team ready to learn Dart? → **Flutter**.
4. Otherwise → **React Native + Expo** for a React team, **Flutter** for a team without a strong React base.

Record the choice and the deciding reason in the contract's framing section.
