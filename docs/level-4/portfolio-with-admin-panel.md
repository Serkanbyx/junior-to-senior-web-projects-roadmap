# Portfolio with Admin Panel

> A modern portfolio site with CMS-like admin panel, Cloudinary uploads, contact form with email notifications, glassmorphism theme, and Framer Motion scroll animations.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://portfolio-with-admin-panel.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/portfolio-with-admin-panel)

---

## Purpose

This project teaches the public/private split: a beautiful public-facing portfolio that
anyone can view, powered by a protected admin panel where you manage all content dynamically.
No hardcoded data — everything comes from the database via the admin CMS. This pattern
applies to any content-managed site where you need to update content without redeploying code.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, React Hook Form
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT + bcryptjs
- **Animation:** Framer Motion 12 (scroll-triggered animations)
- **Image uploads:** Cloudinary 2
- **Email:** Nodemailer (contact form notifications)
- **Validation:** express-validator
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize, cookie-parser
- **UX:** React Icons, glassmorphism dark theme
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the content models.** Project: `{ title, description, image, techStack, liveUrl, githubUrl, featured, order }`. Skill: `{ name, level, category }`. About: `{ bio, avatar, socialLinks }`. All manageable from admin.

2. **Build the public API.** Unauthenticated endpoints: `GET /portfolio/projects`, `GET /portfolio/skills`, `GET /portfolio/about`. Return data sorted by `order` field. These power the public site — no auth required to view.

3. **Build the admin CRUD API.** Authenticated endpoints for managing all content. Only the admin user can create, update, delete, and reorder. Cloudinary pipeline for project screenshots and avatar. Single admin account (seeded or first-register pattern).

4. **Build the public portfolio.** A polished single-page portfolio: hero section with Framer Motion entrance, about section, projects grid (with live/GitHub links), skills section, and contact form. Glassmorphism design with backdrop-blur and translucent panels.

5. **Implement Framer Motion scroll animations.** Elements animate in as the user scrolls: fade-up for text, scale-in for project cards, stagger for skill badges. Use `useInView` hook with `whileInView` prop for scroll-triggered animations. Smooth and performant.

6. **Build the admin panel.** A protected dashboard for managing projects (CRUD + image upload + reorder), skills (add/remove/categorize), and about info (edit bio, avatar, social links). Simple, functional forms focused on content management speed.

7. **Build the contact form.** Public contact form on the portfolio. On submit, the backend sends an email notification via Nodemailer and stores the message in MongoDB. Rate limit the endpoint to prevent spam.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `CLOUDINARY_*`, `SMTP_*`. Frontend on
Netlify with `VITE_API_URL`. Seed an admin account on first deploy.

## Tips

- Glassmorphism: `backdrop-filter: blur(10px)` + semi-transparent background + subtle border. Looks stunning but ensure text contrast meets WCAG standards — add a darker overlay if needed.
- Framer Motion's `whileInView` with `viewport={{ once: true }}` ensures animations play once on scroll. Without `once: true`, elements re-animate every time they enter/exit the viewport.
- Extension: add a blog section with Markdown, page view analytics per project, multiple themes, or a resume PDF generator from the about data.

## README Guidance

The project repo's README should include a description, screenshots of both the public
portfolio and admin panel, tech stack, environment variables, and setup instructions.
