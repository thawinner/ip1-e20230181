# Milestones

Checklist and "explain your design" answers for each milestone. Each milestone is due at the end of its week and submitted as a Git tag (`m0`, `m1`, …).

## Overview
- [ ] M0 Proposal (week 3)
- [ ] M1 Frontend prototype (week 5)
- [ ] M2 Backend API (week 7)
- [ ] M3 Integrated app (week 9)
- [ ] M4 Feature complete (week 12)
- [ ] M5 Deployed (week 14)
- [ ] Final presentation and defence (week 16, code frozen at tag `final` end of week 15)

## M0 Proposal (week 3)
- [ ] `PROPOSAL.md` follows the template in Appendix A
- [ ] Problem stated in two sentences; target users and at least 2 roles named
- [ ] 6–10 user stories, with acceptance criteria for the 3 most important
- [ ] MVP scope split into must-have and nice-to-have
- [ ] Entity list with main attributes and relations; at least 3 entities
- [ ] Chosen stretch feature named
- [ ] Tagged `m0`

**Which story did you cut from the MVP, and why?**

TODO

## M1 Frontend prototype (week 5)
- [ ] Wireframes (photo or tool) of the main screens in `docs/`
- [ ] Vue 3 + TypeScript app created with Vite; strict mode on; ESLint passes
- [ ] At least 4 routes, including a detail page with a route parameter
- [ ] At least one form with client-side validation
- [ ] A Pinia store and a service layer calling a mock API (json-server or local JSON)
- [ ] Loading, empty and error states visible
- [ ] Tagged `m1`

**What state lives in the store and what stays inside a component? Why?**

TODO

## M2 Backend API (week 7)
- [ ] API contract (`docs/api.md`) and ERD in `docs/`
- [ ] NestJS API with one module per resource (controller, service, DTOs)
- [ ] Prisma schema, migrations and a seed script; PostgreSQL runs in Docker
- [ ] CRUD endpoints for at least 3 entities, with server-side validation
- [ ] Correct status codes (200, 201, 204, 400, 404) and consistent error JSON
- [ ] Tagged `m2`

**Why did you choose this relation (1-N or N-N) between two of your entities?**

TODO

## M3 Integrated app (week 9)
- [ ] Frontend calls the real API; the mock is gone
- [ ] Registration, login, logout; passwords hashed
- [ ] Guards on the API for authentication, roles and ownership
- [ ] Route guards in Vue; the UI hides what a role cannot do
- [ ] Security checklist from week 9 run on the app; findings fixed or listed
- [ ] 3-minute demo in the practice session
- [ ] Tagged `m3`

**Where is the token stored in the browser, and what attack does that choice protect against or expose?**

TODO

## M4 Feature complete (week 12)
- [ ] Every MVP user story works end to end
- [ ] Stretch feature implemented
- [ ] Unit tests for core services; e2e tests for the main endpoints; all green
- [ ] Swagger documentation available
- [ ] Tagged `m4`

**Pick one test. What bug would it catch?**

TODO

## M5 Deployed (week 14)
- [ ] Dockerfiles for frontend and backend; `docker-compose.yml` for the whole stack
- [ ] Running on the school server with HTTPS, or starting locally with one `docker compose up`
- [ ] GitHub Actions workflow runs lint, tests and build on every push
- [ ] README complete (Appendix B); no secrets in the repository
- [ ] Tagged `m5`

**What happens, step by step, between `git push` and your change being live?**

TODO

## Final presentation and defence (week 16)
- [ ] Code frozen and tagged `final` (end of week 15)
- [ ] Demo (5 min): main user stories live, logged in as each role
- [ ] Architecture walkthrough (5 min): system diagram, data model, one decision you would change
- [ ] Code defence (10 min): explain any part, trace one request click → DB → back, make a small live change
