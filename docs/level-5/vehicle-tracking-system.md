# Vehicle Tracking System

> A full-stack fleet management system with live GPS tracking, geofencing, trip analytics, and three-tier RBAC — built with NestJS, React, PostgreSQL + PostGIS, and dual WebSocket channels.

**Level:** 5 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://vehicle-tracking-system-lemon.vercel.app) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/vehicle-tracking-system)

---

## Purpose

This project teaches you to build a production-grade IoT data platform. GPS devices emit
coordinates every few seconds — your system must ingest these streams at scale, process them
in real-time (geofence detection, speed alerts), store them efficiently (PostGIS spatial
queries), and visualize them on a live map. The dual WebSocket architecture (device ingest +
dashboard feed) is the same pattern used by Uber, fleet management companies, and logistics
platforms.

## Tech Stack

- **Frontend:** React 19, TanStack Router, TanStack Query, Zustand, Tailwind CSS 4, MapLibre GL JS
- **Backend:** NestJS 11, TypeORM, TypeScript
- **Database:** PostgreSQL 16 + PostGIS (geospatial extension)
- **Real-time:** Native WebSocket (`ws` library) with dual channel architecture
- **Auth:** JWT (access + refresh tokens), Passport, bcrypt, three-tier RBAC (viewer/manager/admin)
- **Monitoring:** Sentry, Pino structured logging, Better Stack/Logtail
- **File uploads:** Cloudinary + Multer
- **Security:** Helmet, @nestjs/throttler (rate limiting)
- **API docs:** @nestjs/swagger (OpenAPI)
- **Build:** Vite 7, Biome (linter/formatter)
- **Testing:** Vitest, Testing Library
- **Deployment:** Vercel (frontend) + Render/Railway (backend)

## Build Steps

1. **Set up the NestJS backend with modular architecture.** NestJS enforces clean separation: modules for vehicles, tracking, geofences, alerts, users, and auth. Each module has its own controller, service, and entity. TypeORM connects to PostgreSQL with PostGIS enabled for spatial data types.

2. **Build the dual WebSocket architecture.** Two separate WebSocket channels: one for **device ingest** (GPS trackers push coordinates to the server) and one for the **dashboard feed** (browser clients subscribe to live updates). This separation lets you scale ingest independently from the dashboard — devices and users never share a connection.

3. **Implement PostGIS geospatial queries.** Store coordinates as PostGIS `geometry(Point, 4326)`. Use spatial indexes for fast queries: `ST_DWithin` (find vehicles within X meters), `ST_Contains` (is vehicle inside geofence polygon?), `ST_Distance` (distance between points). These queries are O(log n) with spatial indexes vs O(n) without.

4. **Build geofence management.** Create polygon and circle geofences on the map (draw tools in MapLibre). Store boundaries as PostGIS geometries. On every GPS update, run `ST_Contains` to detect enter/exit events. Trigger alerts when vehicles cross geofence boundaries.

5. **Implement the smart alerting system.** Three alert types: speed violations (compare consecutive GPS points' calculated speed against limits), idle detection (no movement for X minutes), and geofence breaches. Store alerts with severity and acknowledgment status.

6. **Build the live map with MapLibre GL.** Render vehicle positions as markers on OpenFreeMap tiles. Smooth marker animation between GPS updates (interpolate position with `requestAnimationFrame`). Add heatmap visualization for high-traffic areas. History playback with a timeline slider that replays routes.

7. **Implement trip analytics and three-tier RBAC.** Automatic trip detection (moving → stopped → moving). Aggregate trip stats: distance (PostGIS `ST_Length`), duration, average speed, stops. RBAC: viewers see their assigned vehicles, managers manage a fleet, admins control everything including user management.

## Deployment

Frontend on Vercel, backend on Render/Railway. PostgreSQL with PostGIS on Supabase
(free tier supports PostGIS), Neon, or Railway. Set environment variables: database URL,
JWT secrets, Cloudinary credentials, Sentry DSN.

## Tips

- The dual WebSocket pattern is the key architecture decision. Device connections are long-lived, low-bandwidth (one GPS point every 3-5s). Dashboard connections are short-lived, high-bandwidth (all visible vehicles updating simultaneously). Different concerns, different channels.
- PostGIS is not optional — it's what makes geospatial queries possible at scale. Without spatial indexes, "find all vehicles in this polygon" requires a full table scan. With PostGIS, it's a B-tree lookup on the spatial index.
- NestJS modules map 1:1 to domain concepts. If you can name it (vehicles, geofences, alerts, trips), it's a module. This makes the codebase navigable even at 50+ files.
- Extension: add predictive ETA (based on historical route data and current speed), fuel consumption tracking, driver behavior scoring, or integration with traffic APIs for live congestion overlay.

## README Guidance

The project repo's README should include a description, screenshots of the live map with
vehicles and geofences, architecture diagram (dual WebSocket channels, PostGIS data flow),
tech stack, feature list, environment variables, and setup instructions for both client and
server.
