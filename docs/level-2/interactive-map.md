# Interactive Map

> An interactive map with pin management, category filtering, route directions, and geolocation.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://interactive-mappp.netlify.app/map) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/interactive-map)

---

## Purpose

This project teaches you to integrate a map library (Leaflet) into a React app, manage
geospatial data (latitude/longitude), and build CRUD interactions directly on a map canvas.
You'll learn form validation with React Hook Form + Zod, category-based filtering on spatial
data, and routing/directions APIs. Maps are used in logistics, real estate, delivery, and
social apps — this skill transfers broadly.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** none
- **Database:** LocalStorage (via Zustand persist)
- **Key libraries / tools:** Leaflet (react-leaflet), Zustand, React Hook Form, Zod
- **Deployment:** Netlify

## Build Steps

1. **Set up the map.** Install `react-leaflet` and render a full-screen map centered on a default location. Add OpenStreetMap tile layer. Implement zoom controls and a "locate me" button using the Geolocation API.
2. **Add pin creation.** On map click, open a form (React Hook Form + Zod validation) to create a pin: title, description, category (restaurant, park, shop, etc.), and the clicked coordinates. Validate that title is non-empty and category is selected.
3. **Render pins as markers.** For each pin in the store, render a Leaflet marker with a custom icon based on category. On marker click, show a popup with the pin's details and edit/delete actions.
4. **Implement category filtering.** A sidebar or toolbar with category toggles. When a category is deselected, hide its markers from the map. Use Zustand to store active filters and derive visible pins as a computed selector.
5. **Build route/directions.** Allow the user to select two pins and draw a route between them on the map. Use the OSRM (Open Source Routing Machine) API to get the route polyline. Display distance and estimated time.
6. **Add search and geolocation.** A search bar that geocodes an address (using Nominatim API) and pans the map to that location. The "locate me" button uses `navigator.geolocation` to center on the user's position.
7. **Persist and manage pins.** Store all pins in Zustand with persist. Build a list view sidebar showing all pins sorted by distance from current map center. Allow bulk delete and export as GeoJSON.

## Deployment

Deploy on Netlify. Leaflet tiles and Nominatim geocoding are free (OpenStreetMap).
OSRM routing is also free and requires no API key. No environment variables needed.

## Tips

- react-leaflet v4 uses React context heavily. Always nest map components (`Marker`, `Popup`, `TileLayer`) inside the `MapContainer` — they can't be rendered outside it.
- Geolocation permission requests should be triggered by a user action (button click), not on page load. Browsers may block silent geolocation requests.
- Extension: add marker clustering for dense areas (using `react-leaflet-cluster`), draw polygons/areas, or add real-time location sharing.

## README Guidance

The project repo's README should include a short description, a screenshot showing the map
with pins and a route, the live demo link, tech stack, features list (pins, filtering, routes,
geolocation), and local dev instructions.
