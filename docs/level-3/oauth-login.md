# OAuth Login

> An OAuth2 login backend with Google and GitHub authentication using Passport.js, session-based auth, and MongoDB.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://oauth-login-backend.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/oauth-login-backend)

---

## Purpose

OAuth is how "Login with Google/GitHub" works. Instead of managing passwords yourself, you
delegate authentication to a trusted provider. This project teaches the OAuth 2.0 flow
(redirect → consent → callback → token exchange), Passport.js strategy pattern, and session-based
auth with MongoDB storage. It's a fundamentally different auth model than JWT.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** MongoDB (Mongoose 8)
- **Auth:** Passport.js (passport-google-oauth20 + passport-github2)
- **Sessions:** express-session + connect-mongo (MongoDB session store)
- **Security:** Helmet 8
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Set up OAuth apps.** Register apps on Google Cloud Console and GitHub Developer Settings. Get Client ID and Client Secret for each. Configure callback URLs: `https://your-domain.com/auth/google/callback` and `/auth/github/callback`.

2. **Configure Passport strategies.** Install passport-google-oauth20 and passport-github2. Each strategy takes: clientID, clientSecret, callbackURL, and a verify function. The verify function finds or creates the user in MongoDB from the provider's profile data.

3. **Set up session-based auth.** Unlike JWT (stateless), OAuth uses sessions (stateful). Configure express-session with connect-mongo (stores sessions in MongoDB). Sessions persist across server restarts. Passport's `serializeUser`/`deserializeUser` hooks handle session ↔ user mapping.

4. **Build the OAuth flow.** Route: `GET /auth/google` → Passport redirects to Google's consent screen → user approves → Google redirects to `/auth/google/callback` → Passport exchanges code for token → verify function runs → user is logged in. Same pattern for GitHub.

5. **Build user management.** User model: `{ provider, providerId, email, name, avatar, createdAt }`. On first OAuth login, create the user. On subsequent logins, find the existing user by providerId. Handle the case where a user logs in with both Google and GitHub (same email → link accounts).

6. **Build session endpoints.** `GET /auth/me` (return current user from session or 401), `POST /auth/logout` (destroy session). Protected routes check `req.isAuthenticated()` (Passport's session check).

7. **Deploy to Render.** Set OAuth credentials (GOOGLE_CLIENT_ID, GOOGLE_CLIENT_SECRET, GITHUB_CLIENT_ID, GITHUB_CLIENT_SECRET), MongoDB URI, and SESSION_SECRET. Update callback URLs to production domain.

## Deployment

Deploy on Render.com. MongoDB Atlas for database + session storage. Update OAuth app
callback URLs to production domain. Set all credentials as environment variables.

## Tips

- Sessions vs JWT: OAuth providers return a token, but you don't forward it to the client. Instead, you create a server-side session. The client just gets a session cookie — no token management needed. This is simpler for traditional web apps.
- connect-mongo stores sessions in MongoDB. This means sessions survive server restarts (unlike in-memory session store). It also scales across multiple server instances (all read from the same MongoDB).
- Extension: add more providers (Twitter, Discord, Apple), account linking (connect multiple providers to one account), or role-based access after OAuth login.

## README Guidance

The project repo's README should include a description, OAuth flow diagram, provider setup
instructions, session explanation, tech stack, and deployment guide.
