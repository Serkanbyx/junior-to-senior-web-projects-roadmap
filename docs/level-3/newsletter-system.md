# Newsletter System

> A newsletter service with subscription management, scheduled email sends, HTML templates, and unsubscribe handling.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://newsletter-system-6hvv.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/newsletter-system)

---

## Purpose

This project combines several backend skills into one system: email sending, scheduled tasks,
template rendering, subscription lifecycle management, and compliance (unsubscribe links).
It teaches you to build a production-like feature that involves multiple moving parts — the
kind of system you'd actually maintain at a company.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Nodemailer (SMTP), node-cron (scheduling), Handlebars (email templates)
- **Deployment:** Render.com

## Build Steps

1. **Model subscribers.** Schema: `{ email, name, status: 'active' | 'unsubscribed', subscribedAt, unsubscribedAt, confirmationToken }`. Add a unique index on email. Support double opt-in (send confirmation email on subscribe).
2. **Build subscription endpoints.** `POST /subscribe` (add subscriber, send confirmation), `GET /confirm/:token` (activate subscription), `GET /unsubscribe/:token` (mark as unsubscribed). The token prevents unauthorized unsubscriptions.
3. **Create newsletter CRUD.** Schema: `{ subject, body (HTML), status: 'draft' | 'scheduled' | 'sent', scheduledAt, sentAt, recipientCount }`. Admin endpoints to create, edit, preview, and schedule newsletters.
4. **Build HTML email templates.** Use Handlebars to create reusable email templates with variables (subscriber name, content, unsubscribe link). Include both HTML and plain-text versions. Inline CSS for email client compatibility.
5. **Implement the send engine.** When a newsletter is triggered (manually or by schedule), fetch all active subscribers, render the template for each (personalizing the name and unsubscribe link), and send via Nodemailer. Process in batches to avoid SMTP rate limits.
6. **Add scheduling with cron.** Use node-cron to check every minute for newsletters with `status: 'scheduled'` and `scheduledAt <= now`. When found, trigger the send engine and update status to 'sent'.
7. **Track delivery.** Log send results per subscriber: success or failure with error message. Provide a `GET /newsletters/:id/stats` endpoint showing total sent, failed, and open rate (if tracking pixels are implemented).

## Deployment

Deploy on Render.com. Set `MONGODB_URI`, SMTP credentials (`SMTP_HOST`, `SMTP_USER`,
`SMTP_PASS`), and `BASE_URL` (for unsubscribe links). Use Mailtrap for testing.

## Tips

- Always include an unsubscribe link in every email — it's legally required (CAN-SPAM, GDPR) and prevents spam reports that can get your domain blacklisted.
- Send emails in batches (50-100 at a time with delays) rather than all at once. SMTP providers have rate limits and will reject bulk sends.
- Extension: add open tracking (1x1 pixel), click tracking (redirect links), A/B subject testing, or segment-based targeting.

## README Guidance

The project repo's README should include a description, subscription flow diagram, endpoint
table, environment variables, SMTP provider setup notes, and local development steps.
