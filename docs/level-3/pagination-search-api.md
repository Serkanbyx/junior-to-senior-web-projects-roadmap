# Pagination + Search API

> A REST API demonstrating cursor/offset pagination, full-text search, compound filtering, and database indexing.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://pagination-search-api.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/pagination-search-api)

---

## Purpose

Every production API needs pagination and search. This project teaches you to handle large
datasets efficiently: offset-based and cursor-based pagination, text search with relevance
scoring, compound query building, and database indexing for performance. These patterns apply
to every list endpoint you'll ever build — users, products, posts, logs.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (Mongoose)
- **Key libraries / tools:** Mongoose text indexes, query builders, dotenv
- **Deployment:** Render.com

## Build Steps

1. **Seed the database.** Create a collection with 500+ documents (e.g. products or articles) with varied fields: title, description, category, price, rating, createdAt. Use a seed script that generates realistic data.
2. **Implement offset pagination.** Support `?page=2&limit=20`. Calculate `skip = (page - 1) * limit`. Return metadata: `{ data, total, page, limit, totalPages, hasNext, hasPrev }`. This is the most common pagination pattern.
3. **Add cursor-based pagination.** Support `?cursor=<lastId>&limit=20`. Query with `{ _id: { $gt: cursor } }`. Return `{ data, nextCursor }`. Explain in the response which method is in use. Cursor pagination is faster for large datasets.
4. **Build text search.** Create a MongoDB text index on `title` and `description`. Support `?q=search+term`. Use `$text: { $search }` with `$meta: "textScore"` for relevance sorting. Return results ranked by relevance.
5. **Add compound filtering.** Support `?category=electronics&minPrice=10&maxPrice=100&minRating=4`. Build the query object dynamically — only include filters that are present in the query params.
6. **Implement sorting.** Support `?sort=price,-rating` (price ascending, rating descending). Parse the sort string into a Mongoose sort object. Default to relevance score when searching, createdAt otherwise.
7. **Add database indexes.** Create indexes on commonly filtered/sorted fields (category, price, rating). Create a compound index for common query patterns. Measure query performance with `.explain()` before and after.

## Deployment

Deploy on Render.com. Set `MONGODB_URI`. Run the seed script once after first deploy to
populate the database. Consider using MongoDB Atlas's free tier for a hosted database.

## Tips

- Offset pagination is simple but degrades on large datasets (`skip(10000)` is slow). Cursor pagination scales but doesn't support "jump to page 5." Offer both and let the client choose.
- Always set a maximum limit (e.g. 100) to prevent clients from requesting `?limit=999999` and overloading your database.
- Extension: add fuzzy search (MongoDB Atlas Search or Fuse.js), autocomplete suggestions, or faceted search (counts per category).

## README Guidance

The project repo's README should include a description, endpoint documentation with all
supported query params, pagination response format examples, and local setup steps including
the seed command.
