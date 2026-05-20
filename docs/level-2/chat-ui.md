# Chat UI

> A modern chat interface with Radix UI primitives (shadcn/ui), conversation management, typing indicators, and Zustand state.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://chat-uiii.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/chat-ui)

---

## Purpose

This is a frontend-only chat UI — no real-time backend, but the complete interface for one.
It teaches complex component composition (message bubbles, conversation list, input bar),
extensive use of Radix UI primitives for accessibility, and state management for a deeply
nested UI. When you add Socket.io in Level 4, this UI is ready to connect.

## Tech Stack

- **Framework:** React 19, TypeScript, Vite
- **Styling:** Tailwind CSS v4, tailwindcss-animate, class-variance-authority, clsx, tailwind-merge
- **State:** Zustand
- **UI Components:** Radix UI (avatar, dialog, dropdown-menu, label, popover, scroll-area, separator, tooltip) — shadcn/ui pattern
- **Forms:** React Hook Form + Zod
- **Routing:** React Router
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Build the layout.** Three-panel chat layout: conversation list (sidebar), message area (main), and user info (optional right panel). Responsive: sidebar collapses on mobile.

2. **Build the conversation list.** Radix ScrollArea for smooth scrolling. Each conversation shows: avatar (Radix Avatar with fallback), name, last message preview, timestamp, and unread badge. Click to select.

3. **Build the message area.** Messages rendered as bubbles (sent = right, received = left). Auto-scroll to bottom on new messages. Show timestamps between message groups. Radix ScrollArea for the message container.

4. **Build the message input.** Input bar with text field, send button, and emoji picker (Radix Popover). React Hook Form handles the input. Clear on send. Show typing indicator when simulated.

5. **Build interactive elements.** Radix DropdownMenu on messages (reply, copy, delete). Radix Tooltip on action buttons. Radix Dialog for creating new conversations or viewing user profiles.

6. **Simulate chat behavior.** Mock data with conversations and messages. Simulate typing indicators (random delays). Simulate receiving messages after sending. All state in Zustand.

7. **Polish with animations.** tailwindcss-animate for message entrance animations, skeleton loaders, and transition effects. CVA for consistent message bubble variants.

## Tips

- shadcn/ui pattern: Radix UI provides behavior and accessibility, you provide all styling with Tailwind. This gives you professional-grade accessibility (keyboard nav, focus management, ARIA) without fighting pre-built styles.
- The message grouping logic: group consecutive messages from the same sender within a time window (e.g., 5 minutes). Only show avatar and timestamp on the first message of each group.
- Extension: connect to Socket.io backend (Level 4 chat-app-mern), add file sharing UI, voice message recording UI, or message search.
