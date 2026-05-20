# Expense Tracker MERN

> A fullstack expense tracker with TypeScript frontend, Recharts analytics, server-side pagination, and 32 integration tests.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://expense-tracker-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/expense-tracker-mern)

---

## Purpose

This project connects data visualization with a real backend. The server handles
pagination, filtering, and aggregation — the frontend visualizes results with Recharts.
It teaches the principle of "compute on the server, render on the client," TypeScript
in a React project, and building accessible modals and forms.

## Tech Stack

- **Frontend:** React 19, TypeScript 5.5, Vite 8, Tailwind CSS 4, React Router 7
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT + bcryptjs
- **Charts:** Recharts 3 (bar charts, pie charts)
- **Dates:** date-fns 4
- **Icons:** Heroicons 2
- **Validation:** express-validator (backend), TypeScript (frontend)
- **Security:** Helmet, rate limiting, NoSQL injection prevention, HPP
- **Testing:** 32 integration tests (Jest + Supertest + in-memory MongoDB)
- **UX:** React Hot Toast, accessible modals (focus trap, ARIA, Escape to close)
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build the transaction API with pagination.** CRUD endpoints for transactions (income and expense types). Server-side pagination with configurable limits (up to 100/page). Filter by month, category, and type via query params. Ownership isolation per user.

2. **Implement the config endpoint.** `GET /api/config` returns available categories and transaction types. The frontend reads from this single source of truth — no hardcoded category lists duplicated between client and server.

3. **Build the TypeScript frontend.** Strict-mode TypeScript with shared type definitions for transactions, filters, and API responses. Type-safe Axios calls. This prevents entire categories of runtime bugs.

4. **Build the dashboard with Recharts.** Summary cards (total income, expenses, net balance). Monthly income vs. expense bar chart. Category breakdown pie chart. All charts update reactively when filters change.

5. **Implement advanced filtering.** Filter by month (date picker), category (dropdown from config endpoint), and type (income/expense toggle). Filters apply to both the chart data and the transaction list simultaneously. Instant results without page reload.

6. **Build accessible modals and forms.** Create/edit transaction modals with: focus trap (Tab stays inside modal), Escape to close, `aria-modal` and `role="dialog"` attributes, body scroll locking. Form validation on both client and server sides.

7. **Add testing and deploy.** 32 integration tests covering auth flows and transaction CRUD. Test against in-memory MongoDB for speed. Deploy with responsive mobile-first layout (collapsible sidebar, 44px touch targets).

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`. Frontend on Netlify with `VITE_API_URL`.
The config endpoint eliminates category sync issues between deploys.

## Tips

- The config endpoint pattern (`/api/config`) is underrated. Instead of hardcoding categories in the frontend, fetch them from the backend. When you add a new category, you only change one place — the backend — and all clients automatically get the update.
- Recharts needs clean data shapes. Create utility functions that transform API responses into Recharts-compatible arrays: `[{ name: 'Jan', income: 5000, expense: 3200 }]`.
- Extension: add budget goals with progress bars, recurring transactions, CSV import/export, or PDF monthly reports.

## README Guidance

The project repo's README should include a description, dashboard screenshot with charts,
tech stack (highlighting TypeScript), test coverage, environment variables, and setup instructions.
