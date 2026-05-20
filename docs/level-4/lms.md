# LMS — Learning Management System

> A fullstack MERN platform where instructors publish courses and students enrol, take quizzes, and track progress.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](#) &nbsp;·&nbsp; [Source Code](#)

---

## Purpose

An LMS is one of the strongest junior-to-mid portfolio projects because it forces real
product thinking: multiple user roles, relational data, stateful progress, and quiz
scoring. It proves you can design a non-trivial data model, enforce role-based access,
and connect a React frontend to an Express API end to end. This is the kind of project
that turns an interview from "can you code" into "let's discuss your architecture".

## Tech Stack

- **Frontend:** React, React Router, a state solution (Context or Redux Toolkit)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** JWT auth, bcrypt, a charting library for progress, Cloudinary or S3 for course media
- **Deployment:** Vercel (frontend) + Render/Railway (backend) + MongoDB Atlas

## Build Steps

1. **Design the data model first.** Sketch the entities — User (with a `role`: instructor or student), Course, Lesson, Quiz, Question, and Enrollment (which links a student to a course and holds progress). Get the relationships right before writing code.
2. **Build authentication with roles.** Reuse the Authentication API pattern, but add a `role` field and middleware that distinguishes instructor-only from student-only routes.
3. **Instructor course management.** CRUD endpoints and UI for creating courses, adding lessons, and attaching quizzes. Only the owning instructor may edit a course.
4. **Course catalogue and enrolment.** A public list of courses with search and filter; an authenticated "enroll" action that creates an Enrollment record.
5. **Lesson player and progress.** As a student completes lessons, update the Enrollment's progress. Compute a completion percentage and display it.
6. **Quizzes and scoring.** Render quiz questions, accept answers, score them server-side (never trust the client with the answer key), and store the result on the Enrollment.
7. **Dashboards.** A student dashboard showing enrolled courses and progress; an instructor dashboard showing their courses and enrolment counts.
8. **Polish and protect.** Loading and empty states, consistent error handling, and a check on every endpoint that the caller's role and ownership are valid.

## Deployment

Deploy the React app to Vercel and the API to Render or Railway, with MongoDB Atlas as
the database. Store course images on Cloudinary or S3 rather than the database. Set the
API URL, JWT secret, database URL, and media credentials as environment variables, and
configure CORS to allow only the deployed frontend origin.

## Tips

- **The data model is the project.** If Enrollment is modelled well, progress and quiz
  scoring fall out naturally. If it isn't, you'll fight the code the whole way.
- Score quizzes on the server. Sending the answer key to the browser is the most common
  security mistake in LMS projects.
- Build for one role end to end (instructor creates a course) before starting the other.
  A thin vertical slice beats a wide unfinished one.
- Extension: add certificates on completion, or a review/rating system per course.

## README Guidance

The repo README should open with a screenshot of both dashboards, a live demo link, the
feature list grouped by role, the data model (a diagram or a short description), the
tech stack, and separate setup steps for the client and server.
