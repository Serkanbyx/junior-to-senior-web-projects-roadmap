# E-commerce Frontend

> A product catalog with filtering, pagination, shopping cart with Redux, and a multi-step checkout flow.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://e-commerce-frontendd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/e-commerce-frontend)

---

## Purpose

This is the project that proves you can build a real product page. It combines the filtering
and sorting patterns from earlier projects with cart state management and a multi-step checkout
form. You'll learn to manage complex derived state (cart totals, item counts, filtered products)
and handle the most common e-commerce UX patterns — add to cart, quantity update, and form
validation across multiple steps.

## Tech Stack

- **Frontend:** React 18, TypeScript, Tailwind CSS, Vite
- **Backend:** none (mock product data)
- **Database:** none (cart state in Redux)
- **Key libraries / tools:** Redux Toolkit (cart state), React Router (pages)
- **Deployment:** Netlify

## Build Steps

1. **Create product data.** Define a product type: `{ id, name, price, image, category, rating, description, stock }`. Create a JSON file with 20+ products across categories (electronics, clothing, accessories). This simulates an API response.
2. **Build the product catalog.** A responsive grid of product cards with image, name, price, rating stars, and "add to cart" button. Implement pagination (12 per page) or infinite scroll. Show the total product count.
3. **Add filtering and sorting.** Category filter (multi-select), price range slider, rating filter (minimum stars), and sort (price low-high, price high-low, rating, name). Compose filters so they stack — all active filters apply simultaneously.
4. **Set up the cart with Redux.** Create a Redux slice for the cart: `items: { product, quantity }[]`. Actions: addToCart, removeFromCart, updateQuantity, clearCart. Derive computed values: totalItems, subtotal, tax, grandTotal. Show a cart icon with badge count in the header.
5. **Build the cart page.** List all cart items with image, name, quantity controls (+/-), line total, and remove button. Show order summary: subtotal, shipping, tax, total. Handle empty cart state with a "continue shopping" link.
6. **Implement checkout flow.** A multi-step form: shipping address → payment details → order review → confirmation. Use controlled inputs with validation at each step. Show a progress indicator. On "place order", show a success page and clear the cart.
7. **Add product detail page.** Clicking a product card navigates to a detail page with full description, multiple images, size/color selectors, quantity input, and related products.

## Deployment

Deploy on Netlify with Vite's build output. No environment variables needed since all data
is local. React Router requires a `_redirects` file (`/* /index.html 200`) for client-side routing.

## Tips

- Redux Toolkit's `createSlice` makes cart management trivial — the `addToCart` action can handle both "add new item" and "increment existing item" in one reducer with an `if` check.
- Multi-step forms are cleaner when each step is its own component with local validation, and a parent component manages which step is active and stores the accumulated data.
- Extension: add product search with debounce, wishlist functionality, or integrate with Stripe for real payments (in test mode).

## README Guidance

The project repo's README should include a short description, screenshots of the product grid
and cart/checkout, the live demo link, tech stack, features list, and local dev instructions.
