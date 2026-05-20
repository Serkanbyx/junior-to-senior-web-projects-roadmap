# URL Shortener

> A URL shortening service with hash generation, redirect handling, and click tracking analytics.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://url-shortener-xzz2.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/url-shortener-api)

---

## Purpose

This project teaches you hashing, redirect mechanics, and analytics tracking. A short code
maps to a long URL, and every visit is a 301/302 redirect with metadata logged. It introduces
unique ID generation (nanoid or base62 encoding), HTTP redirect semantics, and the concept of
tracking user behavior without cookies. URL shorteners are deceptively simple but touch on
important concepts: collision avoidance, caching, and abuse prevention.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** nanoid (short ID generation), geoip-lite (optional), dotenv
- **Deployment:** Render.com

## Build Steps

1. **Design the data model.** Schema: `{ shortCode, originalUrl, clicks: Number, clickHistory: [{ timestamp, ip, userAgent, referer }], createdAt, expiresAt? }`. Index `shortCode` for fast lookups.
2. **Create the shorten endpoint.** `POST /shorten` accepts `{ url }`. Validate it's a proper URL (protocol + domain). Generate a unique 6-8 character code using nanoid or base62 encoding of a counter. Store the mapping and return the short URL.
3. **Handle redirects.** `GET /:code` looks up the short code in the database. If found, increment the click counter, log the click metadata (timestamp, IP, user-agent), and respond with a 302 redirect to the original URL. If not found, return 404.
4. **Prevent collisions.** Before saving, check if the generated code already exists. If it does, regenerate. With 6+ alphanumeric characters, collisions are astronomically rare but you must handle them.
5. **Add analytics.** `GET /:code/stats` returns click count, click history (last 100), referrer breakdown, and time-series data (clicks per day). This endpoint does NOT redirect — it returns JSON.
6. **Implement expiration.** Optional `expiresAt` field. On redirect, check if the link has expired. If so, return 410 Gone. Use a TTL index in MongoDB for automatic cleanup of expired documents.
7. **Add abuse prevention.** Rate limit the creation endpoint. Optionally check URLs against a blocklist (malware, phishing). Validate that the URL actually resolves (optional HEAD request).

## Deployment

Deploy on Render.com. Set `MONGODB_URI` and `BASE_URL` (the short domain, e.g.
`https://url-shortener-xzz2.onrender.com`). The redirect must be fast — consider caching
hot URLs in memory.

## Tips

- Use 302 (temporary) redirects, not 301 (permanent). With 301, browsers cache the redirect and never hit your server again — you lose all click tracking for repeat visitors.
- nanoid generates URL-safe random strings. A 7-character nanoid has ~70 billion possibilities — more than enough for most use cases.
- Extension: add custom short codes (vanity URLs), QR code generation for each short link, or a simple frontend dashboard showing analytics.

## README Guidance

The project repo's README should include a description, endpoint table (shorten, redirect,
stats), example curl commands, environment variables, and local setup steps.
