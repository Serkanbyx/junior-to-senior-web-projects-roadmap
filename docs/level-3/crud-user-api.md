# CRUD User API

> A clean, standards-compliant RESTful CRUD User API with MVC architecture, input validation, and interactive Swagger documentation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://crud-user-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/crud-user-api)

---

## Purpose

This is the "Hello World" of backend development. Before adding auth, file uploads, or
external APIs, you need to master the fundamentals: clean MVC architecture, proper HTTP
status codes, input validation, and API documentation. This project is intentionally simple
so you can focus entirely on code organization and REST conventions.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3) — raw SQL queries
- **Validation:** express-validator
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Security:** CORS
- **Deployment:** Render.com

## Build Steps

1. **Set up MVC architecture.** Organize into `src/` with folders: `controllers/`, `routes/`, `models/` (or `db/`). Each layer has a single responsibility: routes define endpoints, controllers handle logic, models interact with SQLite.

2. **Initialize SQLite with better-sqlite3.** Create a database file and define the users table: `id INTEGER PRIMARY KEY, name TEXT, email TEXT UNIQUE, age INTEGER, created_at TEXT`. Use `better-sqlite3`'s synchronous API — it's simpler and faster than async alternatives for SQLite.

3. **Build full CRUD endpoints.** `POST /users` (create), `GET /users` (list all), `GET /users/:id` (get one), `PUT /users/:id` (update), `DELETE /users/:id` (delete). Return proper status codes: 201 Created, 200 OK, 404 Not Found, 400 Bad Request.

4. **Add input validation.** Use express-validator middleware: name is required and non-empty, email is valid format and unique, age is optional positive integer. Return field-specific error messages on validation failure.

5. **Implement centralized error handling.** A global error handler middleware that catches all errors and returns consistent JSON: `{ success: false, error: { message, details } }`. No raw error stacks in production.

6. **Add Swagger documentation.** Annotate routes with JSDoc comments using swagger-jsdoc format. Mount swagger-ui-express at `/api-docs`. Every endpoint is testable directly from the browser.

7. **Deploy to Render.** Configure `render.yaml` for one-click deployment. SQLite file persists on Render's disk. Set environment variables via `.env.example` as reference.

## Deployment

Deploy on Render.com. SQLite is file-based — no external database service needed. The
database file is created automatically on first run.

## Tips

- better-sqlite3 is synchronous by design. Unlike other database drivers, you don't need `async/await` for queries. This makes code simpler: `const user = db.prepare('SELECT * FROM users WHERE id = ?').get(id)`.
- SQLite is perfect for learning and small APIs. It requires zero configuration — no connection strings, no Docker containers, no cloud services. The entire database is a single file.
- Extension: add pagination, sorting, search by name, or soft delete (mark as deleted instead of removing).

## README Guidance

The project repo's README should include a description, API endpoint table, Swagger
screenshot, tech stack, environment variables, and setup instructions.
