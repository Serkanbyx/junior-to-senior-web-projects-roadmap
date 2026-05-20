# Weather App with Login

> A fullstack weather app with user authentication gating API consumption and saved preferences.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-mern.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-app-with-login)

---

## Purpose

This project teaches you to gate features behind authentication — a common SaaS pattern.
The weather data is only accessible to logged-in users, and each user can save favorite
cities. It combines the Level 2 weather frontend with Level 3 auth backend, proving you can
connect previously separate skills into a cohesive fullstack product.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT with protected routes
- **Key libraries / tools:** Axios, OpenWeatherMap API (proxied through backend), React Router
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build the auth backend.** Register, login, and token refresh endpoints. User model with email, hashed password, and a `favorites: [String]` array for saved cities.
2. **Build the weather proxy.** A protected endpoint `GET /weather?city=London` that requires auth, calls OpenWeatherMap with the server-side API key, and returns the data. The API key never reaches the client.
3. **Implement favorites API.** `POST /favorites` (add city), `DELETE /favorites/:city` (remove), `GET /favorites` (list). Each user has their own favorites list stored in their user document.
4. **Build the auth UI.** Login and register pages. On successful auth, redirect to the dashboard. Show the user's name in the header with a logout button. Protect all weather routes with a PrivateRoute.
5. **Build the weather dashboard.** A search bar that calls the backend weather proxy. Display current weather and 5-day forecast. Add a "star" button to save/unsave the current city to favorites.
6. **Display favorite cities.** A section showing weather cards for all favorite cities. Fetch weather for all favorites in parallel on dashboard load. Allow removing favorites with one click.
7. **Handle the logged-out state.** Show a landing page with a preview/description when not logged in. Redirect to login on any attempt to access weather features. Show clear CTAs to register.

## Deployment

Backend on Render (set `MONGODB_URI`, `JWT_SECRET`, `OPENWEATHER_API_KEY`). Frontend on
Netlify (set `VITE_API_URL`). The weather API key stays exclusively on the backend.

## Tips

- This is a great example of the "backend-for-frontend" pattern: the Express server isn't just an API — it's a gateway that adds auth, hides credentials, and shapes responses for the specific frontend.
- Fetching weather for multiple favorites? Use `Promise.allSettled` instead of `Promise.all` — if one city fails, the others still render.
- Extension: add weather alerts/notifications, location-based auto-detection, or a weekly weather digest email.

## README Guidance

The project repo's README should include a description, screenshots of login and weather
dashboard, tech stack, environment variables for both services, and local setup instructions.
