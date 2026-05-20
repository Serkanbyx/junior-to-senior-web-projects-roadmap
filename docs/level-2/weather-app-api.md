# Weather App (API)

> An advanced weather PWA with city search, 5-day forecast, favorites, and offline support — powered by a real weather API.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-app-advancedd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-app-advanced)

---

## Purpose

This is your first project that talks to a real, authenticated API. It teaches you to manage
API keys securely (via serverless functions), handle async data fetching with loading/error
states, and cache responses for offline use. The jump from Level 1's mock-data weather app
to this one mirrors the jump from tutorial projects to production code.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Netlify Functions (serverless proxy for API key)
- **Database:** none (favorites stored client-side via Zustand persist)
- **Key libraries / tools:** Zustand (state management), OpenWeatherMap API, Service Worker (PWA)
- **Deployment:** Netlify (static + serverless functions)

## Build Steps

1. **Scaffold with Vite.** Create a React + TypeScript project. Configure Tailwind CSS for utility-first styling. Set up the folder structure: `components/`, `hooks/`, `store/`, `functions/`.
2. **Build the serverless proxy.** Create a Netlify Function that receives a city name, calls the OpenWeatherMap API with the secret key stored in an environment variable, and returns the JSON. This keeps the API key off the client entirely.
3. **Implement city search.** Build a search input with debouncing (300ms delay) so you don't fire a request on every keystroke. On submit, call your serverless function and display loading/error/success states explicitly.
4. **Render current weather and forecast.** Parse the API response into a current-weather card (temp, condition, icon, humidity, wind) and a 5-day forecast row. Use TypeScript interfaces to type the API response — this catches shape errors at compile time.
5. **Add favorites with Zustand.** Create a global store with `zustand/persist` middleware. Users can star a city to save it. On app load, fetch weather for all favorites in parallel with `Promise.all`.
6. **Make it a PWA.** Register a service worker that caches static assets and API responses. Add a `manifest.json` for installability. Handle the offline state gracefully — show cached data with a "last updated" timestamp.
7. **Polish the UI.** Add weather-appropriate background gradients (blue for clear, gray for cloudy), smooth transitions between states, and responsive breakpoints for mobile/tablet/desktop.

## Deployment

Deploy on Netlify. Set the `OPENWEATHER_API_KEY` environment variable in the Netlify dashboard.
The serverless function automatically deploys from the `netlify/functions/` directory. PWA
features activate once served over HTTPS.

## Tips

- Never expose API keys in client-side code — even if the API is "free." Serverless functions are the simplest solution and Netlify provides them at no cost for low traffic.
- Zustand with `persist` middleware is lighter than Redux for small apps and gives you localStorage persistence in one line.
- Extension: add geolocation-based weather (ask for the user's location), hourly forecast charts, or weather alerts.

## README Guidance

The project repo's README should include a short description, a screenshot showing current
weather + forecast, the live demo link, tech stack, environment variable setup instructions,
and steps to run locally with `npm run dev`.
