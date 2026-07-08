# Buddy Reading Program

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A platform that pairs senior (older) students with junior students for regular reading sessions. The goal is literacy support, mentorship, and a culture of reading — not academic tutoring.

## Core Features
- **Student Registration** — set role (senior/junior), name, faculty, preferred genres
- **Pairing System** — algorithm matches senior + junior by faculty proximity and genre preference
- **Reading Goal Setting** — set weekly page or chapter targets
- **Progress Tracking** — log completed books/chapters; see streak
- **Discussion Prompts** — per-book discussion questions to spark conversation
- **Meeting Scheduler** — set preferred meeting times; calendar view
- **Review System** — juniors rate their buddy experience
- **Badge/Achievement System** — reward consistent participants (e.g. "5 books completed")

## Similar Existing Platforms
- **BookBuddying** (bookbuddying.com) — matchmaking for adult readers (general, not student-specific)
- Reading Buddies Programs: https://app.starredin.com/blog/reading-buddies-programs-pairing-older-and-younger-students
- Benefits of Buddy Reading: https://thereadingroundup.com/reading-buddies-benefits/

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript
- Backend: Node.js + Express or Python Flask
- Database: SQLite
- Real-time: Socket.io for chat between pairs

## Key Modules
1. **Auth Module** — register as senior or junior
2. **Profile Module** — faculty, preferred genres, reading interests
3. **Matching Algorithm** — pair seniors with compatible juniors
4. **Goal Tracker** — set and log reading progress weekly
5. **Meeting Scheduler** — coordinate meet times
6. **Achievement System** — badges for milestones
7. **Chat Module** — simple messaging between matched pairs

## Project Complexity
- Medium — matching logic + progress tracking + achievements
- Achievable for 4-5 members over one semester

## Unique Angle (Sri Lankan Context)
- Support for Sinhala and Tamil books
- Integration with local school/university reading lists
- Faculty-specific pairings (e.g. Arts senior paired with Arts junior)
- WhatsApp integration for meeting reminders

## References
- BookBuddying: https://bookbuddying.com/
- Reading Buddies Benefits: https://www.teachmaverick.com/reading-buddies/
- Benefits of Buddy Reading: https://thereadingroundup.com/reading-buddies-benefits/