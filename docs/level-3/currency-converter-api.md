# Currency Converter API

> A currency conversion API with external rate fetching, response caching, and historical rate tracking.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://currency-converter-api-9rfm.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/currency-converter-api)

---

## Purpose

This project deepens your understanding of the proxy/caching pattern with a focus on data
freshness. Exchange rates change frequently but not every second — knowing when to serve
cached data vs. when to fetch fresh data is a key backend skill. You'll also learn to handle
external API failures gracefully (serve stale cache) and build a useful utility API.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (rate history) or in-memory cache
- **Key libraries / tools:** axios (HTTP client), node-cache (TTL caching), dotenv
- **Deployment:** Render.com

## Build Steps

1. **Choose a rates provider.** Use a free exchange rate API (ExchangeRate-API, Open Exchange Rates, or Fixer.io free tier). Store the API key in environment variables. Understand the provider's rate limits and update frequency.
2. **Build the conversion endpoint.** `GET /convert?from=USD&to=EUR&amount=100`. Validate that currencies are valid ISO codes, amount is positive. Return `{ from, to, amount, result, rate, timestamp }`.
3. **Implement caching.** Cache exchange rates with a 1-hour TTL. On each request, check cache first. On cache miss, fetch from the external API and store. Return cache age in the response headers (`X-Cache: HIT/MISS`, `X-Cache-Age`).
4. **Handle stale cache gracefully.** If the external API is down and the cache has expired, serve the stale cached rates with a warning header rather than returning an error. Stale data is better than no data for exchange rates.
5. **Support multiple conversions.** `GET /rates?base=USD` returns all available rates for a base currency. `GET /convert/batch` accepts multiple conversion pairs in a single request to reduce round trips.
6. **Store rate history.** Periodically save fetched rates to MongoDB. Build a `GET /history?from=USD&to=EUR&days=30` endpoint that returns historical rates for charting.
7. **Add supported currencies list.** `GET /currencies` returns all supported currency codes with their names. Cache this permanently (it rarely changes). Use it for client-side validation.

## Deployment

Deploy on Render.com. Set `MONGODB_URI`, `EXCHANGE_RATE_API_KEY`, and `CACHE_TTL_MINUTES`
as environment variables. The cache ensures you stay within the external API's rate limits.

## Tips

- A 1-hour cache TTL is reasonable for exchange rates in most non-trading contexts. For trading apps, you'd use WebSocket streams — but for a general utility, hourly updates are fine.
- Always validate currency codes against a known list before calling the external API. Invalid codes waste API quota and return confusing errors.
- Extension: add currency conversion with historical rates ("what was 100 USD in EUR on 2024-01-01?"), automatic refresh via cron job, or a simple conversion widget frontend.

## README Guidance

The project repo's README should include a description, endpoint table with example
request/response, cache behavior explanation, environment variables, and local setup steps.
