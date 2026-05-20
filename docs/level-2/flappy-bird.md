# Flappy Bird

> A Flappy Bird clone with HTML5 Canvas rendering, delta-time physics, procedural pipe generation, and Zustand game state.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://flappy-birddddd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/flappy-bird)

---

## Purpose

This project teaches game development fundamentals: a game loop, frame-independent physics
(delta-time), collision detection, and procedural content generation. With minimal
dependencies (just React + Zustand), everything is built from scratch on HTML5 Canvas.
These patterns apply to any animation-heavy UI or interactive visualization.

## Tech Stack

- **Framework:** React 19, TypeScript, Vite
- **Styling:** Tailwind CSS
- **State:** Zustand (game state: score, bird position, pipes, game status)
- **Rendering:** HTML5 Canvas API (custom game loop)
- **Deployment:** Netlify

## Build Steps

1. **Set up the game loop.** `requestAnimationFrame` loop that runs at screen refresh rate. Calculate delta-time (ms since last frame) for frame-independent physics. Separate update (logic) from render (drawing).

2. **Build the bird physics.** Bird has position (y), velocity, and gravity. Each frame: velocity += gravity * dt, position += velocity * dt. On tap/click/space: velocity = jump force (negative = up). Clamp to screen bounds.

3. **Render on Canvas.** Get 2D context. Each frame: clear canvas, draw background, draw bird (rectangle or sprite), draw pipes, draw score. Canvas is the most performant way to render many moving objects.

4. **Implement pipe generation.** Pipes spawn at intervals off the right edge. Each pipe: x position, gap position (random within bounds), gap size. Move left each frame (speed * dt). Remove when off-screen left.

5. **Add collision detection.** Rectangle intersection between bird hitbox and each pipe (top and bottom). Also check: bird hits ground or ceiling. On collision: game over state, show score.

6. **Manage game state with Zustand.** States: menu, playing, game-over. Score increments when bird passes a pipe. Store high score in Zustand (persisted). Actions: start, flap, reset.

7. **Polish and deploy.** Add score display, high score, restart button. Smooth 60fps gameplay. Responsive canvas size. Deploy on Netlify.

## Tips

- Delta-time physics makes the game run at the same speed regardless of frame rate. Without it, the game runs faster on 144Hz monitors and slower on 30fps devices. Always multiply movement by `dt`.
- Collision detection for rectangles: two rectangles overlap when ALL of these are true: `left1 < right2 AND right1 > left2 AND top1 < bottom2 AND bottom1 > top2`.
- Extension: add sprite animations (bird flapping), parallax scrolling background, difficulty progression (increasing speed), sound effects, or a leaderboard.
