# Personal Portfolio Website

> A responsive portfolio site with SEO optimization, WCAG 2.1 AA accessibility, performance best practices, and a contact form.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://personal-portfolio-websiteee.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/personal-portfolio-website)

---

## Purpose

Every developer needs a portfolio, and building one from scratch (no template) proves you
understand semantic HTML, responsive CSS, and progressive enhancement. This project focuses
on the non-functional qualities that separate professional sites from student projects: SEO
meta tags, accessibility compliance, performance budgets, and a working contact flow. It's
the one project from Level 1 that you'll actually ship under your own name.

## Tech Stack

- **Frontend:** HTML5 (semantic), CSS3 (responsive), vanilla JavaScript
- **Backend:** none (contact form via third-party integration)
- **Database:** none
- **Key libraries / tools:** Open Graph meta tags, structured data (JSON-LD), ARIA attributes
- **Deployment:** Netlify (static hosting + form handling)

## Build Steps

1. **Plan the sections.** A portfolio typically has: hero/intro, about, skills, projects, contact, footer. Sketch the layout on paper before coding. Each section maps to a semantic HTML element (`<header>`, `<main>`, `<section>`, `<footer>`).
2. **Write semantic HTML first.** Use `<nav>`, `<article>`, `<figure>`, `<address>` where appropriate. Add heading hierarchy (h1 → h2 → h3) that makes sense when read without CSS. This is the foundation for both SEO and accessibility.
3. **Build responsive CSS.** Start mobile-first: design for 320px width, then add `min-width` media queries for tablet and desktop. Use CSS Grid for the overall layout and Flexbox for component alignment. No fixed pixel widths on containers.
4. **Add SEO meta tags.** Include `<title>`, `<meta name="description">`, Open Graph tags (`og:title`, `og:image`, `og:description`), and a JSON-LD structured data block (`@type: Person`). Add a `robots.txt` and `sitemap.xml` if you have multiple pages.
5. **Implement accessibility (WCAG 2.1 AA).** Ensure color contrast ratios meet 4.5:1 for text. Add skip-to-content link. All interactive elements are keyboard-focusable with visible focus rings. Images have descriptive `alt` text. Test with a screen reader.
6. **Build the contact form.** Create a form with name, email, and message fields. Validate client-side (required fields, email format). Integrate with Netlify Forms, Formspree, or EmailJS for delivery — no backend needed.
7. **Optimize performance.** Compress images (WebP), minify CSS/JS if large, add `loading="lazy"` to below-fold images, use system font stacks or preload web fonts. Target Lighthouse 90+ on all four metrics.

## Deployment

Deploy on Netlify with a custom domain if you have one. Enable Netlify Forms for the
contact form (add `netlify` attribute to the `<form>` tag). Set up redirect from `www` to
the root domain.

## Tips

- Don't over-design the portfolio. Recruiters spend 10–30 seconds scanning — clear hierarchy, fast load, and visible project links matter more than fancy animations.
- Test with Lighthouse, axe DevTools, and the WAVE browser extension. Real accessibility testing catches what code review misses.
- Extension: add a dark/light mode toggle, a blog section with Markdown rendering, or animated section transitions with the Intersection Observer.

## README Guidance

The project repo's README should include a short description, a full-page screenshot (desktop
and mobile), the live demo link, the tech stack, Lighthouse scores, and local setup instructions.
