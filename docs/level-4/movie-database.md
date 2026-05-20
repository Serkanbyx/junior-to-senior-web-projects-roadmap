# Movie Database

> A fullstack movie app combining an external API (TMDB) with user-saved favorites in MongoDB.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://movie-databasee.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/movie-database)

---

## Purpose

This project teaches the hybrid pattern: fetch data from an external API (TMDB) for the
catalog, but store user-specific data (favorites, watchlist, ratings) in your own database.
It's the architecture used by any app that wraps a third-party data source with user features
— think Goodreads (wraps book data) or Letterboxd (wraps movie data).

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT
- **Key libraries / tools:** TMDB API, Axios, React Router
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Set up the TMDB proxy.** Backend endpoint `GET /movies/search?q=...` and `GET /movies/:id` that proxy TMDB API calls with your server-side API key. Transform the response to a cleaner shape.
2. **Build user features API.** `POST /favorites` (save movie ID + basic info to user's favorites), `DELETE /favorites/:movieId`, `GET /favorites` (list user's saved movies). Store enough info (title, poster, year) to render without re-fetching from TMDB.
3. **Build the discovery UI.** A homepage with trending movies, a search bar, and genre filters. All data comes from TMDB via your backend proxy. Render movie cards with poster, title, year, and rating.
4. **Build the movie detail page.** Fetch full movie details from TMDB: synopsis, cast, trailers, similar movies. Add a "Save to Favorites" button that calls your backend. Show whether the movie is already favorited.
5. **Build the favorites page.** Show all saved movies from your MongoDB (not TMDB). This page works even if TMDB is down because you stored the essential data locally when the user favorited it.
6. **Add watchlist and ratings.** Beyond favorites: a "watchlist" (movies to watch later) and user ratings (1-5 stars). Store in MongoDB. Show the user's rating on the detail page if they've rated it.
7. **Handle API failures gracefully.** If TMDB is slow or down, show cached data or a friendly error. Never let the external API's issues crash your UI — the favorites page should always work.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `TMDB_API_KEY`. Frontend on Netlify
with `VITE_API_URL`. The TMDB key stays server-side only.

## Tips

- Store denormalized movie data in favorites (title, poster URL, year) so you can render the favorites page without calling TMDB. This is intentional denormalization for resilience.
- TMDB's API is rate-limited. Add a simple in-memory cache on your backend for popular queries (trending, search results) with a 10-minute TTL.
- Extension: add a "watched" tracker with viewing dates, movie lists (like Letterboxd lists), social features (share favorites), or recommendation based on ratings.

## README Guidance

The project repo's README should include a description, screenshots of movie grid and
detail page, tech stack, TMDB API setup instructions, environment variables, and local setup.
