# Notes MERN

> A fullstack notes app with authentication, rich text, and seamless frontend-backend data flow.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://notes-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/notes-mern)

---

## Purpose

Building on the To-Do MERN foundation, this project adds richer content (notes with titles
and bodies), user-scoped data across the full stack, and more complex state management. It
reinforces the auth → protected routes → user-scoped CRUD pattern and introduces you to
handling larger payloads and text content between frontend and backend.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT with protected routes
- **Key libraries / tools:** Axios, React Router, Zustand or Context API
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the API.** Auth routes (register, login, refresh) + notes CRUD (`GET /notes`, `GET /notes/:id`, `POST /notes`, `PATCH /notes/:id`, `DELETE /notes/:id`). All notes routes require auth middleware. Notes are scoped to the authenticated user.
2. **Build the backend.** Note model: `{ title, content, tags, user, createdAt, updatedAt }`. Implement all CRUD operations with user scoping. Add search via query param (`?q=keyword` searches title and content).
3. **Create the auth flow on frontend.** Register/login forms with validation. Store auth state in context or Zustand. Create a `PrivateRoute` component that redirects to login if unauthenticated. Auto-refresh tokens on expiry.
4. **Build the notes UI.** A two-panel layout: note list (sidebar) + note editor (main area). Clicking a note in the list loads it in the editor. The editor has title and content fields with auto-save (debounced PATCH on every change).
5. **Implement auto-save.** Debounce content changes (500ms). On each debounced trigger, send a PATCH request with only the changed fields. Show a "saving..." / "saved" indicator. Handle conflicts (note was deleted while editing).
6. **Add tags and search.** Tag input on each note. Filter notes by tag in the sidebar. Full-text search that queries the backend and updates the list in real-time.
7. **Deploy and configure.** Backend on Render with `MONGODB_URI` and `JWT_SECRET`. Frontend on Netlify with `VITE_API_URL`. Test the full flow: register → login → create notes → search → logout.

## Deployment

Split deployment: Netlify for the React app, Render for the Express API. Both need
environment variables configured. CORS on the backend must allow the frontend origin.

## Tips

- Auto-save with debouncing is the UX pattern that makes notes apps feel professional. But always handle the edge case where the component unmounts mid-debounce — flush the pending save on unmount.
- For the two-panel layout, use CSS Grid with `grid-template-columns: 300px 1fr` on desktop and a single column with navigation on mobile.
- Extension: add Markdown support in the editor, note sharing via public links, or real-time collaborative editing.

## README Guidance

The project repo's README should include a description, screenshots of the note list and
editor, tech stack, architecture overview, environment variables, and setup instructions.
