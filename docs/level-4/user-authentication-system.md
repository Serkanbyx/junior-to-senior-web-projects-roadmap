# User Authentication System

> A complete auth system with JWT access/refresh tokens, protected routes, and a polished React UI.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://user-authentication-systemm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/user-authentication-system)

---

## Purpose

Authentication is the foundation of every multi-user app, and this project implements it
properly end-to-end. You'll build refresh token rotation (the industry standard), token
storage best practices, automatic token refresh on the frontend, and protected route patterns
in React. This is the auth system you'll copy into every future project.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT (access + refresh tokens), bcrypt
- **Key libraries / tools:** Axios interceptors, React Router, cookie-parser
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the token strategy.** Short-lived access token (15min) in memory. Long-lived refresh token (7 days) in httpOnly cookie. On access token expiry, the client silently calls `/auth/refresh` to get a new pair.
2. **Build auth endpoints.** `POST /auth/register` (hash password, create user, return tokens), `POST /auth/login` (verify password, return tokens), `POST /auth/refresh` (verify refresh token, rotate both), `POST /auth/logout` (invalidate refresh token).
3. **Implement refresh token rotation.** On each refresh, invalidate the old refresh token and issue a new one. Store a token version or whitelist in the database. If a reused token is detected, invalidate all tokens (potential theft).
4. **Build the frontend auth layer.** An AuthContext/provider that holds the access token in state. An Axios interceptor that attaches the token to requests and automatically retries with a refreshed token on 401.
5. **Create protected routes.** A `PrivateRoute` component that checks auth state. If not authenticated and no refresh token, redirect to login. If refresh token exists but access token expired, attempt silent refresh before redirecting.
6. **Build the UI.** Login, register, and "forgot password" pages. A protected dashboard showing user profile info. A settings page for password change. Proper loading states during auth checks.
7. **Add security measures.** Rate limit auth endpoints (prevent brute force). Validate password strength on register. Hash with bcrypt (cost factor 12+). Set secure cookie flags (`httpOnly`, `secure`, `sameSite`).

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `REFRESH_SECRET`, `CLIENT_URL`.
Frontend on Netlify with `VITE_API_URL`. Cookies require `sameSite: 'none'` and `secure: true`
for cross-origin deployment.

## Tips

- Never store tokens in localStorage — it's accessible to any script on the page (XSS vulnerability). Use httpOnly cookies for refresh tokens and in-memory variables for access tokens.
- The Axios interceptor pattern: on 401, queue the failed request, call refresh, then replay all queued requests with the new token. This handles concurrent requests during refresh.
- Extension: add email verification, password reset via email link, OAuth integration, or multi-factor authentication (TOTP).

## README Guidance

The project repo's README should include a description, auth flow diagram, screenshots of
login/register, security features list, environment variables, and setup instructions.
