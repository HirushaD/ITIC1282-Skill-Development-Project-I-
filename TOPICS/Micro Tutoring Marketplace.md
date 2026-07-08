# Micro Tutoring Marketplace

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A peer-to-peer platform where students can offer or book short paid tutoring sessions (15-30 min) in specific subjects. Like a mini fiverr/upwork but scoped to campus tutoring.

## Core Features
- **Tutor Profiles** — set subjects, short bio, hourly rate (or free), availability slots
- **Session Booking** — tutee browses tutors, picks subject, books a slot
- **Time Slot Management** — tutors define available windows; auto-block booked slots
- **Rating & Review** — after session, tutee rates 1-5 stars + short comment
- **Session Types** — text chat, voice call, or video call links (Zoom/Google Meet embed)
- **Wallet/Balance System** — simple credit tracking (no real payment gateway needed for MVP)
- **Search & Filter** — by subject, rating, price (free/paid)
- **Dashboard** — tutor sees earnings, upcoming sessions, history

## Similar Existing Platforms
- **Fiverr / Upwork** — general freelance services (too broad)
- **Preply / Tutor.com** — professional tutoring platforms (too complex)
- Gaurav Tiwari's list of P2P tutoring platforms: https://gauravtiwari.org/8-best-peer-to-peer-tutoring-platforms/

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript
- Backend: Node.js + Express or Python Flask
- Database: SQLite
- Real-time: Socket.io for chat sessions
- Optional: WebRTC for video embedding

## Key Modules
1. **Auth Module** — register as tutor or tutee (or both)
2. **Profile Module** — subjects, bio, rate, availability
3. **Booking Engine** — slot selection, conflict prevention
4. **Review System** — star rating + comment storage
5. **Wallet Module** — credit balance, transaction history
6. **Search Module** — filter by subject/rating/price

## Project Complexity
- Medium-High — booking logic, availability calendar, review system
- Scope manageable for 4-5 members over one semester

## Unique Angle (Sri Lankan Context)
- Local pricing基准 (e.g. LKR 100-500 per session)
- Sinhala/Tamil subject names support
- Integration with WhatsApp for session reminders

## References
- Peer-to-Peer Tutoring Platforms: https://www.f6s.com/software/category/peer-to-peer-tutoring-marketplace
- Tutoring Marketplace Guide: https://education.toolsinfo.com/c/tutoring-platforms