# Analytics Dashboard

> A full-featured analytics dashboard with Redux Toolkit, Recharts, shadcn/ui (Radix), sortable data tables, and Zod-validated auth.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://analytics-dashboardd.netlify.app/login) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/analytics-dashboard)

---

## Purpose

This is the capstone of Level 2 — a professional-grade dashboard combining every pattern
you've learned: Redux for complex state, Recharts for visualization, shadcn/ui for polished
accessible components, data tables with sorting, and a mock auth flow. It's the kind of
interface you'd build at a SaaS company.

## Tech Stack

- **Framework:** React 19, TypeScript, Vite
- **Styling:** Tailwind CSS, tailwindcss-animate, class-variance-authority, clsx, tailwind-merge
- **State:** Redux Toolkit
- **Charts:** Recharts
- **UI Components:** Radix UI (avatar, dialog, dropdown-menu, label, popover, scroll-area, separator, toast) — shadcn/ui pattern
- **Forms:** React Hook Form + Zod
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Build the auth flow.** Login page with React Hook Form + Zod validation. Mock authentication (hardcoded credentials or localStorage). Protected routes redirect to login. Logout clears state.

2. **Build the dashboard layout.** Sidebar with navigation (shadcn pattern), top bar with user avatar (Radix Avatar) and dropdown menu (Radix DropdownMenu), main content area. Responsive: sidebar collapses on mobile.

3. **Build KPI cards.** Key metrics: total users, revenue, active sessions, conversion rate. Each card shows current value, trend (up/down arrow with percentage), and a mini sparkline chart.

4. **Build the charts page.** Multiple Recharts visualizations: line chart (user growth), bar chart (revenue by month), area chart (traffic sources), pie chart (user demographics). Date range selector filters all charts.

5. **Build the data table.** User management table with columns: name, email, role, status, joined date. Sortable columns (click header to sort). Pagination. Row actions via Radix DropdownMenu.

6. **Add toast notifications.** Radix Toast for action feedback: "User deleted," "Settings saved," etc. Auto-dismiss with configurable duration.

7. **Polish and deploy.** tailwindcss-animate for smooth transitions. Loading skeletons during data fetch simulation. Consistent spacing and typography throughout.

## Tips

- Redux Toolkit + shadcn/ui + Recharts is the production stack for internal dashboards at many companies. Mastering this combination makes you immediately productive on real-world projects.
- Data tables with sorting: maintain sort state (column + direction) in Redux or local state. Sort the data array before rendering. Use stable sort to preserve order of equal elements.
- Extension: add real-time data updates (WebSocket simulation), export to PDF, role-based view (admin sees more), or drag-and-drop widget customization.
