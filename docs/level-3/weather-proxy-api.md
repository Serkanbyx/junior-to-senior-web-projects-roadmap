# Weather Proxy API

> A backend proxy that hides API keys, adds caching, and provides a clean interface for weather data.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-proxy-api-yrc5.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-proxy-api)

---

## Purpose

This project teaches the proxy pattern — your server sits between the client and a third-party
API, hiding credentials and adding value (caching, rate limiting, response shaping). It's the
same pattern used at every company that consumes external APIs. You'll learn to forward requests,
transform responses, implement in-memory caching with TTL, and protect your API key from
client-side exposure.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** none (in-memory cache)
- **Key libraries / tools:** node-fetch or axios (HTTP client), node-cache (TTL cache), dotenv
- **Deployment:** Render.com

## Build Steps

1. **Design the proxy endpoints.** Map your clean API to the third-party endpoints: `GET /weather?city=London` calls OpenWeatherMap's API internally. The client never sees the external URL or API key.
2. **Hide the API key.** Store `OPENWEATHER_API_KEY` in environment variables. Your server appends it to outgoing requests. The client only knows your server's URL — the key is never exposed.
3. **Forward and transform responses.** Call the external API with axios/fetch, receive the response, and reshape it into a cleaner format. Strip unnecessary fields, rename cryptic keys, and add any computed values (e.g. "feels like" description).
4. **Add caching with TTL.** Cache responses keyed by the request params (e.g. city name). Set a TTL of 10-15 minutes — weather doesn't change every second. On cache hit, return immediately without calling the external API. Log cache hit/miss for debugging.
5. **Handle external API errors.** If the third-party API returns an error (rate limited, city not found, server error), translate it into a meaningful response for your client. Never proxy raw error responses — they may contain internal details.
6. **Add rate limiting.** Limit clients to N requests per minute to prevent abuse. Use express-rate-limit with an appropriate window. Return 429 with a `Retry-After` header.
7. **Support multiple endpoints.** Add forecast (`/forecast?city=London&days=5`) and geocoding (`/geocode?query=London`) endpoints that proxy different external API routes through the same key.

## Deployment

Deploy on Render.com. Set `OPENWEATHER_API_KEY` as an environment variable. The in-memory
cache resets on deploy/restart — for persistence, swap to Redis (but in-memory is fine for
a demo with a 10-minute TTL).

## Tips

- The proxy pattern isn't just about hiding keys — it also decouples your frontend from the external API. If the provider changes their response format, you update only the proxy, not every client.
- In-memory cache (like `node-cache`) is simple but resets on restart. For production, use Redis. For this project, in-memory is intentional — it teaches the concept without extra infrastructure.
- Extension: add response compression, request logging with analytics (which cities are most queried), or support for multiple weather providers with automatic fallback.

## README Guidance

The project repo's README should include a description, endpoint table, environment variables,
a note explaining the proxy pattern's benefits, and local setup steps.
