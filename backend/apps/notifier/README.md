# Notifier (Microservice)

Purpose: a small microservice responsible for notifications (email/webhook). It can use Redis, RabbitMQ or NATS as transport.

Starter checklist:
- Define transport (Redis/RabbitMQ/NATS) and message contract (events such as `loan.created`).
- Provide a small `notifier.ts` entry and configuration to connect to the chosen broker.

Local run (example):

```bash
cd apps/notifier
bun install
bun run start:notifier
```
