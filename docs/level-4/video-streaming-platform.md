# Video Streaming Platform

> A fullstack video platform with upload, streaming, basic transcoding, and a content library.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://video-streaming-platformm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/video-streaming-platform)

---

## Purpose

Video is the most complex media type on the web. This project teaches you to handle large
file uploads, stream video with range requests (so users can seek), and manage a media library
with metadata. It introduces concepts like chunked uploads, HLS streaming, and the difference
between downloading and streaming — skills relevant to any media-heavy platform.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT
- **Key libraries / tools:** Multer (upload), ffmpeg (transcoding), HTML5 Video API, Cloudinary or local storage
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Build video upload.** Large file upload with progress indicator. Use Multer with a size limit (100MB+). Store videos in cloud storage (Cloudinary) or local disk. Save metadata to MongoDB: `{ title, description, filename, url, duration, thumbnail, author }`.
2. **Implement video streaming.** Serve video with HTTP Range requests (`206 Partial Content`). This enables seeking — the browser requests only the bytes it needs. Set proper `Content-Range` and `Accept-Ranges` headers.
3. **Generate thumbnails.** On upload, use ffmpeg to extract a frame (at the 5-second mark) as the video thumbnail. Store it alongside the video. Show thumbnails in the video library grid.
4. **Build the video library.** A grid of video cards with thumbnail, title, duration, author, and view count. Pagination and search. Category/tag filtering.
5. **Build the video player page.** A custom video player (HTML5 `<video>` with custom controls) or a library like Video.js. Show title, description, author info, and related videos sidebar.
6. **Add view tracking and engagement.** Increment view count on play (debounce to avoid counting refreshes). Add like/dislike. Show view count and engagement on each video.
7. **Build the creator dashboard.** Users can manage their uploaded videos: view analytics (views, likes), edit metadata, delete videos. Show upload progress during new uploads.

## Deployment

Backend on Render. For video storage, use Cloudinary's video API or a cloud storage bucket.
Render's disk is ephemeral. Frontend on Netlify with `VITE_API_URL`.

## Tips

- Range requests are what make video seeking work. Without them, the browser must download the entire file before playing. Always support `Range` headers for media endpoints.
- ffmpeg is powerful but heavy. For thumbnail generation, use the simplest command: `ffmpeg -i input.mp4 -ss 00:00:05 -vframes 1 thumbnail.jpg`. Install it on your server or use a cloud transcoding service.
- Extension: add video quality selection (360p, 720p, 1080p with HLS), comments on videos, playlists, or live streaming with WebRTC.

## README Guidance

The project repo's README should include a description, screenshots of video library and
player, tech stack, ffmpeg setup instructions, environment variables, and local setup steps.
