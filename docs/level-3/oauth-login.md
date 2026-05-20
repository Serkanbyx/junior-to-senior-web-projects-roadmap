# OAuth Login

> An OAuth 2.0 authentication backend with Google and GitHub providers, Passport.js integration, and session management.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://oauth-login-backend-fxh8.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/oauth-login-backend)

---

## Purpose

OAuth is how "Login with Google/GitHub" works — and understanding it requires implementing
it once from scratch. This project teaches the full OAuth 2.0 authorization code flow:
redirect to provider, handle callback, exchange code for token, fetch user profile, and
create/link a local user account. It's the most common auth pattern in modern web apps.

## Tech Stack

- **Frontend:** none (API + redirect flow)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Passport.js, passport-google-oauth20, passport-github2, express-session
- **Deployment:** Render.com

## Build Steps

1. **Register OAuth apps.** Create OAuth applications on Google Cloud Console and GitHub Developer Settings. Get the Client ID and Client Secret for each. Set the callback URLs to your server's redirect endpoints.
2. **Configure Passport strategies.** Install `passport-google-oauth20` and `passport-github2`. Configure each with client ID, secret, and callback URL. The verify callback receives the profile and finds/creates a user in your database.
3. **Build the auth routes.** `GET /auth/google` → redirects to Google. `GET /auth/google/callback` → handles the redirect back with the authorization code. Same for GitHub. Use `passport.authenticate()` middleware.
4. **Handle the callback.** Passport exchanges the code for an access token, fetches the user profile, and calls your verify callback. In the callback: find a user by OAuth provider ID, or create a new one with `{ provider, providerId, email, name, avatar }`.
5. **Manage sessions.** Use `express-session` with a MongoDB session store (connect-mongo). After successful OAuth, Passport serializes the user ID into the session. On subsequent requests, deserialize to get the full user object.
6. **Build user endpoints.** `GET /auth/me` returns the current authenticated user (from session). `GET /auth/logout` destroys the session. Protect routes with a middleware that checks `req.isAuthenticated()`.
7. **Handle account linking.** If a user logs in with Google and later with GitHub using the same email, link both providers to one account rather than creating a duplicate. Check by email on callback.

## Deployment

Deploy on Render.com. Set environment variables: `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`,
`GITHUB_CLIENT_ID`, `GITHUB_CLIENT_SECRET`, `SESSION_SECRET`, `MONGODB_URI`, and `CLIENT_URL`
(for redirecting after auth). Update OAuth app callback URLs to the Render deployment URL.

## Tips

- The OAuth flow has many redirects. Draw it out: Client → Your Server → Google → Your Server (callback) → Client. Understanding this flow visually prevents confusion.
- Never store access tokens long-term unless you need to make API calls on behalf of the user. For simple login, you only need the profile info from the initial token exchange.
- Extension: add refresh token handling (for long-lived API access), JWT-based sessions (stateless alternative to express-session), or additional providers (Discord, Twitter, Apple).

## README Guidance

The project repo's README should include a description, OAuth flow diagram, setup steps for
registering OAuth apps (with screenshots), environment variables, and local dev instructions.
