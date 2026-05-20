# Fitness Tracker

> A fitness tracking app with interactive dashboard, workout logging, goal management, and progress charts.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://fitness-trackerrrrr.netlify.app/dashboard) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/fitness-tracker)

---

## Purpose

This project combines data entry, goal tracking, and visualization into a dashboard-style
app. You'll learn to model time-series data (workouts over days/weeks), compute progress
against targets, and render meaningful charts that update as new data comes in. The goal
system teaches conditional rendering based on computed state (on-track vs. behind).

## Tech Stack

- **Frontend:** React 18, TypeScript, Tailwind CSS
- **Backend:** none
- **Database:** LocalStorage (via Zustand persist)
- **Key libraries / tools:** Zustand, Recharts (charts/graphs)
- **Deployment:** Netlify

## Build Steps

1. **Model workout data.** Define types: `Workout { id, type (cardio/strength/flexibility), name, duration, calories, sets?, reps?, weight?, date }`. Create a Zustand store with add/edit/delete operations and persistence.
2. **Build the workout logger.** A form with dynamic fields based on workout type: cardio shows duration and distance, strength shows sets/reps/weight. Validate with appropriate constraints (positive numbers, required fields). Quick-add buttons for common exercises.
3. **Create the dashboard.** Display KPI cards at the top: total workouts this week, calories burned, streak (consecutive days with workouts), and progress toward weekly goal. Use `useMemo` to compute these from the raw workout array.
4. **Render progress charts.** A line chart showing workouts per day over the past 4 weeks. A bar chart comparing this week vs. last week. A pie chart breaking down workout types. All charts update reactively when new workouts are logged.
5. **Implement goal management.** Let users set weekly goals (e.g. "4 workouts per week", "burn 2000 calories"). Show progress bars for each goal with color coding: green (on track), yellow (behind), red (missed). Store goals in Zustand.
6. **Add workout history.** A searchable, filterable list of all past workouts. Filter by type, date range, or exercise name. Show per-workout details and allow deletion.
7. **Make it responsive.** Dashboard cards stack on mobile, charts resize gracefully, and the logger form uses a bottom sheet or modal on small screens. Ensure touch targets are at least 44px.

## Deployment

Deploy on Netlify as a static app. No backend or API keys needed.
All data persists in the browser via LocalStorage.

## Tips

- Recharts is the easiest charting library for React — it uses JSX components (`<LineChart>`, `<Bar>`) rather than imperative D3 code. But always memoize your chart data to avoid unnecessary re-renders.
- Streak calculation is a fun algorithm: sort workouts by date, then iterate backwards checking for consecutive days. Handle timezone edge cases with date-only comparisons (ignore hours).
- Extension: add body measurements tracking, workout templates for quick logging, or social sharing of achievements.

## README Guidance

The project repo's README should include a short description, a screenshot of the dashboard
with charts, the live demo link, tech stack, features (logging, goals, charts, history), and
local dev instructions.
