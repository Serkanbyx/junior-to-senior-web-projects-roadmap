# Social Media Dashboard

> A social media analytics dashboard tracking followers and engagement across 5 platforms, with Recharts, Redux Toolkit, and dark/light mode.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://social-media-dashboardd.netlify.app/dashboard) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/social-media-dashboard)

---

## Purpose

This project teaches dashboard architecture: multiple data widgets, shared state across
many components, theme switching, and responsive grid layouts. With Redux Toolkit managing
platform data (Instagram, Twitter, Facebook, YouTube, LinkedIn) and Recharts rendering
analytics, it's a comprehensive data visualization exercise.

## Tech Stack

- **Framework:** React 19, TypeScript, Vite
- **Styling:** Tailwind CSS v4
- **State:** Redux Toolkit (platform data, theme, CRUD operations)
- **Charts:** Recharts (line charts, bar charts for engagement)
- **Icons:** Lucide React
- **Utilities:** clsx, tailwind-merge
- **Deployment:** Netlify

## Build Steps

1. **Design the Redux store.** Slices: `platformsSlice` (follower counts, engagement data per platform), `postsSlice` (CRUD for managing posts), `uiSlice` (theme, sidebar state). Type everything with TypeScript.

2. **Build the KPI overview.** Top cards showing: total followers, total engagement, daily growth. Each platform gets a mini-card with its icon, follower count, and daily change (±). Color-coded per platform.

3. **Build analytics charts.** Recharts line chart: follower growth over time (per platform or total). Bar chart: engagement by platform. Area chart: reach/impressions trend. All charts respond to the selected time range.

4. **Implement CRUD for posts.** Create, read, update, delete posts (mock data). Post: platform, content, scheduled time, status. Redux manages the state with full CRUD actions.

5. **Add dark/light mode.** Tailwind dark mode with class strategy. Toggle button in header. Persist preference. All charts and cards adapt to the theme.

6. **Build the responsive grid layout.** CSS Grid for dashboard widgets. Responsive: 4 columns on desktop, 2 on tablet, 1 on mobile. Widgets resize gracefully.

7. **Deploy on Netlify.** Static app with mock analytics data.

## Tips

- Dashboard layouts work best with CSS Grid's `grid-template-columns: repeat(auto-fill, minmax(280px, 1fr))` — cards fill available space and wrap naturally on smaller screens.
- Recharts in dark mode: pass theme-aware colors to chart components. Use CSS variables or React context to switch chart colors when the theme changes.
- Extension: add real API integration (social media APIs), scheduled posting, engagement rate calculations, or competitor tracking.
