# IoT Dashboard

> A full-stack real-time IoT sensor monitoring dashboard with MQTT telemetry ingestion, threshold-based alerting, email notifications, and interactive historical analytics — built with React 19, Express 5, PostgreSQL, Socket.io, and Prisma 7.

**Level:** 5 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://iot-dashboard-one-rouge.vercel.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/iot-dashboard)

---

## Purpose

This project teaches you to build a production-grade IoT data pipeline. Sensors publish
telemetry over MQTT — your system must validate device identity, persist time-series readings,
evaluate threshold rules in real time, notify operators on critical events, and push live
updates to connected dashboards via WebSockets. The MQTT → consumer → database → alert engine →
Socket.io fan-out pattern is the same architecture used in factory monitoring, smart building
systems, and industrial SCADA platforms.

## Tech Stack

- **Frontend:** React 19, Vite 8, TypeScript 6, Tailwind CSS v4, Framer Motion, Recharts 3, Socket.io Client, React Router v7, Axios
- **Backend:** Node.js 20+, Express 5, TypeScript 6, Prisma 7, Socket.io 4, mqtt.js, Nodemailer, Swagger UI
- **Database:** PostgreSQL (Neon serverless)
- **Messaging:** MQTT (Mosquitto locally, HiveMQ Cloud in production)
- **Auth:** JWT + bcryptjs, Admin/Viewer RBAC
- **Security:** Helmet, CORS, tiered rate limiting, express-validator, express-mongo-sanitize
- **Deployment:** Vercel (frontend) + Render (backend) — all free tier

## Build Steps

1. **Design the MQTT topic hierarchy and device whitelist.** Structure topics as `{root}/{floor}/{sensorId}/{type}` (e.g. `factory/floor1/sensor01/temperature`). Only registered, active devices in PostgreSQL may publish — the consumer rejects unknown sensor IDs before writing data.

2. **Build the MQTT consumer service.** Subscribe to the broker, parse incoming payloads, validate against the device registry, persist readings to PostgreSQL, and emit `sensor:data` events via Socket.io. Run the consumer alongside the Express API in the same Node process or as a dedicated service module.

3. **Implement the alert engine.** For each reading, evaluate configurable thresholds per sensor type: `criticalMin ← WARNING ← minValue ← NORMAL → maxValue → WARNING → criticalMax`. Persist alerts, emit `alert:new` via Socket.io, and send email via Nodemailer on CRITICAL severity.

4. **Build the Express 5 REST API with Prisma.** Endpoints for auth, latest readings, raw/aggregated history, paginated alerts, threshold config, and device CRUD. Protect routes with JWT middleware; gate admin actions (settings, devices, alert acknowledge) behind role checks. Document everything with Swagger at `/api-docs`.

5. **Build the React dashboard with real-time updates.** Socket.io context pushes live sensor cards with sparklines and animated values. Floor tabs filter by location. Expand any card for a full Recharts visualization. Historical page: date range picker, minute/hour aggregation windows, brush zoom, and stats summary.

6. **Add alert management and admin panels.** Paginated alert list with severity/type/status filters, single and bulk acknowledge, and cleanup of old alerts. Admin device registry (register, edit, toggle, delete). Settings panel with threshold range visualizer and system status display.

7. **Ship with a sensor simulator and free-tier deployment.** An mqtt.js publisher simulates factory sensors for local dev and demo. Deploy backend to Render (with Prisma migrate + seed), frontend to Vercel, database on Neon, and MQTT broker on HiveMQ Cloud. Handle Render cold starts with a health-check ping and a "Waking up" UI state.

## Deployment

Frontend on Vercel (`client/`), backend on Render (`server/`). PostgreSQL on Neon,
MQTT on HiveMQ Cloud (`mqtts://` on port 8883). Set `CLIENT_URL` on Render to your
Vercel URL for CORS. In production: `NODE_ENV=production`, `ALLOW_REGISTRATION=false`,
and strong `SEED_ADMIN_EMAIL` / `SEED_ADMIN_PASSWORD` before running seed.

## Tips

- The alert engine runs synchronously on every MQTT message — keep threshold lookups cached in memory and batch database writes if throughput grows beyond demo scale.
- Device whitelist enforcement at the consumer is your first line of defense. Never trust MQTT topic structure alone; always verify the sensor ID against your registry.
- Render free tier cold starts (~30s) will disconnect Socket.io clients. Ping `/api/health` on app load and show a graceful "Waking up" state instead of treating the backend as permanently offline.
- Extension: add TimescaleDB hypertables for long-term retention, Grafana integration, OTA firmware update tracking, or multi-tenant organization scoping per device fleet.

## README Guidance

The project repo's README should include a description, architecture diagrams (MQTT data
flow and domain model), screenshots of dashboard/historical/alerts pages, live demo link
with demo credentials, tech stack, API endpoint table, Socket.io event reference,
environment variables, local setup steps (Docker Mosquitto + Prisma migrate + simulator),
and free-tier deployment guide for Render + Vercel + Neon + HiveMQ.
