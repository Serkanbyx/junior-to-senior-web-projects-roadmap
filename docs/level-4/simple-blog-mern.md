# Simple Blog MERN

> A fullstack blog with post creation, routing, and server-rendered content from MongoDB.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://simple-blog-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/simple-blog-mern)

---

## Purpose

A blog is the classic fullstack project because it introduces public vs. private content,
rich text handling, and URL-based routing to specific resources. Unlike notes (private to one
user), blog posts are public — anyone can read them, but only the author can edit/delete.
This duality teaches you to design APIs with mixed access levels.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT (author-only write operations)
- **Key libraries / tools:** React Router, Axios, React Quill or similar rich text editor
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the data model.** Post schema: `{ title, slug, content (HTML), excerpt, author, coverImage, tags, published, createdAt, updatedAt }`. Generate slug from title for SEO-friendly URLs.
2. **Build public API routes.** `GET /posts` (list published posts, with pagination), `GET /posts/:slug` (single post by slug). These are unauthenticated — anyone can read.
3. **Build protected API routes.** `POST /posts`, `PATCH /posts/:id`, `DELETE /posts/:id` — all require auth. Verify the requesting user is the post author before allowing edit/delete.
4. **Create the public blog UI.** A homepage listing posts (title, excerpt, date, cover image) with pagination. A post detail page rendered from the slug route. Clean typography for reading.
5. **Build the author dashboard.** A protected area where the logged-in user can create, edit, and delete their posts. A rich text editor for content (React Quill or TipTap). Draft/published toggle.
6. **Implement slug-based routing.** Use React Router: `/posts/:slug` maps to the detail page. The frontend fetches the post by slug from the API. Handle 404 (post not found) gracefully.
7. **Add SEO basics.** Set page title and meta description dynamically based on the current post (using `document.title` or React Helmet). Generate an excerpt automatically from the first 160 characters of content.

## Deployment

Frontend on Netlify, backend on Render. Set `MONGODB_URI`, `JWT_SECRET` on Render.
Set `VITE_API_URL` on Netlify. Add a Netlify `_redirects` file for client-side routing.

## Tips

- Slugs should be unique and URL-safe. Generate with: `title.toLowerCase().replace(/[^a-z0-9]+/g, '-').replace(/(^-|-$)/g, '')`. Check for duplicates and append a number if needed.
- Rich text editors output HTML. Store it as-is in MongoDB and render with `dangerouslySetInnerHTML` — but sanitize it server-side (with DOMPurify or sanitize-html) to prevent XSS.
- Extension: add comments on posts, a category/tag system with filtered views, or an RSS feed endpoint.

## README Guidance

The project repo's README should include a description, screenshots of blog list and post
detail, tech stack, environment variables, and setup instructions for both client and server.
