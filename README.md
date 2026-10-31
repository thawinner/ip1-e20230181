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
  docs/                  SPEC (detailed spec), wireframes, ERD, API contract (api.md), screenshots
    wireframes/          sketches of the main screens (M1)
    erd/                 database ERD (M2)
    diagrams/            architecture diagram for the final presentation
    screenshots/         app screenshots for the README (M5)
  docker-compose.yml     whole stack: frontend, backend, PostgreSQL (by M5)
  .github/workflows/     ci.yml: lint, tests and build on every push (by M5)
  PROPOSAL.md            M0 proposal (guideline Appendix A)
  MILESTONES.md          M0–M5 checklists and "explain your design" answers
  README.md
```

Secrets live in `backend/.env` (git-ignored); `backend/.env.example` holds placeholder values.

## Docs
- Proposal (problem, roles, user stories, MVP, entities): [PROPOSAL.md](PROPOSAL.md)
- Detailed specification (full acceptance criteria, guard table): [docs/SPEC.md](docs/SPEC.md)
- Wireframes: [docs/wireframes/](docs/wireframes/)
- Milestones checklist and design answers: [MILESTONES.md](MILESTONES.md)
- Course guideline: [docs/Project Guideline.pdf](<docs/Project Guideline.pdf>)

## How to run
Coming soon.