# CollabBoard

> Real-time collaborative whiteboard — draw, brainstorm, and ideate together on an infinite canvas.

![React](https://img.shields.io/badge/React_18-20232A?style=flat&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Socket.io](https://img.shields.io/badge/Socket.io-010101?style=flat&logo=socketdotio&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)

## 📐 Architecture

```mermaid
graph TD
    Client1([User 1]) -->|Interacts| UI
    Client2([User 2]) -->|Interacts| UI

    subgraph "Frontend Repository"
        UI[React + tldraw UI]
        API_Client[Axios Client]
        WS_Client[Socket.io Client]
        UI --> API_Client
        UI --> WS_Client
    end

    API_Client -->|"REST API (Auth/Boards)"| Express
    WS_Client -->|"WebSockets (Draw events)"| SocketIO

    subgraph "Backend Repository"
        Express[Express API]
        SocketIO[Socket.io Server]
        Auth_MW[JWT Auth Middleware]

        Express -.-> Auth_MW
        SocketIO -.-> Auth_MW
    end

    Express -->|Mongoose| MongoDB[(MongoDB)]
    SocketIO -->|Mongoose| MongoDB
```

## ✨ Features

- 🎨 **Infinite canvas** powered by [tldraw](https://tldraw.com) — shapes, text, vectors
- ⚡ **Real-time sync** via Socket.io with sub-100ms latency
- 🔐 **JWT auth** securing both REST endpoints and WebSocket handshakes
- 💾 **Board persistence** — resume sessions exactly where you left off
- 👥 **Multi-user** — see collaborators' cursors and changes live
- 🧹 **Ghost session cleanup** — no stale connections or duplicate users

## 🚀 Quick Start

**1. Clone & run the backend**
```bash
git clone https://github.com/soham-kolhe/CollabBoard-backend
cd CollabBoard-backend && npm install && npm run dev
```

**2. Clone & run the frontend**
```bash
git clone https://github.com/soham-kolhe/CollabBoard-frontend
cd CollabBoard-frontend && npm install && npm run dev
```

Open `http://localhost:5173` — sign up, create a board, share the link.

## 📦 Repositories

| Repo | Stack | Description |
|------|-------|-------------|
| [CollabBoard-frontend](https://github.com/soham-kolhe/CollabBoard-frontend) | React · TypeScript · Vite · Tailwind | UI, canvas, real-time client |
| [CollabBoard-backend](https://github.com/soham-kolhe/CollabBoard-backend) | Node.js · Express · Socket.io · MongoDB | API, auth, WebSocket server |

## 🤝 Contributing

Issues and PRs are welcome in either repository!

---

<div align="center">
  <sub>Built by <a href="https://github.com/soham-kolhe">soham-kolhe</a></sub>
</div>
