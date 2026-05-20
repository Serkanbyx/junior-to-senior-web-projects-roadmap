# Movie Database

> A fullstack movie app powered by TMDB API with favorites, watchlist, trending content, and Framer Motion animations.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://movie-databasee.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/movie-database)

---

## Purpose

This project teaches the hybrid pattern: fetch catalog data from an external API (TMDB)
while storing user-specific data (favorites, watchlist) in your own MongoDB. It's the
architecture used by any app that wraps a third-party data source with user features —
Letterboxd wraps TMDB, Goodreads wraps book APIs. You also learn to add animation polish
with Framer Motion.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, React Hook Form
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT + bcryptjs
- **External API:** TMDB (proxied through backend with server-side Axios)
- **Animation:** Framer Motion 11
- **Email:** Nodemailer
- **Validation:** express-validator
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize
- **UX:** React Icons
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build the TMDB proxy.** Backend endpoints that proxy TMDB API calls with the server-side API key: trending movies/TV (updated daily), search by query, movie/TV details by ID. Transform TMDB's verbose response into a cleaner shape for the frontend.

2. **Build user features API.** Favorites and watchlist management: `POST /favorites` (add), `DELETE /favorites/:id` (remove), `GET /favorites` (list). Store denormalized data (title, poster path, year, media type) so the favorites page works independently of TMDB.

3. **Build the discovery UI.** Homepage showing trending movies and TV shows (fetched daily from TMDB via proxy). Search bar with results grid. Framer Motion page transitions and card hover animations for visual polish.

4. **Build the detail page.** Full movie/TV detail from TMDB: synopsis, cast, rating, genres, trailer (YouTube embed), and similar titles. Favorites and watchlist toggle buttons. Show whether the user has already saved this item.

5. **Build the favorites and watchlist pages.** Display saved items from MongoDB (not TMDB). This page works even if TMDB is down because you stored essential data locally. Separate pages for favorites vs. watchlist with remove functionality.

6. **Add Framer Motion animations.** Page transitions (fade/slide between routes), card entrance animations (stagger effect on grid items), hover scale on movie cards, and smooth modal animations. These elevate the perceived quality significantly.

7. **Handle external API edge cases.** TMDB rate limits, network timeouts, missing poster images (fallback placeholder), and search with no results. The favorites page should always work regardless of TMDB status.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `TMDB_API_KEY`, `SMTP_*`. Frontend on
Netlify with `VITE_API_URL`. The TMDB key stays server-side only.

## Tips

- Store denormalized movie data in favorites (title, poster URL, year) so you can render the favorites page without calling TMDB. This is intentional denormalization for resilience — your favorites page has zero external dependencies.
- Framer Motion's `AnimatePresence` component enables exit animations. Wrap your route outlet with it to get smooth page transitions. Use `layout` prop on list items for automatic reorder animations.
- Extension: add user ratings (1-5 stars), movie lists (custom collections), discover by genre, or a recommendation algorithm based on favorited genres.

## README Guidance

The project repo's README should include a description, screenshots/GIF of the animated
UI, TMDB API setup instructions, tech stack, environment variables, and setup steps.
