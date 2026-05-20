# Notes API

> A secure RESTful Notes API with JWT authentication, ownership-based authorization, full-text search, tag filtering, and Helmet security hardening.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://notes-api-jt6s.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/notes-api)

---

## Purpose

This project extends the To-Do API with richer content (title + body), a tag system, and
full-text search. It teaches you to implement search across multiple columns, filter by
tags (a one-to-many relationship in SQL), and enforce ownership-based authorization —
only the note's creator can read, update, or delete it.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3) — raw SQL queries
- **Auth:** JWT (jsonwebtoken)
- **Validation:** express-validator
- **Security:** Helmet 8, CORS
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Design the notes schema.** Tables: `notes (id, user_id, title, content, tags, pinned, created_at, updated_at)`. Tags stored as comma-separated string or in a separate junction table. Index on `user_id` for fast user-scoped queries.

2. **Build ownership-based authorization.** Beyond authentication (who are you?), implement authorization (can you access this?). Every note operation first checks: does this note belong to `req.userId`? Return 403 Forbidden if not. This prevents horizontal privilege escalation.

3. **Implement full-text search.** SQLite's `LIKE '%keyword%'` on both title and content columns. For better performance, use SQLite's FTS5 (Full-Text Search) extension if available. Search endpoint: `GET /notes?q=keyword` searches across both fields.

4. **Build the tag system.** Tags are stored with each note. Filter by tag: `GET /notes?tag=important`. Support multiple tags per note. Return available tags for the user so the frontend can show a tag cloud.

5. **Add pagination and sorting.** Same pattern as To-Do API: limit, page, sort by date or title. Return pagination metadata. Default sort: newest first, pinned notes always on top.

6. **Harden with Helmet.** Add Helmet middleware for security headers: X-Content-Type-Options, X-Frame-Options, Strict-Transport-Security, etc. This is one line of code that adds significant security.

7. **Deploy with render.yaml.** One-click deployment to Render. SQLite database file persists on disk. Environment variables: JWT_SECRET.

## Deployment

Deploy on Render.com. Helmet is active in production for security headers. SQLite file
auto-creates on first run.

## Tips

- Ownership authorization is separate from authentication. Auth middleware verifies the JWT (authentication). Then each route handler checks if the requested resource belongs to the user (authorization). These are two distinct security layers.
- SQLite's `LIKE` is case-insensitive by default for ASCII. For Unicode, use `COLLATE NOCASE` or normalize input before searching.
- Extension: add note sharing (generate public links), Markdown content support, or export to PDF.

## README Guidance

The project repo's README should include a description, API endpoints with query params,
auth and search documentation, tech stack, and setup instructions.
