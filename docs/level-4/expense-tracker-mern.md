# Expense Tracker MERN

> A fullstack expense tracker with MongoDB aggregation, chart visualization, and category management.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://expense-tracker-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/expense-tracker-mern)

---

## Purpose

This project connects the Level 2 frontend expense tracker with the Level 3 backend
aggregation API. The backend does the heavy computation (aggregation pipelines) and the
frontend visualizes the results with charts. It teaches you the principle of "compute on
the server, render on the client" — the correct architecture for data-heavy dashboards.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS, Recharts
- **Backend:** Node.js, Express, MongoDB (aggregation pipelines)
- **Auth:** JWT
- **Key libraries / tools:** Mongoose, Recharts, Axios, date-fns
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build the aggregation API.** Endpoints: `GET /expenses/summary` (total income/expenses/balance), `GET /expenses/by-category` ($group by category), `GET /expenses/monthly` ($group by year-month). All user-scoped with auth.
2. **Build expense CRUD.** Standard `POST/GET/PATCH/DELETE /expenses` with user scoping. Support filtering by date range, category, and type (income/expense) via query params.
3. **Create the dashboard frontend.** Fetch summary data on load and render: KPI cards (income, expenses, balance), a pie chart for category breakdown, and a line/bar chart for monthly trends.
4. **Build the transaction form.** Amount, category (from a predefined list), description, date, and type toggle (income/expense). On submit, POST to the API and refresh the dashboard data.
5. **Implement date range filtering.** A date picker that sets the range for all dashboard data. When the user changes the range, re-fetch all aggregation endpoints with the new params. Charts and KPIs update reactively.
6. **Add the transaction list.** A paginated table below the charts showing all transactions. Sort by date, filter by category. Inline delete and edit actions that update both the list and the charts.
7. **Deploy and test.** Ensure aggregation pipelines return correct results with various data volumes. Test edge cases: no data (show empty states), single transaction, date ranges with no entries.

## Deployment

Frontend on Netlify, backend on Render. Seed the database with sample data so the demo
shows meaningful charts. Set standard env vars: `MONGODB_URI`, `JWT_SECRET`, `VITE_API_URL`.

## Tips

- Always aggregate on the server. Fetching 10,000 transactions to the client and summing in JavaScript is the #1 performance mistake in dashboard apps. MongoDB's `$group` is orders of magnitude faster.
- Use `$facet` to run category breakdown AND monthly totals in a single aggregation query — one database round trip instead of two.
- Extension: add budget goals with progress bars, recurring transactions, CSV import, or a PDF monthly report generator.

## README Guidance

The project repo's README should include a description, dashboard screenshot with charts,
tech stack, architecture diagram, environment variables, and setup instructions.
