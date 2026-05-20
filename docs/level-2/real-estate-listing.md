# Real Estate Listing

> A property listing app with advanced filtering, interactive Leaflet maps, and responsive card grids.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://real-estate-listingg.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/real-estate-listing)

---

## Purpose

This project teaches you multi-criteria filtering, sorting, and map integration — the core
of any listing/marketplace UI. You'll learn to compose multiple filter states (price range,
bedrooms, property type) into a single derived dataset, render results both as cards and map
markers, and keep both views synchronized. It's the foundation for any "search results" page.

## Tech Stack

- **Frontend:** React 18, TypeScript, Tailwind CSS
- **Backend:** none (uses local/mock data)
- **Database:** none
- **Key libraries / tools:** Zustand (state), Leaflet (maps), shadcn/ui (components)
- **Deployment:** Netlify

## Build Steps

1. **Model the property data.** Define a TypeScript interface for a property: `{ id, title, price, bedrooms, bathrooms, sqft, type, lat, lng, image, description }`. Create a JSON dataset of 30+ properties with realistic UK property data.
2. **Build the filter panel.** Price range (min/max inputs or a slider), bedrooms (1-5+ buttons), property type (flat, house, bungalow), and sort order (price asc/desc, newest). Store all filter state in Zustand.
3. **Derive filtered results.** Write a selector/computed function that takes all properties and active filters, returning only matching items. Apply filters sequentially: price range → bedrooms → type → sort. Memoize the result to avoid re-filtering on every render.
4. **Render the card grid.** Display filtered properties as responsive cards with image, price, key stats (beds, baths, sqft), and a brief description. Use CSS Grid with `auto-fill`. Show a count of results and an empty state when no properties match.
5. **Integrate Leaflet map.** Add a map view showing a marker for each filtered property. Clicking a marker highlights the corresponding card (and vice versa). Use `react-leaflet` for declarative map rendering. Fit the map bounds to the visible markers.
6. **Build list/map toggle.** On desktop, show list and map side by side. On mobile, provide a toggle between list view and full-screen map. Animate the transition between views.
7. **Add property detail.** Clicking a card opens a detail view with full description, image gallery, location map, and key features. Use a modal or a separate route.

## Deployment

Deploy on Netlify as a static site. No API keys needed since data is local.
Leaflet tiles come from OpenStreetMap (free, no key required).

## Tips

- Composable filters are cleaner when each filter is a pure function: `(properties) => filtered`. Chain them together rather than writing one giant filter function with nested conditions.
- Leaflet with React needs careful lifecycle management. Use `react-leaflet` v4+ which handles re-renders properly, or memoize the map component to prevent unnecessary redraws.
- Extension: add a "save search" feature, property comparison view, or integrate with a real estate API for live data.

## README Guidance

The project repo's README should include a short description, screenshots of list view and
map view, the live demo link, tech stack, and local setup instructions with `npm run dev`.
