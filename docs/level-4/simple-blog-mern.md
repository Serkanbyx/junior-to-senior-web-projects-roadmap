# Simple Blog MERN

> A fullstack blog with Markdown-powered content, role-based admin dashboard, Cloudinary image uploads, and category/tag filtering.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://simple-blog-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/simple-blog-mern)

---

## Purpose

A blog introduces public vs. private content and rich rendering. Unlike notes (private),
blog posts are public — anyone can read. The admin writes in Markdown, and the frontend
renders it beautifully with syntax-highlighted code blocks. This teaches you role-based
access, Markdown processing pipelines, SEO-friendly slugs, and image upload workflows.

## Tech Stack

- **Frontend:** React 19, Vite 8, Tailwind CSS 4, React Router 7
- **Backend:** Node.js 18+, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT (7-day expiry) + bcryptjs (12 rounds)
- **Markdown:** react-markdown 10, remark-gfm 4 (GFM support), react-syntax-highlighter 16
- **Image uploads:** Multer 2 + Cloudinary 2 (JPEG/PNG/WebP, 5MB limit)
- **Security:** Helmet 8, rate limiting (100/15min general, 20/15min auth), CORS whitelist
- **UX:** Axios, lazy loading (React.lazy + Suspense), debounced search, load-more pagination
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the post model.** Schema: `{ title, slug, content (Markdown), excerpt, coverImage, category, tags: [String], author, published, createdAt, updatedAt }`. Auto-generate the slug from the title on save. Add indexes for slug (unique) and tags.

2. **Build public API routes.** `GET /posts` (list published posts, paginated with load-more), `GET /posts/:slug` (single post by slug). These are unauthenticated. Support query params for category, tag, and search (debounced on the frontend).

3. **Build the admin API.** `POST /posts`, `PATCH /posts/:id`, `DELETE /posts/:id` — all require auth. Role-based: admin role is auto-assigned via `ADMIN_EMAIL` env var. Multer + Cloudinary pipeline for cover image uploads.

4. **Build the public blog UI.** A post list page with cover images, titles, excerpts, categories, and tags. A post detail page that renders Markdown content with `react-markdown`, GFM tables/task lists via `remark-gfm`, and syntax-highlighted code blocks via `react-syntax-highlighter`. Debounced search with instant results.

5. **Build the admin dashboard.** A protected area for creating and editing posts. Write content in raw Markdown (not a WYSIWYG editor). Cover image upload with preview. Category selector and tag input. Published/draft toggle. Post management table with edit and delete.

6. **Implement the category & tag system.** Predefined categories (dropdown select). Free-form tags (comma-separated input). Frontend filtering: click a category or tag to filter the post list. Backend query params support both.

7. **Add performance and SEO.** React.lazy + Suspense for route-level code splitting. Auto-generated excerpts from the first 160 characters of Markdown content (stripped). SEO-friendly slug URLs. Load-more pagination (not offset-based) for the feed. Health check endpoint for monitoring.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `CLOUDINARY_*`, `ADMIN_EMAIL`.
Frontend on Netlify with `VITE_API_URL`. Add a Netlify `_redirects` for SPA routing.

## Tips

- Markdown content is stored as plain text in the database. Rendering happens entirely on the frontend with `react-markdown`. This means the backend is simple (just store/retrieve strings) while the frontend handles all presentation.
- The `ADMIN_EMAIL` pattern for role assignment is elegant for single-author blogs: whoever registers with that email automatically becomes admin. No seed scripts needed.
- Extension: add comments, reading time estimation, related posts algorithm, or an RSS feed endpoint.

## README Guidance

The project repo's README should include a description, screenshots of blog feed and
Markdown-rendered post, tech stack, environment variables, and setup instructions.
