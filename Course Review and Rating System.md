# Course Review & Rating System

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A platform where students can rate and review their courses and lecturers. Helps future students make informed enrollment decisions and gives faculty useful feedback.

## Core Features
- **Course Directory** — list of all courses with code, name, faculty, year
- **Rating System** — 5-star rating on: teaching quality, workload, materials, overall
- **Written Review** — short text review (280-500 chars) per course/lecturer
- **Anonymous or Identified** — student chooses whether to show name
- **Difficulty Tag** — tag courses as Easy/Medium/Hard
- **Filter & Sort** — by faculty, year, rating, difficulty
- **Lecturer Profile** — see aggregated scores across all their courses
- **Trending Courses** — most reviewed / highest rated this semester
- **Admin Moderation** — remove inappropriate reviews

## Similar Existing Platforms
- **RateMyProfessors** — popular US-based lecturer rating (general, not local)
- **Qualtrics** (qualtrics.com) — enterprise course evaluation software
- **IASystem** (iasystem.org) — university course evaluation suite
- **Creatrix Campus** (creatrixcampus.com) — automated course evaluation

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript
- Backend: Node.js + Express or Python Flask
- Database: SQLite
- Charts: Chart.js for rating visualization

## Key Modules
1. **Auth Module** — student login (verify with university email domain)
2. **Course/Lecturer Database** — add/view courses and lecturer profiles
3. **Rating Engine** — submit ratings, aggregate scores, compute averages
4. **Review Module** — write, edit, delete own reviews
5. **Search & Filter** — by course code, name, faculty, rating
6. **Analytics Dashboard** — average ratings, distribution charts
7. **Moderation Panel** — admin review and removal

## Project Complexity
- Low-Medium — CRUD + ratings aggregation + charts
- Very achievable for 3-4 members in one semester

## Unique Angle (Sri Lankan Context)
- Local university-specific course codes and faculty structure
- Sinhala/Tamil language support for reviews
- Mobile-responsive for quick access before course registration
- WhatsApp share button for sharing reviews

## References
- Course Evaluation Software: https://www.qualtrics.com/education/course-evaluation-software/
- IASystem Features: https://iasystem.org/features-benefits/