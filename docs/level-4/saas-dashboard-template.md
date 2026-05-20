# SaaS Dashboard Template

> A multi-tenant SaaS template with organizations, RBAC, team invitations, mock billing, Recharts analytics, real-time notifications, and PDF report generation.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://saas-dashboard-template.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/saas-dashboard-template)

---

## Purpose

This is the capstone of Level 4 — a production-grade template demonstrating every pattern
needed to launch a SaaS product. Multi-tenancy (organizations with members), subscription
tiers, team management with email invitations, analytics dashboards, and real-time notifications.
If you can build this, you have the architecture knowledge to launch a real SaaS.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, Recharts 2, date-fns 4
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 8), Socket.io 4
- **Auth:** JWT + bcryptjs
- **Validation:** Zod 3 (server-side schema validation)
- **Email:** Nodemailer (team invitations, notifications)
- **PDF:** PDFKit (report generation)
- **Cron:** node-cron (scheduled tasks)
- **Real-time:** Socket.io (live notifications)
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize
- **Testing:** Vitest + React Testing Library (frontend), Vitest (backend)
- **API docs:** Swagger
- **UX:** Lucide React, React Hot Toast, clsx, dark mode
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design multi-tenancy.** Organization model: `{ name, owner, members: [{ user, role }], plan: 'free' | 'pro' | 'enterprise' }`. Every data query is scoped to the user's active organization. Users can belong to multiple orgs and switch between them.

2. **Build RBAC (Role-Based Access Control).** Three roles within each org: owner (full control), admin (manage members, settings), member (use features). Middleware checks `req.user.role` within the active organization. Different UI elements shown/hidden per role.

3. **Implement team invitations.** Invite by email: generate invitation token, send email via Nodemailer with accept link. On accept: add user to org with member role. Handle: already a member, expired invitation, invalid token. Admin page shows pending invitations.

4. **Build mock billing with subscription tiers.** Define plan features: free (3 members, limited), pro (unlimited members, all features), enterprise (custom). Gate features based on org's plan. Show upgrade prompts when limits are hit. Mock payment flow (no real Stripe for the template).

5. **Build the analytics dashboard.** Recharts-powered visualizations: line charts for activity over time, bar charts for usage breakdown, pie charts for distribution. Data fetched from the backend's aggregation endpoints. Date range selector with date-fns formatting.

6. **Add real-time notifications and scheduled tasks.** Socket.io pushes notifications (new member joined, invitation accepted, plan changed). node-cron runs scheduled tasks (usage reports, cleanup). PDFKit generates downloadable reports on demand.

7. **Build the professional layout and dark mode.** Collapsible sidebar with org switcher, top bar with notification bell (unread count badge), breadcrumbs, responsive main content area. Dark mode with system preference detection. Vitest tests for critical UI components.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `SMTP_*`, `CLIENT_URL`. Frontend on
Netlify with `VITE_API_URL`. Seed data populates a demo org with sample analytics.

## Tips

- Multi-tenancy means every database query must include the organization ID. The most common security bug in SaaS apps is forgetting to scope a query — user A sees org B's data because the org filter was missing. Create middleware that auto-injects `orgId` into every request.
- Zod schemas on the backend replace manual validation. Define the shape once, validate with `.parse()`, and get typed output. If validation fails, Zod's error messages are specific and user-friendly out of the box.
- PDFKit generates PDFs programmatically: pipe content to a stream, add headers/tables/charts, and send as a download response. Useful for invoices, reports, and exports.
- Extension: add real Stripe integration (test mode), usage-based billing, SSO/SAML for enterprise, audit logs, or white-labeling (custom domain per org).

## README Guidance

The project repo's README should include a description, screenshots of the dashboard and
organization settings, architecture overview (multi-tenancy diagram), features list, tech
stack, environment variables, and setup instructions with seed data.
