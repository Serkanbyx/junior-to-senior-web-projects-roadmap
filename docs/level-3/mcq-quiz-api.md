# MCQ Quiz API

> A RESTful MCQ Quiz API with Fisher-Yates randomization, category/difficulty filtering, timed sessions, and automatic score calculation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://mcq-quiz-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/mcq-quiz-api)

---

## Purpose

This project teaches you to build stateful API flows — a quiz isn't a single request, it's
a session: start quiz → answer questions → submit → get score. You'll learn to manage
temporary state (active quiz sessions), implement the Fisher-Yates shuffle algorithm for
unbiased randomization, and calculate scores server-side (never trust the client).

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3)
- **Session IDs:** uuid
- **Validation:** express-validator
- **Security:** Helmet 8, express-rate-limit
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Seed the question bank.** Create a questions table: `id, question, options (JSON), correct_answer, category, difficulty ('easy'|'medium'|'hard')`. Seed with 50+ questions across multiple categories. Store options as JSON array.

2. **Build the quiz start endpoint.** `POST /quiz/start` accepts `{ category?, difficulty?, count: 10 }`. Select random questions using the Fisher-Yates shuffle algorithm (not `ORDER BY RANDOM()` which is biased and slow). Create a session with UUID, store selected question IDs and start time.

3. **Implement Fisher-Yates shuffle.** Fetch matching questions from SQLite, then shuffle in memory with Fisher-Yates. Take the first N items. This produces an unbiased random selection — every question has an equal probability of being chosen.

4. **Build the answer submission endpoint.** `POST /quiz/:sessionId/submit` accepts answers array. Compare each answer to the correct answer (server-side lookup — the correct answers were never sent to the client). Calculate score, time taken, and per-question results.

5. **Add timed quizzes.** Store start time in the session. On submit, calculate elapsed time. Optionally enforce a time limit (e.g., 30 seconds per question). If time expires, auto-submit with unanswered questions marked wrong.

6. **Build statistics and leaderboard.** Store completed quiz results: `session_id, score, total, category, difficulty, time_taken, completed_at`. `GET /quiz/leaderboard` returns top scores sorted by score then time.

7. **Protect against cheating.** Never send correct answers to the client during the quiz — only send questions and options. Score calculation happens entirely server-side. Rate limit quiz starts to prevent brute-force answer discovery.

## Deployment

Deploy on Render.com. Question bank persists in SQLite. Sessions can be stored in-memory
(with TTL cleanup) or in SQLite.

## Tips

- Fisher-Yates is the only correct shuffle algorithm. `array.sort(() => Math.random() - 0.5)` is biased — some permutations are more likely than others. Fisher-Yates guarantees uniform distribution in O(n) time.
- Never send correct answers to the client. The quiz flow: server sends questions (without answers) → client submits answers → server compares and returns results. If you send correct answers upfront, anyone can cheat via browser DevTools.
- Extension: add multiplayer quiz mode, question contribution (users submit questions), difficulty progression (start easy, get harder), or a time-attack mode.

## README Guidance

The project repo's README should include a description, quiz flow explanation, API endpoints,
Fisher-Yates algorithm note, tech stack, and setup instructions.
