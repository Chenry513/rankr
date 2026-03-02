# Rankr — Collaborative Real-Time Ranking App

A real-time web application that lets groups create polls, nominate options, and rank their choices collaboratively. Results are computed and displayed instantly as votes come in — no page refreshes, no waiting.

> Built with React, TypeScript, Socket.io, and Redis. Runs locally with Docker.

---

## What This Project Does

Rankr solves the problem of group decision-making by giving everyone a voice in real time:

- **Create a Poll**: Start a session with a topic and get a shareable poll ID
- **Invite Participants**: Share the poll ID — anyone can join instantly
- **Nominate Options**: Each participant submits their suggestions
- **Rank Choices**: Everyone ranks the options once voting opens
- **See Results**: Final rankings are computed and displayed automatically using aggregated vote logic

---

## How It Works

```
Host creates poll → Gets shareable Poll ID → Participants join → 
Everyone nominates → Voting opens → Rankings submitted → Results computed → Displayed live
```

All state is synchronized in real time via Socket.io — every participant sees updates the moment they happen.

---

## Tech Stack

**Frontend:**
- React + TypeScript
- Vite
- Tailwind CSS

**Backend:**
- Node.js
- Socket.io — real-time bidirectional communication
- Redis (RedisJSON) — low-latency session and vote state storage

**Infrastructure:**
- Docker + Docker Compose — containerized local development

---

## Local Setup

```bash
# 1. Clone the repo
git clone https://github.com/Chenry513/rankr
cd rankr

# 2. Install dependencies
npm install concurrently --save-dev

# 3. Start Redis via Docker
docker-compose up -d

# 4. Run the app
npm run start
```

Visit `http://localhost:8080`

> If you hit dependency issues run `npm audit fix`

---

## Project Structure

```
rankr/
├── client/          # React + Vite frontend
├── server/          # Node.js + Socket.io backend
├── shared/          # Shared TypeScript types
├── docker-compose.yml
└── package.json
```

---

## Key Design Decisions

**Why Socket.io over polling?**
HTTP polling would introduce noticeable lag for a collaborative ranking experience. Socket.io gives true bidirectional communication so all participants see state changes instantly.

**Why Redis?**
Poll sessions are ephemeral and read/written frequently by multiple participants simultaneously. Redis handles this with far lower latency than a traditional relational database, and RedisJSON lets us store structured poll state without serialization overhead.

**Why Docker?**
Redis requires a running server — Docker Compose removes the need for participants or contributors to install and configure Redis manually. One command spins up the full environment.

---

## Future Improvements

- Persistent poll history with user accounts
- Weighted ranking algorithms (Borda count, instant-runoff)
- Mobile-optimized UI
- Public deployment with hosted Redis

---

## License

MIT License


