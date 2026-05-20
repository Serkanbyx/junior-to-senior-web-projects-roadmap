# To-Do MERN

> A fullstack task management app with JWT authentication, ownership isolation, and a security-hardened REST API.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://to-do-mernn.netlify.app/login) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/to-do-mern)

---

## Purpose

This is your first end-to-end MERN project. You've built a to-do frontend (Level 1)
and a to-do API (Level 3) separately — now you connect them into a single product. It
teaches the fundamental fullstack loop: React calls Express, Express talks to MongoDB,
data flows back through the same chain. Every MERN project after this follows the same
architecture.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7
- **Backend:** Node.js 18+, Express 5, MongoDB (Mongoose 8)
- **Auth:** JWT (jsonwebtoken 9) + bcrypt
- **Security:** Helmet 8, express-rate-limit, express-validator, CORS whitelist, HPP protection
- **UX:** Axios, React Hot Toast
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Set up the monorepo structure.** Two folders: `client/` (Vite + React) and `server/` (Express API). They communicate via HTTP only — no shared runtime code. Add `.env.example` files to both so others can clone and run locally.

2. **Build the auth API.** Register and login endpoints. Hash passwords with bcrypt. Return a JWT on success. Create auth middleware that verifies the token on every protected request. Ownership isolation: every todo belongs to a user, and queries always filter by `userId`.

3. **Build the todo CRUD API.** Five endpoints: create, list (with filter tabs), get one, update (toggle complete + inline edit), and delete. Add a "clear completed" bulk operation. Validate all input with express-validator. Apply rate limiting (100 req/15min general, 20 req/15min for auth).

4. **Build the frontend auth flow.** Login and register pages. On success, store the JWT and redirect to the dashboard. Use Axios with an interceptor that attaches the token to every request. On 401, auto-redirect to login and clear stale state.

5. **Build the todo UI.** A responsive masonry-style grid showing todo cards. Each card has a checkbox (toggle complete), inline edit (Enter to save, Escape to cancel), and delete button. Add filter tabs: All, Active, Completed. A "Clear Completed" button for bulk cleanup.

6. **Add UX polish.** React Hot Toast for real-time feedback on every action. Reusable spinner components for loading states. Skeleton loaders during data fetches. Protected routes that redirect unauthenticated users automatically.

7. **Harden and deploy.** Apply Helmet for HTTP security headers, express-mongo-sanitize for NoSQL injection prevention, HPP for parameter pollution. Deploy backend to Render, frontend to Netlify with `netlify.toml` config.

## Deployment

Backend on Render (set `MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL`). Frontend on Netlify
(set `VITE_API_URL`). CORS whitelist the Netlify domain on Express.

## Tips

- Ownership isolation is non-negotiable. Every database query for todos must include `{ user: req.userId }`. Without this, users can see each other's data — a security bug that appears in almost every beginner MERN project.
- The 401 auto-redirect pattern: Axios interceptor catches 401 responses globally, clears auth state, and redirects to `/login`. This single interceptor replaces dozens of individual error handlers.
- Extension: add drag-and-drop reordering, due dates with calendar picker, or priority levels with color coding.

## README Guidance

The project repo's README should include a description, screenshots of login and dashboard,
tech stack, security features, environment variables for both client and server, and local
setup steps.
