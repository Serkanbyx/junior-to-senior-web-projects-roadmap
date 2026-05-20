# Chat App Backend

> A real-time chat backend with Socket.io WebSocket connections, room-based messaging, typing indicators, and MongoDB persistence.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://chat-app-backend-f4b8.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/chat-app-backend)

---

## Purpose

This is your introduction to real-time communication. HTTP is request-response (client
asks, server answers). WebSocket is bidirectional (both can send anytime). Socket.io adds
rooms, reconnection, and fallbacks on top of raw WebSocket. You'll learn event-driven
architecture, the Socket.io API, and how to persist messages while maintaining real-time delivery.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** MongoDB (Mongoose 8)
- **Real-time:** Socket.io 4
- **Security:** Helmet 8, express-rate-limit, express-mongo-sanitize
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Set up Socket.io alongside Express.** Create an HTTP server, attach both Express and Socket.io to it. Socket.io uses the same port — it upgrades HTTP connections to WebSocket. Configure CORS for Socket.io separately from Express CORS.

2. **Implement room-based messaging.** Users join rooms (chat channels). `socket.join(roomId)` adds a socket to a room. `io.to(roomId).emit('message', data)` broadcasts to all members. Users can be in multiple rooms simultaneously.

3. **Build the message flow.** Client emits 'send-message' → server receives → saves to MongoDB (for history) → broadcasts to room. Messages have: sender, room, content, timestamp. MongoDB gives you persistent history; Socket.io gives you real-time delivery.

4. **Add direct messaging.** 1-1 messages use a private room (sorted user IDs as room name: `room_user1_user2`). The same room/broadcast pattern works — the room just has two members instead of many.

5. **Implement typing indicators.** Client emits 'typing' when user types (debounced). Server broadcasts 'user-typing' to the room (excluding sender). Client shows "User is typing..." and clears after 3 seconds of no events.

6. **Add online/offline presence.** Track connected sockets. On connect: broadcast 'user-online' to relevant rooms. On disconnect: broadcast 'user-offline'. Maintain an in-memory set of online user IDs. Expose `GET /users/online` REST endpoint.

7. **Build REST endpoints for history.** `GET /messages/:roomId` (paginated message history from MongoDB), `GET /rooms` (list user's rooms). REST for data retrieval, Socket.io for real-time events — the two protocols complement each other.

## Deployment

Deploy on Render.com (Socket.io works natively). Set `MONGODB_URI`. Configure CORS
to allow the frontend origin for both Express and Socket.io.

## Tips

- The hybrid REST + Socket.io architecture: use REST for operations that need reliability (fetch history, create room). Use Socket.io for ephemeral real-time events (new message notification, typing, presence). REST is your backup — if a socket event is missed, the client can always fetch via REST.
- Socket.io rooms are the killer feature. Without rooms, you'd need to manually track which sockets should receive which messages. Rooms handle this automatically — `io.to(roomId).emit()` only reaches room members.
- Extension: add file/image sharing, message reactions, read receipts, message editing/deletion, or end-to-end encryption.

## README Guidance

The project repo's README should include a description, Socket.io events documentation,
REST endpoints, architecture diagram, tech stack, and setup instructions.
