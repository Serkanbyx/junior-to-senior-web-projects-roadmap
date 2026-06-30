<p align="center">
  <img src="./assets/banner.svg?v=2" alt="Junior to Senior Web Projects Roadmap" width="100%" />
</p>

<h1 align="center">Junior → Senior Web Projects Roadmap</h1>

<p align="center">
  A structured, 5-level roadmap of <strong>70+ real-world web projects</strong> that takes you from
  writing your first DOM script to designing senior-grade fullstack systems.
  Every project comes with a short build guide, the source code, and a live demo.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/projects-70%2B-4047E6?style=flat-square" alt="projects" />
  <img src="https://img.shields.io/badge/levels-5-4047E6?style=flat-square" alt="levels" />
  <img src="https://img.shields.io/badge/stack-MERN-4047E6?style=flat-square" alt="stack" />
  <img src="https://img.shields.io/badge/license-MIT-4047E6?style=flat-square" alt="license" />
  <img src="https://img.shields.io/badge/PRs-welcome-4047E6?style=flat-square" alt="PRs welcome" />
</p>

---

## Why this repo exists

Most "project idea" lists are flat — 50 random apps with no order and no reasoning.
This one is **sequenced**. The projects are ordered so that each one builds on the skills
of the previous level, and each level maps to a recognisable point in a web developer's
career: from absolute beginner, through intermediate frontend, into backend, then
fullstack MERN, and finally senior-level distributed/AI/security systems.

If you finish a level, you can honestly claim the skill it represents. That is the point.

## Who this is for

- **Self-taught developers** who want a path instead of a pile of tutorials.
- **Junior developers** trying to make the jump to mid-level with evidence, not vibes.
- **Anyone** building a GitHub portfolio that a recruiter can scan in 30 seconds.

## How to use this roadmap

