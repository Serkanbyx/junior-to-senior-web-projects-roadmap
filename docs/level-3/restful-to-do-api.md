# RESTful To-Do API

> A standards-compliant REST API for task management with resource modeling, proper status codes, and request validation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://restful-to-do-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/restful-to-do-api)

---

## Purpose

This project reinforces REST principles with a slightly more complex domain: tasks have
statuses, priorities, and due dates. You'll learn to model resources with relationships,
implement filtering via query parameters, handle partial updates (PATCH vs PUT), and return
appropriate status codes for every scenario. It's the API you'd build on day one at a job.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Mongoose (ODM), express-validator, dotenv
- **Deployment:** Render.com

## Build Steps

1. **Model the resource.** Define a Todo schema: `{ title, description, status: 'pending' | 'in-progress' | 'completed', priority: 'low' | 'medium' | 'high', dueDate, createdAt, updatedAt }`. Use Mongoose schema validation for enums and required fields.
2. **Design RESTful routes.** `GET /todos` (list with filters), `GET /todos/:id`, `POST /todos`, `PATCH /todos/:id` (partial update), `DELETE /todos/:id`. Use PATCH (not PUT) for partial updates — only sent fields are modified.
3. **Implement query filtering.** Support query params: `?status=pending&priority=high&sort=-createdAt&limit=10&page=2`. Build a dynamic query object from req.query and pass it to Mongoose. Ignore unknown params gracefully.
4. **Add validation middleware.** Validate that title is non-empty, status is one of the allowed values, dueDate is a valid future date, and priority is valid. Return 400 with field-specific errors.
5. **Handle errors consistently.** 404 for non-existent todo (invalid ObjectId or not found), 400 for validation errors, 500 for server errors. Always return `{ success: false, error: { message, details } }`.
6. **Add timestamps and sorting.** Use Mongoose's `timestamps: true` option. Support sort by any field via query param. Default sort is newest first.
7. **Test with HTTP client.** Create a Postman/Thunder Client collection with requests for every endpoint and edge case. Export it and include in the repo.

## Deployment

Deploy on Render.com. Set `MONGODB_URI` environment variable pointing to MongoDB Atlas.
The API is stateless — Render can restart without data loss since MongoDB is external.

## Tips

- PATCH vs PUT: PATCH updates only the fields you send, PUT replaces the entire resource. For todo updates (e.g. just changing status), PATCH is more appropriate and saves bandwidth.
- Mongoose's `findByIdAndUpdate` with `{ new: true, runValidators: true }` returns the updated document and still runs schema validation on the update.
- Extension: add bulk operations (mark multiple as completed), archive functionality, or user-scoped todos (requires auth from the Authentication API project).

## README Guidance

The project repo's README should include a short description, the endpoint table with
request/response examples, environment variables, and local setup steps.
