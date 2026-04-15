# CollabBoard

A high-performance, decoupled full-stack application enabling multiple users to brainstorm and collaborate on an infinite canvas in real-time. This project demonstrates a transition from a monolithic architecture to a distributed Micro-services style pattern, separating the React/Vite frontend from the Node.js/Socket.io backend.

## 📐 System Architecture

The following diagram illustrates the high-level architecture of the CollabBoard application:

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

## 🚀 Repositories & Setup

### 🖥️ [Frontend Application (Client)](https://github.com/soham-kolhe/CollabBoard-frontend)
A modern, type-safe UI designed for responsiveness and smooth user interaction.
- Stack: React 18, TypeScript, Vite, Tailwind CSS, Axios, Lucide Icons.
- Key Achievement: Migrated to a dedicated repository with optimized environment-based API configuration.

### ⚙️ [Backend Service (Server)](https://github.com/soham-kolhe/CollabBoard-backend)
Responsible for API routing, real-time event handling, and database persistence.
- Stack: Node.js, Express, Socket.io, MongoDB, Mongoose, JWT, bcryptjs.
- Key Achievement: Refactored to handle large 10MB payloads for complex board states.

## 🛠️ Core Technical Features
- **Real-Time Conflict Resolution**: Utilizes Socket.io to broadcast granular drawing actions and tldraw state updates, ensuring all participants remain synchronized with sub-100ms latency.
- **Decoupled Authentication**: Implemented a shared JWT (JSON Web Token) strategy that secures both standard REST API endpoints and stateful WebSocket handshakes.
- **State Persistence & Recovery**: Intelligent data layer using MongoDB to store board snapshots, allowing users to resume sessions exactly where they left off.
- **Session Management**: Custom Ghost Session Cleanup logic to manage active users and prevent duplicate connection errors in the database.
- **Infinite Canvas**: Integrated the tldraw engine to provide a professional-grade drawing experience with support for shapes, text, and complex vectors.

## 🤝 Contributing
Feel free to open issues or submit pull requests for either the frontend or backend repositories!
