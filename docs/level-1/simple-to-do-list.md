# Simple To-Do List

> A single-page to-do app with full CRUD, drag-and-drop reordering, filtering, and LocalStorage persistence.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://simple-to-do-listt.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/simple-to-do-list)

---

## Purpose

The to-do list is the "hello world" of application state. It covers all four CRUD operations
(create, read, update, delete) in a single-page context, teaches you to keep the DOM in sync
with a data array, and introduces persistence without a backend. Drag-and-drop adds a
non-trivial UX interaction that you'll use in dashboards and kanban boards later. If you can
build this cleanly, you understand the data → render cycle that every framework automates.

## Tech Stack

- **Frontend:** HTML, CSS (dark theme), vanilla JavaScript
- **Backend:** none
- **Database:** LocalStorage
- **Key libraries / tools:** HTML Drag and Drop API, no external dependencies
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Model the data.** Each to-do is an object: `{ id, text, completed, createdAt }`. Store all to-dos in an array. Generate unique IDs with `Date.now()` or `crypto.randomUUID()`.
2. **Render the list.** Write a single `renderTodos()` function that clears the list container and rebuilds it from the array. Every state change calls this function — this "full re-render" pattern is simple and bug-free for small lists.
3. **Create.** An input field + submit button (or Enter key). On submit, push a new to-do object to the array, persist, and re-render. Validate that the text isn't empty.
4. **Update and delete.** Each to-do item gets a checkbox (toggle `completed`), an edit button (inline editing or prompt), and a delete button. On any action, mutate the array, persist, re-render.
5. **Filter.** Add "All / Active / Completed" filter buttons. Rather than modifying the source array, filter it in the render function: `todos.filter(t => ...)`. The source array stays intact.
6. **Drag and drop reordering.** Make each to-do item `draggable`. On `dragstart`, store the dragged item's index. On `drop`, splice the item out of its old position and insert it at the drop target's position. Persist the new order.
7. **Persist with LocalStorage.** On every state mutation, call `localStorage.setItem('todos', JSON.stringify(todos))`. On page load, hydrate from storage: `JSON.parse(localStorage.getItem('todos')) || []`.

## Deployment

Push to GitHub and deploy on Netlify. No build step, no environment variables.
Static files only.

## Tips

- The HTML Drag and Drop API is verbose but powerful. The key events are `dragstart`, `dragover` (must call `e.preventDefault()` to allow drop), and `drop`. Without the `preventDefault` in `dragover`, drop won't fire.
- Don't store DOM references — always re-derive the UI from the data array. This eliminates an entire class of sync bugs.
- Extension: add categories/tags, due dates, or a "clear completed" bulk action.

## README Guidance

The project repo's README should include a short description, a GIF showing drag-and-drop and
filtering, the live demo link, a features list (CRUD, drag-and-drop, filters, persistence),
and a one-step local run instruction.
