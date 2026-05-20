# Notes MERN

> A fullstack notes app with rich text editing (Quill), color-coded cards, pinning, and instant client-side search.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://notes-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/notes-mern)

---

## Purpose

Building on the To-Do MERN foundation, this project adds rich content. Notes have formatted
text (bold, italic, lists, links via Quill editor), colors, and pinning — far more complex
than plain-text todos. It teaches you to handle rich HTML content across the full stack,
implement client-side filtering without additional API calls, and build visually distinct
UIs with color systems.

## Tech Stack

- **Frontend:** React 19, Vite 8, Tailwind CSS 4, React Router 7
- **Backend:** Node.js 18+, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT (7-day expiry) + bcrypt (12 rounds)
- **Rich Text:** React Quill 3
- **Security:** Helmet 8, HPP, CORS whitelist, rate limiting, NoSQL injection sanitizer
- **UX:** Axios, React Hot Toast
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build the auth system.** Register and login with JWT (7-day expiry). bcrypt with 12 salt rounds for password hashing. Auth middleware on all note endpoints. Ownership validation on every CRUD operation.

2. **Build the notes CRUD API.** Note model: `{ title, content (HTML from Quill), color, pinned, user, timestamps }`. Standard CRUD endpoints. Ownership isolation: users only see their own notes. Return notes sorted by pinned first, then by date.

3. **Integrate React Quill on the frontend.** Install and configure React Quill with toolbar options (bold, italic, underline, ordered/unordered lists, links). Store the HTML output as the note's content. Handle Quill's controlled component pattern.

4. **Build the color system.** Six preset colors for notes. A color picker in the create/edit form. Store the color value in the note document. Render note cards with the selected background color for visual organization.

5. **Implement pinning.** A pin toggle on each note card. Pinned notes always appear at the top of the list regardless of creation date. The API sorts: `{ pinned: -1, createdAt: -1 }`.

6. **Add instant client-side search.** A search bar that filters notes in real-time as the user types. Strip HTML tags from content before searching (so you search text, not markup). Filter across both title and content simultaneously. No additional API calls needed — filter the already-fetched array.

7. **Build the responsive grid layout.** A 1-4 column masonry-style grid that adapts to screen size. Each note card shows title, a preview of content (truncated), color accent, and pin indicator. Add a delete confirmation modal to prevent accidental deletions.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL`. Frontend on Netlify
with `VITE_API_URL`. Include `render.yaml` and `netlify.toml` for one-click deployment.

## Tips

- React Quill stores HTML. When searching, you need to strip tags: `content.replace(/<[^>]*>/g, '')`. Otherwise searching for "bold" would match every note with `<b>` tags.
- The color system is simple but impactful for UX. Six colors is the sweet spot — enough variety without overwhelming choice. Store as a string enum on the backend for validation.
- Extension: add tags/categories, drag-and-drop reordering, trash/archive system, or Markdown export.

## README Guidance

The project repo's README should include a description, screenshots of the note grid with
colors and the Quill editor, tech stack, environment variables, and setup instructions.
