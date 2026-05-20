# Expense Tracker

> A personal expense tracker with interactive charts, category management, CSV export, and dark mode.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://expense-trackerrrrrrrr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/expense-tracker)

---

## Purpose

This project is about data entry, aggregation, and visualization. You'll learn to model
financial data with categories, compute running totals and breakdowns, render charts from
dynamic data, and export structured data to CSV. It's the classic CRUD app elevated with
data visualization — a pattern used in every analytics-facing product.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** none
- **Database:** LocalStorage (via Zustand persist)
- **Key libraries / tools:** Zustand, Recharts (or similar), CSV export logic
- **Deployment:** Netlify

## Build Steps

1. **Model an expense.** Define the shape: `{ id, amount, category, description, date, type: 'income' | 'expense' }`. Create a Zustand store with CRUD actions (add, edit, delete) and persist middleware for LocalStorage.
2. **Build the entry form.** Amount input (number), category selector (predefined + custom categories), date picker, description text field, and income/expense toggle. Validate that amount is positive and category is selected.
3. **Render the transaction list.** Show all expenses sorted by date (newest first). Each row displays date, category icon, description, and formatted amount (green for income, red for expense). Add inline delete and edit actions.
4. **Compute aggregations.** Calculate total income, total expenses, and balance. Break down expenses by category (food, transport, entertainment, etc.). Compute monthly totals for trend analysis. Use `useMemo` to avoid recalculating on every render.
5. **Build interactive charts.** A pie/donut chart for category breakdown and a bar/line chart for monthly spending trends. Charts should update reactively when data changes. Add tooltips and legends for clarity.
6. **Implement filtering and date ranges.** Filter by category, date range (this week, this month, custom), and type (income/expense). The charts and totals should reflect the active filters.
7. **Add CSV export and dark mode.** Generate a CSV string from the filtered data and trigger a download with `Blob` + `URL.createObjectURL`. Implement dark mode with Tailwind's `dark:` variant and a toggle that persists preference.

## Deployment

Deploy on Netlify as a static React app. No backend or environment variables needed.
All data lives in the browser's LocalStorage.

## Tips

- Financial calculations should use integers (cents) internally to avoid floating-point errors. Display with `(amount / 100).toFixed(2)` and format with `Intl.NumberFormat`.
- CSV export is simpler than it looks: join headers, then map each row to comma-separated values. Wrap fields containing commas in quotes.
- Extension: add budget limits per category with visual warnings, recurring transactions, or multi-currency support.

## README Guidance

The project repo's README should include a short description, screenshots of the dashboard
with charts and transaction list, the live demo link, tech stack, features list, and local
dev instructions.
