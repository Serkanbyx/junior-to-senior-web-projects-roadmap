# File Upload API

> A secure REST API for file uploads with type/size validation, dual storage (local disk + Cloudinary), and interactive Swagger documentation.

**Level:** 3 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://file-upload-api-gyrf.onrender.com/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/file-upload-api)

---

## Purpose

File uploads are tricky — you need to handle multipart form data, validate file types
(prevent executable uploads), enforce size limits (prevent disk exhaustion), and choose
a storage strategy (local vs cloud). This project implements both local disk and Cloudinary
storage, teaching you the patterns for any file upload scenario.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** None (file metadata in response only)
- **File handling:** Multer (multipart parsing + local storage)
- **Cloud storage:** Cloudinary + multer-storage-cloudinary
- **IDs:** uuid
- **Security:** Helmet 8, express-rate-limit, CORS
- **Documentation:** Swagger (swagger-jsdoc + swagger-ui-express)
- **Deployment:** Render.com

## Build Steps

1. **Configure Multer for local storage.** Set up Multer with disk storage: define destination directory, generate unique filenames with uuid, and configure size limits (5MB default). Multer parses multipart/form-data and makes the file available as `req.file`.

2. **Add file type validation.** Create a file filter function that checks MIME type. Allow only: images (jpeg, png, gif, webp) and documents (pdf, docx). Reject everything else with a clear error message. Never trust the file extension alone — check the MIME type.

3. **Configure Cloudinary storage.** Set up multer-storage-cloudinary as an alternative storage engine. Same Multer interface, but files go directly to Cloudinary instead of local disk. Return the Cloudinary URL in the response.

4. **Build upload endpoints.** `POST /upload/local` stores on disk, returns file path. `POST /upload/cloud` stores on Cloudinary, returns URL. Both validate type and size. Return metadata: filename, size, mimetype, url/path.

5. **Add size limit enforcement.** Multer's `limits: { fileSize: 5 * 1024 * 1024 }` rejects oversized files. Handle the `LIMIT_FILE_SIZE` error with a user-friendly message. Different endpoints can have different limits.

6. **Build a health check and docs.** `GET /health` for uptime monitoring. Swagger documents both upload endpoints with multipart/form-data request body, file field name, and response schema.

7. **Deploy to Render.** Set `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` for cloud uploads. Local uploads use Render's disk (ephemeral — files lost on redeploy).

## Deployment

Deploy on Render.com. Cloudinary credentials as env vars. Local storage is ephemeral on
Render — use Cloudinary for persistent file storage in production.

## Tips

- Never trust file extensions. A user can rename `malware.exe` to `image.jpg`. Always validate the MIME type (Content-Type header from Multer) and optionally use magic bytes (file signature) for deeper validation.
- Render's disk is ephemeral — files are lost on each deploy. This makes Cloudinary the correct production choice. Local disk is only useful for development or temporary processing.
- Extension: add image resizing (sharp library), multiple file upload, presigned URLs for direct-to-cloud upload, or file metadata storage in a database.

## README Guidance

The project repo's README should include a description, upload endpoint docs with curl
examples, supported file types, size limits, tech stack, and setup instructions.
