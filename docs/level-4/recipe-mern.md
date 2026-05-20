# Recipe App MERN

> A fullstack recipe app with CRUD, search, favorites, and user-generated content.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://recipe-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/recipe-mern)

---

## Purpose

Unlike the Level 2 recipe app (which consumed an external API), this one stores user-created
recipes in your own database. It teaches full CRUD with rich content (ingredients lists,
step-by-step instructions, images), search across your own data, and the favorites pattern
where users save other users' content — a many-to-many relationship.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT
- **Key libraries / tools:** Mongoose, Multer (image upload), Axios, React Router
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Model the recipe.** Schema: `{ title, description, ingredients: [{ name, amount, unit }], steps: [String], cookTime, servings, category, image, author: ObjectId, favorites: [userId] }`. Rich nested data with arrays of objects.
2. **Build CRUD API.** Create recipe (with image upload via Multer), read (list with pagination + search), update (only by author), delete (only by author). Public read access, auth-required write access.
3. **Implement search and filtering.** Text search on title and description. Filter by category (breakfast, lunch, dinner, dessert). Sort by newest, most favorited, or cook time. Combine filters with pagination.
4. **Build the recipe form.** A multi-section form: basic info (title, description, time, servings), dynamic ingredient list (add/remove rows), ordered steps list (add/remove/reorder), image upload with preview, and category selector.
5. **Display recipes.** A grid of recipe cards (image, title, cook time, favorites count). A detail page with full recipe: hero image, ingredient checklist, numbered steps, and author info.
6. **Implement favorites.** A heart button on each recipe card and detail page. `POST /recipes/:id/favorite` toggles the user's ID in the favorites array. A "My Favorites" page showing all saved recipes.
7. **Add the "My Recipes" section.** A dashboard showing recipes created by the current user with edit/delete options. Show view count and favorites count as simple analytics.

## Deployment

Frontend on Netlify, backend on Render. For image uploads, use Cloudinary (set
`CLOUDINARY_URL`) or store on Render disk (ephemeral). Set standard env vars.

## Tips

- Dynamic form fields (add/remove ingredient rows) are cleanest with `useFieldArray` from React Hook Form, or a simple state array with add/remove handlers.
- For the ingredient list, use a compound object `{ name, amount, unit }` rather than a single string. Structured data enables features like auto-generating shopping lists later.
- Extension: add nutritional info calculation, meal planning, social sharing, or a "cook mode" with step-by-step timer.

## README Guidance

The project repo's README should include a description, screenshots of recipe grid and
detail page, tech stack, environment variables, and setup instructions.
