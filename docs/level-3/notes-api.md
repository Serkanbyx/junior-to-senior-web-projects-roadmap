# Notes API (Auth)

> A user-scoped notes API with JWT authentication middleware and user-isolated data access.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://notes-api-7mai.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/notes-api)

---

## Purpose

This project combines CRUD with authentication to create user-scoped data — the pattern
behind every multi-user app. A user can only see and modify their own notes. It teaches you
to write auth middleware that extracts and verifies a JWT, attach the user to the request
object, and scope all database queries to that user. This is the bridge between "I can build
an API" and "I can build a secure API."

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** jsonwebtoken (JWT), bcrypt, auth middleware
- **Deployment:** Render.com

## Build Steps

1. **Set up user auth.** Reuse patterns from the Authentication API: register (hash password, store user), login (verify password, return JWT). The JWT payload contains the user ID.
2. **Create auth middleware.** A function that reads the `Authorization: Bearer <token>` header, verifies the JWT with the secret, and attaches `req.user = { id, email }`. If invalid/missing, return 401.
3. **Model user-scoped notes.** Schema: `{ title, content, tags: [String], user: ObjectId (ref: 'User'), createdAt, updatedAt }`. The `user` field links every note to its owner.
4. **Scope all queries.** Every note operation includes the user filter: `Note.find({ user: req.user.id })`, `Note.findOne({ _id: id, user: req.user.id })`. A user can never access another user's notes — not even by guessing the ID.
5. **Build CRUD routes.** All routes sit behind the auth middleware: `GET /notes`, `GET /notes/:id`, `POST /notes`, `PATCH /notes/:id`, `DELETE /notes/:id`. The user ID comes from the token, never from the request body.
6. **Add tag filtering.** Support `GET /notes?tag=work` to filter notes by tag. Tags are an array of strings — use MongoDB's `$in` operator for querying.
7. **Handle authorization errors.** If a user tries to access a note that exists but belongs to another user, return 404 (not 403) to avoid leaking the existence of other users' data.

## Deployment

Deploy on Render.com. Set `MONGODB_URI`, `JWT_SECRET`, and `JWT_EXPIRES_IN` as environment
variables. The secret must be a long random string — never use a short or guessable value.

## Tips

- Return 404 (not 403) when a user accesses another user's resource. Returning 403 confirms the resource exists, which is an information leak in multi-tenant systems.
- Always scope by user ID from the token, never from a URL parameter like `/users/:userId/notes`. The token is the source of truth for identity.
- Extension: add note sharing (grant read access to another user), full-text search across note content, or note pinning/archiving.

## README Guidance

The project repo's README should include a description, endpoint table showing auth-required
routes, example request/response with Authorization header, environment variables, and setup steps.
