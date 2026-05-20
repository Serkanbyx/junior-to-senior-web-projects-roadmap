# Event Booking System

> A fullstack event booking platform with role-based access (Attendee/Organizer/Admin), QR code tickets, atomic capacity management, and email confirmations.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://event-booking-systemm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/event-booking-system)

---

## Purpose

This project introduces resource contention — multiple users trying to book limited spots.
You'll learn atomic operations to prevent overbooking, QR code generation for tickets,
role-based dashboards for different user types, and transactional emails. These are the
exact challenges faced by Eventbrite, Calendly, and any reservation system.

## Tech Stack

- **Frontend:** React 19, Vite 6, Tailwind CSS 4, React Router 7, React Hook Form
- **Backend:** Node.js, Express 5, MongoDB (Mongoose 9)
- **Auth:** JWT + bcryptjs
- **QR Codes:** qrcode library (ticket generation)
- **Email:** Nodemailer (Outlook SMTP) — booking confirmations
- **Dates:** date-fns 4
- **Validation:** express-validator
- **Security:** Helmet, multi-tier rate limiting, express-mongo-sanitize
- **UX:** React Icons, React Hot Toast
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Design the role system.** Three roles: Attendee (browse + book), Organizer (create events + manage bookings), Admin (moderate everything). Each sees a different dashboard with role-appropriate actions.

2. **Build event CRUD for organizers.** Organizers create events with: title, description, date, location, capacity, price, and cover image. They manage their events and view attendee lists. Events have status: upcoming, ongoing, past, cancelled.

3. **Implement atomic booking.** `POST /events/:id/book` — use `findOneAndUpdate` with condition `{ bookedCount: { $lt: capacity } }` and `$inc: { bookedCount: 1 }`. If it returns null, the event is full. This single atomic operation prevents overbooking under concurrent requests.

4. **Generate QR code tickets.** On successful booking, generate a QR code containing the booking reference. Include it in the confirmation email and display it on the "My Tickets" page. Organizers can scan QR codes at the event entrance for verification.

5. **Send confirmation emails.** On booking: send HTML email with event details, booking reference, QR code, and cancellation link. On cancellation: send cancellation confirmation. Use Nodemailer with Outlook SMTP and clean HTML templates.

6. **Build the attendee flow.** Browse events (with search, date filtering, category). View event detail (remaining capacity shown). Book → receive confirmation email with QR ticket. "My Bookings" page with ticket status and cancellation option.

7. **Build the admin and organizer dashboards.** Organizer: event management, attendee lists per event, booking stats. Admin: moderate all events, manage users, platform analytics. Multi-tier rate limiting (strict on booking endpoint to prevent abuse).

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, `SMTP_*` (Outlook credentials).
Frontend on Netlify with `VITE_API_URL`.

## Tips

- Atomic `findOneAndUpdate` with a capacity condition is the ONLY correct way to prevent overbooking. Never read capacity, check in application code, then write — the race condition between read and write will oversell under concurrent load.
- QR codes contain just the booking reference (a short string). The verification happens by looking up the reference in the database, not by decoding complex data from the QR code itself.
- Extension: add waitlists (notify when spots open), recurring events, ticket types (VIP, general), payment integration (Stripe), or calendar export (ICS file).

## README Guidance

The project repo's README should include a description, screenshots of event list, booking
flow, and QR ticket, role system explanation, tech stack, and setup instructions.
