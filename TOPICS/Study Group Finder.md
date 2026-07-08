# Study Group Finder

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A platform that helps university students find study partners or join study groups based on shared subjects, courses, and availability.

## Core Features
- **Student Profile Setup** — name, university, faculty, year, subjects enrolled
- **Subject/Course Matching** — search by course code or subject name
- **Group Creation** — create a new study group with subject, time, and max members
- **Group Discovery** — browse and filter available groups by subject or faculty
- **Join Request System** — request to join a group; admin approves/rejects
- **Availability Scheduler** — set weekly available time slots for matching
- **In-App Chat/Discussion Board** — simple messaging for matched group members
- **Reminder Notifications** — browser notifications for upcoming sessions

## Similar Existing Platforms
- **StudyMesh** (studymesh.app) — AI-based matching by availability + preferences
- **Academync** (academync.com) — study partner finder with AI quizzes and Pomodoro tools

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript (Vanilla or simple framework)
- Backend: Node.js + Express (or Python Flask)
- Database: SQLite (simple, file-based, enough for a semester project)
- Real-time: Socket.io for chat

## Key Modules
1. **Auth Module** — register/login (email or student ID)
2. **Profile Module** — subject registration, availability input
3. **Matching Engine** — algorithm to suggest compatible groups/students
4. **Group Management** — create, edit, delete, join/approve
5. **Chat Module** — per-group messaging
6. **Notification Module** — email or browser push reminders

## Project Complexity
- Medium — requires matching logic + real-time chat + scheduling
- Scope manageable for 4-5 members over one semester

## Unique Angle (for Sri Lankan Context)
- Match by local university/ faculty/ course codes (e.g. CS101, ENG201)
- Support for both English and Sinhala/Tamil interface labels
- Mobile-responsive for student phone usage

## References
- StudyMesh: https://studymesh.app/
- Academync: https://academync.com/
- Study Group Finder (new/p/blink): https://blink.new/p/study-group-finder-0c3fakm4