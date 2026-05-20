# Expense Tracker

> A modern expense tracker with Recharts visualization, category management, CSV export, dark mode, and localStorage persistence.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://expense-trackerrrrrrrr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/expense-tracker)

---

## Purpose

This project combines data entry, state management, and visualization. You'll build a
complete personal finance tool: add income/expenses, categorize them, view breakdowns in
charts, and export data. It teaches Zustand persistence, Recharts for data viz, and building
forms with proper validation — all patterns you'll reuse in every data-heavy frontend.

## Tech Stack

- **Framework:** React, TypeScript, Vite
- **Styling:** Tailwind CSS
- **State:** Zustand with localStorage persistence
- **Charts:** Recharts (pie charts, bar charts)
- **Forms:** React Hook Form + Zod validation
- **Dates:** date-fns
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Design the Zustand store.** Transactions array with: id, amount, type (income/expense), category, description, date. Persisted to localStorage. Actions: add, edit, delete, filter.

2. **Build the transaction form.** React Hook Form with Zod: validate amount (positive number), category (from predefined list), date (valid date via date-fns). Toggle between income and expense.

3. **Build the dashboard summary.** KPI cards: total income, total expenses, net balance. Calculate from the transactions array. Update reactively when transactions change.

4. **Add Recharts visualizations.** Pie chart for category breakdown (what percentage goes to food, transport, etc.). Bar chart for monthly income vs expenses. Transform transaction data into Recharts-compatible arrays.

5. **Implement filtering.** Filter by month, category, or type. Filters apply to both the transaction list and charts simultaneously. Date-fns handles month calculations.

6. **Add CSV export.** Convert filtered transactions to CSV format. Trigger browser download. Useful for importing into Excel or other finance tools.

7. **Add dark mode and deploy.** Tailwind dark mode class strategy. Toggle persisted in Zustand. Deploy as static site on Netlify.

## Tips

- Zustand persist + localStorage is the simplest "database" for frontend-only apps. All transactions survive page refresh with zero backend. Perfect for personal tools.
- Recharts data format: `[{ name: 'Food', value: 450 }, { name: 'Transport', value: 200 }]` for pie charts. Create a utility function that transforms raw transactions into this shape.
- Extension: add budget goals per category, recurring transactions, multi-currency support, or bank statement import (parse CSV).
