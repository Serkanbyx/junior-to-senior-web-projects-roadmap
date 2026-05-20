# Chat UI

> A real-time messaging interface with conversation management, typing indicators, and component composition.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://chat-uiii.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/chat-ui)

---

## Purpose

This project teaches you to build a complex, interactive UI with many moving parts that must
stay in sync: conversation list, message thread, input field, typing indicators, and read
receipts. It's a masterclass in component composition — breaking a complex interface into
small, focused components that communicate through shared state. The patterns here transfer
directly to any real-time collaborative app.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** none (simulated with mock data and timers)
- **Database:** none (state in Zustand)
- **Key libraries / tools:** Zustand (state management)
- **Deployment:** Netlify

## Build Steps

1. **Model the data.** Define types: `Conversation { id, participants, lastMessage, unreadCount }`, `Message { id, conversationId, senderId, text, timestamp, status: 'sent' | 'delivered' | 'read' }`, `User { id, name, avatar, isOnline }`. Seed with realistic mock data.
2. **Build the conversation list.** A sidebar showing all conversations sorted by most recent message. Each item shows the other participant's avatar, name, last message preview (truncated), timestamp, and unread badge. Highlight the active conversation.
3. **Render the message thread.** Display messages in chronological order with sender alignment (own messages right, others left). Group consecutive messages from the same sender. Show timestamps between message groups. Auto-scroll to the bottom on new messages.
4. **Build the message input.** A text input with send button (and Enter key submit). Show a typing indicator ("User is typing...") when the input is focused and has content. Simulate receiving typing indicators from others using `setTimeout`.
5. **Add message status indicators.** Show sent/delivered/read status with checkmark icons on your own messages. Simulate status updates: sent → delivered (after 1s) → read (after 3s). This teaches you to update existing items in an array reactively.
6. **Implement conversation management.** Create new conversation, search/filter conversations, mark as read (clear unread badge on open), and delete conversation. Handle the empty state when no conversation is selected.
7. **Make it responsive.** On mobile, show only the conversation list by default. Tapping a conversation navigates to the full-screen message view with a back button. On desktop, show both panels side by side.

## Deployment

Deploy on Netlify as a static app. No backend needed — all "real-time" behavior is simulated
with timers and mock data. No environment variables required.

## Tips

- Auto-scrolling to the bottom should only happen when the user is already at the bottom. If they've scrolled up to read history, don't force them back down — show a "new messages" indicator instead.
- Component composition is the key: `ChatLayout` → `ConversationList` + `MessageThread` → `MessageBubble` + `MessageInput`. Keep each component focused on one responsibility.
- Extension: add image/file sharing (preview URLs), emoji picker, message reactions, or connect to a real WebSocket backend (the Level 3 Chat App Backend project).

## README Guidance

The project repo's README should include a short description, a screenshot showing the
split-panel chat interface, the live demo link, tech stack, features (typing indicators,
read receipts, responsive), and local dev instructions.
