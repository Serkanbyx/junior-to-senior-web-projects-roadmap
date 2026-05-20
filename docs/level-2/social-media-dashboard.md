# Social Media Dashboard

> A social media analytics dashboard tracking followers, engagement, and posts across multiple platforms with CRUD and charts.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://social-media-dashboardd.netlify.app/dashboard) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/social-media-dashboard)

---

## Purpose

This project teaches you to build a multi-widget dashboard layout — the most common pattern
in SaaS and admin interfaces. You'll manage data from multiple "sources" (platforms), display
KPI cards with trend indicators, render engagement charts, and implement CRUD for posts.
The dark/light mode with Tailwind v4 teaches theming at scale.

## Tech Stack

- **Frontend:** React 19, TypeScript, Tailwind CSS v4
- **Backend:** none (mock data)
- **Database:** none (state in Redux)
- **Key libraries / tools:** Redux Toolkit, Recharts (charts), dark/light mode
- **Deployment:** Netlify

## Build Steps

1. **Design the data model.** Define platform accounts (Instagram, Twitter, Facebook, YouTube, LinkedIn) with metrics: followers, following, engagement rate, posts count. Create mock time-series data for follower growth and engagement over 30 days.
2. **Build the KPI cards.** A row of cards at the top, one per platform. Each shows the platform icon, follower count, and daily change (up/down arrow with green/red coloring). Format large numbers with abbreviations (1.2K, 45.6K).
3. **Render analytics charts.** A line chart for follower growth over time (all platforms overlaid or selectable). A bar chart for engagement by platform. An area chart for post reach. Use Recharts with responsive containers.
4. **Implement post management.** A CRUD interface for scheduling/managing posts: create (text, platform, schedule date), read (list with filters), update (edit content), delete (with confirmation). Use Redux Toolkit slices for state.
5. **Add platform filtering.** Toggle which platforms are visible in charts and KPIs. The dashboard should reactively update all widgets when a platform is toggled on/off.
6. **Implement dark/light mode.** Use Tailwind v4's dark mode variant with a toggle button. Persist preference in localStorage. Ensure all components (cards, charts, tables) look correct in both modes — especially chart colors and borders.
7. **Make it responsive.** Desktop: multi-column grid with sidebar. Tablet: 2 columns. Mobile: single column with collapsible sections. Charts resize to fit their container at every breakpoint.

## Deployment

Deploy on Netlify as a static React app. No environment variables or backend needed.
All data is mock/simulated.

## Tips

- Dashboard layouts work best with CSS Grid and named template areas. Define different grid templates per breakpoint for clean responsive behavior.
- Tailwind v4's dark mode is simpler than v3: the `dark:` variant just works with the `@media (prefers-color-scheme)` or a class toggle — no special configuration needed.
- Extension: add real API integration (Twitter/X API, Instagram Graph API), notification system for engagement spikes, or scheduled post publishing.

## README Guidance

The project repo's README should include a short description, screenshots in both light and
dark mode, the live demo link, tech stack, features (multi-platform, charts, CRUD, dark mode),
and local dev instructions.
