# Weather App (API)

> An advanced weather PWA with city search, 5-day forecast, favorites, charts, and offline support via Service Worker.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-app-advancedd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-app-advanced)

---

## Purpose

This is the Level 1 weather app rebuilt properly. Instead of basic fetch calls, you now
handle real API integration with key protection (Netlify Functions), state management with
persistence (Zustand), data visualization (Recharts), and offline capability (PWA). It
teaches the patterns that separate toy projects from production apps.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS, tailwind-merge, clsx
- **State:** Zustand with persistence (favorites survive page reload)
- **Charts:** Recharts (temperature trends)
- **Forms:** React Hook Form + Zod validation
- **API proxy:** Netlify Functions (hides OpenWeatherMap API key)
- **PWA:** vite-plugin-pwa + Workbox (offline support)
- **UX:** Sonner (toast notifications), Lucide React (icons), React Router
- **Deployment:** Netlify (static + serverless functions)

## Build Steps

1. **Set up Netlify Functions as API proxy.** Create a serverless function in `netlify/functions/` that calls OpenWeatherMap with the server-side API key. The frontend calls your function — never the external API directly. This keeps your key secret.

2. **Build the search with React Hook Form + Zod.** City search input validated with Zod (non-empty, reasonable length). On submit, call the Netlify Function. Handle loading, error, and empty states explicitly.

3. **Implement Zustand for state.** Store current weather, forecast, and favorites in Zustand. Use the `persist` middleware to save favorites to localStorage — they survive page reload and even offline.

4. **Build the 5-day forecast with Recharts.** Fetch forecast data and render a temperature line chart with Recharts. Show daily high/low, humidity, and weather icons. The chart makes trends visible at a glance.

5. **Add favorites system.** Save cities to Zustand (persisted). Show weather cards for all favorites on the dashboard. One-click add/remove. Limit to prevent abuse.

6. **Make it a PWA.** Configure vite-plugin-pwa with Workbox for offline caching. Add a manifest.json, service worker, and install prompt. The app works without internet using cached data.

7. **Deploy on Netlify.** `netlify.toml` configures both the static site and the serverless function. Set `OPENWEATHER_API_KEY` in Netlify environment variables.

## Tips

- Netlify Functions are the simplest way to hide API keys in a frontend-only project. No separate backend needed — just a `netlify/functions/weather.ts` file that proxies the request.
- Zustand's persist middleware: `create(persist((set) => ({...}), { name: 'weather-storage' }))` — one line to make any store persist to localStorage.
- Extension: add geolocation auto-detect, weather alerts, hourly forecast, or theme based on weather condition.
