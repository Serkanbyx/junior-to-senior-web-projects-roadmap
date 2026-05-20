# E-commerce Frontend

> A fully responsive e-commerce frontend with product catalog, Redux Toolkit cart, Headless UI components, and checkout flow with validation.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://e-commerce-frontendd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/e-commerce-frontend)

---

## Purpose

E-commerce is the ultimate frontend challenge: product grids with filtering, a cart that
persists across pages, a multi-step checkout, and accessible interactive elements (modals,
dropdowns). This project uses Redux Toolkit for cart state (shared across many components)
and Headless UI for accessible components.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS, tailwind-merge, clsx
- **State:** Redux Toolkit (cart, filters, wishlist)
- **Routing:** React Router
- **UI Components:** Headless UI (accessible dropdowns, modals, transitions)
- **Forms:** React Hook Form + Zod (checkout form)
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Set up Redux store with cart slice.** Cart items: `{ product, quantity }`. Actions: addToCart, removeFromCart, updateQuantity, clearCart. Selectors: cartTotal, cartItemCount. Persist to localStorage.

2. **Build the product catalog.** Grid of product cards with image, title, price, and "Add to Cart" button. Responsive grid (1-4 columns based on viewport).

3. **Implement filtering and pagination.** Filter by category, price range, and rating. Sort by price, newest, or popularity. Client-side pagination or infinite scroll. Filters combine with AND logic.

4. **Build the shopping cart.** Slide-over panel (Headless UI Transition) showing cart items. Quantity adjust (+/-), remove item, subtotal per item, grand total. Persistent across page navigation via Redux.

5. **Build accessible components with Headless UI.** Dropdown menus for sort options, Dialog for quick product view, Transition for smooth animations. All fully keyboard navigable and screen-reader friendly.

6. **Build the checkout flow.** Multi-step form: shipping address → payment details → order review. React Hook Form + Zod validates each step. Show order summary. Simulated "Place Order" (no real payment).

7. **Deploy on Netlify.** Static site with mock product data (JSON). No backend needed.

## Tips

- Headless UI gives you accessible behavior (keyboard nav, focus management, ARIA) with zero styling. You add all visual design with Tailwind — full control over appearance with guaranteed accessibility.
- Redux Toolkit for cart makes sense because cart state is accessed from: product cards (add button), header (count badge), cart drawer (full list), and checkout (summary). Many components need the same state.
- Extension: add product reviews, recently viewed, size/color variants, wishlist, or a product comparison feature.
