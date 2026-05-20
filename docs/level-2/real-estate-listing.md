# Real Estate Listing

> A UK property listing app with advanced filtering, interactive Leaflet maps, shadcn/ui components, and Zustand state management.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://real-estate-listingg.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/real-estate-listing)

---

## Purpose

This project teaches complex filtering (multiple criteria simultaneously), map integration
(Leaflet), and building polished UIs with shadcn/ui (Radix primitives + Tailwind). Property
listings are the perfect domain: users filter by price range, bedrooms, location, and type
— all at once. The map view adds a spatial dimension to the data.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS, shadcn/ui (Radix-based component library)
- **State:** Zustand
- **Maps:** Leaflet + react-leaflet
- **UI Components:** Radix UI (dialog, select, slider)
- **Forms:** React Hook Form + Zod
- **Icons:** Lucide React
- **Utilities:** clsx
- **Deployment:** Netlify

## Build Steps

1. **Set up the data layer.** Property data from a JSON file (`api-data.json`). Each property: title, price, bedrooms, bathrooms, area, type, coordinates, images. Zustand store holds properties and active filters.

2. **Build the filter system.** Multiple simultaneous filters: price range (Radix slider), bedrooms (select), property type (select), search by location. Filters combine with AND logic. Show result count that updates as filters change.

3. **Build the property card grid.** Responsive grid of property cards with image, price, bedrooms/bathrooms count, and area. Click to view detail. Cards re-render efficiently when filters change.

4. **Integrate Leaflet map.** Map view showing property markers at their coordinates. Click a marker to see property preview popup. Map and list are synced — filtering updates both views.

5. **Build the detail view.** Radix Dialog showing full property info: image gallery, description, features list, location on map, and contact form.

6. **Style with shadcn/ui.** Pre-built accessible components (Select, Slider, Dialog) that use Radix primitives under the hood with Tailwind styling. Consistent, professional UI without building everything from scratch.

7. **Deploy on Netlify.** Static site with JSON data. No backend needed.

## Tips

- Leaflet with React: use react-leaflet for declarative map components. `<MapContainer>`, `<TileLayer>`, `<Marker>`, `<Popup>` — compose like any React component.
- shadcn/ui is not a library you install — it's components you copy into your project. You own the code and can customize everything. This gives you the polish of a component library with the flexibility of custom code.
- Extension: add saved searches, property comparison, contact agent form, or virtual tour integration.
