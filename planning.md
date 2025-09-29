# Guest List App for Events – Project Planning

## 1. Project Overview
- **Project Name:** Guest List Manager
- **Description:**  
  A web application for event organizers to create events, register artists and staff, and manage guest lists. Organizers can generate unique links for each artist/staff, allowing them to edit their guest list without needing to sign up.
- **Purpose & Goals:**  
  - Simplify guest list management for events.
  - Allow artists and staff to manage their own guest lists easily without waiting for someone's response.
  - Reduce administrative overhead for organizers.

## Motivation

Managing guest lists for events is still a manual and error-prone process in many venues. Artists often have to send their guest lists to organizers ahead of time, making last-minute changes difficult or impossible. This can lead to situations where guest lists are not registered properly, forcing artists to resolve issues at the entrance during the event—sometimes even leaving guests waiting outside.

This app aims to solve these problems by providing a seamless, real-time guest list management system. Artists and staff can view and edit their guest lists directly, with changes instantly synced to the organizer and reception. This eliminates the need for back-and-forth communication, reduces mistakes, and ensures a smoother experience for everyone involved.

## 2. Features & Requirements

### Core Features
- [ ] Organizer authentication and event creation
- [ ] Register artists/staff with names and guest list spot limits
- [ ] Generate and share individual guest list edit links (no signup required for artists/staff)
- [ ] Artists/staff can add, edit, and remove guests via their link
- [ ] Organizer dashboard to view and export all guest lists
- [ ] Reception page to search and check in guests

### Future considerations
- [ ] Email notifications for organizers and artists/staff
- [ ] Register resident artists and set default guest list amounts for organizers to avoid repeating the same process on recurring events
- [ ] Event summary and analytics (total guests, spots used, etc.)
- [ ] Make the ticket type more flexible. Enable organizers to have more than free and reduced.

## 3. Technical Stack

### Frontend
- [ ] Next.js
- [ ] State Management (Zustand or Redux Toolkit)
- [ ] UI Framework (Tailwind CSS, shadcn/ui)
- [ ] Routing (Next.js App Router)
- [ ] Testing (Jest, React Testing Library)

### Backend
- [ ] Next.js API routes
- [ ] API Type (REST)
- [ ] Authentication (Auth.js for organizers, token-based for guest list links)
- [ ] Testing Framework (Jest)
- [ ] Other: Prisma ORM

### Database
- [ ] PostgreSQL (via Supabase or self-hosted)

### DevOps
- [ ] Version Control (GitHub)
- [ ] Deployment (Vercel)
- [ ] CI/CD (GitHub Actions)
- [ ] Containerization (Docker)

## 4. Architecture Overview

- **Frontend Routes & Page Summaries:**  

- `/login`  
  Organizer login page.

- `/dashboard`  
  Main organizer dashboard. View all events, event details, and guest lists.

- `/events/create`  
  Page for organizers to create a new event.

- `/events/:eventId/edit`  
  Edit event details, artists/staff, and guest list spot limits.

- `/events/:eventId/artists`  
  Manage artists/staff for a specific event (add, edit, delete, set limits).

- `/guestlist/:token`  
  Guest List Edit Page for artists/staff. Accessed via unique link; allows adding, editing, and removing guests.

- `/reception/:eventId`  
  Reception Check-In Page. Search for guests and mark them as checked in.

- `/settings`  
  Organizer profile and app settings.

- **API Endpoints:**  
  - `POST /api/auth/login`  
  - `POST /api/events`  
  - `GET /api/events/:id`  
  - `PUT /api/events/:id`  
  - `DELETE /api/events/:id`  
  - `POST /api/events/:id/artists`  
  - `GET /api/artists/:id/guestlist`  
  - `PUT /api/artists/:id/guestlist`  
  - `GET /api/events/:id/guestlists`  
  - `POST /api/events/:id/export`

- **Data Models:**  
  - **User (Organizer):** id, name, email, passwordHash, createdAt  
  - **Event:** id, organizerId, name, date, location, createdAt  
  - **Artist/Staff:** id, eventId, name, guestListLimitFree, guestListLimitReduced, uniqueLink, createdAt  
  - **Guest:** id, artistId, eventId, name, email, type (enum: 'free', 'reduced'), checkedIn (boolean), createdAt

- **Check-In Functionality:**  
  - When a guest is checked in (`checkedIn: true`), their entry becomes locked (`locked: true`) and cannot be edited or deleted from the guest list.
  - The Guest List Edit Page should disable editing for checked-in guests.
  - Organizer dashboard can view check-in status for all guests.

## 5. Resources & References

- [Design Mockups or Wireframes] (to be created in Figma)
- [API documentation] (OpenAPI/Swagger, to be drafted)
- [External Libraries or Tools]  
  - uuid (unique link generation)
  - date-fns (date utilities)
  - dotenv (env management)

## 6. Notes

- Ensure guest list links are secure and expire after the event.
- Focus on mobile-friendly design for on-the-go access.
- Consider privacy and data protection for guest information.
- Plan for future features like check-in management or integration with ticketing systems.

---