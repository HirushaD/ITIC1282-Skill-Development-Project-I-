# Campus Meme Corner

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A moderated meme feed where students post, upvote, and downvote memes. Top memes surface to a trending page. All moderation is human-curated to keep it clean.

## Core Features
- **Meme Submission** — upload image or paste image URL + optional caption
- **Upvote / Downvote** — community voting system
- **Feed Views** — New / Trending / Top (All Time) tabs
- **Tag System** — tag memes by category (#examstress #hostellife #professorlife)
- **Moderation Queue** — admins review flagged/pending posts before going live
- **Report System** — users flag inappropriate content
- **User Reputation** — earn karma points for highly upvoted posts
- **Meme of the Week** — highlighted top meme with announcement
- **Leaderboard** — top posters by karma this month

## Similar Existing Platforms
- **Reddit** — general upvote/downvote content platform
- **Feature Upvote** (featureupvote.com) — upvote boards with moderation
- **Upvoty** (upvoty.com) — feedback boards with upvoting and moderation
- **Lemmy** — decentralized Reddit alternative

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript
- Backend: Node.js + Express or Python Flask
- Database: SQLite
- Image Storage: local folder or cloud storage URL
- Real-time: Socket.io for live vote count updates

## Key Modules
1. **Post Module** — submit meme (image upload or URL), view feed
2. **Voting Module** — upvote/downvote (one vote per user per post)
3. **Feed Engine** — sort by New / Trending (velocity-based) / Top
4. **Tag System** — tag and filter by category
5. **Moderation Panel** — admin approves/flags/removes posts
6. **Report System** — user flags go to mod queue
7. **Reputation System** — karma points for highly upvoted content
8. **Leaderboard** — monthly top posters

## Moderation Rules (Important)
- No racism, sexism, harassment, or hate speech
- No identifying personal information
- No explicit content
- Memes must be original or properly credited

## Project Complexity
- Low-Medium — image upload + voting + feed sorting
- Very achievable for 3-4 members in one semester

## Unique Angle (Sri Lankan Context)
- Local meme culture tags (#SLexams #Kottu #RaggingLife)
- Sinhala/English meme captions
- Campus-specific humor (e.g. SLIIT/University specific memes)
- Moderation team from the student body

## References
- Feature Upvote: https://featureupvote.com/
- Upvoty: https://upvoty.com/
- Upvote/Downvote Widget: https://www.commoninja.com/widgets/comments