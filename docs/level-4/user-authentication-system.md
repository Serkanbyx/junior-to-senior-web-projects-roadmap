# User Authentication System

> A production-ready auth system with dual JWT tokens, email verification, password reset, and 68 automated tests.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://user-authentication-systemm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/user-authentication-system)

---

## Purpose

Authentication is the foundation of every multi-user app, and this project implements it
properly and completely. Dual tokens (access + refresh), email verification, password reset
flow, automatic token refresh with request queuing, and three-tier rate limiting. With 68
automated tests, this is the auth system you'll reference (or copy) into every future project.

## Tech Stack

- **Frontend:** React 19, Vite 8, Tailwind CSS 4, React Router 7
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT dual tokens (access + refresh), bcryptjs (12 rounds)
- **Email:** Nodemailer 8 (Gmail SMTP) — verification and password reset
- **Validation:** express-validator 7
- **Security:** Helmet 8, three-tier rate limiting, express-mongo-sanitize, HPP
- **Testing:** 68 tests — Jest + Supertest (backend), Vitest + React Testing Library (frontend)
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the dual-token strategy.** Short-lived access token (15min) for API requests. Long-lived refresh token (7 days) for silent renewal. On access token expiry, the Axios interceptor automatically calls `/auth/refresh`, queues pending requests, and replays them with the new token — zero user interruption.

2. **Build auth endpoints.** `POST /auth/register` (hash password, create unverified user, send verification email), `POST /auth/login` (verify password + email verified, return both tokens), `POST /auth/refresh` (issue new token pair), `POST /auth/logout` (invalidate refresh token).

3. **Implement email verification.** On registration, generate a verification token (24h expiry). Send an email with a verification link. The user must verify before accessing protected resources. Resend verification option for expired tokens.

4. **Build password reset flow.** `POST /auth/forgot-password` sends a reset email (10-minute token expiry). The link leads to a reset form. `POST /auth/reset-password` validates the token and updates the password. Email enumeration prevention: always return success regardless of whether the email exists.

5. **Build the Axios interceptor with request queuing.** On 401, pause all outgoing requests, call refresh, then replay the queued requests with the new token. This handles concurrent requests during token refresh — multiple API calls don't each trigger separate refresh attempts.

6. **Build the frontend UI.** Register (with password strength indicator + rule checklist), login, forgot password, reset password, email verification pages. Profile management: update name, change email (triggers re-verification), change password (requires current password). Protected and guest route guards.

7. **Add three-tier rate limiting and testing.** Global rate limit, stricter auth-route limit, and strictest sensitive-endpoint limit (forgot-password, reset). Write 68 automated tests covering all auth flows, edge cases (expired tokens, invalid inputs), and frontend components.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `REFRESH_SECRET`, `SMTP_*` credentials,
`CLIENT_URL`. Frontend on Netlify with `VITE_API_URL`. Graceful shutdown handles process signals.

## Tips

- The request queuing pattern in the Axios interceptor is the key insight. Without it, if 5 requests fire simultaneously and the token is expired, you'd trigger 5 refresh calls. With queuing, only one refresh happens and all 5 requests replay afterward.
- Email enumeration prevention: the forgot-password endpoint always returns "If that email exists, we sent a reset link" — never confirm or deny email existence. This prevents attackers from discovering valid accounts.
- Extension: add OAuth providers (Google, GitHub), multi-factor authentication (TOTP), session management UI (revoke sessions from other devices), or login history with IP/device info.

## README Guidance

The project repo's README should include a description, auth flow diagram, screenshots of
all auth pages, security features list, test coverage, environment variables, and setup instructions.
