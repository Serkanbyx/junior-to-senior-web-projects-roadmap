# Flappy Bird

> A Flappy Bird clone with HTML5 Canvas rendering, delta-time physics, procedural pipe generation, and 60fps gameplay.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://flappy-birddddd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/flappy-bird)

---

## Purpose

This project introduces the game loop pattern — `requestAnimationFrame` driving update and
render cycles at 60fps. You'll learn delta-time physics (frame-rate-independent movement),
collision detection (rectangle intersection), and procedural content generation (random pipe
gaps). These concepts apply to any animation-heavy UI: scroll-driven animations, physics-based
transitions, or interactive data visualizations.

## Tech Stack

- **Frontend:** React 19, TypeScript, Tailwind CSS, Vite
- **Backend:** none
- **Database:** none
- **Key libraries / tools:** HTML5 Canvas API, Zustand (game state), requestAnimationFrame
- **Deployment:** Netlify

## Build Steps

1. **Set up the Canvas.** Render a `<canvas>` element sized to the game viewport. Get the 2D rendering context. Use a React ref to access the canvas and start the game loop on mount. Clean up on unmount.
2. **Build the game loop.** Use `requestAnimationFrame` to create a continuous loop. Calculate `deltaTime` (time since last frame) to make physics frame-rate-independent. The loop calls `update(dt)` then `render(ctx)` every frame.
3. **Implement the bird.** The bird has position (x, y), velocity, and gravity. Each frame: `velocity += gravity * dt`, `y += velocity * dt`. On tap/click/spacebar: set velocity to a negative "jump" value. Clamp y to prevent going off-screen.
4. **Generate pipes procedurally.** Spawn a new pipe pair at intervals. Each pair has a random gap position (within bounds). Pipes move left at constant speed. Remove pipes that have scrolled off-screen. Increment score when a pipe passes the bird's x position.
5. **Detect collisions.** Check if the bird's bounding rectangle overlaps with any pipe rectangle (top pipe or bottom pipe) or the ground/ceiling. Use axis-aligned bounding box (AABB) intersection: overlap on both x and y axes means collision.
6. **Manage game states.** Three states: menu (waiting for first tap), playing (active loop), and game-over (show score, high score, restart). Use Zustand to manage state transitions. Persist high score in localStorage.
7. **Add polish.** Parallax scrolling background, animated bird sprite (wing flap on tap), pipe color variation, score display with drop shadow, screen shake on death, and touch support for mobile play.

## Deployment

Deploy on Netlify as a static Vite build. No environment variables needed.
Canvas games work in all modern browsers without polyfills.

## Tips

- Delta-time physics is critical: `position += speed * deltaTime` gives consistent speed regardless of frame rate. Without it, the game runs faster on high-refresh-rate displays and slower on laggy devices.
- AABB collision is sufficient for Flappy Bird. Don't overcomplicate with pixel-perfect or circular collision — rectangles work fine for pipes and a bird.
- Extension: add difficulty progression (pipes speed up over time), different bird skins, or a leaderboard using a simple backend.

## README Guidance

The project repo's README should include a short description, a GIF of gameplay, the live
demo link, tech stack, controls (tap/space/click), and local dev instructions.
