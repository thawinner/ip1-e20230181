# ShopStock

ShopStock is a web app that tracks the storage place of a small shop: storekeepers record stock coming in and going out, and the manager approves write-offs and counts, sees a reorder list, and gets a monthly report.

Individual project for Internet Programming I · I4-GIC · ITC · 2026–2027

## Roles
- Staff (storekeeper): records deliveries, goods sent to the shop, write-offs and stock counts
- Manager: everything staff can do, plus manages products, staff, categories and suppliers, approves write-offs and counts, and sees the reorder list and monthly report

## Tech stack
- Frontend: Vue 3 + Vite + TypeScript
- Backend: NestJS 11 + Prisma + PostgreSQL 16

## Folder structure
One repository for the whole project, following the course guideline:

```
ip1-e20230181/
  frontend/              Vue 3 app (Vite + TypeScript, Vue Router, Pinia)
  backend/               NestJS API (one module per resource, with prisma/ for schema, migrations, seed)
  docs/                  SPEC, wireframes, ERD, API contract (api.md), screenshots
    wireframes/          sketches of the main screens
  docker-compose.yml     whole stack: frontend, backend, PostgreSQL (by M5)
  .github/workflows/     ci.yml: lint, tests and build on every push (by M5)
  PROPOSAL.md            M0 proposal (guideline Appendix A)
  MILESTONES.md          "explain your design" answers for each milestone
  CHECK.md               checklist progress per milestone
  DECISIONS.md           design decisions and why
  AI_LOG.md              log of AI tool use
  README.md
```

Secrets live in `backend/.env` (git-ignored); `backend/.env.example` holds placeholder values.

## Docs
- User stories: [docs/SPEC.md](docs/SPEC.md)
- Wireframes: [docs/wireframes/](docs/wireframes/)

## How to run
Coming soon.