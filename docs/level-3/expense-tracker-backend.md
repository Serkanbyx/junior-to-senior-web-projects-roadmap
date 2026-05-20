# Expense Tracker Backend

> A RESTful API for tracking personal expenses with JWT authentication, Prisma ORM, PostgreSQL, monthly aggregations, and category summaries.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://expense-tracker-backend-wwyp.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/expense-tracker-backend)

---

## Purpose

This project introduces a professional ORM (Prisma) and a production database (PostgreSQL).
Unlike the SQLite projects with raw SQL, here you use Prisma's schema-first approach:
define your data model in a schema file, run migrations, and query with a type-safe client.
The aggregation endpoints teach you to compute reports (monthly totals, category breakdowns)
at the database level.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** PostgreSQL (via Prisma ORM)
- **ORM:** Prisma 6 (@prisma/client)
- **Auth:** JWT (jsonwebtoken) + bcryptjs
- **Validation:** express-validator + Joi
- **Security:** Helmet 8, express-rate-limit
- **Logging:** Morgan
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Set up Prisma with PostgreSQL.** Initialize Prisma (`npx prisma init`), configure the database URL, and define models in `prisma/schema.prisma`. Models: User (id, email, password, name) and Expense (id, userId, amount, type, category, description, date). Run `prisma migrate dev` to create tables.

2. **Build auth with Prisma.** Register: create user with Prisma (`prisma.user.create`), hash password with bcryptjs. Login: find user with `prisma.user.findUnique`, verify password, return JWT. Auth middleware verifies token and attaches userId.

3. **Build expense CRUD.** Create, read (list with filters), update, delete — all scoped to the authenticated user. Prisma queries: `prisma.expense.findMany({ where: { userId } })`. Support filtering by date range, category, and type (income/expense).

4. **Implement monthly aggregation.** `GET /expenses/summary/monthly` groups expenses by year-month. Use Prisma's `groupBy` or raw SQL for complex aggregations. Return: `[{ month: '2024-01', income, expense, net }]`. This powers the frontend's bar charts.

5. **Implement category breakdown.** `GET /expenses/summary/categories` groups by category and sums amounts. Return: `[{ category, total, count, percentage }]`. Calculate percentages server-side. This powers pie charts.

6. **Add dual validation.** Use Joi for schema validation (complex rules, nested objects) and express-validator for route-level input sanitization. Both layers catch different types of invalid input.

7. **Deploy with Prisma migrations.** Deploy to Render with a PostgreSQL database. Run `prisma migrate deploy` on start. Set `DATABASE_URL` (Render PostgreSQL connection string) and `JWT_SECRET`.

## Deployment

Deploy on Render.com with Render PostgreSQL (free tier available). Run Prisma migrations
on deploy. Set `DATABASE_URL` and `JWT_SECRET` as environment variables.

## Tips

- Prisma's schema-first approach: you define your data model in `schema.prisma`, and Prisma generates both the database tables (via migrations) AND the TypeScript client (via generate). One source of truth for your entire data layer.
- `groupBy` in Prisma is powerful but limited. For complex aggregations (running totals, percentages, window functions), use `prisma.$queryRaw` with raw SQL. Prisma doesn't prevent raw SQL — it just makes the common case easy.
- Extension: add recurring expenses, budget goals with alerts, CSV import/export, or multi-currency support with conversion.

## README Guidance

The project repo's README should include a description, Prisma schema diagram, API endpoints
with aggregation examples, tech stack, environment variables, and setup instructions.
