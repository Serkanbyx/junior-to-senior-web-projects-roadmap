# Social Media Platform

> A fullstack social platform with follow graph, personalized feed, notifications, and user profiles.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://social-media-platformm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/social-media-platform)

---

## Purpose

This is one of the most complex Level 4 projects — it combines posts, likes, comments,
follows, a personalized feed, and notifications into a cohesive platform. It teaches you to
model social graphs (who follows whom), generate feeds from followed users' content, and
handle the notification lifecycle. This is the architecture behind Twitter, Instagram, and LinkedIn.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT
- **Key libraries / tools:** Mongoose populate, Axios, React Router, Socket.io (notifications)
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Model the social graph.** User has `followers: [userId]` and `following: [userId]`. `POST /users/:id/follow` toggles the follow relationship (update both users atomically). Track follower/following counts.
2. **Build the post system.** Posts with text, optional image, author reference. Like/unlike (same as Blog MERN). Comment system. All posts are public but the feed is personalized.
3. **Generate the personalized feed.** `GET /feed` returns posts from users the current user follows, sorted by newest. Query: `Post.find({ author: { $in: req.user.following } }).sort('-createdAt')`. Paginate with cursor-based pagination.
4. **Build user profiles.** Public profile page showing user info, post count, follower/following counts, and their posts. Follow/unfollow button. Show mutual followers if applicable.
5. **Implement notifications.** Notification model: `{ recipient, sender, type: 'like' | 'comment' | 'follow', post?, read, createdAt }`. Create notifications on user actions. Mark as read when viewed.
6. **Build the notification UI.** A bell icon with unread count. Dropdown showing recent notifications with sender avatar, action text, and timestamp. Mark all as read on open. Link to the relevant content.
7. **Add explore/discover.** A page showing trending posts (most liked in 24h), suggested users to follow (not yet followed, most popular), and a search for users by name.

## Deployment

Backend on Render, frontend on Netlify. Standard MERN env vars. Seed with sample users
and posts for a meaningful demo.

## Tips

- Feed generation with `$in` on followed users works for thousands of users. For millions (Twitter scale), you'd use a fan-out-on-write pattern — but that's Level 5 territory. Keep it simple here.
- Notifications should be created asynchronously (don't slow down the like/comment response). Use a simple in-process queue or fire-and-forget the notification creation.
- Extension: add stories (24h expiring content), direct messages, hashtags/trending topics, or content moderation (report/block).

## README Guidance

The project repo's README should include a description, screenshots of feed and profile,
tech stack, features list, environment variables, and setup instructions.
