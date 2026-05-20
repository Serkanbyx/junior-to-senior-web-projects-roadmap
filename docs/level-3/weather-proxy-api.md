# Weather Proxy API

> A secure weather proxy that hides API keys from clients, with in-memory caching, rate limiting, and input validation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-proxy-api-4l5h.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-proxy-api)

---

## Purpose

This project teaches the Backend-for-Frontend (BFF) proxy pattern. Instead of calling
OpenWeatherMap directly from the browser (exposing your API key), your Express server acts
as a proxy: the client calls your server, your server calls OpenWeatherMap with the hidden
key, and returns the data. This is the correct architecture for any third-party API integration.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** None (in-memory cache only)
- **HTTP Client:** Axios
- **Validation:** express-validator
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Build the proxy endpoint.** `GET /weather?city=London` calls OpenWeatherMap's API with your server-side key. Transform the verbose response into a clean shape the frontend expects. Return only the data you need (temperature, humidity, description, icon).

2. **Implement in-memory caching.** Store responses in a JavaScript Map with a TTL (e.g., 10 minutes). On request, check cache first — if fresh, return cached. If stale or missing, fetch from OpenWeatherMap and cache. This reduces API calls and improves response times.

3. **Add input validation.** Validate the city parameter: non-empty string, reasonable length, no special characters that could cause issues. Use express-validator. Return 400 with a clear message for invalid input.

4. **Apply rate limiting.** Limit requests per IP to prevent abuse of your OpenWeatherMap quota. express-rate-limit with a window (e.g., 100 requests per 15 minutes). Return 429 Too Many Requests with retry-after header.

5. **Add error handling for external API.** If OpenWeatherMap returns 404 (city not found), pass it through as 404 to the client. If it returns 500 or times out, return 503 Service Unavailable. Never expose the raw external API error to the client.

6. **Add Swagger documentation.** Document the single endpoint with query parameters, response schema, and error responses. This makes it easy for frontend developers to integrate.

7. **Deploy to Render.** Set `OPENWEATHER_API_KEY` as an environment variable. In-memory cache resets on deploy (acceptable — it refills quickly). No database needed.

## Deployment

Deploy on Render.com. Set `OPENWEATHER_API_KEY` in environment variables. No database
service required — cache lives in memory.

## Tips

- The proxy pattern isn't just about hiding keys. It also lets you: transform responses (clean up verbose APIs), cache aggressively (reduce costs), add auth (gate access to the data), and combine multiple API calls into one endpoint.
- In-memory cache is simple but resets on server restart. For production with multiple instances, use Redis. For a single Render instance, in-memory is perfectly fine.
- Extension: add 5-day forecast endpoint, geocoding (coordinates → city name), or batch multiple cities in one request.

## README Guidance

The project repo's README should include a description, API endpoint documentation, caching
explanation, rate limiting details, tech stack, and setup instructions.
