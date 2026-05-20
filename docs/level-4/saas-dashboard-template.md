# SaaS Dashboard Template

> A multi-tenant SaaS dashboard with billing-ready patterns, team management, and subscription tiers.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://saas-dashboard-template.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/saas-dashboard-template)

---

## Purpose

This is the capstone of Level 4 — a production-grade template that demonstrates every
pattern needed to launch a SaaS product. Multi-tenancy (organizations with members),
subscription tiers with feature gating, billing UI, and team management. If you can build
this, you have the architecture knowledge to launch a real SaaS.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT with organization context
- **Key libraries / tools:** Stripe (mock/test mode), React Router, Zustand, shadcn/ui
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design multi-tenancy.** Organization model: `{ name, owner, members: [{ user, role }], plan: 'free' | 'pro' | 'enterprise', createdAt }`. Every data query is scoped to the user's active organization. Users can belong to multiple orgs.
2. **Build organization management.** Create org, invite members (by email), accept invitations, remove members, transfer ownership. Role-based permissions within the org (owner, admin, member).
3. **Implement subscription tiers.** Define plan features: free (limited), pro (full features), enterprise (custom). Gate features based on the org's plan. Show upgrade prompts when a free-tier user hits a limit.
4. **Build the billing UI.** A settings page showing current plan, usage metrics, and upgrade/downgrade buttons. Integrate Stripe in test mode: create checkout sessions, handle webhooks for subscription events (payment success, cancellation).
5. **Create the dashboard layout.** A professional SaaS layout: collapsible sidebar with navigation, top bar with org switcher and user menu, breadcrumbs, and a responsive main content area. Use shadcn/ui for polished components.
6. **Build feature pages.** Create 2-3 feature pages that demonstrate the template: an analytics overview, a data table with CRUD, and a settings panel. These show how new features plug into the template.
7. **Add team management.** An admin page showing all org members with their roles. Invite flow: enter email → send invitation → user accepts → joins org. Role management (promote/demote). Activity log.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `STRIPE_SECRET_KEY`,
`STRIPE_WEBHOOK_SECRET`. Frontend on Netlify with `VITE_API_URL` and `VITE_STRIPE_PUBLIC_KEY`.
Use Stripe test mode for the demo.

## Tips

- Multi-tenancy means every database query must include the organization ID. The most common security bug in SaaS apps is forgetting to scope a query — user A sees user B's data because the org filter was missing.
- Stripe's test mode is fully functional — use it for the demo. Test cards: `4242424242424242` (success), `4000000000000002` (decline). Webhooks can be tested locally with the Stripe CLI.
- Extension: add usage-based billing (metered pricing), audit logs, SSO/SAML for enterprise, or white-labeling (custom domain per org).

## README Guidance

The project repo's README should include a description, screenshots of the dashboard and
billing page, tech stack, architecture overview (multi-tenancy diagram), Stripe setup
instructions, environment variables, and local setup steps.
