# Analytics Dashboard

> A business analytics dashboard with interactive charts, user management tables, and authentication with Zod validation.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://analytics-dashboardd.netlify.app/login) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/analytics-dashboard)

---

## Purpose

This is the capstone of Level 2 — it combines everything: authentication flow, protected routes,
data tables with sorting/pagination, and chart visualizations. It mirrors what a junior
developer would build at a SaaS company. You'll learn to gate content behind login, manage
user sessions, build reusable table components, and compose a full admin interface from
a component library.

## Tech Stack

- **Frontend:** React 19, TypeScript, Tailwind CSS
- **Backend:** none (mock auth + data)
- **Database:** none (state in Redux)
- **Key libraries / tools:** Redux Toolkit, Recharts, shadcn/ui, Zod (form validation), React Router
- **Deployment:** Netlify

## Build Steps

1. **Set up authentication.** Build a login page with email/password fields validated by Zod. Simulate authentication (check against hardcoded credentials or a mock API). Store the auth token/user in Redux. Redirect to dashboard on success.
2. **Protect routes.** Create a `PrivateRoute` wrapper that checks auth state. If not logged in, redirect to `/login`. If logged in, render the dashboard layout (sidebar + main content area). Add logout functionality.
3. **Build the dashboard layout.** A collapsible sidebar with navigation links (Overview, Users, Analytics, Settings). A top bar with user avatar, notifications icon, and breadcrumbs. Main content area renders the active page.
4. **Create KPI overview.** Cards showing key metrics: total users, revenue, conversion rate, active sessions. Each card has a sparkline mini-chart and a trend percentage. Animate numbers on first load with a count-up effect.
5. **Render interactive charts.** A revenue line chart with time range selector (7d, 30d, 90d, 1y). A user growth area chart. A traffic sources pie chart. A top pages bar chart. All charts are interactive (tooltip, click-to-drill-down).
6. **Build the user management table.** A sortable, searchable data table with columns: name, email, role, status, joined date. Implement sort (click column header), search (filter by name/email), and pagination (10/25/50 per page). Use shadcn/ui table components.
7. **Add settings page.** Profile edit form (name, email, avatar) with Zod validation. Preferences (theme, notifications). Account actions (change password, delete account — mock operations with confirmation dialogs).

## Deployment

Deploy on Netlify. Add a `_redirects` file for client-side routing. No environment variables
needed since auth is mocked. The login page is the entry point — use demo credentials shown
on the login form.

## Tips

- shadcn/ui is not a dependency you install — it's a component library you copy into your project. This means you own the code and can customize every component. It's built on Radix UI primitives for accessibility.
- For data tables, separate the data logic (sorting, filtering, pagination) from the rendering. Write a custom hook (`useTableData`) that accepts raw data and returns the processed slice — the table component just renders what it's given.
- Extension: add role-based access control (admin sees all, user sees subset), real-time notifications with a toast system, or data export (CSV/PDF).

## README Guidance

The project repo's README should include a short description, screenshots of the login page
and dashboard, the live demo link (with demo credentials noted), tech stack, features list,
and local dev instructions.
