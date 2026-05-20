# BMI Calculator

> A responsive BMI calculator with metric/imperial toggle, color-coded results, visual indicator bar, calculation history, and PWA support.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://bmi-calculatorrrrr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/BMI-calculator)

---

## Purpose

Form handling is a fundamental web skill, and this project covers it end-to-end: reading
numeric inputs, validating them, computing a result, and presenting that result with visual
context (color, range, indicator). The unit toggle teaches you to manage two parallel data
models (metric vs. imperial) from a single UI. Adding PWA support and LocalStorage history
rounds it out as a "small but complete" app.

## Tech Stack

- **Frontend:** HTML5, CSS3 (Glassmorphism), vanilla JavaScript
- **Backend:** none
- **Database:** LocalStorage (history persistence)
- **Key libraries / tools:** Service Worker + Manifest (PWA), CSS `backdrop-filter` (glass effect)
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Build the form.** Two number inputs (height, weight) with labels. Add a unit toggle (metric: cm/kg vs. imperial: ft-in/lbs) that swaps placeholders and labels. Use `<input type="number">` with `min`, `max`, and `step` for basic browser validation.
2. **Validate input.** On submit, check that both fields have positive numeric values within realistic ranges (e.g. height 50–300 cm, weight 10–500 kg). Show inline error messages for invalid entries — don't use `alert()`.
3. **Calculate BMI.** Metric: `weight / (height_m)²`. Imperial: `(weight × 703) / (height_inches)²`. Convert units internally so the formula always works with consistent values.
4. **Display results with color coding.** Map the BMI value to a category (underweight, normal, overweight, obese) and assign a color. Show the numeric result, the category label, and the ideal weight range for the user's height.
5. **Build the visual indicator.** Create a horizontal bar or gauge that marks where the user's BMI falls on the spectrum (15–40 range). Use CSS gradients or positioned markers. This turns a number into something immediately understandable.
6. **Store calculation history.** On each calculation, push `{ date, height, weight, bmi, category }` into a LocalStorage-backed array. Render a history list below the calculator. Allow clearing history.
7. **Add PWA and accessibility.** Register a service worker for offline caching. Add ARIA labels to inputs and the result area. Ensure full keyboard navigation and screen-reader compatibility.

## Deployment

Push to GitHub and deploy on Netlify. The service worker needs HTTPS (provided by Netlify).
No environment variables or build steps required.

## Tips

- Glassmorphism (`backdrop-filter: blur()`) doesn't work in all browsers — always set a solid fallback background color so the UI remains usable.
- The BMI formula is trivial; the real challenge is presenting the result in a way that's instantly meaningful. Invest time in the visual indicator — it's what makes this project portfolio-worthy.
- Extension: add a chart (using `<canvas>`) showing BMI history over time, or add body fat percentage estimation.

## README Guidance

The project repo's README should include a short description, a screenshot showing the glass
UI with a calculated result, the live demo link, features (unit toggle, PWA, history, accessibility),
and a one-step local run instruction.
