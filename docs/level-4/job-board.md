# Job Board

> A multi-role job board with company dashboards, applicant tracking, and role-based access control.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://job-board-with-company-user-dashboard.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/job-board-with-company-user-dashboard)

---

## Purpose

This project introduces multi-role systems — different users see different interfaces and
have different permissions. Companies post jobs and review applicants; job seekers browse
and apply. It teaches role-based access control (RBAC), multi-dashboard architectures, and
the applicant tracking workflow. This is a real SaaS-level project.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT with roles (company, user, admin)
- **Key libraries / tools:** React Router, Axios, Multer (resume upload)
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the role system.** User model with `role: 'jobseeker' | 'company' | 'admin'`. Each role has different permissions. Middleware checks role before allowing access to endpoints.
2. **Build the company flow.** Companies: register as company → create job listings → review applications → update application status (reviewing, shortlisted, rejected, accepted).
3. **Build the jobseeker flow.** Jobseekers: register → browse jobs → view detail → apply (with resume upload and cover letter) → track application status.
4. **Implement role-based dashboards.** After login, redirect to the appropriate dashboard based on role. Company dashboard: manage listings, view applicants. Jobseeker dashboard: applied jobs, saved jobs, profile.
5. **Build the job listing page.** Public job list with filters: location, job type (full-time, part-time, remote), experience level, and search. Paginated results with clear job cards.
6. **Implement the application system.** `POST /jobs/:id/apply` with resume file upload. Store application: `{ job, applicant, resume, coverLetter, status, appliedAt }`. Companies see applicants per job with status management.
7. **Add admin features.** Admin can moderate listings (approve/reject), manage users, and view platform analytics (total jobs, applications, users).

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, and Cloudinary credentials for resume
storage. Frontend on Netlify with `VITE_API_URL`. Seed sample data for demo (companies,
jobs, applications).

## Tips

- Role-based middleware is a single function: `authorize(...roles)` returns a middleware that checks `req.user.role` against the allowed roles. Apply it per-route or per-router.
- The biggest UX challenge is the post-login redirect. Store the intended destination before redirecting to login, then navigate there after successful auth.
- Extension: add email notifications (new applicant, status change), company verification, job alerts/subscriptions, or an admin analytics dashboard.

## README Guidance

The project repo's README should include a description, screenshots of both dashboards
(company and jobseeker), tech stack, role system explanation, environment variables, and
setup instructions with seed data.
