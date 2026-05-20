# Contact Form API

> A production-ready Contact Form REST API with email notifications, SQLite storage, rate limiting, and Swagger documentation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://contact-form-api-k26g.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/contact-form-api)

---

## Purpose

Every website needs a contact form. This project teaches you to build the backend for one:
receive form submissions, validate them, store them in a database, and send email notifications
to the site owner. It introduces Nodemailer for transactional email — a skill you'll use in
every project that sends emails (verification, password reset, notifications).

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3)
- **Email:** Nodemailer
- **Validation:** express-validator
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Design the submissions table.** Schema: `id, name, email, subject, message, status ('new'|'read'|'replied'), created_at`. All fields required except subject. Store every submission for record-keeping.

2. **Build the submission endpoint.** `POST /contact` accepts name, email, subject, and message. Validate all fields (email format, message length). Store in SQLite. Return 201 Created with the submission ID.

3. **Configure Nodemailer.** Set up a transporter with SMTP credentials (Gmail, Outlook, or a transactional service like SendGrid). On new submission, send an email to the site owner with the form data formatted in a clean HTML template.

4. **Add rate limiting.** Contact forms are spam targets. Apply strict rate limiting: max 5 submissions per IP per hour. Use express-rate-limit with a clear error message: "Too many submissions, please try again later."

5. **Build admin endpoints.** `GET /contacts` (list all submissions with pagination), `GET /contacts/:id` (single submission), `PATCH /contacts/:id` (update status to read/replied). These could be protected with a simple API key or basic auth.

6. **Add Helmet security.** Apply all Helmet defaults for security headers. Combined with rate limiting and input validation, this creates a production-ready endpoint safe to expose publicly.

7. **Deploy to Render.** Set SMTP credentials as environment variables. SQLite stores submissions persistently. Rate limiter state resets on deploy (acceptable for this scale).

## Deployment

Deploy on Render.com. Set `SMTP_HOST`, `SMTP_USER`, `SMTP_PASS`, `NOTIFY_EMAIL` in
environment variables.

## Tips

- Nodemailer with Gmail requires an "App Password" (not your regular password) if 2FA is enabled. For production, use a transactional email service (SendGrid, Mailgun) — they have better deliverability and don't hit Gmail's sending limits.
- Rate limiting the contact endpoint is critical. Without it, bots will flood your inbox with thousands of spam submissions. 5 per hour per IP is reasonable for legitimate users.
- Extension: add CAPTCHA verification, auto-reply to the submitter, attachment support, or a spam scoring system.

## README Guidance

The project repo's README should include a description, API endpoints, email setup
instructions, rate limiting details, tech stack, and setup instructions.
