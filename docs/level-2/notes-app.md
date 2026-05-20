# Notes App

> A responsive note-taking app with Markdown rendering (react-markdown + remark-gfm), tagging system, auto-save, and Zustand persistence.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://notes-web-apppp.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/notes-web-app)

---

## Purpose

This project teaches you to build a content creation tool with live Markdown preview.
Notes are written in Markdown and rendered as rich HTML in real-time. Combined with a
tagging system and auto-save, it's a productivity tool you might actually use daily.
It introduces the pattern of separating input format (Markdown) from display format (HTML).

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS
- **State:** Zustand with localStorage persistence
- **Markdown:** react-markdown + remark-gfm (GitHub Flavored Markdown)
- **Forms:** React Hook Form + Zod
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Build the note model in Zustand.** Note: `{ id, title, content (Markdown), tags: string[], createdAt, updatedAt }`. Persisted to localStorage. CRUD actions.

2. **Build the Markdown editor.** A split-pane view: textarea on the left (raw Markdown input), rendered preview on the right (react-markdown output). Live preview updates as you type.

3. **Configure react-markdown + remark-gfm.** GFM adds: tables, strikethrough, task lists, and autolinks. These render correctly in the preview without any extra work.

4. **Implement the tagging system.** Add/remove tags per note. Tag input with autocomplete from existing tags. Filter notes by tag in the sidebar. Color-coded tag badges.

5. **Add auto-save.** Debounce content changes (500ms). On each debounced trigger, update the note in Zustand (which persists to localStorage). Show "saved" indicator. No manual save button needed.

6. **Build the note list sidebar.** List all notes with title and date. Search across titles and content. Sort by recently modified. Click to load in editor.

7. **Deploy on Netlify.** Static site. All data lives in localStorage — no backend needed.

## Tips

- react-markdown renders Markdown to React components (not raw HTML). This is safer than `dangerouslySetInnerHTML` — no XSS risk from Markdown content.
- Auto-save with debounce: use a `useEffect` with a timer. On every content change, reset the timer. When the timer fires (no changes for 500ms), persist. This prevents saving on every keystroke.
- Extension: add note folders/notebooks, Markdown toolbar buttons, export as PDF, or sync across devices (would need a backend).
