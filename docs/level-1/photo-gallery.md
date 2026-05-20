# Photo Gallery

> A responsive photo gallery with masonry grid, lightbox modal, keyboard/touch navigation, category filtering, and lazy loading.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://photo-galleryyyyy.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/photo-gallery)

---

## Purpose

This project is about layout and performance. You'll learn CSS Grid in a real context (masonry
layout), implement a modal overlay system from scratch, handle keyboard and touch navigation,
and tackle image performance with lazy loading. It's the project that proves you can build
a polished, accessible media experience without reaching for a library.

## Tech Stack

- **Frontend:** HTML5, CSS3 Grid, vanilla JavaScript (ES6+)
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** Intersection Observer API (lazy loading), CSS Grid (masonry), no external dependencies
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Structure the image data.** Create an array of image objects: `{ src, thumbnail, alt, category }`. Keep images in an `assets/` folder or use placeholder URLs. Categorize them (nature, architecture, people, etc.).
2. **Build the masonry grid.** Use CSS Grid with `grid-template-columns: repeat(auto-fill, minmax(250px, 1fr))` and varying `grid-row-end` spans to create the masonry effect. Alternatively, use CSS `columns` for a simpler approach. The grid must be responsive — no fixed breakpoints.
3. **Implement lazy loading.** Use the Intersection Observer API to load images only when they scroll into view. Start with a tiny placeholder or blurred thumbnail, then swap in the full image when observed. This dramatically improves initial page load on image-heavy pages.
4. **Add category filtering.** Render filter buttons from the unique categories in your data. On click, hide/show images by toggling a CSS class or re-rendering only matching items. Add a smooth CSS transition for the show/hide so it doesn't feel jarring.
5. **Build the lightbox modal.** On image click, open a full-screen overlay showing the image at full resolution. Include close (X button + click outside + Escape key), previous/next navigation arrows, and the image caption.
6. **Handle keyboard and touch navigation.** In the lightbox: Left/Right arrows cycle images, Escape closes. On mobile: detect swipe gestures (track `touchstart` and `touchend` X coordinates) for previous/next. Trap focus inside the modal for accessibility.
7. **Ensure accessibility.** Every image has a meaningful `alt` attribute. The lightbox traps focus and returns it on close. Buttons have ARIA labels. The gallery is navigable by keyboard alone.

## Deployment

Push to GitHub and deploy on Netlify. Optimize images before committing — use WebP format
or compress JPEGs. Large unoptimized images will make the repo bloated and the site slow
despite lazy loading.

## Tips

- The Intersection Observer is far better than scroll-event-based lazy loading — it's performant, non-blocking, and requires zero throttling logic.
- For the masonry effect, the simplest pure-CSS approach is `columns: 3` on the container — but it orders items top-to-bottom per column rather than left-to-right. CSS Grid with JavaScript-calculated row spans gives you more control.
- Extension: add an infinite scroll that loads more images as the user scrolls to the bottom, or integrate with the Unsplash API for real photos.

## README Guidance

The project repo's README should include a short description, a screenshot of the masonry grid
and a lightbox view, the live demo link, a features list (masonry, lightbox, lazy loading,
filtering, keyboard nav), and a one-step local run instruction.
