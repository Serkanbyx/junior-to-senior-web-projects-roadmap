# Job Queue

> A production-ready Job Queue REST API with BullMQ, Redis, TypeScript, email/PDF workers, Winston logging, and Bull Board monitoring.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://job-queue-f62a.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/job-queue-api)

---

## Purpose

Not everything should happen in the request-response cycle. Email sending, PDF generation,
and report compilation should happen in the background. This project teaches you to
decouple work from HTTP requests using BullMQ — a Redis-backed job queue. You'll learn
producers, workers, retry logic, monitoring dashboards, and the async processing pattern
used at every scale.

## Tech Stack

- **Runtime:** Node.js, TypeScript
- **Framework:** Express 5
- **Queue:** BullMQ 5 + ioredis 5
- **Monitoring:** Bull Board 7 (@bull-board/api + @bull-board/express)
- **Email:** Nodemailer
- **PDF:** PDFKit
- **Auth:** JWT (jsonwebtoken) + express-basic-auth (for Bull Board)
- **Validation:** Joi
- **Logging:** Winston + winston-daily-rotate-file
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Set up BullMQ with Redis.** Connect to Redis via ioredis. Create named queues (email-queue, report-queue). Understand the architecture: producers add jobs to Redis, workers pull and process them independently. The API responds immediately — processing happens async.

2. **Build the producer API.** `POST /jobs` accepts `{ type: 'email' | 'report', data, options }`. Options: delay (run after N ms), priority (1-10), attempts (retry count). Add the job to the appropriate queue. Return job ID immediately (202 Accepted).

3. **Build the email worker.** Listens on the email queue. Processes each job by sending an email via Nodemailer. On success, mark complete. On failure (SMTP error), BullMQ retries automatically with exponential backoff.

4. **Build the report worker.** Listens on the report queue. Generates PDF reports using PDFKit or CSV files. Simulates heavy computation. Reports progress events (0% → 50% → 100%) that the API can relay to clients.

5. **Implement retry and failure handling.** Configure: `attempts: 3`, `backoff: { type: 'exponential', delay: 5000 }`. After all retries fail, jobs move to the "failed" set. Build an endpoint to retry failed jobs or view failure reasons.

6. **Add Bull Board monitoring.** Mount Bull Board at `/admin/queues` (protected with express-basic-auth). Visualize: active jobs, waiting, completed, failed, delayed. Retry or delete jobs from the UI. This is your ops dashboard.

7. **Add Winston logging and deploy.** Structured JSON logging with Winston. Daily log rotation with winston-daily-rotate-file. Log job lifecycle events: created, started, completed, failed. Deploy to Render with Redis (Upstash or Render Redis).

## Deployment

Deploy on Render.com with Redis (Upstash free tier or Render Redis). Set `REDIS_URL`,
`SMTP_*` credentials, and `BULL_BOARD_PASSWORD`. TypeScript compiles before deploy.

## Tips

- BullMQ's killer feature: jobs survive server restarts. They live in Redis. If your server crashes mid-processing, the job returns to the queue after a visibility timeout and is picked up by another worker (or the same one after restart).
- The 202 Accepted pattern: when work takes longer than a reasonable HTTP timeout, return 202 with a job ID immediately. The client polls `GET /jobs/:id/status` for progress. This is how every async API works (AWS, Stripe, etc.).
- Extension: add webhook callbacks on job completion, priority queues (paid users first), job scheduling (cron-like recurring jobs), or a dead letter queue for permanently failed jobs.

## README Guidance

The project repo's README should include a description, architecture diagram (Producer → Redis → Worker), job lifecycle explanation, Bull Board screenshot, tech stack, and setup instructions.
