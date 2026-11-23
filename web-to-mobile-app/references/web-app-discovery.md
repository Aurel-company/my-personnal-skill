# Web app discovery

Used at step 0. How to extract the feature inventory from the web app's code, so the user corrects a draft instead of dictating one.

## Where things live, by stack

| Stack | Routes and pages | Layouts | API calls and server logic | Roles and permissions |
|-------|------------------|---------|----------------------------|-----------------------|
| Next.js, app router | `app/**/page.tsx`; dynamic `[id]`, catch-all `[...slug]`, groups `(group)`, parallel `@slot`, intercepted `(.)` | `app/**/layout.tsx`, `template.tsx`, `loading.tsx`, `error.tsx` | `app/**/route.ts`, server actions (`"use server"`), `fetch` in server components | `middleware.ts`, auth helpers called in layouts and actions |
| Next.js, pages router | `pages/**` (except `_app`, `_document`, `api/`) | `_app.tsx`, per-page `getLayout` | `pages/api/**`, `getServerSideProps`, `getStaticProps` | `middleware.ts`, checks in `getServerSideProps` |
| React Router (v6/v7) | `createBrowserRouter`, `<Route>` trees, `app/routes.ts` in framework mode | Routes with `<Outlet />` | `loader` and `action` functions, API client module (`api/`, `services/`) | Wrapper routes, loaders that redirect |
| Vue (Vue Router) | `src/router/index.*` | Components with `<router-view>` | API modules, Pinia/Vuex actions | `beforeEach` / `beforeEnter` guards, route `meta` |
| Nuxt | `pages/**` | `layouts/`, `app.vue` | `server/api/**`, `useFetch` / `$fetch` calls | `middleware/`, `definePageMeta({ middleware })` |
| Angular | `app.routes.ts`, `*-routing.module.ts`, `loadChildren` / `loadComponent` | Components with `<router-outlet>` | Services using `HttpClient`, interceptors | `canActivate` / `canMatch` guards |
| SvelteKit | `src/routes/**/+page.svelte` | `+layout.svelte`, `+layout.server.ts` | `+page.server.ts` (`load`, `actions`), `+server.ts` | `hooks.server.ts`, checks in `load` |
| Rails | `config/routes.rb` (`bin/rails routes`) | `app/views/layouts/` | Controllers, `app/views/**`, JSON views or serializers | `before_action`, Pundit policies, CanCanCan abilities |
| Laravel | `routes/web.php`, `routes/api.php` (`php artisan route:list`) | Blade layouts, Inertia layouts | Controllers, Livewire components, Form Requests | Middleware, Policies, Gates |
| Django | `urls.py` files (`show_urls` with django-extensions) | Base templates (`{% extends %}`) | Views, DRF viewsets and routers, forms | Decorators (`login_required`, `permission_required`), DRF permission classes, groups |

For a single-page app talking to a separate backend, read both: the frontend gives the screens, the backend gives the operations (some exist only as API endpoints, used by another client or by an admin script).

## Hidden features

Features that are not a page in the nav but that users rely on.

| Where | What to look for | Typical mobile verdict |
|-------|------------------|------------------------|
| Feature flags | Flag SDK calls (LaunchDarkly, Unleash, GrowthBook, Flagsmith), `isEnabled(`, `FEATURE_` env vars, plan or tier checks | Ask which flags are on in production; off flags are out of scope |
| Admin and back-office | `/admin` routes, Django admin, role checks (`isAdmin`, `role ===`), staff-only menus | Usually drop; keep read-only views a manager uses on the go |
| Emails | Mailer classes, email templates (`emails/`, `mailers/`, `resources/views/emails`), transactional email provider calls | Each email is a feature: digest, reminder, alert → candidate for push |
| Jobs and schedules | Cron config, Sidekiq / Celery / BullMQ / Laravel scheduler, queued jobs | Reminders and reports → push or in-app inbox |
| Webhooks in | Endpoints receiving Stripe, GitHub, Slack… | Usually no screen; their effects (payment status, sync) need states |
| Real time | WebSocket, SSE, Pusher, Ably, Supabase / Firebase listeners | Live updates on screen; push when the app is closed |
| Settings | Settings and account pages, user preferences, notification preferences, API keys, billing | Split: everyday preferences keep; billing and API keys often drop or "continue on desktop" |
| Exports and imports | CSV / PDF generation, bulk import | Usually drop or replace with share sheet |
| Keyboard and power-user | `keydown`, hotkey libraries, command palette | Adapt: search, quick actions |
| Print and download | `window.print`, file downloads | Replace with share sheet or in-app viewer |
| Onboarding and empty states | First-run flows, sample data, tours | Rethink for mobile at step 5 |
| Localization | i18n files, locale switcher, RTL support | Carry over; flag text length and RTL for design |
| Legal and consent | Cookie banners, terms acceptance, GDPR export / deletion | Account deletion must exist in the app if accounts are created there (see `release-and-stores.md`) |

## Method

1. List every route with its access level (public, logged in, role).
2. Group routes into features by user goal, not by URL.
3. For each feature, note the API operations it uses.
4. Sweep the hidden-feature table above.
5. Mark what you could not determine (unused routes, flags of unknown state) as questions for the user.

## Output: draft of the step 1 table

Same columns as the contract's features table, verdict left empty, plus two working columns removed once validated.

```md
| # | Feature | What it does | Web location | Verdict | Mobile problem | Solution | Priority | Offline | Status | Source in code | Confidence |
|---|---------|--------------|--------------|---------|----------------|----------|----------|---------|--------|----------------|------------|
| 1 | Invoice list | Lists, filters and sorts invoices | /invoices | | | | | | proposed | app/invoices/page.tsx, GET /api/invoices | high |
| 2 | Overdue reminder | Emails the client 7 days after due date | (email) | | | | | | proposed | jobs/overdue_reminder.rb | medium: flag state unknown |
```

Confidence is judgment: **high** when route, UI and API agree, **medium** when one is missing or a flag hides it, **low** when only dead code or a backend endpoint suggests it.
