# Online Code Editor

> A fullstack collaborative code editor with Monaco editor, real-time sync, and code execution.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://online-code-editorr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/online-code-editor)

---

## Purpose

This is one of the most technically impressive Level 4 projects. It combines the Monaco editor
(the engine behind VS Code), real-time collaboration via WebSockets, and server-side code
execution in sandboxed environments. It teaches you to integrate a complex third-party
component, handle operational transforms or CRDT for collaboration, and safely execute
untrusted code.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, Socket.io, MongoDB
- **Auth:** JWT
- **Key libraries / tools:** Monaco Editor (@monaco-editor/react), Socket.io, Docker (sandboxed execution)
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Integrate Monaco Editor.** Install `@monaco-editor/react`. Configure it with language support (JavaScript, TypeScript, Python), theme (dark/light), and options (minimap, line numbers, word wrap). Handle value changes.
2. **Build file/project management.** Create, save, rename, and delete files in MongoDB. A file explorer sidebar showing the project structure. Load file content into the editor on select.
3. **Implement real-time collaboration.** Use Socket.io to sync editor changes between users. On each keystroke, emit the change (position + text). Apply incoming changes from other users to the local editor. Handle cursor positions.
4. **Add code execution.** A "Run" button that sends the code to the backend. The backend executes it in a sandboxed environment (Docker container or Node's `vm` module with timeout). Return stdout/stderr to the client.
5. **Build the output panel.** A terminal-like panel below the editor showing execution output. Support for stdin (basic input prompts). Clear output on new run. Show execution time and memory usage.
6. **Add sharing and sessions.** Generate shareable links for collaborative editing sessions. Anyone with the link can join and see real-time changes. Show connected users with their cursor colors.
7. **Build project management.** A dashboard showing saved projects. Fork (duplicate) other users' public projects. Templates for quick start (blank, HTML boilerplate, Node starter).

## Deployment

Backend on Render (Socket.io supported). Code execution requires Docker on the server —
for demo purposes, use Node's `vm` module with strict timeouts. Frontend on Netlify.

## Tips

- Never execute user code directly with `eval()` or `child_process.exec()` without sandboxing. Use Docker containers with CPU/memory limits and network isolation, or at minimum Node's `vm` module with a timeout.
- Monaco Editor is large (~2MB). Use dynamic import (`React.lazy`) and show a loading skeleton while it loads. This prevents blocking the initial page render.
- Extension: add language server protocol (LSP) for autocomplete, git integration, deployment from the editor, or AI code suggestions.

## README Guidance

The project repo's README should include a description, screenshots of the editor with
collaboration, tech stack, architecture diagram, security notes about sandboxing, environment
variables, and setup instructions.
