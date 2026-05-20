# Multiplayer Game Backend

> A full-stack real-time multiplayer game platform with Socket.io, room management, matchmaking, spectator mode, and leaderboard — built as a type-safe monorepo.

**Level:** 5 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://multiplayer-game-backend-nu.vercel.app) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/multiplayer-game-backend)

---

## Purpose

This project is the culmination of everything you've learned — real-time communication,
database design, auth, state management — combined into a system where milliseconds matter.
A multiplayer game server demands authoritative state (the server decides who wins),
sub-second latency (Socket.io events), and resilient connections (auto-reconnect with state
recovery). The platform supports multiple game types, matchmaking, spectators, and an admin
panel — a production-grade system architecture.

## Tech Stack

- **Frontend:** React 19, Vite 8, TypeScript, Tailwind CSS 4, React Router 7
- **Backend:** Express 5, Socket.io 4, TypeScript
- **Database:** PostgreSQL (Neon serverless) via Drizzle ORM
- **Cache/Queue:** Redis (ioredis) for matchmaking queues, sessions, real-time state
- **Auth:** JWT (guest + registered modes), bcryptjs
- **Monorepo:** Shared TypeScript types (`@mpg/shared`) across client and server
- **Testing:** Vitest, Supertest, Testcontainers, Testing Library, MSW
- **Tooling:** Biome (linter/formatter), Pino (structured logging), Swagger UI
- **Deployment:** Vercel (frontend) + Render/Railway (backend)

## Build Steps

1. **Set up the monorepo.** Three packages: `client/`, `server/`, and `shared/`. The shared package exports TypeScript types for Socket.io events, API contracts, room states, and game models. This ensures compile-time type safety — if you change a server event, the client breaks at build time, not at runtime.

2. **Build the auth system with guest mode.** Two JWT strategies: registered users (full features, persistent stats) and guests (play instantly without signup, short-lived token, limited features). bcryptjs with 12 rounds for password hashing. Refresh token rotation for registered users.

3. **Implement the room system.** Rooms with unique 6-character codes. Public rooms (visible in lobby) and private rooms (join by code). Room states: waiting → in-progress → finished. Redis stores active room state for fast reads. PostgreSQL persists completed matches for history.

4. **Build the matchmaking queue.** Redis-backed queue with estimated wait times. Players enter the queue, the server matches compatible players (by game type and skill), creates a room, and notifies both via Socket.io. Handle queue timeouts and cancellation.

5. **Implement game logic (Tic-Tac-Toe + Card Game).** The server is authoritative — it validates every move. Clients send intentions ("place X at row 1, col 2"), the server validates (is it your turn? is the cell empty?), updates state, and broadcasts to all players in the room. The card game extends this to 4 players with hidden information (only send each player their own hand).

6. **Add spectator mode.** Spectators join a room in read-only mode. They receive all public state updates but never see hidden information (like other players' cards). System announcements differentiate spectator chat from player chat.

7. **Build reconnection with grace period.** On disconnect, start a timer (30s). If the player reconnects within the grace period, restore their full game state from Redis. If they don't, forfeit the game. This handles network blips without ruining matches.

8. **Add leaderboard, profiles, and admin panel.** PostgreSQL stores match history, win/loss stats, and rankings. Profile pages with avatar upload (Multer with MIME whitelist, 5MB cap). Admin dashboard: platform stats, user management, room oversight, and match history.

## Deployment

Frontend on Vercel, backend on Render or Railway. PostgreSQL on Neon (serverless).
Redis on Upstash or Railway. Socket.io requires a persistent connection — ensure the
backend host supports WebSocket (not purely serverless).

## Tips

- The monorepo shared package is the key architectural decision. Typed Socket.io events mean you can't emit an event the client doesn't expect or vice versa. This eliminates an entire category of runtime bugs.
- Redis for real-time state, PostgreSQL for persistent data. Active game state lives in Redis (fast reads, TTL for cleanup). Completed matches are written to PostgreSQL (durable, queryable for leaderboards).
- Guest mode lowers friction dramatically — users can play immediately and convert to registered accounts later. The short-lived JWT limits abuse without requiring signup.
- Extension: add more game types (Chess, Connect 4), ELO-based matchmaking, tournament brackets, or replay recording (store all moves and replay deterministically).

## README Guidance

The project repo's README should include a description, architecture diagram (monorepo
structure, Socket.io event flow, Redis/PostgreSQL split), screenshots of gameplay and
matchmaking, feature list, environment variables, and setup instructions for all three
packages.
