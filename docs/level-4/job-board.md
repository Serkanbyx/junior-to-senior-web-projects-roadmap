# Job Board

> A production-ready job board with three-role dashboards, 8-dimension search, 6-state application workflow, JWT refresh token rotation, and OWASP Top 10 security.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://job-board-with-company-user-dashboard.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/job-board-with-company-user-dashboard)

---

## Purpose

This is one of the most complex Level 4 projects. Three distinct user types (Candidate,
Company, Admin) each with full dashboards, a multi-state application workflow, advanced
search across 8 dimensions, and security hardened to OWASP Top 10 standards. It teaches
you to build a real SaaS-level product with production-grade architecture.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, React Hook Form
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT with refresh token rotation + bcryptjs
- **File uploads:** Cloudinary 2 (resumes, company logos)
- **Email:** Nodemailer + nodemailer-express-handlebars (HTML email templates)
- **File validation:** file-type library (MIME whitelist)
- **Validation:** express-validator
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize (OWASP Top 10 compliant)
- **UX:** React Icons, React Hook Form
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the three-role system.** Candidate (browse + apply), Company (post jobs + manage applicants), Admin (moderate platform). JWT with refresh token rotation: on each refresh, invalidate the old token and issue a new pair. Detect token reuse (potential theft).

2. **Build the 8-dimension job search.** Search across: keyword, location, job type (full-time/part-time/remote/contract), experience level, salary range, category, company, and date posted. Combine all dimensions in a single MongoDB query with `$and` conditions. Paginated results.

3. **Implement the 6-state application workflow.** Application states: `submitted → reviewed → shortlisted → interview → offered → hired` (or `rejected` at any point). Companies move applications through states. Candidates see real-time status updates. Email notifications on state changes.

4. **Build the company dashboard.** Post job listings (with rich details: requirements, benefits, salary range). View applicants per listing with state management. Company analytics: views per listing, application conversion rate. Company profile with logo upload.

5. **Build the candidate dashboard.** Applied jobs with status tracking. Saved/bookmarked jobs. Profile with resume upload (file-type validation, MIME whitelist). In-app notifications for application status changes.

6. **Build email notifications with Handlebars templates.** nodemailer-express-handlebars renders HTML email templates with dynamic data. Send on: new application (to company), status change (to candidate), job posted (to matching candidates). Professional, branded email design.

7. **Build admin panel and security hardening.** Admin moderates listings, manages users, views platform stats. OWASP Top 10 compliance: injection prevention, broken auth protection, XSS mitigation, rate limiting, security headers. Comprehensive input validation on all endpoints.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `REFRESH_SECRET`, `CLOUDINARY_*`,
`SMTP_*`. Frontend on Netlify with `VITE_API_URL`.

## Tips

- Refresh token rotation is the gold standard for token security. Each time a refresh token is used, it's invalidated and a new one is issued. If an old token is used again (token reuse), all tokens for that user are revoked — likely indicating theft.
- The 6-state workflow maps directly to a state machine. Each state has valid transitions (e.g., "submitted" can go to "reviewed" or "rejected," but not directly to "hired"). Validate transitions server-side to prevent invalid state jumps.
- Extension: add Stripe payments for featured listings, applicant scoring/ranking, interview scheduling, or a recommendation engine based on candidate skills.

## README Guidance

The project repo's README should include a description, screenshots of all three dashboards,
application workflow diagram, security features, tech stack, and setup instructions.
