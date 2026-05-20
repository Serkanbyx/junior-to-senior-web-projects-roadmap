# To-Do MERN

> A fullstack to-do app with React frontend, Express API, and MongoDB — your first end-to-end MERN project.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://to-do-mernn.netlify.app/login) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/to-do-mern)

---

## Purpose

This is the project where frontend and backend meet for the first time. You've built a to-do
frontend (Level 1) and a to-do API (Level 3) separately — now you connect them. It teaches
the fundamental fullstack pattern: React calls Express, Express talks to MongoDB, data flows
back through the same chain. Every MERN project after this follows the same architecture.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT (access + refresh tokens)
- **Key libraries / tools:** Axios, React Router, bcrypt, jsonwebtoken
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Set up the monorepo.** Create `client/` and `server/` folders. The backend is a standalone Express API; the frontend is a Vite React app. They communicate via HTTP — no shared code at runtime.
2. **Build the API.** REST endpoints: `POST /auth/register`, `POST /auth/login`, full CRUD for `/todos` (all auth-protected). Each todo belongs to a user. Return proper status codes and error messages.
3. **Implement auth on the frontend.** Login and register pages. On success, store the JWT in memory (or httpOnly cookie). Create an Axios interceptor that attaches the token to every request. Redirect to login on 401.
4. **Connect frontend to API.** Use Axios (or fetch) to call your backend. Create a custom hook (`useTodos`) that manages fetching, creating, updating, and deleting todos. Handle loading and error states explicitly.
5. **Build the todo UI.** List todos with checkboxes (toggle complete), inline edit, delete button, and an "add" form. Optimistically update the UI on actions — revert if the API call fails.
6. **Add filtering and sorting.** Client-side filters (all/active/completed) and sort by date or priority. These operate on the already-fetched data — no additional API calls needed.
7. **Deploy split-stack.** Deploy the backend on Render (set `MONGODB_URI`, `JWT_SECRET`). Deploy the frontend on Netlify (set `VITE_API_URL` to the Render backend URL). Configure CORS on the backend to allow the Netlify origin.

## Deployment

Frontend on Netlify, backend on Render. The critical connection is the `VITE_API_URL`
environment variable on Netlify pointing to the Render backend. CORS must whitelist
the Netlify domain on the Express server.

## Tips

- The most common bug in your first MERN app is CORS. Set `cors({ origin: process.env.CLIENT_URL, credentials: true })` on Express and you'll avoid hours of debugging.
- Store JWTs in memory (a React ref or context), not localStorage. localStorage is vulnerable to XSS. For a more secure approach, use httpOnly cookies with `sameSite: 'none'`.
- Extension: add drag-and-drop reordering (synced to the backend), shared/collaborative todos, or real-time updates with Socket.io.

## README Guidance

The project repo's README should include a description, screenshots of login and todo list,
architecture diagram (React → Express → MongoDB), the live demo link, environment variables
for both client and server, and local setup steps for both.
