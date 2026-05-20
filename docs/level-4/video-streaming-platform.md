# Video Streaming Platform

> A fullstack video platform with FFmpeg HLS transcoding, adaptive streaming, TypeScript monorepo with shared Zod schemas, and brutalist glitch-aesthetic UI.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://video-streaming-platformm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/video-streaming-platform)

---

## Purpose

Video is the most complex media type on the web. This project teaches you real video
engineering: upload raw videos, transcode them server-side with FFmpeg into HLS (HTTP Live
Streaming) format, and stream adaptively to the client with HLS.js. The TypeScript monorepo
with shared Zod schemas ensures end-to-end type safety. This is the architecture behind
YouTube, Twitch, and Netflix.

## Tech Stack

- **Frontend:** React 19, TypeScript, Vite 6, Tailwind CSS 4, React Router 7, TanStack React Query
- **Backend:** Node.js, Express 5, TypeScript, MongoDB (Mongoose 8), Socket.io 4
- **Video:** FFmpeg (fluent-ffmpeg) for HLS transcoding, HLS.js + React Player for playback
- **Monorepo:** Shared Zod schemas (`shared/` package) for end-to-end validation
- **Auth:** JWT + bcryptjs
- **File storage:** Cloudinary + Multer + Streamifier
- **Security:** Helmet, express-rate-limit, express-mongo-sanitize
- **API docs:** Swagger
- **Deployment:** Fly.io (backend, Dockerized) + Netlify (frontend)

## Build Steps

1. **Set up the TypeScript monorepo.** Three packages: `client/`, `server/`, and `shared/`. The shared package exports Zod schemas for validation — same schema validates on both client (form submission) and server (API input). `tsconfig.base.json` at root with project references.

2. **Build video upload with progress.** Large file upload via Multer. Show upload progress on the frontend. Store the raw file temporarily. Save metadata to MongoDB: `{ title, description, filename, url, duration, thumbnail, author, views }`. File size limits and MIME type validation.

3. **Implement FFmpeg HLS transcoding.** After upload, run `fluent-ffmpeg` to convert the raw video into HLS format (`.m3u8` playlist + `.ts` segments). This enables adaptive bitrate streaming — the player automatically switches quality based on network speed. Store transcoded output.

4. **Build the HLS video player.** Use `hls.js` with React Player on the frontend. HLS.js handles the `.m3u8` manifest, fetches segments on demand, and adapts quality. The player supports seeking, fullscreen, and quality switching — all built into the HLS protocol.

5. **Build the video library.** Grid of video cards with thumbnails (extracted from video or auto-generated), title, duration, view count, and author. Pagination and search. Category filtering. TanStack Query handles caching and background refetching.

6. **Build creator features.** Upload management dashboard: view own videos with analytics (views, likes). Edit video metadata. Delete videos (cascade deletes transcoded files). Video management CRUD with creator-only authorization.

7. **Add shared Zod schemas and deploy.** Zod schemas in `shared/`: validate video upload form on client before sending, validate same data on server. If schemas change, TypeScript errors appear in both packages immediately. Deploy: Dockerized backend on Fly.io, frontend on Netlify.

## Deployment

Backend Dockerized and deployed on Fly.io (with `fly.toml` and `Dockerfile`). FFmpeg must
be available in the Docker image. Frontend on Netlify. Cloudinary for file storage.

## Tips

- HLS is the industry standard for video streaming. The key insight: instead of serving one huge file, you serve a playlist of small segments (2-10 seconds each). The client fetches segments on demand, enabling seeking without downloading the entire video.
- The shared Zod schema pattern eliminates validation drift. When you change a field (e.g., max title length), the change propagates to both frontend validation and backend validation from a single source of truth.
- FFmpeg in production: use a Docker image that includes FFmpeg (e.g., `node:18` + `apt-get install ffmpeg`). Process transcoding asynchronously — don't block the upload response. Show "processing" status until transcoding completes.
- Extension: add multiple quality levels (360p, 720p, 1080p), live streaming with WebRTC, video comments with timestamps, or content recommendation based on viewing history.

## README Guidance

The project repo's README should include a description, screenshots of the video library
and player, architecture diagram (upload → transcode → stream), tech stack, Docker setup,
environment variables, and local development instructions.
