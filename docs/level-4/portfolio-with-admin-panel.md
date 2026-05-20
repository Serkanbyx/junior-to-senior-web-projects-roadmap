# Portfolio with Admin Panel

> A public portfolio site with a protected admin CMS for managing projects, skills, and content.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://portfolio-with-admin-panel.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/portfolio-with-admin-panel)

---

## Purpose

This project teaches the public/private split: a beautiful public-facing site that anyone can
view, powered by a protected admin panel where you manage all content. It's essentially a
headless CMS you build yourself. The pattern applies to any content-managed website — company
sites, landing pages, blogs — where non-developers need to update content.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT (admin-only access)
- **Key libraries / tools:** React Router, Axios, Multer (image uploads)
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the content models.** Project: `{ title, description, image, techStack, liveUrl, githubUrl, featured, order }`. Skill: `{ name, level, category }`. About: `{ bio, avatar, resume, socialLinks }`. All manageable from the admin.
2. **Build the public API.** Unauthenticated endpoints: `GET /portfolio/projects`, `GET /portfolio/skills`, `GET /portfolio/about`. These serve the public site. Return data sorted by the `order` field.
3. **Build the admin API.** Authenticated CRUD for all content types. Only the admin user can create, update, delete, and reorder items. A single admin account (seeded or registered once).
4. **Build the public portfolio site.** A polished, responsive portfolio: hero section, about, projects grid, skills section, and contact form. All content fetched from the API — nothing hardcoded.
5. **Build the admin panel.** A protected dashboard with sections for managing projects, skills, and about info. CRUD forms with image upload. Drag-and-drop reordering for projects. Live preview of changes.
6. **Implement image management.** Upload project screenshots and avatar via Multer. Store in Cloudinary or on disk. Show image previews in the admin forms. Handle image replacement on update.
7. **Add a contact form.** Public contact form that sends messages to the admin's email (via Nodemailer) and stores them in the database. An "Inbox" section in the admin panel to review messages.

## Deployment

Frontend on Netlify, backend on Render. Seed an admin account on first deploy. Set
`MONGODB_URI`, `JWT_SECRET`, `SMTP_*` credentials, and `VITE_API_URL`.

## Tips

- The public site should be blazing fast. Consider fetching data at build time (SSG with a rebuild webhook) rather than on every page load — but for this project, client-side fetching is fine as a learning exercise.
- Keep the admin panel simple and functional — it's a tool for you, not a product for users. Focus on correctness and speed of content management over visual polish.
- Extension: add a blog section with Markdown editor, analytics (page views per project), or a theme switcher for the public site.

## README Guidance

The project repo's README should include a description, screenshots of both the public site
and admin panel, tech stack, environment variables, and setup instructions.
