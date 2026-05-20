# Chat App MERN

> A production-grade real-time chat platform with Socket.io, 1-1 and group messaging, presence tracking, read receipts, emoji reactions, and admin moderation.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://chat-app-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/chat-app-mern)

---

## Purpose

This project combines REST (for persistent data) with WebSocket (for real-time events) in
a single application. Messages are stored via REST for history but delivered via Socket.io
for instant delivery. It teaches the dual-protocol architecture used by Slack, Discord, and
WhatsApp Web — plus advanced real-time patterns like presence, typing indicators, and read receipts.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, TanStack React Query
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 8), Socket.io 4
- **Auth:** JWT (httpOnly cookies) + bcryptjs
- **Image uploads:** Cloudinary + Multer + Streamifier
- **Security:** Helmet 8, express-rate-limit, express-mongo-sanitize
- **API docs:** Swagger (swagger-jsdoc + swagger-ui-express)
- **UX:** Lucide React (icons), React Hot Toast, socket.io-client
- **Deployment:** Netlify (frontend) + Render (backend, with `render.yaml`)

## Build Steps

1. **Set up Socket.io with auth.** The server creates a Socket.io instance alongside Express. On connection, verify the JWT from the handshake. Authenticated socket connections join a room named after their userId for targeted message delivery.

2. **Build the conversation system.** Two types: 1-1 (direct message) and group. Conversation model stores participants and last message. On opening the chat, fetch conversation list via REST (TanStack Query), then listen for real-time updates via Socket.io to reorder when new messages arrive.

3. **Implement real-time messaging.** On send: save message to MongoDB via REST API, then emit via Socket.io to all participants. Recipients get the message instantly via socket event. TanStack Query invalidation keeps the cache consistent. Image messages via Cloudinary upload.

4. **Add presence tracking.** On socket connect, broadcast "user online" to relevant contacts. On disconnect, broadcast "user offline" with timestamp. Show green dots on online users. Display "last seen X minutes ago" for offline users.

5. **Implement typing indicators and read receipts.** Emit "typing" event (debounced) when user types in a conversation. Show "is typing..." to the other participant. Read receipts: when a user views a message, emit "read" event — sender sees double-check marks.

6. **Add emoji reactions.** Users can react to any message with emoji. Store reactions in the message document. Real-time broadcast to all conversation participants. Show reaction counts below messages.

7. **Build group chat and admin moderation.** Group creation with name and participants. Group admin can add/remove members. Platform admin panel for moderation: view reported messages, ban users, platform statistics. Role-based access on all moderation endpoints.

## Deployment

Backend on Render (Socket.io works natively on Render) with `render.yaml` for one-click
deploy. Set `MONGODB_URI`, `JWT_SECRET`, `CLOUDINARY_*`, `CLIENT_URL`. Frontend on Netlify
with `VITE_API_URL` and `VITE_SOCKET_URL`.

## Tips

- The dual REST + Socket.io architecture: REST for operations that need reliability and persistence (send message, upload image). Socket.io for ephemeral real-time events (typing, presence, new message notification). Never rely solely on Socket.io for critical data — sockets can disconnect.
- TanStack React Query + Socket.io: when a socket event arrives (new message), invalidate the relevant query. This keeps the REST-based data cache in sync with real-time events without manual state management.
- Extension: add voice messages (MediaRecorder API), message search, message pinning, disappearing messages, or end-to-end encryption.

## README Guidance

The project repo's README should include a description, screenshots of the chat interface
with presence and reactions, architecture diagram, tech stack, environment variables, and
setup instructions.
