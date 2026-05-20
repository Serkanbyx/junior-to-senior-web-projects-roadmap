# Newsletter System

> An email automation backend with subscription management, scheduled newsletter delivery via cron jobs, and Swagger API documentation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://newsletter-system.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/newsletter-system)

---

## Purpose

This project teaches scheduled automation — code that runs without user interaction. A cron
job triggers newsletter delivery on a schedule. Combined with subscription management
(subscribe, unsubscribe, confirm), it covers the full email marketing pipeline. You'll learn
node-cron for scheduling, Nodemailer for delivery, and how to manage subscriber state.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3)
- **Email:** Nodemailer
- **Scheduling:** node-cron
- **IDs:** uuid
- **Validation:** express-validator
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Design the data model.** Tables: `subscribers (id, email, name, status, token, subscribed_at)` and `newsletters (id, subject, content, sent_at, recipient_count)`. Status: 'pending' (awaiting confirmation), 'active', 'unsubscribed'.

2. **Build subscription endpoints.** `POST /subscribe` (add subscriber with confirmation token, send confirmation email), `GET /confirm/:token` (activate subscriber), `POST /unsubscribe` (deactivate, include in every newsletter as one-click link).

3. **Build newsletter CRUD.** `POST /newsletters` (create draft), `GET /newsletters` (list all), `POST /newsletters/:id/send` (manually trigger send to all active subscribers). Store send history.

4. **Configure Nodemailer.** Set up SMTP transport. Build HTML email templates for: confirmation email, newsletter content, and unsubscribe confirmation. Include unsubscribe link in every newsletter footer (legally required by CAN-SPAM).

5. **Implement scheduled delivery.** Use node-cron to schedule newsletter sends: `cron.schedule('0 9 * * 1', sendWeeklyNewsletter)` (every Monday at 9am). The cron job fetches unsent newsletters and delivers to all active subscribers.

6. **Handle email delivery at scale.** Send emails in batches (not all at once) to avoid SMTP rate limits. Add delays between batches. Track delivery: successful sends, bounces, and failures per newsletter.

7. **Deploy to Render.** Set SMTP credentials as env vars. node-cron runs inside the server process. SQLite stores subscribers and newsletter history persistently.

## Deployment

Deploy on Render.com. Set `SMTP_HOST`, `SMTP_USER`, `SMTP_PASS`. Cron jobs run as long
as the server is running (Render keeps it alive with the web service plan).

## Tips

- node-cron syntax: `'0 9 * * 1'` = minute 0, hour 9, any day, any month, Monday. Use crontab.guru to build and verify expressions. Always include timezone awareness.
- CAN-SPAM compliance requires: unsubscribe link in every email, physical address, honest subject lines. Non-compliance can result in $50,000+ fines per email. Always include one-click unsubscribe.
- Extension: add email templates (drag-and-drop builder), A/B subject line testing, open/click tracking (pixel tracking + link wrapping), or subscriber segmentation.

## README Guidance

The project repo's README should include a description, subscription flow diagram, API
endpoints, cron schedule explanation, tech stack, and setup instructions.
