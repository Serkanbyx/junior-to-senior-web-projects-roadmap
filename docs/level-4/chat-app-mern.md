# Chat App MERN

> A fullstack real-time chat app with Socket.io messaging, notifications, and online presence.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://chat-app-mernn.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/chat-app-mern)

---

## Purpose

This is the Level 3 Chat Backend brought to life with a full React frontend. It teaches you
to integrate Socket.io on the client side, manage real-time state updates alongside REST data,
and build a production chat interface. The combination of HTTP (for history, auth) and
WebSocket (for real-time events) is the architecture used by Slack, Discord, and WhatsApp Web.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, Socket.io, MongoDB
- **Auth:** JWT (for both HTTP and WebSocket)
- **Key libraries / tools:** socket.io-client, Zustand, React Router, Axios
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Set up Socket.io client.** Connect to the server on login (pass JWT as auth). Listen for events: `new-message`, `user-online`, `user-offline`, `typing`. Disconnect on logout.
2. **Build the conversation list.** Fetch conversations from REST API on load. Listen for real-time updates (new message in any conversation) to reorder the list. Show unread count badges.
3. **Build the message view.** On conversation select, fetch message history (paginated) from REST. New messages arrive via Socket.io and append to the list. Auto-scroll to bottom on new messages.
4. **Implement sending messages.** On send, emit via Socket.io (for real-time delivery) AND save via REST (for persistence). Show the message immediately in the UI (optimistic) with a "sending" indicator.
5. **Add typing indicators.** Emit `typing` events (debounced) when the user types. Show "User is typing..." in the active conversation. Clear after 3 seconds of no typing.
6. **Build online presence.** Track connected users. Show green dots next to online users. Update in real-time as users connect/disconnect. Show "last seen" for offline users.
7. **Add notifications.** Browser notifications (via Notification API) for new messages when the tab is not focused. In-app notification badges. Sound effect on new message.

## Deployment

Backend on Render (Socket.io works on Render natively). Frontend on Netlify. Set
`MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL` on backend. Set `VITE_API_URL` and
`VITE_SOCKET_URL` on frontend.

## Tips

- The dual HTTP + WebSocket architecture: use REST for data that needs persistence and reliability (message history, user profile). Use WebSocket for ephemeral real-time events (typing, presence, new message notifications).
- Socket.io reconnects automatically. But your app must re-join rooms and re-sync state after reconnection. Listen to the `connect` event and re-initialize.
- Extension: add group chats, file/image sharing, message reactions, voice messages, or end-to-end encryption.

## README Guidance

The project repo's README should include a description, screenshots of the chat interface,
architecture diagram (HTTP + WebSocket), tech stack, environment variables, and setup instructions.
