# RESTful To-Do API

> A secure RESTful API for task management with JWT authentication, priority levels, pagination, and interactive Swagger documentation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://restful-to-do-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/restful-to-do-api)

---

## Purpose

Building on the CRUD User API, this project adds authentication and more complex querying.
Tasks have priorities, statuses, and due dates — requiring filtering, sorting, and pagination.
JWT auth means every endpoint is protected and data is user-scoped. This is the API pattern
you'll use in every authenticated application.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3) — raw SQL queries
- **Auth:** JWT (jsonwebtoken) + bcryptjs
- **Validation:** express-validator
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Security:** CORS
- **Deployment:** Render.com

## Build Steps

1. **Build the auth system.** User table: `id, email, password_hash, created_at`. Register endpoint hashes password with bcryptjs and stores the user. Login endpoint verifies credentials and returns a JWT. Auth middleware extracts and verifies the token from the Authorization header.

2. **Design the todos table.** Schema: `id, user_id, title, description, status ('pending'|'in-progress'|'completed'), priority ('low'|'medium'|'high'), due_date, created_at, updated_at`. Foreign key to users table. Index on `user_id` for fast lookups.

3. **Build CRUD with user scoping.** All todo queries include `WHERE user_id = ?` — users only see their own data. Create, read (list + single), update (PATCH for partial updates), and delete. Return 404 for todos that don't exist or belong to another user.

4. **Implement filtering and sorting.** Query params: `?status=pending&priority=high&sort=-created_at&limit=10&page=2`. Build dynamic SQL WHERE clauses from filters. Support sort by any column (ascending/descending). Validate all query params.

5. **Add pagination.** Calculate offset from page and limit: `OFFSET = (page - 1) * limit`. Return metadata: `{ data: [...], pagination: { page, limit, total, totalPages } }`. Default limit: 10, max limit: 100.

6. **Document with Swagger.** Every endpoint documented: auth routes (register/login), todo CRUD routes with query params. Show the JWT auth scheme in Swagger UI so testers can authenticate directly in the docs.

7. **Deploy to Render.** SQLite database file persists on disk. JWT_SECRET set as environment variable. No external database service required.

## Deployment

Deploy on Render.com with `render.yaml`. Set `JWT_SECRET` in environment variables.
SQLite needs no external configuration.

## Tips

- SQL filtering with dynamic WHERE clauses: build an array of conditions and params, then join with AND. Never concatenate user input directly into SQL — always use parameterized queries (`?` placeholders) to prevent SQL injection.
- Pagination metadata helps the frontend know when to show "Load More" or page numbers. Always return `total` and `totalPages` alongside the data.
- Extension: add due date reminders, batch operations (mark all as complete), or categories/tags.

## README Guidance

The project repo's README should include a description, API endpoints table, auth flow
explanation, Swagger screenshot, tech stack, and setup instructions.
