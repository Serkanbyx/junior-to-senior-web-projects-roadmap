# Countdown Timer

> A multi-timer app with pause/resume, dark mode, and export/import — persisted with LocalStorage.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://countdown-timerrrr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/countdown-timer)

---

## Purpose

Timers are the first project where you deal with **time as state**. You'll learn how
`setInterval` drifts, why you should store target timestamps instead of decrementing a counter,
and how to format durations for display. Supporting multiple simultaneous timers introduces
array-of-objects state management — the same pattern that scales into any list-based UI.
LocalStorage persistence means the user's timers survive a page refresh.

## Tech Stack

- **Frontend:** HTML, CSS3, vanilla JavaScript
- **Backend:** none
- **Database:** LocalStorage (browser persistence)
- **Key libraries / tools:** CSS custom properties (dark mode), JSON import/export
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Model a timer.** Each timer is an object: `{ id, label, targetDate, remainingMs, isRunning }`. Store all timers in an array. This is your single source of truth.
2. **Create the input form.** Let the user set a target date/time or a duration (hours, minutes, seconds). Validate that the target is in the future. On submit, add a new timer object to the array.
3. **Run the countdown loop.** Use a single `setInterval` (1 second) that iterates all active timers. For each one, calculate `remainingMs = targetDate - Date.now()`. Don't decrement a counter — clock drift makes that inaccurate over minutes.
4. **Format the display.** Convert `remainingMs` into days, hours, minutes, seconds using integer division and modulo. Pad single digits with leading zeros. Update the DOM for each timer.
5. **Implement pause/resume.** On pause, store the remaining milliseconds and clear the timer's `isRunning` flag. On resume, compute a new `targetDate = Date.now() + remainingMs` and restart.
6. **Persist with LocalStorage.** On every state change (add, delete, pause, resume), serialize the timer array to `localStorage`. On page load, rehydrate from storage and resume any running timers.
7. **Add dark mode and export/import.** Toggle a `data-theme` attribute on `<html>` and switch CSS custom properties. For export, serialize timers to a JSON file download. For import, read a JSON file and merge into state.

## Deployment

Push to GitHub, deploy on Netlify. No build tools or environment variables required.
LocalStorage works without any server-side setup.

## Tips

- Never rely on `setInterval` firing exactly every 1000ms — always recalculate remaining time from `Date.now()` vs. the target. Intervals can be delayed by browser throttling (especially in background tabs).
- Use `Intl.RelativeTimeFormat` or simple modulo math for formatting — don't pull in a date library for this.
- Extension: add browser notifications (`Notification API`) that fire when a timer reaches zero, even if the tab is in the background.

## README Guidance

The project repo's README should include a short description, a screenshot showing multiple
active timers, the live demo link, a features list (multi-timer, dark mode, export/import,
persistence), and a one-step local run instruction.
