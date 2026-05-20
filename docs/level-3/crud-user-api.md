# CRUD User API

> A RESTful CRUD API for user management with MVC architecture, Swagger documentation, and centralized error handling.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://crud-user-api-slmp.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/crud-user-api)

---

## Purpose

This is the "hello world" of backend development — a clean CRUD API that follows REST
conventions perfectly. It teaches you to structure a Node.js project with MVC separation,
design RESTful routes with proper HTTP verbs and status codes, validate input before it
reaches the database, and document your API with Swagger so other developers can use it
without reading your code.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express 5
- **Database:** SQLite
- **Key libraries / tools:** express-validator, Swagger (swagger-ui-express), MVC pattern
- **Deployment:** Render.com (Web Service)

## Build Steps

1. **Scaffold the project.** Initialize with `npm init`, install Express 5. Create the MVC folder structure: `routes/`, `controllers/`, `models/`, `middleware/`. Set up a centralized error handler and a `server.js` entry point.
2. **Design the routes.** Follow REST conventions strictly: `GET /users` (list), `GET /users/:id` (detail), `POST /users` (create), `PUT /users/:id` (update), `DELETE /users/:id` (delete). Use Express Router to keep route files clean.
3. **Create the data model.** Define a User schema with fields: id, name, email, age, createdAt. Set up SQLite with a simple query abstraction. Write model methods for each CRUD operation.
4. **Build controllers.** Each controller method receives `(req, res, next)`, calls the model, and returns a properly formatted JSON response with the correct HTTP status code (200, 201, 204, 404, 500).
5. **Add input validation.** Use express-validator to validate request bodies: email must be valid format, name is required and trimmed, age is a positive integer. Return 400 with specific error messages on validation failure.
6. **Implement centralized error handling.** Create an error middleware that catches all errors, logs them, and returns a consistent JSON error response `{ error: { message, statusCode } }`. Never leak stack traces in production.
7. **Add Swagger documentation.** Write OpenAPI 3.0 spec (inline or YAML file) describing all endpoints, request/response schemas, and examples. Serve it with swagger-ui-express at `/api-docs`.

## Deployment

Deploy on Render.com as a Web Service. SQLite file persists on Render's disk (for demo
purposes). Set `NODE_ENV=production` as an environment variable. The Swagger UI is accessible
at the `/api-docs` endpoint.

## Tips

- Express 5 supports `async` route handlers natively — errors thrown in async functions propagate to the error middleware without `try/catch` wrappers or `express-async-errors`.
- SQLite is perfect for small APIs and demos. For production, swap to PostgreSQL by changing only the model layer — the controllers and routes stay the same (that's the point of MVC).
- Extension: add pagination to the list endpoint, filtering by name/email, or soft-delete functionality.

## README Guidance

The project repo's README should include a short description, the API endpoint table, the
Swagger UI screenshot, the live demo URL, environment variables, and local setup steps
(`npm install && npm run dev`).
