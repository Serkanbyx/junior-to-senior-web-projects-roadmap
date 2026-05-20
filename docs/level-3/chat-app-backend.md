# Chat App Backend

> A real-time chat backend with WebSocket communication, room management, user presence, and message persistence.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://chat-app-backend-zww3.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/chat-app-backend)

---

## Purpose

This is the capstone of Level 3 — it introduces real-time communication with WebSockets,
a fundamentally different paradigm from REST. Instead of request-response, you have persistent
bidirectional connections where the server can push data to clients. You'll learn Socket.io
event handling, room-based broadcasting, presence tracking, and the challenge of combining
real-time events with database persistence.

## Tech Stack

- **Frontend:** none (WebSocket API only)
- **Backend:** Node.js, Express, Socket.io
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Socket.io (WebSocket abstraction), JWT (auth for socket connections)
- **Deployment:** Render.com

## Build Steps

1. **Set up Socket.io.** Create an HTTP server with Express, then attach Socket.io to it. Configure CORS for the socket server. Handle the `connection` event — this fires when a client connects via WebSocket.
2. **Authenticate socket connections.** Use Socket.io middleware to verify a JWT token passed during connection (`io.use()`). Reject unauthenticated connections. Attach the user info to the socket object for use in event handlers.
3. **Implement rooms.** Create a room system: `socket.join(roomId)` adds a user to a room. Emit events only to room members with `io.to(roomId).emit()`. Build events: `join-room`, `leave-room`, `list-rooms`.
4. **Handle messages.** On `send-message` event, validate the message, save to MongoDB (`{ roomId, userId, text, timestamp }`), then broadcast to the room with `io.to(roomId).emit('new-message', message)`. The sender also receives it (for confirmation).
5. **Track user presence.** Maintain an in-memory map of connected users per room. On connect: add to map, broadcast "user joined." On disconnect: remove from map, broadcast "user left." Emit the current online users list periodically.
6. **Add typing indicators.** On `typing-start` event, broadcast `user-typing` to the room (exclude sender). On `typing-stop`, broadcast `user-stopped-typing`. Use debouncing client-side to avoid spamming these events.
7. **Persist and load history.** On room join, send the last 50 messages from MongoDB. New messages are saved to DB in real-time. Support pagination for loading older messages (`load-more` event).

## Deployment

Deploy on Render.com as a Web Service. Socket.io works over HTTP/HTTPS — Render supports
WebSocket connections natively. Set `MONGODB_URI`, `JWT_SECRET`, and `CLIENT_URL` (CORS origin).

## Tips

- Socket.io is NOT pure WebSockets — it adds automatic reconnection, room support, and fallback to polling. This makes it much more practical than raw `ws` for production apps.
- Don't store presence in the database — it changes too frequently. Keep it in memory (a Map). If you need cross-server presence (multiple instances), use Redis pub/sub.
- Extension: add direct messages (1-to-1 rooms), message reactions, file sharing via socket events, or read receipts (last-read timestamp per user per room).

## README Guidance

The project repo's README should include a description, Socket.io event table (event name,
payload, direction), architecture diagram, environment variables, and local setup steps with
a socket testing tool recommendation (e.g. Postman WebSocket or socket.io-client CLI).
