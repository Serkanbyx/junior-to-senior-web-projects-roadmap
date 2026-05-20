# MCQ/Quiz API

> A quiz engine API with nested question data, scoring logic, timed sessions, and leaderboard tracking.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://mcq-quiz-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/mcq-quiz-api)

---

## Purpose

This project teaches you to model nested/hierarchical data (quizzes contain questions contain
options) and implement stateful business logic (scoring, timing, answer validation). It's more
complex than simple CRUD because the API must enforce rules: you can't see answers before
submitting, you can't submit after time expires, and the score must be calculated server-side
to prevent cheating.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Mongoose subdocuments, dotenv
- **Deployment:** Render.com

## Build Steps

1. **Model the data.** Quiz: `{ title, description, questions: [Question], timeLimit, createdAt }`. Question: `{ text, options: [{ text, isCorrect }], points }`. Use Mongoose subdocuments — questions are embedded in the quiz document.
2. **Build quiz CRUD.** Admin endpoints to create, update, and delete quizzes. When returning a quiz for play, strip `isCorrect` from options — the client should never see answers before submission.
3. **Start a quiz session.** `POST /quizzes/:id/start` creates a session: `{ quizId, startedAt, expiresAt: startedAt + timeLimit }`. Return the questions (without answers) and a session token/ID.
4. **Submit answers.** `POST /quizzes/:id/submit` accepts `{ sessionId, answers: [{ questionId, selectedOption }] }`. First check if the session has expired. Then compare each answer against the correct option and calculate the score.
5. **Calculate scoring.** For each question: if the selected option's `isCorrect` is true, award the question's points. Return a breakdown: total score, max possible, percentage, and per-question results (correct/incorrect).
6. **Build a leaderboard.** Store completed sessions with scores. `GET /quizzes/:id/leaderboard` returns top scores sorted descending, with username and completion time. Support pagination.
7. **Enforce timing rules.** If `Date.now() > session.expiresAt`, reject the submission with a 400 and return the score as 0. The time check must happen server-side — never trust the client's clock.

## Deployment

Deploy on Render.com. Set `MONGODB_URI`. Seed with a few sample quizzes using a seed script
so the demo API has content to interact with.

## Tips

- Never send correct answers to the client before submission. The API should return questions with options but `isCorrect` stripped. Only reveal correct answers in the submission response.
- Server-side timing is critical for fairness. Store `expiresAt` on session creation and validate against it on submission — the client's reported time is irrelevant.
- Extension: add categories/tags for quizzes, difficulty levels, randomized question order per session, or a question bank that samples N questions from a larger pool.

## README Guidance

The project repo's README should include a description, API flow diagram (create quiz → start
session → submit answers → view score), endpoint table, and local setup steps.
