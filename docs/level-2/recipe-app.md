# Recipe App

> A recipe discovery app with search, cuisine filtering, and offline favorites — powered by the Spoonacular API.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://recipe-web-appp.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/recipe-web-app)

---

## Purpose

This project builds on API consumption by adding multi-parameter search, category filtering,
and detail views with nested data. It teaches you to manage list → detail navigation patterns,
handle paginated API responses, and build a "search + filter" UX that feels instant. The
favorites system introduces client-side data persistence with offline access.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Netlify Functions (serverless API proxy)
- **Database:** none (favorites persisted via Zustand persist)
- **Key libraries / tools:** Zustand, Spoonacular API, Service Worker (PWA)
- **Deployment:** Netlify (static + functions)

## Build Steps

1. **Set up the API proxy.** Create a Netlify Function that wraps the Spoonacular API. Accept query parameters (search term, cuisine type, number of results) and forward them with the API key. Return the JSON response.
2. **Build the search interface.** A search bar with debounced input and a cuisine filter dropdown (Italian, Mexican, Asian, etc.). Combine both into a single API call. Show a loading skeleton while fetching.
3. **Render the recipe grid.** Display results as responsive cards with recipe image, title, cook time, and servings. Use CSS Grid with `auto-fill` for a fluid layout. Handle the empty state ("No recipes found") explicitly.
4. **Implement detail view.** On card click, fetch the full recipe details (ingredients, steps, nutrition). Render in a modal or a new route. Parse the structured ingredients list and numbered instructions from the API response.
5. **Add favorites.** A heart icon on each card that toggles the recipe in/out of a Zustand store with `persist` middleware. Create a dedicated "Favorites" page that renders saved recipes from local storage — works offline.
6. **Handle edge cases.** Rate limit errors from the API (show a friendly "try again later" message), missing images (show a placeholder), and recipes without complete instructions (show a fallback).
7. **PWA and offline.** Cache the app shell and previously viewed recipes via service worker. When offline, serve cached content and disable search (show an offline banner).

## Deployment

Deploy on Netlify with the `SPOONACULAR_API_KEY` environment variable. The function proxy
keeps the key secure. PWA caching makes previously viewed recipes available offline.

## Tips

- Spoonacular has strict rate limits on the free tier. Cache responses in memory or localStorage to avoid redundant calls during the same session.
- The list → detail pattern (grid of cards → full detail view) is one of the most common UI patterns in web apps. Master it here and you'll use it in every CRUD app.
- Extension: add meal planning (select recipes for each day of the week) or a shopping list that aggregates ingredients from multiple recipes.

## README Guidance

The project repo's README should include a short description, a screenshot of the recipe grid
and a detail view, the live demo link, tech stack, API setup instructions, and local dev steps.
