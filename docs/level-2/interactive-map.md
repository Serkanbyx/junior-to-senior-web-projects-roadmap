# Interactive Map

> An interactive map application with pin management, category filtering, route directions, Leaflet, and TanStack React Query.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://interactive-mappp.netlify.app/map) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/interactive-map)

---

## Purpose

This project teaches geospatial UI: placing markers on maps, clustering, filtering by
category, and drawing routes. It also introduces TanStack React Query for server state
management — the modern alternative to fetching in useEffect. You'll learn to think
spatially: coordinates, zoom levels, bounding boxes, and marker interactions.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS, tailwind-merge, clsx
- **State:** Zustand (local state) + TanStack React Query (server/async state)
- **Maps:** Leaflet + react-leaflet
- **Forms:** React Hook Form + Zod (pin creation form)
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Set up Leaflet with React.** Install leaflet and react-leaflet. Create the base map with `MapContainer`, `TileLayer` (OpenStreetMap tiles). Handle map events: click (add pin), zoom, pan.

2. **Build pin management.** Click map to add a pin (opens form dialog). Pin data: name, description, category, coordinates. Store pins in Zustand. Render as Leaflet Markers with popup info.

3. **Implement category filtering.** Predefined categories (restaurants, parks, shops, etc.) with color-coded markers. Filter sidebar: toggle categories on/off. Only matching pins display on the map.

4. **Add route directions.** Select two pins and draw a route between them. Use Leaflet Routing Machine or a routing API. Show distance and estimated time.

5. **Integrate TanStack React Query.** For any async data (geocoding, routing API calls), use React Query instead of manual fetch + state. Automatic caching, refetching, and loading/error states.

6. **Build the pin form with RHF + Zod.** Create/edit pin dialog: name (required), description (optional), category (select). Coordinates auto-filled from map click position.

7. **Deploy on Netlify.** Static app with all pins stored client-side.

## Tips

- TanStack React Query replaces the `useEffect → fetch → setState → loading/error` pattern with a single `useQuery` hook. It handles caching, background refetch, stale data, and retry logic automatically.
- Leaflet markers need explicit icon configuration in React (the default icon paths break with bundlers). Import the icon from leaflet and configure it, or use a custom SVG marker.
- Extension: add geolocation (center map on user's location), marker clustering (for many pins), heatmap layer, or offline map tiles.
