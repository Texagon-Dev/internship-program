# Texagon Backend Internship (Bun + Node 24)

[![CI](https://github.com/ORG/REPO/actions/workflows/ci.yml/badge.svg)](https://github.com/ORG/REPO/actions/workflows/ci.yml)
[![Node](https://img.shields.io/badge/node-24.x-339933)](https://nodejs.org)
[![Bun](https://img.shields.io/badge/bun-1.x-000000)](https://bun.sh)

> **Outcome:** produce job‑ready backend engineers in **4 weeks** (3 weeks training + 1 week capstone). Deliverables are verifiable, tested, and reviewed via PRs.

---

## Table of Contents

* [Overview](#overview)
* [Tech Stack](#tech-stack)
* [Repository Layout](#repository-layout)
* [Quickstart](#quickstart)
* [Environment](#environment)
* [Global API Conventions](#global-api-conventions)
* [Weekly Plan](#weekly-plan)

  * [Week 1 — Express + Prisma](#week-1--express--prisma)
  * [Week 2 — NestJS Essentials](#week-2--nestjs-essentials)
  * [Week 3 — Microservices, Caching, Ops](#week-3--microservices-caching-ops)
  * [Week 4 — Capstone (Production-Grade)](#week-4--capstone-production-grade)
* [Testing & CI](#testing--ci)
* [Submission & Pass Bar](#submission--pass-bar)
* [AI Policy](#ai-policy)

---

## Overview

* **DX/Runtime:** **Bun** for install/test/dev, **Node.js 24** for runtime (Bun‑only allowed if all deps are compatible).
* **Stack:** TypeScript, **Express → NestJS**, PostgreSQL, Prisma, Redis, Docker, Jest + Supertest, Swagger/OpenAPI.
* **Pass bar:** **≥ 70/100** (+10 bonus). Interns must explain code live.

---

## Help & Escalation — avoid wasting seniors' time

This section explains where to ask for help, what information to include, and the escalation flow. Follow these rules exactly so seniors can help quickly and you don't block the team.

Checklist (requirements for any help request)
- Reproduce locally (or provide a reproducible minimal example).
- Run tests and include failing test output (if any).
- Git branch name, commit SHA, and PR/issue link (if applicable).
- Clear error logs and the exact command you ran.
- What you already tried (commands, stacktrace analysis, search links).

If any of the above is missing, the request will be triaged as "insufficient info" and you will be asked to update it before a senior spends time.

Communication channels (use in this order)
- 1) Documentation & README: first check this file and `backend/.github/` templates.
- 2) Issues: open a structured issue in the repo (use the issue template). Non-blocking requests belong here.
- 3) Slack/Teams — channel: `#backend-help` — use for timed questions (include the triage checklist in your first message).
- 4) Pager / On-call: `#backend-oncall` — only for production incidents or when the app is down in shared dev/staging.

Office hours & SLAs
- Office hours: Mon–Fri 09:00–17:00 PKT— mentors available for live code review and quick pairing.
- Normal question SLA: answer within 24 hours on Issues/Slack during working days.
- Urgent SLA (blocking development for >4 hours): escalate to the on-call channel and ping `@oncall-backend` (use GitHub issue link + reproduction steps).

How to ask for help — exact template (copy/paste)
```
Title: [SHORT] <one-line summary>

Context:
 - Branch: feat/...
 - Commit: <short-sha>
 - Service: api | worker | notifier

Problem: One short paragraph describing the observed behavior vs expected.

Reproduction steps (exact commands):
1. bun install
2. docker compose -f docker/docker-compose.yml up -d
3. cp .env.example .env (edit DB to local)
4. bunx prisma migrate dev && bunx prisma db seed
5. bun run dev
6. curl -v "http://localhost:8000/api/..."

What I tried (bullet list):
- grep logs, ran `bun run test --testNamePattern="..."`
- changed X to Y, checked Z

Logs / Errors (paste full stack or attach file):
```

Attach: failing test, minimal repro repo or single-file gist, relevant logs.

When to escalate to a senior
- You hit a blocker that prevents the whole cohort from progressing for >4 hours.
- Production outage or staging environment broken for multiple users.
- Security vulnerability or leaked secret.

Escalation flow (follow exactly)
1. Try to resolve with peers and by following the checklist.
2. If still blocked after 30–60 minutes, open a GitHub Issue with the template and tag `team/backend` + `triage` label.
3. If this blocks the cohort for >4 hours, post in `#backend-oncall` with the issue link and subject `BLOCKER`.
4. On-call will acknowledge within 30 minutes during working hours. If no acknowledgement in 30 minutes, escalate in Slack to `@tech-lead`.

Code review & PR guidelines (to reduce back-and-forth)
- PR title: type(scope): short description — e.g. feat(api): add loans endpoint
- Include a PR description with: what changed, why, how to run locally, and test plan.
- Always attach screenshots, curl examples, and exact commands to run e2e or unit tests.
- Keep PRs small (aim for < 300 LOC). Huge PRs will be returned for rework.
- Add a checklist in the PR body and mark items completed:
  - [ ] Manual testing steps
  - [ ] Unit tests added
  - [ ] E2E tests added (if applicable)
  - [ ] .env.example updated
  - [ ] Swagger updated (if API changed)

Reviewer expectations
- Reviewers focus on correctness, security, and maintainability.
- If reviewer requests changes, implement them in a follow-up commit and reply with a short summary.

Common quick fixes you should try before asking
- Rebuild dev containers / docker compose down && up
- Clear node/bun cache (`bun cache clean`), reinstall deps, remove `node_modules`/bun.lockb
- Run `bun run test` with `--runInBand` or specific test name
- Search repo for similar issues and check PR history

Templates to add (recommended files)
- `.github/ISSUE_TEMPLATE/help-request.md` — use the "How to ask for help" template above.
- `.github/PULL_REQUEST_TEMPLATE.md` — include the PR checklist.

Quick blockers & emergency checklist
- If production is down:
  1. Post to `#backend-oncall` with `PROD DOWN` and issue link.
  2. Assign an engineer and set status page / ops note.
  3. If sensitive data is involved, follow the security playbook (notify SecOps).

Privacy & Safety
- Never post secrets in Slack or GitHub issues. Use `sops`/vault for sharing secrets. If a secret was leaked, immediately rotate and escalate to `@security`.

---

## Tech Stack

* **Runtime/Tooling:** Node 24.x, Bun 1.x, Docker, docker‑compose
* **Frameworks:** Express, NestJS 
* **Data:** PostgreSQL, Prisma ORM, Redis
* **Quality:** TypeScript strict, ESLint/Prettier, Jest + Supertest, Swagger UI
* **CI/CD:** GitHub Actions, multi‑stage Docker build

---

## Repository Layout

```
backend/
  apps/
    api/                # NestJS HTTP API
    worker/             # BullMQ consumers
    notifier/           # Microservice (Redis/RabbitMQ/NATS transport)
  docker/
    docker-compose.yml
  prisma/
  .github/workflows/ci.yml
```

---

## Quickstart

```bash
# 1) prerequisites
node -v   # should be v24
bun -v    # bun 1.x

# 2) clone & install
bun install

# 3) spin up infra (Postgres/Redis)
docker compose -f docker/docker-compose.yml up -d

# 4) env
cp .env.example .env
# edit values (DATABASE_URL, JWT_ACCESS_SECRET, JWT_REFRESH_SECRET, REDIS_URL, CORS_ORIGIN, PORT)

# 5) database
bunx prisma migrate dev
bunx prisma db seed

# 6) develop (Nest)
bun run dev     # nest start --watch

# 7) run tests
bun run test
```

---

## Environment

**Required variables** (example):

```
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/texagon
REDIS_URL=redis://localhost:6379
PORT=3000
NODE_ENV=development
CORS_ORIGIN=http://localhost:5173
JWT_ACCESS_SECRET=change-me
JWT_REFRESH_SECRET=change-me-too
JWT_ACCESS_TTL=15m
JWT_REFRESH_TTL=7d
```

* Provide `.env.example` and validate at runtime (e.g., via zod/class‑validator).

---

## Global API Conventions

* **IDs:** `uuidv4` strings
* **Dates:** ISO‑8601 UTC
* **Auth:** JWT access **15m**, refresh **7d**, HS256, header `Authorization: Bearer <token>`
* **Pagination:** `?page=1&limit=20` (max 100); response `{ data, page, limit, total }`
* **Filtering:** contains‑match for text fields unless stated
* **Uploads:** `multipart/form-data`, ≤ **2 MB**, `jpg|jpeg|png|webp`, store under `/uploads`, DB saves file path
* **Status Codes:** `200/201/204/400/401/403/404/409/422/429/500`
* **Error Envelope:**

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "string",
    "details": [{ "field": "title", "issue": "Required" }],
    "requestId": "uuid"
  }
}
```

* **Health:** `GET /health` → `{ status: "ok" }` (wk1+)
* **Readiness:** `GET /ready` checks DB/Redis (wk3+)
* **Metrics:** `GET /metrics` (Prometheus, wk3+)

---

## Weekly Plan

### Week 1 – Express + Prisma

**Goal:** learn HTTP semantics, async/concurrency, and ship **full CRUD** with Postgres.

**Day 1 – JS/TS + HTTP Request Types**

* Methods GET/POST/PUT/PATCH/DELETE; idempotency; status codes; headers; auth headers; lifecycle.
* **Task:** in‑memory `/api/product` with all 5 verbs (fields: `id`, `name`).

**Day 2 – Async & Concurrency**

* `async/await`, Promise methods (all/race/allSettled/any), timeouts, **AbortController**, backoff + jitter.
* **Task:** aggregator hitting 3 public APIs in controlled parallelism with timing logs.

**Day 3 – Express Foundations**

* Middleware pipeline, central error handler, logs (pino), input validation.
* **Task:** health route, error envelope, validation scaffolding.

**Day 4 – PostgreSQL + Prisma**

* Schema, migrations, relations, transactions, seed script.

**Day 5 – Long Final Project: Library Manager API (Full CRUD)**
Models: **Author**, **Book**, **Member**, **Loan**.
Rules: cannot loan when not available or an active loan exists; return sets `returnedAt` and `available=true`; optional: member ≤ **5** active loans.
Endpoints: Authors/Books/Members CRUD; Books search `?q=`; Loans `POST /loans` and `POST /loans/:id/return`.
Seed: 5 authors, 8 books, 3 members, 1 active loan.
**Auto‑tests (min):** CRUD (happy/404/422), loan conflict 409, return flow, `/books?q=`, `/health`, migrations + seed.

---

### Week 2 – NestJS Essentials

**Goal:** re‑platform Week‑1 to Nest; implement **auth**, **uploads**, **pagination/filtering**, **Swagger**, and tests.

**Day 1 – Architecture & Validation**
Nest CLI; modules/controllers/services; DI; ConfigModule with env validation; global ValidationPipe; ExceptionFilters; Interceptors.

**Day 2 – Data Layer (Prisma in Nest)**
Models/relations/migrations; repo pattern; ownership fields (`createdBy`, etc.).

**Day 3 – AuthN/Z (complete)**
**argon2** hashing; **JWT** access(15m)/refresh(7d) with **rotation**; Guards (**AuthGuard**, **RolesGuard**); decorators `@CurrentUser`, `@Roles`.

**Day 4 – File Uploads + Hardening & Docs**
Multer (≤2MB, images only), avatar/cover; **API versioning `/v1`**, CORS, Helmet; **Swagger** with auth button.

**Day 5 – Migration Day: Convert Week‑1 to NestJS + TS**
Parity for Authors/Books/Members/Loans; **pagination & filtering** on lists; reuse auth + guards/decorators; upload endpoints; full Swagger; **e2e (auth + 2 entities)** and **service unit tests**.

**Week‑2 Checklist:** Swagger complete; `.env.example` updated; migrations/seeders; uploads strategy; Nest migration merged; CI green.

---

### Week 3 – Microservices, Caching, Ops

**Goal:** scale, resilience, and operability.

**Services & Contracts**

* **Notifier microservice** (Redis transport)

  * Queue: `email:send`
  * Event: `loan.created` payload `{ loanId, memberEmail, bookTitle }`
* **Background Jobs**: BullMQ queue `jobs:low`; supports `idempotencyKey`
* **Caching**: Redis keys `summary:book:{id}`, TTL **30s**; bust on book update/return
* **Rate Limit**: 100 req / 5 min / IP (429 with `X-RateLimit-*` headers)
* **Realtime**: WebSocket namespace `/ws`; events: `loan:created`, `loan:returned`
* **Scheduling**: Nightly `0 0 * * *` (UTC) to email overdue loans
* **Observability**: correlation ID `X-Request-Id`; `/health`, `/ready`, `/metrics`

**Auto‑tests (min):** enqueue on loan create; worker processes job; cache hit vs miss & bust; 101st call → 429; WS event after POST /loans; `/ready` 503 when DB/Redis down.

**Deployability**: multi‑stage Dockerfile; docker‑compose (api + worker + db + cache + notifier); GitHub Actions (lint → test → build → docker build). One‑command local start; CI badge.

---

### Week 4 – Capstone (Production‑Grade)

Pick one and meet all criteria.

**A) TaskFlow Pro (multi‑tenant)**
Organizations/teams, roles, projects, tasks, comments, attachments, realtime updates, email jobs.

**B) Shop API (headless commerce)**
Catalog, inventory, carts, checkout (mock Stripe), orders, webhooks, admin RBAC.

**Acceptance Criteria (must‑have)**

* Clean Nest modules; SOLID service boundaries; DI correct
* Postgres schema + migrations + seeds
* **Auth complete** (argon2, JWT access+refresh with rotation) + Guards/Decorators
* **Uploads** for attachments/avatars
* **Pagination & filtering** on all list endpoints
* Global error envelope; structured logs with request IDs
* **Swagger** complete; versioning, CORS, Helmet
* **Tests:** ≥80% service coverage + critical E2E
* **Ops:** docker‑compose up full stack; CI green; README runbook

**Mandatory E2E Flows**

* **TaskFlow Pro**: register → create org → invite user → create project → create task → comment → upload attachment → WS update broadcast
* **Shop API**: register → admin adds product → user adds to cart → checkout (mock) → order created → webhook processed

**Bonus (+10):** Prometheus dashboards; k6 perf budget; blue‑green deploy notes.

---

## Testing & CI

* **Unit & E2E:** Jest + Supertest; target ≥80% service coverage (wk4)
* **CI (GitHub Actions):** lint → test → build → docker build
* **Fixtures/Seeds:** deterministic seeds for tests; fail on coverage or lint errors

---

## Submission & Pass Bar

* Weekly PR + checklist + ≤3‑min demo; Capstone: tagged release + 5‑min demo + production README
* **Pass bar:** **≥ 70/100** (+10 bonus)

---

## AI Policy

Use AI to learn concepts only. Deliverables must be original and explainable live.

---

> Replace `ORG/REPO` in the badge URL once this README is placed in your GitHub repository.
