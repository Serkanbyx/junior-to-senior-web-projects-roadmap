# Contact Form API

> A backend for contact forms with email sending via Nodemailer and database storage for message history.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://contact-form-api-woaf.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/contact-form-api)

---

## Purpose

Every website needs a contact form, and this project teaches you how to handle the backend:
receive form data, validate it, send an email notification, and store the message for later
review. It introduces Nodemailer for SMTP email sending, environment-based configuration for
email credentials, and the pattern of "process then persist" — doing the important action
(email) and the storage in the right order with proper error handling.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Nodemailer (SMTP email), express-validator, dotenv
- **Deployment:** Render.com

## Build Steps

1. **Design the endpoint.** `POST /contact` accepts `{ name, email, subject, message }`. Validate all fields: email format, name and message non-empty, subject max length. Return 400 with specific errors on failure.
2. **Configure Nodemailer.** Create a transporter with SMTP credentials (Gmail, SendGrid, or Mailtrap for testing). Store host, port, user, and password in environment variables. Never hardcode credentials.
3. **Build the email template.** Compose an HTML email with the contact form data: sender's name, email, subject, and message body. Include a plain-text fallback. Set proper `from`, `to`, and `replyTo` headers.
4. **Send the email.** On successful validation, call `transporter.sendMail()`. Handle SMTP errors gracefully — if email sending fails, still store the message in the DB and return a partial success response.
5. **Store in database.** Save every submission to MongoDB: `{ name, email, subject, message, emailSent: boolean, createdAt }`. This creates an audit trail and lets you retry failed emails later.
6. **Add rate limiting.** Prevent spam by limiting submissions per IP (e.g. 5 per hour). Use express-rate-limit on the contact endpoint specifically. Return 429 with a "try again later" message.
7. **Build an admin endpoint.** `GET /contact/messages` (protected) returns all stored messages with pagination. This lets you review submissions even if emails were missed.

## Deployment

Deploy on Render.com. Set environment variables: `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`,
`SMTP_PASS`, `CONTACT_EMAIL` (recipient), and `MONGODB_URI`. Use Mailtrap for testing
to avoid sending real emails during development.

## Tips

- Use Mailtrap or Ethereal Email for development — they catch all outgoing emails without delivering them. Switch to a real SMTP provider (SendGrid, Mailgun) only in production.
- Always set `replyTo` to the sender's email so when you reply to the notification, it goes to the person who submitted the form.
- Extension: add file attachments (combine with the File Upload API project), email templates with HTML/CSS, or a webhook notification to Slack/Discord.

## README Guidance

The project repo's README should include a description, the endpoint spec, environment
variables list with descriptions, a note about SMTP providers, and local setup steps.
