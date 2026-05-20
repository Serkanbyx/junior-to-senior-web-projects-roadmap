# Expense Tracker Backend

> A backend API for expense tracking with MongoDB aggregation pipelines, reporting, and user-scoped data.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://expense-tracker-backend-wwyp.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/expense-tracker-backend)

---

## Purpose

This project introduces MongoDB's aggregation framework — the most powerful feature of Mongo
that most developers never learn properly. You'll build pipelines that group expenses by
category, compute monthly totals, calculate running balances, and generate summary reports.
It's the backend counterpart to the Level 2 Expense Tracker frontend, and it teaches you to
do heavy data processing on the database layer rather than in application code.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose + aggregation pipelines)
- **Key libraries / tools:** Mongoose, JWT auth, dotenv
- **Deployment:** Render.com

## Build Steps

1. **Model expenses.** Schema: `{ user: ObjectId, amount, type: 'income' | 'expense', category, description, date, createdAt }`. Index on `user + date` for efficient queries. Categories: food, transport, entertainment, bills, salary, etc.
2. **Build CRUD endpoints.** Standard authenticated routes: create, read (list with filters), update, delete. All scoped to the authenticated user. Support filtering by date range, category, and type.
3. **Implement aggregation: category breakdown.** `GET /expenses/summary/categories` uses `$group` to sum amounts per category. Return `[{ category, total, count, percentage }]`. Use `$match` first to filter by date range.
4. **Implement aggregation: monthly totals.** `GET /expenses/summary/monthly` groups by year-month using `$dateToString`. Return income, expenses, and net balance per month. This powers time-series charts on the frontend.
5. **Implement aggregation: running balance.** Calculate the cumulative balance over time using `$setWindowFields` (MongoDB 5.0+) or a sorted query with application-level accumulation. Return daily balance snapshots.
6. **Build the reports endpoint.** `GET /expenses/report?start=2024-01-01&end=2024-12-31` returns a comprehensive report: total income, total expenses, net savings, top categories, average daily spend, and month-over-month comparison.
7. **Add budget alerts.** Let users set budget limits per category. On each new expense, check if the category total for the current month exceeds the budget. Return a warning in the response if over budget.

## Deployment

Deploy on Render.com. Set `MONGODB_URI` and `JWT_SECRET`. Seed with sample expense data
using a script so the aggregation endpoints have interesting data to return.

## Tips

- Always do aggregation in MongoDB, not in JavaScript. A `$group` pipeline on 10,000 documents is milliseconds; fetching all documents and summing in JS is seconds and uses 100x more memory.
- Use `$facet` to run multiple aggregation pipelines in a single query. For example, get category breakdown AND monthly totals in one database call.
- Extension: add recurring expenses (auto-create monthly entries), budget forecasting (project future balance based on trends), or export to PDF report.

## README Guidance

The project repo's README should include a description, endpoint table (CRUD + aggregation),
example aggregation responses, environment variables, and local setup steps with seed script.
