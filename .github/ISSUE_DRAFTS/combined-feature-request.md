## Title
Add academy-manager features: persistence, GraphQL, dashboard, auth, UI improvements

## Summary
This single consolidated issue requests adding a set of features inspired by the `bq-educacion/academy-manager` project to the `skills-integrate-mcp-with-copilot` repository. The goal is to grow the current simple FastAPI + static UI into a more production-ready extracurricular management platform (incrementally).

## Motivation
- Current project stores activities in-memory and provides only basic REST endpoints and a minimal static UI. Adding the features below will enable persistence, admin functionality, structured schedules, richer domain model, auth, and developer tooling.

## Proposed features (combined)
1. Persistence: replace in-memory `activities` with a database (SQLite for minimal footprint or MongoDB for parity). Add a migration strategy.
2. GraphQL API (optional): add a GraphQL layer with schema and codegen (or keep REST and add typed OpenAPI schemas). This is optional — list as a stretch goal.
3. Dashboard & analytics: add an admin dashboard showing aggregated counts (active activities, participants, capacity usage) and simple charts.
4. Structured schedules & timetable editor: switch schedule strings to a structured model (days, start/end times, recurrence) and add a small JS editor to create timetables.
5. Authentication & authorization: add JWT-based auth and optional Google OAuth for admin/teacher roles; protect admin endpoints.
6. Multi-role frontends: scaffold (or separate) a back-office admin UI and a basic teacher UI (Next.js or keep static but modularized) — role-specific views.
7. Shared UI components: extract and create a small component library (buttons, modals, inputs, options/multi-selects) for reuse and consistent styling.
8. Search & filters: add server-side search, and client-side filters (multi-select OptionsBox-like control).
9. Multi-step create/edit flows (modals): implement guided creation flows for new entities (activities, instructors, students) using modal steps and client-side validation.
10. Domain model expansion: add `instructors` and `students` entities and connect them to activities (profiles, contact info, availability).
11. Developer tooling & deployment: add basic pre-commit hooks (formatting/linters), Docker Compose with a DB service, and a short `README` run section.
12. i18n/localization: add translation support (simple key-based system) with a `useTranslate`-style helper.

## Acceptance criteria
- Activities persist after server restarts using a DB.
- Admin dashboard shows aggregate counts and a basic list view of entities.
- Users can create structured schedules and see them in the UI.
- Signup/unregister endpoints require no changes in API contract for public signup (unless auth is enabled for admin-only actions).
- Basic authentication protects admin pages and mutations.

## Suggested implementation plan (phased)
1. Add persistence (SQLite via `databases` or `SQLModel` / or small MongoDB compose service). Migrate `activities` to DB models and update endpoints.
2. Add domain models for `students` and `instructors` and simple CRUD endpoints.
3. Add dashboard endpoints (counts) and a small admin UI page to display them.
4. Add structured schedule model and a minimal timetable component in `src/static` to edit schedules.
5. Add JWT auth and a simple admin login; protect admin UI pages.
6. Optional: incrementally add GraphQL or a Next.js-based admin UI and component library.

## Tasks (checklist)
- [ ] Design DB schema and choose DB (SQLite or MongoDB)
- [ ] Implement persistence and migrations
- [ ] Create models for students & instructors
- [ ] Implement dashboard endpoints
- [ ] Add schedule data model and UI editor
- [ ] Add JWT auth and admin roles
- [ ] Improve front-end UI components and add search/filtering
- [ ] Add pre-commit hooks and Docker Compose
- [ ] Add i18n support

## Risks & notes
- GraphQL + codegen is a larger change; start with REST + DB then consider GraphQL as a later migration.
- If choosing MongoDB, include a `docker-compose.yml` DB service for local dev.

## Labels (suggested)
`enhancement`, `feature`, `backend`, `frontend`, `infra`, `medium-priority`

## Assignees / Reviewers
- (leave blank)

---
_Draft created by automation — review and edit before opening as a GitHub Issue._
