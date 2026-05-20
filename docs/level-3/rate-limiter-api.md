# Rate Limiter API

> A configurable rate limiting middleware with store-backed throttling, multiple strategies, and Swagger documentation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://rate-limiter-api-p1y1.onrender.com/api-docs/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/rate-limiter-api)

---

## Purpose

Rate limiting protects your API from abuse, DDoS, and runaway clients. This project teaches
you to build it from scratch: understanding sliding windows vs. fixed windows vs. token bucket
algorithms, storing request counts in a persistent store, and returning proper 429 responses
with `Retry-After` headers. Every production API needs this — building it yourself gives you
deep understanding of what libraries like `express-rate-limit` do internally.

## Tech Stack

- **Frontend:** none (API only, with Swagger UI)
- **Backend:** Node.js, Express
- **Database:** Redis or MongoDB (rate limit store)
- **Key libraries / tools:** ioredis (or mongodb driver), swagger-ui-express, dotenv
- **Deployment:** Render.com

## Build Steps

1. **Choose an algorithm.** Implement at least two: Fixed Window (count requests per time window, e.g. 100/minute) and Sliding Window Log (track exact timestamps of each request). Understand the tradeoffs: fixed window has burst issues at boundaries; sliding window is precise but uses more memory.
2. **Build the middleware.** Create a reusable middleware function: `rateLimiter({ windowMs, max, keyGenerator })`. The key generator determines what to limit by (IP address, API key, user ID). Default to IP.
3. **Implement the store.** Store request counts/timestamps in Redis (fast, shared across instances) or MongoDB (simpler setup). For Redis: use `INCR` + `EXPIRE` for fixed window, or sorted sets for sliding window.
4. **Return proper headers.** On every response: `X-RateLimit-Limit` (max allowed), `X-RateLimit-Remaining` (left in window), `X-RateLimit-Reset` (when the window resets, as Unix timestamp). On 429: add `Retry-After` header in seconds.
5. **Make it configurable per route.** Different routes get different limits: auth endpoints (5/minute — prevent brute force), public API (100/minute), admin endpoints (unlimited). Apply different middleware instances to different route groups.
6. **Add a demo API.** Build a few sample endpoints (e.g. `/api/resource`) that are rate-limited. Include one endpoint that's not limited for comparison. Document the limits in Swagger.
7. **Handle edge cases.** Distributed rate limiting (multiple server instances sharing state via Redis), IPv6 addresses, and proxy headers (`X-Forwarded-For` when behind a load balancer).

## Deployment

Deploy on Render.com. If using Redis, set `REDIS_URL` (use Render's Redis or Redis Cloud
free tier). The Swagger documentation is available at `/api-docs`.

## Tips

- `X-Forwarded-For` is essential when your app is behind a reverse proxy (which it always is on Render/Heroku/Vercel). Without it, all requests appear to come from the proxy's IP and share one rate limit.
- Token Bucket is a third algorithm worth knowing: it allows bursts up to a maximum, then refills at a steady rate. It's used by AWS and most cloud APIs.
- Extension: add tiered rate limits (free tier: 100/hr, paid tier: 10000/hr), dynamic rate limiting based on server load, or a rate limit dashboard.

## README Guidance

The project repo's README should include a description, algorithm explanations, Swagger UI
screenshot, rate limit headers documentation, environment variables, and local setup steps.
