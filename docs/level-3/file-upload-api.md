# File Upload API

> A file upload service with Multer multipart handling, file type validation, size limits, and storage management.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://file-upload-api-bnql.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/file-upload-api)

---

## Purpose

File uploads are one of the trickiest parts of web development — multipart form data,
binary streams, validation, storage, and serving. This project teaches you to handle all of
it: configure Multer for multipart parsing, validate file types and sizes, store files (local
disk or cloud), generate unique filenames, and serve them back. Every app with user avatars,
document uploads, or media needs this.

## Tech Stack

- **Frontend:** none (API only)
- **Backend:** Node.js, Express
- **Database:** MongoDB (file metadata)
- **Key libraries / tools:** Multer (multipart parsing), sharp (image processing, optional), uuid (filenames)
- **Deployment:** Render.com

## Build Steps

1. **Configure Multer.** Set up Multer with disk storage: custom destination folder, unique filename generation (uuid + original extension). Set file size limit (e.g. 5MB) and create a file filter that accepts only allowed MIME types.
2. **Build the upload endpoint.** `POST /upload` accepts `multipart/form-data` with a file field. On success, return file metadata: `{ id, originalName, filename, mimeType, size, url, uploadedAt }`. Support single and multiple file uploads.
3. **Validate file types.** In the Multer file filter, check `file.mimetype` against an allowlist (images: jpeg/png/gif/webp, documents: pdf/doc). Reject disallowed types with a clear error message before writing to disk.
4. **Store metadata in DB.** Save file info (original name, stored filename, size, MIME type, upload date) to MongoDB. This lets you list, search, and delete files via the API without scanning the filesystem.
5. **Serve uploaded files.** `GET /files/:filename` serves the file from disk using `res.sendFile()` or Express static middleware. Set proper `Content-Type` headers. Support inline display (images) and download (documents) via `Content-Disposition`.
6. **Add file management.** `GET /files` lists all uploaded files (with pagination). `DELETE /files/:id` removes the file from both disk and database. Handle the case where the DB record exists but the file doesn't (or vice versa).
7. **Handle errors robustly.** Multer errors (file too large, wrong type) need custom error messages. Disk full errors, permission errors, and partial upload failures must all return meaningful responses.

## Deployment

Deploy on Render.com. Uploaded files are stored on Render's ephemeral disk (they may be lost
on redeploy). For production, use cloud storage (S3, Cloudinary). Set `MONGODB_URI` and
`MAX_FILE_SIZE` as environment variables.

## Tips

- Render's disk is ephemeral — files disappear on redeploy. For a persistent demo, use Cloudinary's free tier or AWS S3. For this learning project, ephemeral storage is fine.
- Always generate unique filenames server-side (uuid). Never trust user-provided filenames — they can contain path traversal attacks (`../../etc/passwd`) or overwrite existing files.
- Extension: add image resizing with Sharp, thumbnail generation, virus scanning with ClamAV, or presigned upload URLs for direct-to-S3 uploads.

## README Guidance

The project repo's README should include a description, endpoint table with multipart examples
(curl commands), file type/size limits, environment variables, and local setup steps.
