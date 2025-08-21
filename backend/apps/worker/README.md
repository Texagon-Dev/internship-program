# Worker (BullMQ)

Purpose: background job processors. The worker should subscribe to job queues (BullMQ) and process tasks such as email jobs, report generation, and retries.

Starter checklist:
- Add `package.json` and required packages (bullmq, ioredis, dotenv, ts-node).
- Provide a `worker.ts` entry that connects to Redis and registers processors.

Local run (example):

```bash
cd apps/worker
bun install
bun run start:worker
```
