# Recipe App MERN

> A fullstack recipe sharing platform with user authentication, CRUD operations, favorites, and admin dashboard.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://recipe-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/recipe-mern)

---

## Purpose

This project teaches full CRUD with rich, structured content. Recipes have ingredients
lists, step-by-step instructions, images, and metadata. Combined with a favorites system
and admin dashboard, it demonstrates building a content platform where users both create
and consume content — the pattern behind every recipe site, blog platform, and social app.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, React Hook Form
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT + bcryptjs
- **Image uploads:** Cloudinary 2
- **Email:** Nodemailer
- **Validation:** express-validator
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize
- **UX:** React Icons, React Hot Toast, dark mode
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the recipe model.** Schema: `{ title, description, ingredients: [{ name, amount, unit }], instructions: [String], cookTime, servings, category, image, author, favorites: [userId], createdAt }`. Rich nested data with arrays of objects.

2. **Build recipe CRUD API.** Create (with Cloudinary image upload), read (list with pagination + search + category filter), update (author only), delete (author only). Public read access, auth-required write access. express-validator on all inputs.

3. **Implement the favorites system.** Toggle endpoint: `POST /recipes/:id/favorite`. If user already favorited, remove; otherwise add. User's favorites page shows all saved recipes. Favorites count displayed on each recipe card.

4. **Build the recipe form.** Multi-section form with React Hook Form: basic info (title, description, time, servings), dynamic ingredient rows (add/remove with proper validation), ordered instructions (add/remove/reorder steps), image upload with preview, and category selector.

5. **Build the public recipe grid.** Responsive card grid with recipe image, title, cook time, servings, and favorites count. Click to view full recipe detail: hero image, ingredient checklist, numbered instructions, and author info.

6. **Build the admin dashboard.** View platform stats, manage all recipes (edit/delete any), manage users. Admin can feature recipes on the homepage. Separate from regular user's "My Recipes" section.

7. **Add search, filtering, and dark mode.** Search by title/description. Filter by category (breakfast, lunch, dinner, dessert, snack). Sort by newest or most favorited. Dark mode toggle with persistent preference.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `CLOUDINARY_*`, `SMTP_*`. Frontend on
Netlify with `VITE_API_URL`.

## Tips

- Dynamic form fields (add/remove ingredient rows) are cleanest with React Hook Form's `useFieldArray`. Each ingredient is an object `{ name, amount, unit }` — structured data enables features like auto-generating shopping lists later.
- The favorites toggle pattern: one endpoint handles both add and remove. Check if the userId exists in the array — if yes, `$pull`; if no, `$addToSet`. Atomic, idempotent, and simple.
- Extension: add nutritional info calculation, meal planning, social sharing with recipe cards, or a "cook mode" with step-by-step timer.

## README Guidance

The project repo's README should include a description, screenshots of recipe grid and
detail page, tech stack, environment variables, and setup instructions.
