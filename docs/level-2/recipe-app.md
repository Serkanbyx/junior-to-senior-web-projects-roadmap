# Recipe App

> A PWA-enabled recipe discovery app with search, cuisine filtering, Radix UI components, and secure API proxying via Netlify Functions.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://recipe-web-appp.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/recipe-web-app)

---

## Purpose

This project teaches you to consume a complex external API (Spoonacular), handle rich
structured data (ingredients, instructions, nutrition), and build accessible UI with Radix
components. The PWA capability means recipes are available offline — critical for a cooking
app where you might lose signal in the kitchen.

## Tech Stack

- **Framework:** React, TypeScript, Vite
- **Styling:** Tailwind CSS, class-variance-authority (CVA), clsx, tailwind-merge
- **State:** Zustand (favorites, search history)
- **UI Components:** Radix UI (dialog, label, tabs)
- **Forms:** React Hook Form + Zod validation
- **Security:** DOMPurify (XSS protection for API HTML content)
- **API proxy:** Netlify Functions (hides Spoonacular API key)
- **PWA:** vite-plugin-pwa + Workbox
- **HTTP:** Axios
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Set up Spoonacular API proxy.** Netlify Function proxies recipe search and detail requests. Transform the verbose API response into a cleaner shape.

2. **Build the search and filter UI.** Search by keyword, filter by cuisine (Italian, Mexican, Asian, etc.) using Radix UI tabs. Display results in a responsive card grid with recipe image, title, and cook time.

3. **Build the recipe detail view.** Radix Dialog for modal-based recipe detail: ingredients checklist, step-by-step instructions, nutritional info. DOMPurify sanitizes any HTML from the API to prevent XSS.

4. **Implement favorites with Zustand.** Save recipes to favorites (persisted). Offline-friendly: store enough data to render favorites without re-fetching.

5. **Style with CVA pattern.** class-variance-authority creates reusable component variants (button sizes, card styles). Combined with Tailwind, this produces a consistent, maintainable design system.

6. **Add PWA support.** Offline recipe viewing, installable on mobile, cached API responses for previously viewed recipes.

7. **Deploy with Netlify Functions.** Static site + serverless proxy in one deployment. API key hidden server-side.

## Tips

- DOMPurify is essential when rendering HTML from external APIs. Spoonacular returns HTML in instructions — without sanitization, XSS attacks could execute in your app.
- CVA (class-variance-authority) solves the "which Tailwind classes for this variant?" problem. Define variants once: `cva('base-classes', { variants: { size: { sm: '...', lg: '...' } } })`.
- Extension: add meal planning, shopping list generation, nutritional comparison, or recipe scaling (adjust servings).
