# Social Media Platform

> A fullstack social platform with real-time notifications, follow system, post interactions, dark mode, and Socket.io-powered live updates.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://social-media-platformm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/social-media-platform)

---

## Purpose

This project combines posts, likes, comments, follows, and real-time notifications into a
cohesive social platform. It teaches you to model social graphs (who follows whom), build
personalized feeds, handle real-time interactions at scale, and create polished dark-mode
interfaces. This is the architecture behind Twitter, Instagram, and LinkedIn.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, Inter font
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 8), Socket.io 4
- **Auth:** JWT (httpOnly cookies) + bcryptjs
- **Image uploads:** Cloudinary + Multer + Streamifier
- **Security:** Helmet 8, express-rate-limit, express-mongo-sanitize
- **API docs:** Swagger (swagger-jsdoc + swagger-ui-express)
- **UX:** Lucide React (icons), React Hot Toast, socket.io-client, dark mode
- **Architecture:** Service layer pattern (controllers → services → models)
- **Deployment:** Netlify (frontend) + Render (backend, with `render.yaml`)

## Build Steps

1. **Design the social graph.** User model with `followers` and `following` references. Follow/unfollow endpoint toggles the relationship (update both users). Track counts for display on profiles. The service layer separates business logic from route handlers.

2. **Build the post system.** Create posts with text and optional image (Cloudinary). Like/unlike toggle. Comment with text. All interactions stored in MongoDB with user references. Public feed shows all posts; personalized feed shows followed users' posts only.

3. **Implement real-time notifications.** Socket.io connection authenticated via JWT. Notification model: `{ recipient, sender, type: 'like' | 'comment' | 'follow', post?, read }`. When someone likes your post, an instant Socket.io event reaches your client. Notification bell with unread count.

4. **Build user profiles.** Profile page with avatar (Cloudinary upload), bio, follower/following counts, and user's posts. Follow/unfollow button. Edit own profile. View other users' profiles from the feed.

5. **Build the feed.** Two views: "For You" (all posts, sorted by newest) and "Following" (only from users you follow). Infinite scroll or pagination. Each post card shows: author avatar + name, content, image, like/comment counts, and interaction buttons.

6. **Implement dark mode.** System-wide dark theme as the default (with light mode option). Persistent preference stored in state. Tailwind CSS dark mode utilities throughout. Consistent color palette using CSS custom properties.

7. **Add seed data and deploy.** Seed script populates the database with sample users, posts, and follows for a meaningful demo. Service layer architecture keeps code maintainable: `controllers/` handle HTTP, `services/` contain business logic, `models/` define schemas.

## Deployment

Backend on Render (with `render.yaml`) — `MONGODB_URI`, `JWT_SECRET`, `CLOUDINARY_*`,
`CLIENT_URL`. Frontend on Netlify (`netlify.toml`) with `VITE_API_URL`.

## Tips

- The service layer pattern: controllers parse requests and send responses; services contain all business logic. This makes testing easier (test services without HTTP) and prevents fat controllers that mix concerns.
- Real-time notifications should be fire-and-forget from the action's perspective. When a user likes a post, the like response returns immediately — notification creation happens asynchronously. Never slow down the primary action for a secondary effect.
- Extension: add stories (24h expiring content), direct messages, hashtags with trending topics, content moderation (report/block), or an explore page with algorithmic recommendations.

## README Guidance

The project repo's README should include a description, screenshots of feed and profile
(dark mode), features list, architecture overview, tech stack, and setup instructions.
