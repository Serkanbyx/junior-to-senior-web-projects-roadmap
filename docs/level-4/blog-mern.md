# Blog with Comments & Likes

> A fullstack blog platform with three-tier role system (User → Author → Admin), post approval workflow, guest likes, and a comprehensive admin panel.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://blog-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/blog-mern)

---

## Purpose

This project adds organizational complexity to blogging: multiple roles with different
permissions, content moderation workflows, and engagement features. Users can read and
comment, authors can write posts pending approval, and admins moderate everything. It
teaches role-based access control, approval workflows, fingerprint-based guest interactions,
and building distinct interfaces for different user types.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, React Hook Form
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT (httpOnly cookies) + bcryptjs
- **Image uploads:** Cloudinary 2
- **Email:** Nodemailer
- **Validation:** express-validator
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize
- **UX:** React Icons, dark/light theme with persistent preferences
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the three-tier role system.** User (read + comment), Author (write posts), Admin (moderate everything). Users can request Author promotion. Admins review and approve/reject author requests. Each role sees a different dashboard.

2. **Build the post approval workflow.** Authors submit posts → status is "pending." Admins see pending posts in their dashboard and can approve or reject (with reason). Only approved posts appear on the public blog. Authors see their post statuses.

3. **Implement guest likes with fingerprinting.** Visitors can like posts without registering. Use browser fingerprinting (combination of user-agent, screen resolution, etc.) to identify unique guests and prevent duplicate likes. This increases engagement without forcing registration.

4. **Build the comment system.** Registered users can comment on posts. Comments show author name and timestamp. Authenticated author feedback on their own posts is visually distinct. Delete own comments. Admin can moderate any comment.

5. **Build the admin panel.** Dashboard with platform stats. User management (view users, approve author requests). Post moderation (approve/reject pending posts). Comment oversight. All in a dedicated admin layout with sidebar navigation.

6. **Add theme and privacy features.** Dark/light mode with CSS variables and persistent user preference (stored in profile). Privacy controls: toggle public profile visibility, toggle liked posts visibility. Settings page with appearance, privacy, notifications, and content preferences.

7. **Build the public blog UI.** Post feed with pagination and sorting (newest, popular, most commented). Category tags for filtering. Individual post pages with Cloudinary-hosted cover images. Responsive drawer navigation for mobile.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `CLOUDINARY_*`, `SMTP_*`. Frontend on
Netlify with `VITE_API_URL`. JWT in httpOnly cookies requires `sameSite` and `secure` flags.

## Tips

- The approval workflow pattern: separate "draft" from "published" status with an intermediate "pending" state. This is how real CMS platforms (WordPress, Medium partner program) handle content moderation at scale.
- Guest likes with fingerprinting trade accuracy for frictionlessness. Some users will bypass it (incognito mode), but the engagement boost from not requiring login far outweighs the minor inflation.
- Extension: add nested comment replies, reaction types (love, insightful, funny), author analytics dashboard, or email notifications on new comments.

## README Guidance

The project repo's README should include a description, screenshots of public blog, author
dashboard, and admin panel, role system explanation, tech stack, and setup instructions.
