# URL Shortener

> A fast URL shortener REST API with nanoid-generated short codes, click tracking, duplicate detection, and rate limiting.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://url-shortener-api-i9na.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/url-shortener-api)

---

## Purpose

URL shorteners are deceptively simple — they teach important concepts: ID generation
strategies, redirect mechanics (301 vs 302), click analytics, and handling high-frequency
reads (redirect lookups) vs low-frequency writes (URL creation). This project uses nanoid
for collision-resistant short codes and SQLite for persistence.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3)
- **ID Generation:** nanoid 5
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Design the URLs table.** Schema: `id, short_code (UNIQUE), original_url, clicks (DEFAULT 0), created_at`. Index on `short_code` for O(1) redirect lookups. Store the URL in the `data/` directory.

2. **Build the shorten endpoint.** `POST /shorten` accepts a URL, validates it (must be a valid URL format), checks for duplicates (if already shortened, return the existing short code), generates a nanoid (7-8 chars), stores it, and returns the short URL.

3. **Implement redirect.** `GET /:shortCode` looks up the original URL by short code. If found, increment the click counter and redirect (302 Found). If not found, return 404. This is the most performance-critical endpoint.

4. **Add click tracking.** Every redirect increments a counter. `GET /stats/:shortCode` returns: original URL, short code, total clicks, and creation date. This provides basic analytics without complex event tracking.

5. **Implement duplicate detection.** Before creating a new short URL, check if the original URL already exists in the database. If it does, return the existing short code instead of creating a duplicate. This saves storage and keeps URLs consistent.

6. **Add rate limiting and security.** Rate limit the creation endpoint (prevent abuse) but not the redirect endpoint (must be fast). Helmet for security headers. Validate URLs to prevent XSS via malicious redirect targets.

7. **Deploy to Render.** SQLite in the `data/` directory. No external services needed. Short URLs use the Render domain as the base.

## Deployment

Deploy on Render.com. The short URL base is your Render domain. No external database
or cache services required.

## Tips

- nanoid generates URL-safe, collision-resistant IDs. At 7 characters with the default alphabet (64 chars), you get ~4.4 trillion possible combinations. Collisions are astronomically unlikely — but check for uniqueness on insert anyway.
- Use 302 (temporary) redirect, not 301 (permanent). With 301, browsers cache the redirect forever — you can never update or disable the short URL. With 302, every click hits your server (enabling accurate tracking).
- Extension: add custom short codes (user-chosen aliases), expiration dates, password-protected links, or a QR code generator for each short URL.

## README Guidance

The project repo's README should include a description, API endpoints with examples,
how redirect works, tech stack, and setup instructions.
