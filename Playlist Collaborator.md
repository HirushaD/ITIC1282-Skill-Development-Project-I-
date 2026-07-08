# Playlist Collaborator

## Project Type
Web Application (HTML + CSS + JavaScript + Backend)

## What It Is
A shared music queue platform where friends can add songs to a collective playlist. Anyone can contribute, and songs play in order of total votes — creating a democratic, party-style queue.

## Core Features
- **Room Creation** — create a listening room with a shareable link/code
- **Song Submission** — paste a YouTube or Spotify link; auto-fetches title/thumbnail
- **Upvote Queue System** — songs rise in queue based on votes
- **Skip Voting** — enough skip votes removes a song from queue
- **Now Playing Display** — current song with video embed (YouTube) or Spotify player
- **Room Chat** — live text chat for the room
- **Room Settings** — owner can lock room, set max songs per person, enable explicit content filter
- **History** — past rooms and songs remain viewable

## Similar Existing Platforms
- **QueueMySong** (queuemysong.com) — real-time collaborative music queue
- **SongUp** (songup.tv) — open source shared music queue for parties
- **Groovia** (grooviamusic.com) — democratic music queue platform
- **GroupTube** (group.tube) — synchronized music with voice/video

## Tech Stack
- Frontend: HTML5, CSS3, JavaScript
- Backend: Node.js + Express
- Database: SQLite
- Real-time: Socket.io for live queue updates and chat
- Media: YouTube IFrame API or Spotify Web Playback SDK

## Key Modules
1. **Room Module** — create room, generate shareable code, set settings
2. **Song Queue Engine** — add song, upvote, downvote, auto-sort by votes
3. **Now Playing Module** — embed YouTube/Spotify player, sync state
4. **Real-time Sync** — Socket.io for live queue changes across all clients
5. **Chat Module** — live room chat alongside music
6. **Skip Voting** — democratic skip mechanism

## Project Complexity
- Medium — real-time sync + third-party media embedding
- Achievable for 4-5 members in one semester

## Unique Angle (Sri Lankan Context)
- Local music scene support (Sinhala/Tamil songs)
- Integration with local radio show requests
- University event playlist collaboration (e.g. fresher's night, award ceremonies)
- WhatsApp share link generation

## References
- QueueMySong: https://queuemysong.com/
- SongUp: https://songup.tv/
- Collaborative Playlists: https://appmus.com/feature/collaborative-playlists