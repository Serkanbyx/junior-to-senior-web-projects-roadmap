# Memory Game

> A card-matching memory game with 3D flip animations, progressive difficulty levels, and real-time stats tracking.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://memory-gameeeeee.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/memory-game)

---

## Purpose

This project is about managing hidden state — you have data the user can't always see, and
you reveal it based on interaction. It teaches array shuffling, pair-matching logic, and CSS
3D transforms. The "two cards at a time" constraint introduces a locking mechanism you'll
use in many future UIs (disable input while an animation or async action completes).

## Tech Stack

- **Frontend:** HTML, CSS3, vanilla JavaScript
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** CSS 3D transforms (`perspective`, `rotateY`), no external dependencies
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Define the card set.** Create an array of symbol/image pairs. Duplicate each entry so every symbol appears twice. This is your "deck."
2. **Shuffle the deck.** Use the Fisher-Yates shuffle algorithm to randomize the array in place. This guarantees uniform randomness — don't use `sort(() => Math.random() - 0.5)`, which is biased.
3. **Render the grid.** Generate one card element per array item. Each card has a front face (hidden symbol) and a back face (generic pattern). Use CSS Grid to arrange them. The grid size changes with difficulty level (e.g. 4×3, 4×4, 6×4).
4. **Handle card flips.** On click, add a "flipped" class that triggers a CSS 3D `rotateY(180deg)` transform. Track flipped cards in a temporary array. Ignore clicks on already-matched or already-flipped cards.
5. **Check for a match.** When two cards are flipped, compare their symbols. If they match, mark both as "matched" and leave them face-up. If not, wait ~1 second (so the player can see both), then flip both back.
6. **Lock input during comparison.** Between flipping the second card and resolving the match/no-match, disable further clicks. This prevents the player from flipping a third card mid-animation.
7. **Track stats and detect win.** Count moves (each pair flip = 1 move) and elapsed time. When all pairs are matched, show a victory screen with final stats. Offer difficulty levels that increase the grid size.

## Deployment

Push the static files to GitHub and connect to Netlify. No build step needed.
The 3D transforms work in all modern browsers without polyfills.

## Tips

- Use `backface-visibility: hidden` on both card faces — without it, the back face bleeds through during the flip.
- The 1-second delay before flipping unmatched cards back is crucial for UX. Without it, the game feels punishing and users can't learn card positions.
- Extension: add a "best score" tracker using `localStorage`, or add a timer-based challenge mode.

## README Guidance

The project repo's README should include a short description, a GIF showing the flip animation
and a successful match, the live demo link, a features list (difficulty levels, stats, 3D
animations), and a one-step local run instruction.
