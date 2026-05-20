# Travel Planner

> A travel planning app with drag-and-drop itinerary (dnd-kit), Unsplash city images, date picker, and multi-format export.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://travel-plannerrr.netlify.app/plans) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/travel-planner)

---

## Purpose

This project teaches drag-and-drop — one of the most complex UI interactions to implement
correctly. Using dnd-kit (the modern React DnD library), you'll build reorderable itinerary
items, date-based trip planning, and data export. It combines multiple advanced patterns:
DnD, date handling, multi-step state, and external API integration.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS, class-variance-authority, clsx, tailwind-merge
- **State:** Zustand
- **Drag & Drop:** dnd-kit (core, sortable, modifiers, utilities)
- **UI Components:** Radix UI (dialog, label, select, tabs)
- **Date picker:** react-day-picker
- **Dates:** date-fns
- **Routing:** React Router
- **Validation:** Zod
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Build the trip CRUD.** Create trips with: destination, start date, end date, cover image (from Unsplash API). List all trips. Delete trips. Store in Zustand with persistence.

2. **Integrate Unsplash for city images.** On trip creation, fetch a city photo from Unsplash API to use as the trip cover. Display beautiful destination imagery throughout the app.

3. **Build the itinerary with dnd-kit.** Each day of the trip has activities. Activities are drag-and-drop sortable within a day (reorder) and between days (move to different day). Use `@dnd-kit/sortable` with sensors and modifiers.

4. **Add the date picker.** react-day-picker for selecting trip dates. Validate: end date must be after start date. Auto-generate day slots in the itinerary based on the date range. date-fns for all date math.

5. **Build activity management.** Add activities to each day: name, time, location, notes. Edit and delete. The itinerary is a nested structure: trip → days → activities (reorderable).

6. **Implement multi-format export.** Export the complete itinerary as JSON (machine-readable) or CSV (spreadsheet-friendly). Generate a downloadable file with trip details and all activities.

7. **Style with Radix + CVA.** Radix Dialog for modals, Select for dropdowns, Tabs for view switching. CVA for consistent component variants throughout the app.

## Tips

- dnd-kit is the successor to react-beautiful-dnd. It's modular: import only what you need (core for basic DnD, sortable for lists, modifiers for constraints). The `useSortable` hook makes any component draggable.
- Nested sortable lists (activities within days) require `SortableContext` per day with unique IDs. Moving items between days uses the `onDragEnd` handler to detect which container the item was dropped into.
- Extension: add map view with pins for each activity, budget tracking per trip, collaborative planning (share trip link), or integration with booking APIs.
