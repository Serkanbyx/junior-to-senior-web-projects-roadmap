# Pagination & Search API

> A RESTful API demonstrating server-side pagination, regex-powered search, category filtering, and flexible sorting over SQLite.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://pagination-search-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/pagination-search-api)

---

## Purpose

Every real API needs pagination (you can't return 10,000 records at once) and search
(users need to find things). This project focuses entirely on these two patterns: building
a robust pagination system with metadata, implementing SQL-level search with LIKE/regex,
and combining filters, sorting, and pagination in a single flexible endpoint.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** SQLite (better-sqlite3)
- **Validation:** express-validator
- **Security:** Helmet 8
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Seed the database.** Create a products/items table with enough data to paginate (50-100 records). Include varied categories, prices, and descriptions to make filtering meaningful. Seed script runs on first start.

2. **Build basic pagination.** Query params: `?page=1&limit=10`. SQL: `LIMIT ? OFFSET ?` where offset = (page - 1) * limit. Count total records with a separate `SELECT COUNT(*)`. Return: `{ data, pagination: { page, limit, total, totalPages, hasNext, hasPrev } }`.

3. **Implement search.** `?q=keyword` searches across title and description using `WHERE title LIKE ? OR description LIKE ?` with `%keyword%` wildcards. Case-insensitive with `COLLATE NOCASE`. Search combines with pagination — page through search results.

4. **Add category filtering.** `?category=electronics` adds a `WHERE category = ?` condition. Multiple filters combine with AND. Available categories discoverable via a dedicated endpoint: `GET /categories`.

5. **Implement flexible sorting.** `?sort=price&order=asc` or `?sort=-price` (minus prefix = descending). Whitelist valid sort columns to prevent SQL injection. Default sort: newest first. Sorting works with all other filters.

6. **Combine everything.** A single endpoint handles all combinations: `GET /items?q=phone&category=electronics&sort=price&order=asc&page=2&limit=5`. Build the SQL query dynamically from present params. Missing params use defaults.

7. **Document the query interface.** Swagger documents every query param with its type, default, and allowed values. Show example responses with pagination metadata.

## Deployment

Deploy on Render.com. SQLite database seeds automatically on first run. No external
services required.

## Tips

- Always validate and whitelist sort columns. If you blindly interpolate `req.query.sort` into SQL, it's an injection vector. Maintain an array of allowed columns and reject anything not in the list.
- Return `hasNext` and `hasPrev` booleans in pagination metadata — they let the frontend show/hide Next/Previous buttons without calculating from page numbers.
- Extension: add cursor-based pagination (more efficient for real-time data), full-text search with ranking, or faceted filtering (show count per category).

## README Guidance

The project repo's README should include a description, API endpoint with all query params
documented, example responses with pagination, tech stack, and setup instructions.
