# Anonymous Feedback Wall

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A real-time anonymous message board where campus users can post thoughts, suggestions, or reactions. Others can upvote/downvote posts. Moderators can pin or remove content.

## Core Features
- **Anonymous Posting** — no login required to post or vote; optional display name
- **Upvote / Downvote** — community voting to surface best content
- **Categories/Tags** — filter by topic (e.g. #campus, #faculty, #facilities, #events)
- **Real-time Updates** — new posts and vote counts update without refresh
- **Moderation Panel** — admin can pin, hide, or delete posts
- **Report System** — users can flag inappropriate content
- **Character Limit** — short-form posts (e.g. 280 chars) to keep it focused
- **Trending View** — top voted posts of the day/week

## Similar Existing Platforms
- **Slido** (slido.com) — live polling and Q&A (more structured)
- **AnonPolls** (anonpolls.com) — anonymous poll maker
- **JellyForm** (jellyform.com) — anonymous suggestion box software
- GitHub reference: https://github.com/Joshuakaranja/anonymous-feedback-site

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript (Vanilla)
- Backend: Node.js + Express or Python Flask
- Database: SQLite
- Real-time: Socket.io for live vote counts and new posts

## Key Modules
1. **Post Module** — create post, view all, filter by category
2. **Voting Module** — upvote/downvote (one vote per device/IP per post)
3. **Real-time Broadcast** — push new posts/votes to all connected clients
4. **Moderation Module** — admin login, pin/hide/delete posts
5. **Report Module** — flag post for review
6. **Trending Engine** — sort by votes within time window

## Project Complexity
- Low-Medium — straightforward CRUD + voting + real-time
- Very achievable for 3-4 members in one semester

## Unique Angle (Sri Lankan Context)
- Sinhala/Tamil language support for posts
- Campus-specific categories (e.g. #hostel, #canteen, #exam)
- Anonymous feedback for university administration

## References
- Anonymous Feedback Tools: https://www.theysaid.io/blog/top-anonymous-feedback-tools
- JellyForm: https://www.jellyform.com/