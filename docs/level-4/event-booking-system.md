# Event Booking System

> A fullstack event booking platform with availability management, booking flow, and email confirmations.

**Level:** 4 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://event-booking-systemm.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/event-booking-system)

---

## Purpose

This project introduces resource contention — multiple users trying to book limited spots.
You'll learn to handle availability checks, prevent overbooking with atomic operations,
implement a booking confirmation flow, and send transactional emails. These are the exact
challenges faced by Eventbrite, Calendly, and any reservation system.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express, MongoDB (Mongoose)
- **Auth:** JWT
- **Key libraries / tools:** Nodemailer, Mongoose transactions, date-fns, Axios
- **Deployment:** Netlify (frontend) + Render (backend)

## Build Steps

1. **Model the data.** Event: `{ title, description, date, location, capacity, bookedCount, price, organizer }`. Booking: `{ event, user, status: 'confirmed' | 'cancelled', bookedAt }`. The `bookedCount` tracks availability.
2. **Build event CRUD.** Organizers create/edit/delete events. Public endpoint lists upcoming events with available spots. Detail endpoint shows full info including remaining capacity.
3. **Implement the booking endpoint.** `POST /events/:id/book` — atomically check capacity and increment `bookedCount`. Use `findOneAndUpdate` with a condition: `{ _id: id, bookedCount: { $lt: capacity } }`. If it returns null, the event is full.
4. **Send confirmation emails.** On successful booking, send an email with event details, booking reference, and a cancellation link. Use Nodemailer with a clean HTML template.
5. **Build the booking flow UI.** Event list → event detail (show availability) → "Book Now" button → confirmation page. Show real-time availability (remaining spots). Disable the button when full.
6. **Add cancellation.** Users can cancel their booking from "My Bookings" page. On cancellation, decrement `bookedCount` atomically and send a cancellation confirmation email. Update the booking status.
7. **Build the organizer dashboard.** Event creators see their events with booking stats: total bookings, attendee list, revenue (if paid). Allow exporting the attendee list as CSV.

## Deployment

Backend on Render with `MONGODB_URI`, `JWT_SECRET`, and SMTP credentials. Frontend on
Netlify with `VITE_API_URL`. Test the overbooking protection with concurrent requests.

## Tips

- The atomic `findOneAndUpdate` with a capacity condition is the correct way to prevent overbooking. Never do a separate read-then-write — a race condition between the check and the update will oversell.
- For paid events, don't confirm the booking until payment is received. The flow becomes: reserve spot → payment → confirm. Use a TTL on reservations to release unpaid spots after 15 minutes.
- Extension: add waitlists (notify when spots open), recurring events, ticket types (VIP, general), or calendar integration (ICS file download).

## README Guidance

The project repo's README should include a description, screenshots of event list and
booking confirmation, tech stack, environment variables, and setup instructions.
