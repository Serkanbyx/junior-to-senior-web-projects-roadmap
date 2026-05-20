# Weather App with Login

> A fullstack weather app with server-side API proxy, 5-day forecasts, favorites system, and JWT authentication.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-mern.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-app-with-login)

---

## Purpose

This project teaches the "backend-for-frontend" proxy pattern — the Express server hides
the OpenWeatherMap API key from the client, adds auth gating, and shapes responses. The
favorites system (save up to 10 cities) demonstrates user-scoped data attached to an
external API. It connects your Level 2 weather frontend with your Level 3 auth backend
into a cohesive product.

## Tech Stack

- **Frontend:** React 19, Vite 8, Tailwind CSS 4, React Router 7
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT (jsonwebtoken 9) + bcrypt
- **External API:** OpenWeatherMap (proxied through backend)
- **Security:** Helmet, rate limiting, CORS whitelist
- **UX:** Axios interceptors (auto token injection), skeleton loaders, React Hot Toast
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build the auth backend.** Register and login endpoints. JWT-based stateless auth. User model with email, hashed password, and `favorites: [String]` array (max 10 cities). Protected routes require valid token.

2. **Build the weather proxy endpoint.** `GET /api/weather?city=London` — requires auth, calls OpenWeatherMap with the server-side API key, transforms the response into a clean shape (current weather + 5-day forecast), and returns it. The API key never reaches the client.

3. **Build the favorites API.** `POST /api/favorites` (add city, max 10), `DELETE /api/favorites/:city` (remove), `GET /api/favorites` (list). Stored in the user document. Validate city name before saving.

4. **Build the auth UI.** Login and register pages with form validation. Protected routes redirect unauthenticated users. Axios interceptors auto-inject the JWT and handle 401 globally (redirect + state cleanup).

5. **Build the weather dashboard.** Search bar that queries the proxy endpoint. Display current conditions (temperature, humidity, wind, icon) and 5-day forecast with daily ranges. Skeleton loaders during API calls. User-friendly errors for invalid cities or network failures.

6. **Implement the favorites system.** A star/heart button on the weather card to save/unsave the current city. A favorites section showing saved cities for quick access (click to load their weather). Limit enforcement (10 max) with clear messaging.

7. **Handle edge cases.** Invalid city names (show friendly error), network timeouts, API rate limits from OpenWeatherMap, unauthenticated access attempts, and empty favorites state.

## Deployment

Backend on Render (set `MONGODB_URI`, `JWT_SECRET`, `OPENWEATHER_API_KEY`, `CLIENT_URL`).
Frontend on Netlify (set `VITE_API_URL`). The weather API key stays exclusively on the backend.

## Tips

- The proxy pattern is essential for any project using paid or rate-limited external APIs. Without it, anyone can inspect your frontend code, extract the API key, and abuse your quota.
- Axios interceptors handle two things: (1) auto-inject the auth token on every request, (2) catch 401 responses globally and redirect to login. This eliminates repetitive auth logic from every component.
- Extension: add geolocation-based auto-detection, weather alerts/notifications, hourly forecast, or a weekly digest email to users with their favorites' weather.

## README Guidance

The project repo's README should include a description, screenshots of login and weather
dashboard, tech stack, environment variables, and setup instructions.
