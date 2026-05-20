# Currency Converter API

> A production-ready RESTful Currency Converter API supporting 160+ currencies with Redis caching, rate limiting, and graceful degradation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://currency-converter-api-l38v.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/currency-converter-api)

---

## Purpose

This project introduces Redis as a caching layer — the most important performance pattern
in backend development. Exchange rates don't change every second, so caching them avoids
hitting the external API on every request. You'll learn Redis commands, TTL-based expiry,
cache-aside pattern, and graceful degradation (what happens when Redis is down?).

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Cache:** Redis 5 (redis npm package)
- **HTTP Client:** Axios (for ExchangeRate-API)
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Set up the conversion endpoint.** `GET /convert?from=USD&to=EUR&amount=100` calls ExchangeRate-API for the rate, calculates the result, and returns: `{ from, to, amount, rate, result, cached }`.

2. **Integrate Redis caching.** Before calling the external API, check Redis: `GET rate:USD:EUR`. If it exists and is fresh, return it immediately (add `cached: true` to response). If missing, fetch from API, store in Redis with TTL (e.g., `EX 3600` for 1 hour), then return.

3. **Implement the cache-aside pattern.** The flow: check cache → if hit, return → if miss, fetch from source → store in cache → return. This is the most common caching pattern. All cache reads are optimistic (best-effort).

4. **Add graceful degradation.** If Redis is unavailable (connection error), don't crash — fall back to calling the external API directly (slower but functional). Log the Redis failure for monitoring. The API continues working without cache.

5. **Build supporting endpoints.** `GET /currencies` (list all 160+ supported currencies), `GET /health` (check API + Redis status). Cache the currencies list aggressively (24h TTL) since it rarely changes.

6. **Add rate limiting.** Protect both your API and the upstream ExchangeRate-API from abuse. Limit to 100 requests per 15 minutes per IP. Return 429 with clear messaging.

7. **Deploy to Render.** Set `EXCHANGE_RATE_API_KEY` and `REDIS_URL` (use Upstash or Render Redis). In-memory fallback if Redis is unavailable ensures zero downtime.

## Deployment

Deploy on Render.com. Redis on Upstash (free tier) or Render Redis add-on. Set
`EXCHANGE_RATE_API_KEY` and `REDIS_URL` as environment variables.

## Tips

- The cache-aside pattern with Redis: `GET key` → null means cache miss → fetch data → `SET key value EX ttl` → return. This pattern appears in every high-performance backend. Master it here, use it everywhere.
- Graceful degradation is what separates production code from tutorial code. If your cache dies, your API should still work (slower, but functional). Never let a cache failure cascade into an API outage.
- Extension: add historical rates endpoint, rate change alerts, batch conversion, or WebSocket for real-time rate updates.

## README Guidance

The project repo's README should include a description, API endpoints, caching strategy
explanation, Redis setup instructions, tech stack, and deployment guide.
