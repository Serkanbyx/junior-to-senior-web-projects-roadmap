# Job Queue

> A background job processing system with BullMQ, Redis, retries, scheduled jobs, and a monitoring dashboard.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://job-queue-f62a.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/job-queue-api)

---

## Purpose

Not everything should happen in the request-response cycle. Email sending, image processing,
report generation, and webhook deliveries should happen in the background. This project
teaches you to decouple work from HTTP requests using a job queue — the same pattern used at
every company that processes async work. You'll learn Redis-backed queues, workers, retry
logic, and job lifecycle management.

## Tech Stack

- **Frontend:** none (API + worker)
- **Backend:** Node.js, Express
- **Database:** Redis (job queue storage)
- **Key libraries / tools:** BullMQ (queue library), ioredis, Bull Board (monitoring UI)
- **Deployment:** Render.com

## Build Steps

1. **Set up Redis and BullMQ.** Connect to Redis via ioredis. Create a queue instance with BullMQ. Understand the concepts: producers add jobs, consumers (workers) process them, Redis stores the state.
2. **Define job types.** Create multiple job types: `send-email` (simulated), `generate-report` (CPU-intensive simulation), `webhook-delivery` (HTTP call to external URL). Each type has its own processing logic.
3. **Build the producer API.** `POST /jobs` accepts `{ type, data, options }`. Options include delay (run after N ms), priority, and attempts (retry count). Return the job ID immediately — the client doesn't wait for processing.
4. **Build the worker.** A separate process (or the same process in dev) that listens for jobs and processes them. Each job type has a handler function. Simulate work with `setTimeout`. Log progress events.
5. **Implement retry logic.** Configure jobs with `attempts: 3` and `backoff: { type: 'exponential', delay: 5000 }`. On failure, BullMQ automatically retries with increasing delays. After all attempts fail, move to the "failed" queue.
6. **Add scheduled/delayed jobs.** Support `delay: 60000` (run after 1 minute) and cron-based repeating jobs (e.g. daily cleanup at midnight). Build a `POST /jobs/schedule` endpoint for delayed execution.
7. **Add monitoring.** Integrate Bull Board to provide a web UI showing all queues, pending/active/completed/failed jobs, and retry controls. Mount it at `/admin/queues` (protected).

## Deployment

Deploy on Render.com. Set `REDIS_URL` (use Render Redis or Redis Cloud free tier).
The worker runs in the same process for simplicity. In production, you'd run it as a
separate Render Background Worker service.

## Tips

- Always make jobs idempotent — if a job runs twice (due to retry after a crash), the result should be the same. Use unique identifiers and check-before-write patterns.
- BullMQ stores all job data in Redis. Large payloads (e.g. file contents) should NOT be in the job data — store them elsewhere and pass a reference (URL or ID) in the job.
- Extension: add job progress reporting (percentage updates while processing), priority queues (urgent jobs processed first), or dead letter queue handling with manual retry UI.

## README Guidance

The project repo's README should include a description, architecture diagram (API → Redis → Worker),
job types and their payloads, Bull Board screenshot, environment variables, and local setup steps.