1. **Find your level.** Don't start at Level 1 if you already ship React apps — start where it gets uncomfortable.
2. **Build, don't read.** Open the project's guide, understand the goal, then build it yourself before looking at the reference code.
3. **Ship every project.** Each one gets its own repo and a live deployment. A project that isn't deployed doesn't count.
4. **Write the README.** Treat every project's README as practice for technical communication — it matters as much as the code.
5. **Move up only when comfortable.** A level is done when you could rebuild any project in it without a guide.
6. **Track your progress.** [Fork this repo](https://github.com/Serkanbyx/junior-to-senior-web-projects-roadmap/fork) and use the [Progress Tracker](./docs/PROGRESS.md) to check off projects as you go.

## A note on AI tools

AI coding assistants (Copilot, Cursor, ChatGPT) are part of modern development — but
**when** you use them matters more than **whether** you use them.

| Level | AI approach |
|-------|-------------|
| **1 – 2** | **Don't use AI.** Write every line yourself. You're building muscle memory for the language, the DOM, and the browser. If AI writes it for you, you skip the struggle that makes it stick. |
| **3 – 4** | **Use AI as a pair programmer.** You design the architecture, write the core logic, and let AI help with boilerplate, debugging, and refactoring. Always understand what it generates before you commit it. |
| **5** | **Use AI as a power tool and build with it.** Leverage AI for rapid prototyping, complex integrations, and code review — and build AI-powered products yourself (chatbots, recommendation engines, computer vision). |

The rule of thumb: if you can't explain what the AI wrote, you're not ready to use it at
that level yet.

## Find your starting level

Not sure where to begin? Use the table below for a quick match, or take the
[detailed self-assessment quiz](./docs/find-your-level.md) to be sure.

| If you can honestly say… | Start at |
|--------------------------|----------|
| "I'm new to JavaScript or still learning the basics" | **[Level 1 — JS Fundamentals](#level-1--javascript-fundamentals)** |
| "I can write vanilla JS but haven't consumed real APIs" | **[Level 2 — Intermediate Frontend](#level-2--intermediate-frontend)** |
| "I build frontends comfortably but never touched Node or Express" | **[Level 3 — Backend Fundamentals](#level-3--backend-fundamentals)** |
| "I know backend basics but haven't shipped a fullstack app" | **[Level 4 — Fullstack MERN](#level-4--fullstack-mern)** |
| "I ship fullstack apps and want architecture-level challenges" | **[Level 5 — Senior-Level Systems](#level-5--senior-level-systems)** |

## Roadmap

<p align="center">
  <img src="./assets/roadmap.svg" alt="Roadmap — Level 1 through Level 5" width="100%" />
</p>

> **Legend:** ✅ built & deployed · 🚧 planned / in progress

---

## Level 1 — JavaScript Fundamentals

Plain JavaScript, the DOM, events, and clean simple UI. No frameworks. The goal is to be
fluent in the language and the browser before adding any abstraction.

**Skills you'll gain:**

- DOM manipulation & event-driven UI (click, keydown, input, touch, drag)
- State management with plain arrays and objects — the data → render cycle
- CSS Grid, Flexbox & responsive layouts (masonry, mobile-first)
- CSS 3D transforms & micro-animations (flip, fade, ripple effects)
- Timer mechanics — `setInterval`, `Date.now()`, drift-safe countdowns
- Form handling, input validation & conditional rendering
- LocalStorage persistence, data hydration & JSON export/import
- `fetch` + `async/await` for API consumption and error handling
- Browser APIs: Intersection Observer, Web Speech, Web Audio, Drag and Drop
- PWA fundamentals — Service Worker, manifest, offline caching
- Accessibility (ARIA labels, keyboard navigation, WCAG 2.1 AA)
- SEO essentials — Open Graph, JSON-LD structured data, semantic HTML
- Algorithm thinking — Fisher-Yates shuffle, Shunting-yard expression parsing

<p align="center">
  <a href="https://photo-galleryyyyy.netlify.app/"><img src="./assets/screenshots/level-1/photo-gallery.png" width="19%" alt="Photo Gallery" /></a>
  <a href="https://basic-calculatorrrr.netlify.app/"><img src="./assets/screenshots/level-1/calculator.png" width="19%" alt="Basic Calculator" /></a>
  <a href="https://memory-gameeeeee.netlify.app/"><img src="./assets/screenshots/level-1/memory-game.png" width="19%" alt="Memory Game" /></a>
  <a href="https://type-speed-testt.netlify.app/"><img src="./assets/screenshots/level-1/type-speed-test.png" width="19%" alt="Type Speed Test" /></a>
  <a href="https://quote-generatorrrrr.netlify.app/"><img src="./assets/screenshots/level-1/quote-generator.png" width="19%" alt="Quote Generator" /></a>
</p>
<p align="center">
  <a href="https://weather-app-basicc.netlify.app/"><img src="./assets/screenshots/level-1/weather-app.png" width="19%" alt="Weather App" /></a>
  <a href="https://tic-tac-toeeeeeeeeee.netlify.app/"><img src="./assets/screenshots/level-1/tic-tac-toe.png" width="19%" alt="Tic Tac Toe" /></a>
  <a href="https://countdown-timerrrr.netlify.app/"><img src="./assets/screenshots/level-1/countdown-timer.png" width="19%" alt="Countdown Timer" /></a>
  <a href="https://simple-to-do-listt.netlify.app/"><img src="./assets/screenshots/level-1/todo-list.png" width="19%" alt="Simple To-Do List" /></a>
  <a href="https://bmi-calculatorrrrr.netlify.app/"><img src="./assets/screenshots/level-1/bmi-calculator.png" width="19%" alt="BMI Calculator" /></a>
</p>
<p align="center">
  <a href="https://personal-portfolio-websiteee.netlify.app/"><img src="./assets/screenshots/level-1/portfolio.png" width="19%" alt="Personal Portfolio" /></a>
</p>


| Project | What you'll build | Guide | Links |
|---------|-------------------|-------|-------|
| ✅ Tic Tac Toe | Game state, win detection, click-driven DOM | [Guide](./docs/level-1/tic-tac-toe.md) | [Code](https://github.com/Serkanbyx/tic-tac-toe) · [Demo](https://tic-tac-toeeeeeeeeee.netlify.app/) |
| ✅ Basic Calculator | Input handling, operations, UI state | [Guide](./docs/level-1/basic-calculator.md) | [Code](https://github.com/Serkanbyx/basic-calculator) · [Demo](https://basic-calculatorrrr.netlify.app/) |
| ✅ Type Speed Test | Timers, keyboard events, WPM calculation | [Guide](./docs/level-1/type-speed-test.md) | [Code](https://github.com/Serkanbyx/type-speed-test) · [Demo](https://type-speed-testt.netlify.app/) |
| ✅ Memory Game | Array shuffling, match logic, flip animation | [Guide](./docs/level-1/memory-game.md) | [Code](https://github.com/Serkanbyx/memory-game) · [Demo](https://memory-gameeeeee.netlify.app/) |
| ✅ Countdown Timer | `setInterval`, date math, formatting | [Guide](./docs/level-1/countdown-timer.md) | [Code](https://github.com/Serkanbyx/countdown-timer) · [Demo](https://countdown-timerrrr.netlify.app/) |
| ✅ BMI Calculator | Form input, validation, formula output | [Guide](./docs/level-1/bmi-calculator.md) | [Code](https://github.com/Serkanbyx/BMI-calculator) · [Demo](https://bmi-calculatorrrrr.netlify.app/) |
| ✅ Quote Generator | Data arrays, random selection, share action | [Guide](./docs/level-1/quote-generator.md) | [Code](https://github.com/Serkanbyx/quote-generator) · [Demo](https://quote-generatorrrrr.netlify.app/) |
| ✅ Simple To-Do List | In-memory CRUD, list rendering, filtering | [Guide](./docs/level-1/simple-to-do-list.md) | [Code](https://github.com/Serkanbyx/simple-to-do-list) · [Demo](https://simple-to-do-listt.netlify.app/) |
| ✅ Photo Gallery | Grid layout, lightbox modal, lazy loading | [Guide](./docs/level-1/photo-gallery.md) | [Code](https://github.com/Serkanbyx/photo-gallery) · [Demo](https://photo-galleryyyyy.netlify.app/) |
| ✅ Personal Portfolio Website | Responsive layout, semantic HTML, CSS craft | [Guide](./docs/level-1/personal-portfolio-website.md) | [Code](https://github.com/Serkanbyx/personal-portfolio-website) · [Demo](https://personal-portfolio-websiteee.netlify.app/) |
| ✅ Weather App (Basic) | Static UI, layout, conditional rendering | [Guide](./docs/level-1/weather-app-basic.md) | [Code](https://github.com/Serkanbyx/weather-app-basic) · [Demo](https://weather-app-basicc.netlify.app/) |

## Level 2 — Intermediate Frontend

Real APIs, client-side state, responsive design, and a couple of games for logic practice.
By the end of this level you can call yourself a junior frontend developer.

**Skills you'll gain:**

- React + TypeScript + Vite — modern frontend toolchain from scratch
- State management with Zustand (simple) and Redux Toolkit (complex — slices, thunks, selectors)
- Data visualization with Recharts — line, bar, pie, and area charts
- Form validation with React Hook Form + Zod schema definitions
- Accessible UI components with Radix UI, Headless UI & shadcn/ui pattern
- Map integration with Leaflet + react-leaflet (markers, routes, geospatial filtering)
- Server state & caching with TanStack React Query
- Drag-and-drop with dnd-kit — sortable lists, cross-container moves
- HTML5 Canvas game loop — `requestAnimationFrame`, delta-time physics, collision detection
- HTML5 Audio API — playback control, seekable progress, shuffle/repeat algorithms
- Markdown rendering with react-markdown + remark-gfm
- API key protection via Netlify Functions (serverless proxy)
- PWA with vite-plugin-pwa + Workbox — offline caching, installability
- XSS protection with DOMPurify for external API content
- Complex algorithm design — chess move validation, check/checkmate detection

<p align="center">
  <a href="https://recipe-web-appp.netlify.app/"><img src="./assets/screenshots/level-2/recipe-app.png" width="19%" alt="Recipe App" /></a>
  <a href="https://stock-market-dashboarddd.netlify.app/"><img src="./assets/screenshots/level-2/stock-market.png" width="19%" alt="Stock Market Dashboard" /></a>
  <a href="https://real-estate-listingg.netlify.app/"><img src="./assets/screenshots/level-2/real-estate.png" width="19%" alt="Real Estate Listing" /></a>
  <a href="https://music-playerrrrr.netlify.app/player"><img src="./assets/screenshots/level-2/music-player.png" width="19%" alt="Music Player" /></a>
  <a href="https://fitness-trackerrrrr.netlify.app/dashboard"><img src="./assets/screenshots/level-2/fitness-tracker.png" width="19%" alt="Fitness Tracker" /></a>
</p>
<p align="center">
  <a href="https://e-commerce-frontendd.netlify.app/"><img src="./assets/screenshots/level-2/e-commerce.png" width="19%" alt="E-commerce Frontend" /></a>
  <a href="https://social-media-dashboardd.netlify.app/dashboard"><img src="./assets/screenshots/level-2/social-media-dashboard.png" width="19%" alt="Social Media Dashboard" /></a>
  <a href="https://interactive-mappp.netlify.app/"><img src="./assets/screenshots/level-2/interactive-map.png" width="19%" alt="Interactive Map" /></a>
  <a href="https://flappy-birddddd.netlify.app/"><img src="./assets/screenshots/level-2/flappy-bird.png" width="19%" alt="Flappy Bird" /></a>
  <a href="https://basic-chess-board-logic.netlify.app/"><img src="./assets/screenshots/level-2/chess.png" width="19%" alt="Chess Board" /></a>
</p>
<p align="center">
  <a href="https://weather-app-advancedd.netlify.app/"><img src="./assets/screenshots/level-2/weather-app.png" width="19%" alt="Weather App API" /></a>
  <a href="https://expense-trackerrrrrrrr.netlify.app/"><img src="./assets/screenshots/level-2/expense-tracker.png" width="19%" alt="Expense Tracker" /></a>
  <a href="https://notes-web-apppp.netlify.app/"><img src="./assets/screenshots/level-2/notes-app.png" width="19%" alt="Notes App" /></a>
  <a href="https://chat-uiii.netlify.app/"><img src="./assets/screenshots/level-2/chat-ui.png" width="19%" alt="Chat UI" /></a>
  <a href="https://travel-plannerrr.netlify.app/"><img src="./assets/screenshots/level-2/travel-planner.png" width="19%" alt="Travel Planner" /></a>
</p>
<p align="center">
  <a href="https://analytics-dashboardd.netlify.app/login"><img src="./assets/screenshots/level-2/analytics-dashboard.png" width="19%" alt="Analytics Dashboard" /></a>
</p>

| Project | What you'll build | Guide | Links |
|---------|-------------------|-------|-------|
| ✅ Weather App (API) | `fetch`, async/await, API keys, error states | [Guide](./docs/level-2/weather-app-api.md) | [Code](https://github.com/Serkanbyx/weather-app-advanced) · [Demo](https://weather-app-advancedd.netlify.app/) |
| ✅ Recipe App | Search, API consumption, detail views | [Guide](./docs/level-2/recipe-app.md) | [Code](https://github.com/Serkanbyx/recipe-web-app) · [Demo](https://recipe-web-appp.netlify.app/) |
| ✅ Stock Market Dashboard | Charts, polling, number formatting | [Guide](./docs/level-2/stock-market-dashboard.md) | [Code](https://github.com/Serkanbyx/stock-market-dashboard) · [Demo](https://stock-market-dashboarddd.netlify.app/) |
| ✅ Real Estate Listing | Filtering, sorting, card grids | [Guide](./docs/level-2/real-estate-listing.md) | [Code](https://github.com/Serkanbyx/real-estate-listing) · [Demo](https://real-estate-listingg.netlify.app/) |
| ✅ Expense Tracker | State management, categories, totals | [Guide](./docs/level-2/expense-tracker.md) | [Code](https://github.com/Serkanbyx/expense-tracker) · [Demo](https://expense-trackerrrrrrrr.netlify.app/) |
| ✅ Notes App | Persistence with `localStorage`, CRUD | [Guide](./docs/level-2/notes-app.md) | [Code](https://github.com/Serkanbyx/notes-web-app) · [Demo](https://notes-web-apppp.netlify.app/) |
| ✅ Music Player | Audio API, playlist state, progress bar | [Guide](./docs/level-2/music-player.md) | [Code](https://github.com/Serkanbyx/music-player) · [Demo](https://music-playerrrrr.netlify.app/player) |
| ✅ Travel Planner | Multi-step state, itinerary building | [Guide](./docs/level-2/travel-planner.md) | [Code](https://github.com/Serkanbyx/travel-planner) · [Demo](https://travel-plannerrr.netlify.app/plans) |
| ✅ Interactive Map | Leaflet/Mapbox, markers, geolocation | [Guide](./docs/level-2/interactive-map.md) | [Code](https://github.com/Serkanbyx/interactive-map) · [Demo](https://interactive-mappp.netlify.app/map) |
| ✅ Fitness Tracker | Data entry, progress visualization | [Guide](./docs/level-2/fitness-tracker.md) | [Code](https://github.com/Serkanbyx/fitness-tracker) · [Demo](https://fitness-trackerrrrr.netlify.app/dashboard) |
| ✅ E-commerce Frontend | Product grid, filters, cart state | [Guide](./docs/level-2/e-commerce-frontend.md) | [Code](https://github.com/Serkanbyx/e-commerce-frontend) · [Demo](https://e-commerce-frontendd.netlify.app/) |
| ✅ Chat UI | Message list, input, component composition | [Guide](./docs/level-2/chat-ui.md) | [Code](https://github.com/Serkanbyx/chat-ui) · [Demo](https://chat-uiii.netlify.app/) |
| ✅ Flappy Bird | Game loop, collision detection, canvas | [Guide](./docs/level-2/flappy-bird.md) | [Code](https://github.com/Serkanbyx/flappy-bird) · [Demo](https://flappy-birddddd.netlify.app/) |
| ✅ Chess Board Logic | Board representation, move validation | [Guide](./docs/level-2/chess-board-logic.md) | [Code](https://github.com/Serkanbyx/basic-chess-board-logic) · [Demo](https://basic-chess-board-logic.netlify.app/) |
| ✅ Social Media Dashboard | Widget layout, mock data, responsive grid | [Guide](./docs/level-2/social-media-dashboard.md) | [Code](https://github.com/Serkanbyx/social-media-dashboard) · [Demo](https://social-media-dashboardd.netlify.app/dashboard) |
| ✅ Analytics Dashboard | Charts, KPI cards, data visualization | [Guide](./docs/level-2/analytics-dashboard.md) | [Code](https://github.com/Serkanbyx/analytics-dashboard) · [Demo](https://analytics-dashboardd.netlify.app/login) |

## Level 3 — Backend Fundamentals

Node.js, Express, and databases (MongoDB / PostgreSQL). REST design, authentication,
middleware, queues. This is where you become a backend developer.

**Skills you'll gain:**

- Node.js + Express 5 server architecture with MVC pattern
- REST API design — proper status codes, consistent error shapes, CRUD conventions
- Authentication: JWT (stateless) and OAuth 2.0 with Passport.js (session-based)
- Databases: SQLite (raw SQL), MongoDB (Mongoose), PostgreSQL (Prisma ORM + migrations)
- Redis — caching (cache-aside pattern, TTL), distributed rate limiting, job queues
- Input validation with express-validator and Joi
- API documentation with Swagger (swagger-jsdoc + swagger-ui-express)
- File uploads with Multer + Cloudinary (multipart handling, MIME validation)
- Transactional email with Nodemailer (SMTP, templates, bulk delivery)
- Background jobs with BullMQ — producer/worker pattern, retry/backoff, Bull Board monitoring
- Real-time communication with Socket.io — rooms, typing indicators, online presence
- Security hardening — Helmet, rate limiting (tiered + RFC headers), CORS, mongo-sanitize
- Scheduled automation with node-cron and structured logging with Winston
- Server-side pagination, full-text search, dynamic filtering & aggregation

<p align="center">
  <a href="https://authentication-api-3bfr.onrender.com/"><img src="./assets/screenshots/level-3/authentication-api.png" width="19%" alt="Authentication API" /></a>
  <a href="https://crud-user-api-slmp.onrender.com/"><img src="./assets/screenshots/level-3/crud-user-api.png" width="19%" alt="CRUD User API" /></a>
  <a href="https://restful-to-do-api.onrender.com/"><img src="./assets/screenshots/level-3/restful-todo-api.png" width="19%" alt="RESTful To-Do API" /></a>
  <a href="https://notes-api-7mai.onrender.com/"><img src="./assets/screenshots/level-3/notes-api.png" width="19%" alt="Notes API" /></a>
  <a href="https://contact-form-api-woaf.onrender.com/"><img src="./assets/screenshots/level-3/contact-form-api.png" width="19%" alt="Contact Form API" /></a>
</p>
<p align="center">
  <a href="https://url-shortener-xzz2.onrender.com/"><img src="./assets/screenshots/level-3/url-shortener.png" width="19%" alt="URL Shortener" /></a>
  <a href="https://weather-proxy-api-yrc5.onrender.com/"><img src="./assets/screenshots/level-3/weather-proxy-api.png" width="19%" alt="Weather Proxy API" /></a>
  <a href="https://pagination-search-api.onrender.com/"><img src="./assets/screenshots/level-3/pagination-search-api.png" width="19%" alt="Pagination & Search API" /></a>
  <a href="https://mcq-quiz-api.onrender.com/"><img src="./assets/screenshots/level-3/mcq-quiz-api.png" width="19%" alt="MCQ Quiz API" /></a>
  <a href="https://file-upload-api-bnql.onrender.com/"><img src="./assets/screenshots/level-3/file-upload-api.png" width="19%" alt="File Upload API" /></a>
</p>
<p align="center">
  <a href="https://newsletter-system-6hvv.onrender.com/"><img src="./assets/screenshots/level-3/newsletter-system.png" width="19%" alt="Newsletter System" /></a>
  <a href="https://currency-converter-api-9rfm.onrender.com/"><img src="./assets/screenshots/level-3/currency-converter-api.png" width="19%" alt="Currency Converter API" /></a>
  <a href="https://rate-limiter-api-p1y1.onrender.com/api-docs/"><img src="./assets/screenshots/level-3/rate-limiter-api.png" width="19%" alt="Rate Limiter API" /></a>
  <a href="https://expense-tracker-backend-wwyp.onrender.com/"><img src="./assets/screenshots/level-3/expense-tracker-backend.png" width="19%" alt="Expense Tracker Backend" /></a>
  <a href="https://job-queue-f62a.onrender.com/"><img src="./assets/screenshots/level-3/job-queue.png" width="19%" alt="Job Queue" /></a>
</p>
<p align="center">
  <a href="https://oauth-login-backend-fxh8.onrender.com/"><img src="./assets/screenshots/level-3/oauth-login.png" width="19%" alt="OAuth Login" /></a>
  <a href="https://chat-app-backend-zww3.onrender.com/"><img src="./assets/screenshots/level-3/chat-app-backend.png" width="19%" alt="Chat App Backend" /></a>
</p>

| Project | What you'll build | Guide | Links |
|---------|-------------------|-------|-------|
| ✅ Authentication API | JWT/sessions, password hashing, protected routes | [Guide](./docs/level-3/authentication-api.md) | [Code](https://github.com/Serkanbyx/authentication-api) · [Demo](https://authentication-api-3bfr.onrender.com/) |
| ✅ CRUD User API | REST design, controllers, DB models | [Guide](./docs/level-3/crud-user-api.md) | [Code](https://github.com/Serkanbyx/crud-user-api) · [Demo](https://crud-user-api-slmp.onrender.com/) |
| ✅ RESTful To-Do API | Resource modeling, status codes, validation | [Guide](./docs/level-3/restful-to-do-api.md) | [Code](https://github.com/Serkanbyx/restful-to-do-api) · [Demo](https://restful-to-do-api.onrender.com/) |
| ✅ Notes API (Auth) | Auth middleware, user-scoped data | [Guide](./docs/level-3/notes-api.md) | [Code](https://github.com/Serkanbyx/notes-api) · [Demo](https://notes-api-7mai.onrender.com/) |
| ✅ Contact Form API | Email sending (Nodemailer) + DB storage | [Guide](./docs/level-3/contact-form-api.md) | [Code](https://github.com/Serkanbyx/contact-form-api) · [Demo](https://contact-form-api-woaf.onrender.com/) |
| ✅ URL Shortener | Hashing, redirects, click tracking | [Guide](./docs/level-3/url-shortener.md) | [Code](https://github.com/Serkanbyx/url-shortener-api) · [Demo](https://url-shortener-xzz2.onrender.com/) |
| ✅ Weather Proxy API | Hiding API keys, caching, proxying | [Guide](./docs/level-3/weather-proxy-api.md) | [Code](https://github.com/Serkanbyx/weather-proxy-api) · [Demo](https://weather-proxy-api-yrc5.onrender.com/) |
| ✅ Pagination + Search API | Query params, indexing, filtering | [Guide](./docs/level-3/pagination-search-api.md) | [Code](https://github.com/Serkanbyx/pagination-search-api) · [Demo](https://pagination-search-api.onrender.com/) |
| ✅ MCQ/Quiz API | Nested data, scoring logic | [Guide](./docs/level-3/mcq-quiz-api.md) | [Code](https://github.com/Serkanbyx/mcq-quiz-api) · [Demo](https://mcq-quiz-api.onrender.com/) |
| ✅ File Upload API | Multipart handling with Multer, validation | [Guide](./docs/level-3/file-upload-api.md) | [Code](https://github.com/Serkanbyx/file-upload-api) · [Demo](https://file-upload-api-bnql.onrender.com/) |
| ✅ Newsletter System | Subscriptions, scheduled sends, templates | [Guide](./docs/level-3/newsletter-system.md) | [Code](https://github.com/Serkanbyx/newsletter-system) · [Demo](https://newsletter-system-6hvv.onrender.com/) |
| ✅ Currency Converter API | External API, caching, rate handling | [Guide](./docs/level-3/currency-converter-api.md) | [Code](https://github.com/Serkanbyx/currency-converter-api) · [Demo](https://currency-converter-api-9rfm.onrender.com/) |
| ✅ Rate Limiter API | Middleware, store-backed throttling | [Guide](./docs/level-3/rate-limiter-api.md) | [Code](https://github.com/Serkanbyx/rate-limiter-api) · [Demo](https://rate-limiter-api-p1y1.onrender.com/api-docs/) |
| ✅ Expense Tracker Backend | Aggregation, reports, user data | [Guide](./docs/level-3/expense-tracker-backend.md) | [Code](https://github.com/Serkanbyx/expense-tracker-backend) · [Demo](https://expense-tracker-backend-wwyp.onrender.com/) |
| ✅ Job Queue | Background jobs with BullMQ + Redis, retries | [Guide](./docs/level-3/job-queue.md) | [Code](https://github.com/Serkanbyx/job-queue-api) · [Demo](https://job-queue-f62a.onrender.com/) |
| ✅ OAuth Login | OAuth2 flow with Google/GitHub, Passport | [Guide](./docs/level-3/oauth-login.md) | [Code](https://github.com/Serkanbyx/oauth-login-backend) · [Demo](https://oauth-login-backend-fxh8.onrender.com/) |
| ✅ Chat App Backend | WebSockets with Socket.io, rooms, events | [Guide](./docs/level-3/chat-app-backend.md) | [Code](https://github.com/Serkanbyx/chat-app-backend) · [Demo](https://chat-app-backend-zww3.onrender.com/) |

## Level 4 — Fullstack MERN

MongoDB, Express, React, Node — end to end. This is the level that takes you from
**junior to mid-level**. By the end you can design, build, and ship a complete product.

**Skills you'll gain:**

- End-to-end MERN architecture — React ↔ Express ↔ MongoDB data flow
- Monorepo structure with shared TypeScript + Zod schemas for end-to-end type safety
- Role-based access control (RBAC) — multi-role dashboards with permission-gated UI
- Dual JWT strategy — access + refresh token rotation with Axios request queuing
- Real-time with Socket.io — dual REST + WebSocket, presence, typing, read receipts
- Rich text & code editing — React Quill, Markdown + syntax highlighting, Monaco Editor
- Real-time collaboration — Yjs CRDT for conflict-free concurrent editing
- Video engineering — FFmpeg HLS transcoding, adaptive streaming with HLS.js
- Animation polish — Framer Motion page transitions, scroll animations, stagger effects
- Cloudinary upload pipelines — images, resumes, videos with MIME validation
- Multi-tenancy — organization-scoped data, team invitations, subscription tiers
- Atomic database operations — `findOneAndUpdate` for concurrent-safe booking
- Content workflows — approval systems, state machines (6-state application pipeline)
- Automated testing — Jest + Supertest (API), Vitest + React Testing Library (UI)
- Deployment — Netlify + Render split, Docker on Fly.io, `render.yaml` configs

<p align="center">
  <a href="https://to-do-mernn.netlify.app/login"><img src="./assets/screenshots/level-4/todo-mern.png" width="19%" alt="To-Do MERN" /></a>
  <a href="https://notes-mernn.netlify.app/"><img src="./assets/screenshots/level-4/notes-mern.png" width="19%" alt="Notes MERN" /></a>
  <a href="https://simple-blog-mernn.netlify.app/"><img src="./assets/screenshots/level-4/simple-blog.png" width="19%" alt="Simple Blog MERN" /></a>
  <a href="https://weather-mern.netlify.app/"><img src="./assets/screenshots/level-4/weather-mern.png" width="19%" alt="Weather App" /></a>
  <a href="https://user-authentication-systemm.netlify.app/"><img src="./assets/screenshots/level-4/auth-system.png" width="19%" alt="Auth System" /></a>
</p>
<p align="center">
  <a href="https://expense-tracker-mernn.netlify.app/"><img src="./assets/screenshots/level-4/expense-tracker.png" width="19%" alt="Expense Tracker" /></a>
  <a href="https://blog-mernn.netlify.app/"><img src="./assets/screenshots/level-4/blog-mern.png" width="19%" alt="Blog MERN" /></a>
  <a href="https://recipe-mernn.netlify.app/"><img src="./assets/screenshots/level-4/recipe-mern.png" width="19%" alt="Recipe App" /></a>
  <a href="https://movie-databasee.netlify.app/"><img src="./assets/screenshots/level-4/movie-database.png" width="19%" alt="Movie Database" /></a>
  <a href="https://portfolio-with-admin-panel.netlify.app/"><img src="./assets/screenshots/level-4/portfolio-admin.png" width="19%" alt="Portfolio Admin" /></a>
</p>
<p align="center">
  <a href="https://event-booking-systemm.netlify.app/"><img src="./assets/screenshots/level-4/event-booking.png" width="19%" alt="Event Booking" /></a>
  <a href="https://job-board-with-company-user-dashboard.netlify.app/"><img src="./assets/screenshots/level-4/job-board.png" width="19%" alt="Job Board" /></a>
  <a href="https://chat-app-mernn.netlify.app/"><img src="./assets/screenshots/level-4/chat-app.png" width="19%" alt="Chat App" /></a>
  <a href="https://social-media-platformm.netlify.app/"><img src="./assets/screenshots/level-4/social-media.png" width="19%" alt="Social Media" /></a>
  <a href="https://lms-mernn.netlify.app/"><img src="./assets/screenshots/level-4/lms-mern.png" width="19%" alt="LMS" /></a>
</p>
<p align="center">
  <a href="https://video-streaming-platformm.netlify.app/"><img src="./assets/screenshots/level-4/video-streaming.png" width="19%" alt="Video Streaming" /></a>
  <a href="https://online-code-editorr.netlify.app/"><img src="./assets/screenshots/level-4/code-editor.png" width="19%" alt="Code Editor" /></a>
  <a href="https://saas-dashboard-template.netlify.app/"><img src="./assets/screenshots/level-4/saas-dashboard.png" width="19%" alt="SaaS Dashboard" /></a>
</p>

| Project | What you'll build | Guide | Links |
|---------|-------------------|-------|-------|
| ✅ To-Do MERN | Full CRUD across React + Express + Mongo | [Guide](./docs/level-4/to-do-mern.md) | [Code](https://github.com/Serkanbyx/to-do-mern) · [Demo](https://to-do-mernn.netlify.app/login) |
| ✅ Notes MERN | Auth + notes, fullstack data flow | [Guide](./docs/level-4/notes-mern.md) | [Code](https://github.com/Serkanbyx/notes-mern) · [Demo](https://notes-mernn.netlify.app/) |
| ✅ Simple Blog MERN | Posts, routing, fullstack rendering | [Guide](./docs/level-4/simple-blog-mern.md) | [Code](https://github.com/Serkanbyx/simple-blog-mern) · [Demo](https://simple-blog-mernn.netlify.app/) |
| ✅ Weather App with Login | Auth-gated API consumption | [Guide](./docs/level-4/weather-app-with-login.md) | [Code](https://github.com/Serkanbyx/weather-app-with-login) · [Demo](https://weather-mern.netlify.app/) |
| ✅ User Authentication System | JWT + bcrypt, refresh tokens, protected UI | [Guide](./docs/level-4/user-authentication-system.md) | [Code](https://github.com/Serkanbyx/user-authentication-system) · [Demo](https://user-authentication-systemm.netlify.app/) |
| ✅ Expense Tracker | Mongo aggregation + chart visualization | [Guide](./docs/level-4/expense-tracker-mern.md) | [Code](https://github.com/Serkanbyx/expense-tracker-mern) · [Demo](https://expense-tracker-mernn.netlify.app/) |
| ✅ Blog with Comments & Likes | Relations, nested resources, optimistic UI | [Guide](./docs/level-4/blog-mern.md) | [Code](https://github.com/Serkanbyx/blog-mern) · [Demo](https://blog-mernn.netlify.app/) |
| ✅ Recipe App MERN | CRUD + search + favorites, fullstack | [Guide](./docs/level-4/recipe-mern.md) | [Code](https://github.com/Serkanbyx/recipe-mern) · [Demo](https://recipe-mernn.netlify.app/) |
| ✅ Movie Database | External API + user-saved favorites | [Guide](./docs/level-4/movie-database.md) | [Code](https://github.com/Serkanbyx/movie-database) · [Demo](https://movie-databasee.netlify.app/) |
| ✅ Portfolio w/ Admin Panel | Public site + protected CMS | [Guide](./docs/level-4/portfolio-with-admin-panel.md) | [Code](https://github.com/Serkanbyx/portfolio-with-admin-panel) · [Demo](https://portfolio-with-admin-panel.netlify.app/) |
| ✅ Event Booking System | Bookings, availability, email confirmations | [Guide](./docs/level-4/event-booking-system.md) | [Code](https://github.com/Serkanbyx/event-booking-system) · [Demo](https://event-booking-systemm.netlify.app/) |
| ✅ Job Board | Multi-role dashboards, applications | [Guide](./docs/level-4/job-board.md) | [Code](https://github.com/Serkanbyx/job-board-with-company-user-dashboard) · [Demo](https://job-board-with-company-user-dashboard.netlify.app/) |
| ✅ Chat App | Realtime messaging + notification system | [Guide](./docs/level-4/chat-app-mern.md) | [Code](https://github.com/Serkanbyx/chat-app-mern) · [Demo](https://chat-app-mernn.netlify.app/) |
| ✅ Social Media Platform | Follow graph, feed, notifications | [Guide](./docs/level-4/social-media-platform.md) | [Code](https://github.com/Serkanbyx/social-media-platform) · [Demo](https://social-media-platformm.netlify.app/) |
| ✅ LMS | Courses, quizzes, progress tracking, roles | [Guide](./docs/level-4/lms.md) | [Code](https://github.com/Serkanbyx/lms-mern) · [Demo](https://lms-mernn.netlify.app/) |
| ✅ Video Streaming Platform | Upload, streaming, transcoding basics | [Guide](./docs/level-4/video-streaming-platform.md) | [Code](https://github.com/Serkanbyx/video-streaming-platform) · [Demo](https://video-streaming-platformm.netlify.app/) |
| ✅ Online Code Editor | Monaco editor + realtime collaboration | [Guide](./docs/level-4/online-code-editor.md) | [Code](https://github.com/Serkanbyx/online-code-editor) · [Demo](https://online-code-editorr.netlify.app/) |
| ✅ SaaS Dashboard Template | Multi-tenant patterns, billing-ready UI | [Guide](./docs/level-4/saas-dashboard-template.md) | [Code](https://github.com/Serkanbyx/saas-dashboard-template) · [Demo](https://saas-dashboard-template.netlify.app/) |

## Level 5 — Senior-Level Systems

Distributed systems, real-time architecture, AI/ML integration, security, and blockchain.
These projects are about **architectural reasoning** — the kind of work that ends the
"junior" conversation for good.

**Skills you'll gain:**

- Authoritative server architecture — server validates all state changes, clients send intentions
- Dual WebSocket channels — separate device ingest and dashboard streams for independent scaling
- Hybrid storage — Redis for real-time state + PostgreSQL for persistent data
- PostGIS geospatial queries — spatial indexes, polygon containment, distance calculations
- NestJS modular backend with TypeORM and Drizzle ORM
- Real-time map visualization — MapLibre GL with smooth marker interpolation
- Matchmaking and ride-matching — Redis-backed queues, geospatial pairing, dynamic pricing
- Reconnection resilience — grace periods with state recovery from Redis
- Geofencing — boundary detection, enter/exit events, spatial alerting
- IoT data pipelines — MQTT protocol, device telemetry ingestion, time-series storage
- AI/ML integration — LLM context windows, streaming responses, collaborative filtering, embeddings
- Computer vision & audio — face detection model integration, speech-to-text transcription APIs
- Metrics & observability — Sentry, structured logging (Pino), alerting dashboards, uptime monitoring
- Financial security — transaction isolation, audit logging, ACID compliance, fraud prevention
- Blockchain fundamentals — smart contracts, immutable ledgers, cryptographic verification
- Networking concepts — tunneling logic, encryption layers, VPN protocol simulation
- TypeScript monorepo with shared types for compile-time event safety

<p align="center">
  <a href="https://multiplayer-game-backend-nu.vercel.app"><img src="./assets/screenshots/level-5/multiplayer-game.png" width="30%" alt="Multiplayer Game Backend" /></a>
  <a href="https://vehicle-tracking-system-lemon.vercel.app"><img src="./assets/screenshots/level-5/vehicle-tracking.png" width="30%" alt="Vehicle Tracking System" /></a>
  <a href="https://iot-dashboard-one-rouge.vercel.app/"><img src="./assets/screenshots/level-5/iot-dashboard.png" width="30%" alt="IoT Dashboard" /></a>
</p>

| Project | What you'll build | Guide | Links |
|---------|-------------------|-------|-------|
| ✅ Multiplayer Game Backend | Authoritative server, state sync, latency handling | [Guide](./docs/level-5/multiplayer-game-backend.md) | [Code](https://github.com/Serkanbyx/multiplayer-game-backend) · [Demo](https://multiplayer-game-backend-nu.vercel.app) |
| ✅ Vehicle Tracking System | Real-time GPS streams, geofencing | [Guide](./docs/level-5/vehicle-tracking-system.md) | [Code](https://github.com/Serkanbyx/vehicle-tracking-system) · [Demo](https://vehicle-tracking-system-lemon.vercel.app) |
| ✅ IoT Dashboard | Device telemetry, MQTT, time-series data | [Guide](./docs/level-5/iot-dashboard.md) | [Code](https://github.com/Serkanbyx/iot-dashboard) · [Demo](https://iot-dashboard-one-rouge.vercel.app/) |
| 🚧 Ride-Sharing Backend | Matching, geospatial queries, pricing | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Remote Monitoring System | Metrics ingestion, alerting, dashboards | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 AI-Powered Chatbot | LLM integration, context windows, streaming | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Content Recommendation System | Collaborative filtering, embeddings | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Face Detection App | Computer vision, model integration | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Speech Recognition App | Audio processing, transcription APIs | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 VPN Simulation | Networking concepts, tunneling logic | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Online Banking System | Transactions, security, audit logging | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Blockchain Voting System | Smart contracts, immutability, verification | [Guide](#) | [Code](#) · [Demo](#) |
| 🚧 Crypto Exchange (frontend) | Order book UI, real-time price feeds | [Guide](#) | [Code](#) · [Demo](#) |

---

## Repository structure

```
junior-to-senior-web-projects/
├── README.md            ← you are here
├── CONTRIBUTING.md       ← how to add your own project
├── assets/
│   └── banner.svg
└── docs/
    ├── TEMPLATE.md       ← copy this for every new project guide
    ├── PROGRESS.md        ← fork & track your progress
    ├── find-your-level.md ← self-assessment quiz
    ├── level-1/ … level-5/
    │   └── <project>.md  ← one short build guide per project
```

Each guide follows the same shape: **purpose → tech stack → numbered build steps →
deployment → tips → README guidance.** Copy [`docs/TEMPLATE.md`](./docs/TEMPLATE.md) to start a new one.

## Contributing

This roadmap is meant to grow. If you've built one of these projects — or have a better
project idea for a level — open a PR. See [CONTRIBUTING.md](./CONTRIBUTING.md).

## Author

Built and maintained by **Serkan** — [GitHub](https://github.com/Serkanbyx)

If this roadmap helped you, a ⭐ helps other developers find it.

[![Share on X](https://img.shields.io/badge/Share_on-X-000000?style=flat-square&logo=x)](https://twitter.com/intent/tweet?text=A%20structured%2C%205-level%20roadmap%20of%2070%2B%20real-world%20web%20projects%20%E2%80%94%20from%20JS%20basics%20to%20senior-level%20systems.%20Build%20guides%2C%20source%20code%2C%20and%20live%20demos%20included.&url=https%3A%2F%2Fgithub.com%2FSerkanbyx%2Fjunior-to-senior-web-projects-roadmap) [![Share on Reddit](https://img.shields.io/badge/Share_on-Reddit-FF4500?style=flat-square&logo=reddit&logoColor=white)](https://www.reddit.com/submit?url=https%3A%2F%2Fgithub.com%2FSerkanbyx%2Fjunior-to-senior-web-projects-roadmap&title=A%20structured%2C%205-level%20roadmap%20of%2070%2B%20real-world%20web%20projects%20%E2%80%94%20from%20JS%20basics%20to%20senior-level%20systems)

## License

Released under the [MIT License](./LICENSE). Use it, fork it, learn from it.
