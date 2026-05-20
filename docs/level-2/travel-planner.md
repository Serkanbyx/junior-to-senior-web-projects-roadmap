# Travel Planner

> A travel planning app with drag-and-drop itinerary management, Unsplash city images, and multi-format export.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://travel-plannerrr.netlify.app/plans) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/travel-planner)

---

## Purpose

This project teaches you multi-step state management and drag-and-drop reordering in a React
context. You'll manage nested data (trips → days → activities), handle complex user interactions
(dragging items between lists), and integrate with an image API. The export feature introduces
client-side file generation in multiple formats — a skill used in any app with "download" functionality.

## Tech Stack

- **Frontend:** React 18, TypeScript, Tailwind CSS
- **Backend:** none
- **Database:** LocalStorage (via Zustand persist)
- **Key libraries / tools:** Zustand, dnd-kit (drag-and-drop), Unsplash API (city images)
- **Deployment:** Netlify

## Build Steps

1. **Model the data.** Define nested types: `Trip { id, destination, startDate, endDate, coverImage, days: Day[] }`, `Day { id, date, activities: Activity[] }`, `Activity { id, title, time, notes, location }`. Store in Zustand with persist.
2. **Build trip CRUD.** A form to create a trip (destination, dates). On creation, automatically generate `Day` objects for each date in the range. Show all trips as cards with cover images fetched from the Unsplash API based on the destination name.
3. **Build the itinerary view.** Display a trip's days as columns (or tabs on mobile). Each day shows its activities in time order. An "add activity" button opens a form for title, time, notes, and location.
4. **Implement drag-and-drop.** Use dnd-kit to make activities draggable within a day (reorder) and between days (reschedule). Handle the `onDragEnd` event to update the Zustand store: remove from source array, insert into target array at the drop index.
5. **Integrate Unsplash.** On trip creation, fetch a city photo from the Unsplash API using the destination as a search query. Display it as the trip's cover image. Handle API failures with a placeholder gradient.
6. **Add multi-format export.** Generate a downloadable itinerary in multiple formats: plain text (`.txt`), Markdown (`.md`), and JSON. Build the content string programmatically from the trip data and trigger download with `Blob` + `URL.createObjectURL`.
7. **Polish the UX.** Add visual drag feedback (ghost element, drop indicators), smooth animations on reorder, empty states for days without activities, and a responsive layout that works on mobile (single column with day tabs).

## Deployment

Deploy on Netlify. If using the Unsplash API, set the access key as a Netlify environment
variable and proxy through a serverless function. For demo purposes, a limited number of
requests can be made directly with the client key.

## Tips

- dnd-kit is the modern React drag-and-drop library (replaces react-beautiful-dnd which is deprecated). Its `useSortable` hook handles most reorder cases with minimal code.
- Nested state updates (moving an activity from Day A to Day B) are the trickiest part. Use Immer or spread carefully — a shallow copy at the wrong level will cause stale state bugs.
- Extension: add a map view with pins for each activity's location, budget tracking per trip, or collaborative planning with shareable links.

## README Guidance

The project repo's README should include a short description, screenshots of the trip list
and itinerary view with drag-and-drop, the live demo link, tech stack, features list, and
local dev instructions.
