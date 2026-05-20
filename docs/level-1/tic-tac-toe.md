# Tic Tac Toe

> A two-player Tic Tac Toe game in the browser with win and draw detection.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](#) &nbsp;·&nbsp; [Source Code](#)

---

## Purpose

This is the first project where logic and UI meet. It proves you can hold game state in
JavaScript, render that state to the DOM, respond to user events, and detect a terminal
condition (win or draw). Every concept here — state, rendering, events — scales directly
into framework work later. If you can build this cleanly without copying, you understand
the browser.

## Tech Stack

- **Frontend:** HTML, CSS, vanilla JavaScript
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** none — this is intentionally framework-free
- **Deployment:** Netlify or GitHub Pages (static hosting)

## Build Steps

1. **Lay out the board.** Create a 3×3 grid with CSS Grid. Each cell is a clickable element with a data attribute storing its index (0–8).
2. **Model the state.** Keep the board as a 9-element array and a `currentPlayer` variable (`"X"` or `"O"`). The array is the single source of truth — the DOM only reflects it.
3. **Handle a move.** On cell click, ignore the click if the cell is already filled or the game is over. Otherwise write the current player into the array and re-render.
4. **Detect a win.** Define the 8 winning lines (3 rows, 3 columns, 2 diagonals) as index triples. After every move, check whether any line holds three identical non-empty values.
5. **Detect a draw.** If the board has no empty cells and there's no winner, the game is a draw.
6. **Render the result.** Show a status message ("X wins", "Draw") and freeze further input once the game ends.
7. **Add a reset.** A button that clears the array, resets the current player, and re-renders an empty board.

## Deployment

Push the static files to a repo and connect it to Netlify, or enable GitHub Pages on the
`main` branch. No build step or environment variables needed.

## Tips

- Separate the **render** function from the **game logic**. Logic mutates the array; render reads it. Mixing them is the most common reason this project gets messy.
- Don't hardcode win checks for X and O separately — one generic line-check function handles both.
- Extension: add an unbeatable single-player mode with the minimax algorithm. It's a great Level 1.5 challenge.

## README Guidance

The project repo's README should include a short description, a GIF of a full game,
the live demo link, the tech stack line, and a one-step "open `index.html`" run note.
