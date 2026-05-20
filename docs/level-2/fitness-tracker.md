# Fitness Tracker

> A fitness tracking PWA with workout logging, Recharts dashboard, goal management, date-fns utilities, and localStorage persistence.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://fitness-trackerrrrr.netlify.app/dashboard) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/fitness-tracker)

---

## Purpose

This project combines data entry (workout logging) with progress visualization (Recharts
dashboard). It teaches you to track state over time, calculate streaks and trends, and
present progress data in a motivating way. The PWA capability means users can log workouts
offline at the gym and sync later.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS
- **State:** Zustand with localStorage persistence
- **Charts:** Recharts (line charts, bar charts for progress)
- **Forms:** React Hook Form + Zod
- **Dates:** date-fns
- **PWA:** vite-plugin-pwa + Workbox (workbox-precaching, workbox-routing)
- **Icons:** Lucide React, clsx
- **Deployment:** Netlify

## Build Steps

1. **Design the data model.** Workout: `{ id, type, duration, calories, date, notes }`. Goal: `{ id, type, target, current, deadline }`. All stored in Zustand with localStorage persistence.

2. **Build the workout logging form.** Select workout type, enter duration, optionally add calories and notes. date-fns for date selection and formatting. React Hook Form + Zod validation.

3. **Build the dashboard with Recharts.** Weekly activity bar chart (workouts per day). Monthly progress line chart (calories burned trend). Goal progress rings or bars. Summary cards (total workouts, streaks, personal bests).

4. **Implement goal management.** Create goals (e.g., "Run 3x/week" or "Burn 2000 cal/week"). Track progress against goals automatically from logged workouts. Show completion percentage.

5. **Calculate streaks and stats.** Current streak (consecutive days with workouts). Longest streak ever. Weekly/monthly totals. Use date-fns to calculate day differences and group by week/month.

6. **Add PWA support.** vite-plugin-pwa with Workbox for offline caching. Users can log workouts without internet. The app is installable on mobile home screen.

7. **Deploy on Netlify.** Static PWA. All data in localStorage.

## Tips

- Streak calculation: sort workouts by date, iterate backwards from today. A streak continues as long as each day has at least one workout (or is today). Break on the first gap.
- Recharts `ResponsiveContainer` makes charts resize with their parent. Always wrap charts in it — hardcoded widths break on mobile.
- Extension: add exercise library with sets/reps tracking, social sharing of milestones, Apple Health / Google Fit integration, or AI workout suggestions.
