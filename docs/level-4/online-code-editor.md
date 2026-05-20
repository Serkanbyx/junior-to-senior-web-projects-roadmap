# Online Code Editor

> CodeNest — a fullstack online code editor with real-time collaboration via Yjs CRDT, Monaco Editor, snippet sharing, and Socket.io sync.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://online-code-editorr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/online-code-editor)

---

## Purpose

This project integrates Monaco Editor (the engine behind VS Code) with real-time
collaborative editing via Yjs — a Conflict-free Replicated Data Type (CRDT) library.
CRDTs solve the hardest problem in collaboration: multiple users editing the same document
simultaneously without conflicts. This is the technology behind Google Docs and Figma's
multiplayer. You'll also build snippet sharing and code execution.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 8), Socket.io 4
- **Code Editor:** Monaco Editor (@monaco-editor/react 4, monaco-editor 0.52)
- **Collaboration:** Yjs 13 + y-protocols (CRDT-based real-time sync)
- **Auth:** JWT + bcryptjs
- **Real-time:** Socket.io (transport layer for Yjs sync)
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize
- **API docs:** Swagger
- **UX:** Lucide React, React Hot Toast, clsx
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Integrate Monaco Editor.** Install `@monaco-editor/react` and configure: multi-language support (JavaScript, TypeScript, Python, HTML, CSS), dark/light themes, minimap, line numbers, word wrap. Handle controlled value updates without cursor jumping.

2. **Set up Yjs for collaboration.** Create a Yjs document (`Y.Doc`) with a `Y.Text` type for the editor content. Connect it to Monaco via the Yjs Monaco binding. Every keystroke is a Yjs operation — automatically mergeable with concurrent edits from other users.

3. **Build the Socket.io sync provider.** Yjs needs a transport layer to sync between clients. Use Socket.io: when a user makes an edit, Yjs generates an update (binary diff). Emit it via Socket.io to the server, which broadcasts to all other clients in the same session. Apply incoming updates to the local Yjs doc — Monaco updates automatically.

4. **Build session/room management.** Users create collaborative sessions with unique IDs. Share the session link. Anyone with the link joins and sees real-time edits. Show connected users with their cursor positions and colors. Handle disconnect/reconnect gracefully.

5. **Build snippet CRUD.** Save code as reusable snippets to MongoDB: `{ title, language, code, author, public }`. Browse and fork public snippets. Snippet ownership and privacy controls. Load a snippet into the editor for editing or forking.

6. **Add code execution (sandboxed).** A "Run" button that sends code to the backend. Execute in a sandboxed environment (Node.js `vm` module with strict timeout). Return stdout/stderr to the client. Display in an output panel below the editor. Never use raw `eval()`.

7. **Build the user experience.** User authentication (JWT), saved snippets dashboard, fork other users' public snippets, syntax highlighting for 10+ languages, keyboard shortcuts (Cmd+S to save), and responsive layout with resizable panels.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL`. Frontend on Netlify
with `VITE_API_URL`. Monaco Editor is ~2MB — use dynamic import for initial load performance.

## Tips

- Yjs CRDTs are the key technology. Unlike Operational Transform (OT), CRDTs guarantee convergence without a central server ordering operations. Two users can edit offline, reconnect, and their documents will merge correctly — mathematically proven.
- Monaco Editor is heavy (~2MB). Load it lazily with React.lazy and show a code-themed skeleton while it loads. This prevents blocking the initial page render for users who haven't navigated to the editor yet.
- Socket.io as Yjs transport: Yjs updates are binary (`Uint8Array`). Send them as binary frames over Socket.io for efficiency. The server doesn't need to understand the content — it just broadcasts to room participants.
- Extension: add Language Server Protocol (LSP) for autocomplete, multiple file tabs, git integration, deployment from the editor, or AI code suggestions.

## README Guidance

The project repo's README should include a description, screenshots of collaborative editing
(multiple cursors), architecture diagram (Monaco ↔ Yjs ↔ Socket.io), tech stack, security
notes about sandboxed execution, and setup instructions.
