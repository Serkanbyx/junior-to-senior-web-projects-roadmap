# Type Speed Test

> A typing speed test with real-time WPM calculation, accuracy tracking, and difficulty levels — built as a Progressive Web App.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://type-speed-testt.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/type-speed-test)

---

## Purpose

This project forces you to handle real-time keyboard events, measure time intervals accurately,
and update the UI on every keystroke without lag. It's the first place you'll confront the
difference between "works" and "feels responsive." The addition of a service worker and manifest
introduces you to PWA concepts — offline capability and installability — without a framework.

## Tech Stack

- **Frontend:** HTML5, CSS3, vanilla JavaScript (ES6+)
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** Service Worker API, Web App Manifest (PWA), zero external dependencies
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Prepare the word bank.** Create arrays of words grouped by difficulty (easy: common short words, medium: longer words, hard: uncommon or technical words). Shuffle and serve a random subset for each test.
2. **Render the test area.** Display the target text as a sequence of `<span>` elements — one per character. The current character gets a cursor highlight. Correctly typed characters turn green; mistakes turn red.
3. **Capture keystrokes.** Listen to the `input` event on a hidden text field (not `keydown` — this handles IME and mobile keyboards too). On each event, compare the typed character against the expected character at the current index.
4. **Start the timer on first keystroke.** Use `performance.now()` or `Date.now()` to record the start time. Update a live countdown or elapsed-time display using `requestAnimationFrame` or a short `setInterval`.
5. **Calculate WPM and accuracy.** WPM = (characters typed / 5) / minutes elapsed. Accuracy = correct keystrokes / total keystrokes × 100. Update both values in real-time as the user types.
6. **End the test.** When the user finishes all characters or time runs out, freeze input, show final stats (WPM, accuracy, time), and offer a restart button.
7. **Add PWA support.** Write a `manifest.json` with app name, icons, and theme color. Register a service worker that caches static assets for offline use. This makes the app installable on mobile home screens.

## Deployment

Push to GitHub and connect to Netlify. The service worker requires HTTPS to activate —
Netlify provides this by default. No build step or environment variables needed.

## Tips

- Don't use `keydown` for typing input — it misses composed characters and behaves inconsistently across browsers. The `input` event on a text field is more reliable.
- WPM is traditionally "words per minute" where a "word" = 5 characters. This is the standard typing-test convention.
- Extension: add a results history stored in `localStorage` so users can track improvement over sessions.

## README Guidance

The project repo's README should include a short description, a screenshot or GIF showing a
test in progress, the live demo link, a features list (PWA, difficulty levels, real-time stats),
and instructions to run locally (open `index.html` or use Live Server).
