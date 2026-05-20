# Blog with Comments & Likes

> A fullstack blog with comment threads, like system, and optimistic UI updates.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://blog-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/blog-mern)

---

## Purpose

This project adds relational data to the blog: posts have comments, comments have authors,
and posts can be liked. It teaches you to model one-to-many relationships in MongoDB, handle
nested resources in REST APIs, and implement optimistic UI (update the interface immediately,
then sync with the server). These patterns are core to any social or content platform.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT
- **Key libraries / tools:** Mongoose populate, Axios, optimistic state updates
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Model relationships.** Post: `{ title, content, author, likes: [userId], likesCount, commentsCount }`. Comment: `{ post: ObjectId, author: ObjectId, text, createdAt }`. Use Mongoose `populate` to resolve author names.
2. **Build post API with social features.** `POST /posts/:id/like` (toggle like — add or remove userId from likes array). `GET /posts/:id/comments` (paginated). `POST /posts/:id/comments` (add comment). All require auth.
3. **Implement like toggle.** One endpoint handles both like and unlike: if userId is in the likes array, remove it (unlike); otherwise add it (like). Update `likesCount` atomically with `$inc`. Return the new state.
4. **Build the optimistic like UI.** On click, immediately update the like count and icon color in React state. Then send the API request. If it fails, revert the state. This makes the UI feel instant.
5. **Build the comment section.** Below each post, show comments with author name, text, and timestamp. A form to add a new comment. On submit, optimistically add the comment to the list, then confirm with the API response.
6. **Add comment count and preview.** On the post list page, show the comment count and the first 1-2 comments as a preview. Fetch this data from the API in a single call (use MongoDB `$lookup` or populate with limit).
7. **Handle edge cases.** Deleted users' comments (show "Deleted User"), rapid like toggling (debounce or disable during API call), and comment pagination (load more button).

## Deployment

Frontend on Netlify, backend on Render. Standard MERN deployment with `MONGODB_URI`,
`JWT_SECRET`, and `VITE_API_URL`.

## Tips

- Optimistic updates make your app feel 10x faster. The pattern: update local state → call API → on error, revert state and show a toast. For likes, this eliminates the perceived latency entirely.
- Store likes as an array of userIds on the post document for simplicity. For high-traffic posts (millions of likes), you'd use a separate collection — but for this scale, embedded is correct.
- Extension: add nested replies (comments on comments), reaction types (like, love, laugh), or a notification when someone comments on your post.

## README Guidance

The project repo's README should include a description, screenshots showing posts with
likes and comments, tech stack, environment variables, and setup instructions.
