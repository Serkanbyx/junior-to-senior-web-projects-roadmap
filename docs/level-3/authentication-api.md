# Authentication API

> A production-shaped REST API for user registration, login, and protected routes using JWT.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](#) &nbsp;·&nbsp; [Source Code](#)

---

## Purpose

Authentication is the single most reused backend pattern, and doing it correctly
separates a junior backend developer from someone who only follows tutorials. This
project proves you understand password hashing, stateless tokens, middleware-based
route protection, and the difference between authentication and authorization. Treat the
result as a boilerplate you can clone into every later backend project.

## Tech Stack

- **Frontend:** none — API only, exercised with a REST client (Postman / Thunder Client)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose) or PostgreSQL — the pattern is the same
- **Key libraries / tools:** `bcrypt` for hashing, `jsonwebtoken` for tokens, `dotenv` for config
- **Deployment:** Render or Railway, with a managed database

## Build Steps

1. **Set up the project.** Initialise the Express app, connect to the database, and load secrets from environment variables — never hardcode the JWT secret.
2. **Model the user.** A user has a unique email and a password. Store only the hash, never the plain password.
3. **Implement register.** Validate the input, check the email isn't taken, hash the password with bcrypt (let bcrypt generate the salt), persist the user, and return a token.
4. **Implement login.** Look up the user by email, compare the submitted password against the stored hash, and on success issue a signed JWT containing the user id and an expiry.
5. **Write the auth middleware.** Read the token from the `Authorization` header, verify the signature, and attach the decoded user to the request. Reject missing or invalid tokens with `401`.
6. **Add a protected route.** A `/me` endpoint that returns the current user's profile, reachable only through the auth middleware.
7. **Handle errors consistently.** Return clear status codes — `400` for bad input, `401` for auth failure, `409` for a duplicate email — with a predictable JSON error shape.
8. **Consider refresh tokens.** For a stronger version, issue a short-lived access token plus a long-lived refresh token, and add a rotation endpoint.

## Deployment

Deploy to Render or Railway with the database as a managed add-on. Set `JWT_SECRET`,
`DATABASE_URL`, and `NODE_ENV` as environment variables in the dashboard. Confirm the
token expiry and CORS settings are correct for the consuming frontend.

## Tips

- **Authentication** is "who are you"; **authorization** is "what may you do". Build the second only once the first is solid.
- Never return the password hash in any API response — exclude it at the model layer.
- Keep token expiry short. A 15-minute access token plus refresh rotation is far safer than a 7-day token.
- This repo is reusable: every Level 4 MERN project that needs login can start from this codebase.

## README Guidance

The repo README should list every endpoint with its method, path, required body, and
sample response, plus the environment variables and a one-command local setup. Treat the
endpoint table as the headline of the README.
