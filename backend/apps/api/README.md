# API (NestJS)

Purpose: HTTP API app. This folder should contain a NestJS application (TypeScript) that implements the public endpoints described in the backend README.

Starter checklist:
- Add a `package.json` (or `bunfig`) and install deps via `bun install` or `npm install`.
- Add NestJS bootstrap (main.ts) and `src/` layout (modules/controllers/services).
- Use `process.env` for configuration and `@nestjs/config` for validation.

Local run (example):

```bash
# from backend/
cd apps/api
bun install     # or npm install
bun run dev     # or npm run start:dev
```
