# Notes App

> A note-taking app with Markdown support, tagging system, auto-save, and full-text search.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://notes-web-apppp.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/notes-web-app)

---

## Purpose

This project teaches you to build a content-rich CRUD app with structured data relationships
(notes ↔ tags). You'll implement Markdown parsing, auto-save with debouncing, and a tagging
system that lets users organize content without rigid folders. The search feature introduces
client-side full-text filtering across multiple fields — title, body, and tags simultaneously.

## Tech Stack

- **Frontend:** React 18, TypeScript, Tailwind CSS
- **Backend:** none
- **Database:** LocalStorage (via Zustand persist)
- **Key libraries / tools:** Zustand, Markdown parser (marked or react-markdown)
- **Deployment:** Netlify

## Build Steps

1. **Model a note.** Define the shape: `{ id, title, body (markdown), tags: string[], createdAt, updatedAt }`. Create a Zustand store with CRUD operations and persist to LocalStorage.
2. **Build the notes list.** A sidebar showing all notes sorted by last updated. Each item shows the title, first line preview, date, and tag badges. Highlight the currently selected note.
3. **Implement the editor.** A split or togglable view: edit mode (textarea for raw Markdown) and preview mode (rendered Markdown). Use a Markdown library to parse and render. Support common syntax: headings, bold, italic, code blocks, links, lists.
4. **Add auto-save.** Debounce save operations (500ms after the user stops typing). Show a subtle "saving..." / "saved" indicator. Never lose work — persist on every meaningful change and on `beforeunload`.
5. **Build the tagging system.** An input that creates tags on Enter or comma. Display tags as colored badges on each note. Allow filtering the note list by tag (click a tag to filter). Support removing tags inline.
6. **Implement search.** A search bar that filters notes by matching the query against title, body content, and tags simultaneously. Highlight matching text in results. Use `String.includes()` or a simple scoring algorithm for relevance.
7. **Add note management.** Delete with confirmation, pin important notes to the top, duplicate a note, and export individual notes as `.md` files.

## Deployment

Deploy on Netlify as a static app. No backend or environment variables needed.
All persistence is client-side via LocalStorage.

## Tips

- Auto-save needs debouncing, not throttling. Debouncing waits until the user pauses; throttling would save mid-keystroke which can cause jank if serialization is slow.
- For Markdown rendering, `react-markdown` with `remark-gfm` gives you GitHub-Flavored Markdown (tables, task lists, strikethrough) with zero configuration.
- Extension: add note folders/categories, Markdown export as PDF, or sync across devices with a simple backend.

## README Guidance

The project repo's README should include a short description, screenshots showing the editor
and preview mode, the live demo link, tech stack, features list (Markdown, tags, auto-save,
search), and local dev instructions.
