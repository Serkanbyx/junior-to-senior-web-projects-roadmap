# Rate Limiter API

> A distributed rate limiter built with Express, Redis, and multiple limiting strategies (Global, Strict, Auth tiers).

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://rate-limiter-api-0853.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/rate-limiter-api)

---

## Purpose

Rate limiting is critical infrastructure — it protects APIs from abuse, DDoS, and excessive
usage. This project teaches you to build a distributed rate limiter backed by Redis (works
across multiple server instances). You'll implement multiple strategies and understand
RFC Draft-7 headers that tell clients exactly how many requests they have left.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Store:** Redis 5 (redis npm package) + rate-limit-redis
- **Rate limiting:** express-rate-limit with Redis store
- **HTTP Client:** Axios
- **Security:** Helmet 8
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Set up Redis-backed rate limiting.** Configure express-rate-limit with rate-limit-redis store. Unlike in-memory limiting (resets on restart, per-instance only), Redis-backed limits persist across restarts and work across multiple server instances.

2. **Implement multiple tiers.** Three rate limit strategies: Global (100 req/15min for all endpoints), Strict (20 req/15min for sensitive operations), Auth (5 req/min for login/register to prevent brute force). Apply different limiters to different route groups.

3. **Add RFC Draft-7 headers.** Every response includes: `RateLimit-Limit` (max requests), `RateLimit-Remaining` (requests left), `RateLimit-Reset` (seconds until window resets). Clients use these to implement backoff without guessing.

4. **Build demo endpoints.** Create test routes that demonstrate each tier in action: `/public` (global limit), `/strict` (strict limit), `/auth/login` (auth limit). Each returns its current limit status in the response body.

5. **Handle limit exceeded.** On 429 Too Many Requests, return a JSON body with: error message, retry-after seconds, and which tier was exceeded. Include `Retry-After` header for HTTP compliance.

6. **Implement graceful Redis fallback.** If Redis is unavailable, fall back to in-memory rate limiting (per-instance). Log the degradation. This ensures the API doesn't become unprotected if Redis goes down.

7. **Document the limiting behavior.** Swagger documents the rate limit headers on every endpoint. Include a "Rate Limiting" section explaining tiers, headers, and best practices for clients.

## Deployment

Deploy on Render.com with Redis (Upstash or Render Redis). Set `REDIS_URL`.
Fallback to in-memory if Redis is unavailable.

## Tips

- Distributed rate limiting (Redis) vs local (in-memory): with 3 server instances and in-memory limits, a user gets 3x the intended rate (100 per instance = 300 total). Redis is shared — the limit is truly global.
- RFC Draft-7 headers are the modern standard (replacing the older `X-RateLimit-*` convention). They give clients all the information needed to implement smart retry logic without trial-and-error.
- Extension: add sliding window (more accurate than fixed window), per-API-key limits, dynamic limits based on subscription tier, or a leaky bucket algorithm implementation.

## README Guidance

The project repo's README should include a description, rate limit tiers table, header
examples, Redis setup, tech stack, and deployment instructions.
