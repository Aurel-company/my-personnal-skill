# Implementation waves

Used at step 7. Waves are ordered by dependency; within a wave, agents work in parallel on independent screens.

| Wave | Scope | Done when |
|------|-------|-----------|
| 0. Foundations | Project setup, navigation shell matching the graph (tabs, stacks, modals with placeholder screens), design tokens, API client, auth and secure storage, error and offline handling, state components (skeleton, empty, error) | The whole graph is navigable with placeholders on both platforms |
| 1. Core features | Every feature marked core in the contract, with its states | Core tasks work end to end |
| 2. Secondary features | Every feature marked secondary | |
| 3. Native extras and polish | Push and deep links, biometrics, share, widgets, haptics, motion, accessibility pass, store assets | Ready for TestFlight / internal testing |

## Rules for agents
- The contract is the only spec. An agent does not invent features, screens or states; it raises an open decision instead.
- One agent per set of independent screens; shared components belong to wave 0.
- Each agent ticks its rows in the contract's waves table and notes any deviation in the change log.
- Run the next wave only after the user validates the previous one.
- After each wave, check the result against the contract: navigation, states and platform conventions.
