# 🎖️ SentinelOps – Soldier Mission Coordination & Emergency Communication System

> **Real-time Military Simulation Platform** | Built for the Valkey Hackathon

SentinelOps is a real-time command center designed for **military training exercises and disaster-response simulations**. It demonstrates how **Valkey** can serve as a high-performance, multi-purpose in-memory intelligence layer far beyond a simple cache.

---

## 🚀 Live Demo

> Clone and run locally (see setup below)

---

## 🎯 Problem Statement

In high-risk field operations and disaster scenarios:
- Soldiers need to send **emergency SOS signals instantly** — even offline
- Commanders need **real-time coordination** across multiple units
- Systems need to work under **network degradation**
- Response time to find **nearest rescue units** must be milliseconds

SentinelOps solves all of these using **Valkey at the core**.

---

## 🗄️ How We Use Valkey (5 Core Features)

| Feature | Valkey Command | Use Case |
|---|---|---|
| **GEO Indexing** | `GEOADD`, `GEOSEARCH` | Store soldier positions, find nearest 3 rescue units instantly |
| **Sorted Sets** | `ZADD`, `ZRANGE` | Mission Priority Queue (Emergency → Patrol) |
| **Pub/Sub** | `PUBLISH`, `SUBSCRIBE` | Broadcast SOS alerts to all commanders in <100ms |
| **Streams** | `XADD`, `XRANGE` | Mission Replay — rewind any mission event-by-event |
| **Key-Value Cache** | `SET`, `GET`, `TTL` | JWT sessions, AI threat scores, soldier status |

---

## ⚡ SOS Emergency Flow

```
Soldier taps SOS
    → AES-256 encrypts signal
    → WebSocket sends to server
    → Valkey GEOSEARCH finds 3 nearest rescue units
    → Pub/Sub broadcasts ALERT to all commanders
    → Commander dashboard receives alert in <100ms
    → Nearest unit dispatched
    → Event stored in Valkey Stream + PostgreSQL
```

---

## 👥 Three User Roles

### 🟢 Commander
- Live tactical map with all soldier positions
- Mission Priority Queue (Emergency > Investigation > Patrol > Training)
- TDSS — Tactical Decision Support System alerts
- Mission Replay via Valkey Streams
- AI-generated threat heatmap

### 🔴 Soldier
- **Giant SOS button** — one tap sends distress signal
- Valkey GEO finds 3 nearest rescue units automatically
- Works **offline** — reports queue in LocalStorage, auto-sync on reconnect
- AES-256 encrypted chat with command center
- Real-time mission assignment

### 🔵 Admin
- **Live Valkey Memory Inspector** — see all keys, values, TTL
- System Health Dashboard — connections, uptime, memory
- User management — create/assign roles
- Full audit log of all actions

---

## 🤖 AI Threat Prediction Engine (TIE)

- Analyzes SOS signal clusters to identify high-risk zones
- Calculates threat score per grid cell
- Generates heatmap overlay on tactical map
- Recommends nearest rescue route
- Predicts next likely threat zone
- Auto-generates mission summary report

---

## 🔐 Security

- **AES-256 encryption** on all WebSocket messages
- **JWT authentication** with role-based access control
- **3 roles**: Commander, Soldier, Admin — each with restricted views

---

## 📡 Offline-First Architecture

- Soldiers can work **without internet**
- Reports and SOS signals queue in **LocalStorage**
- Auto-syncs with server on reconnection
- No data loss in field operations

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js, Vite, Tailwind CSS v4, Framer Motion |
| Backend | Node.js, Express.js, Socket.IO |
| In-Memory DB | **Valkey** (via ioredis) |
| Database | PostgreSQL (with in-memory fallback) |
| Security | AES-256 (CryptoJS), JWT, RBAC |
| Real-time | Socket.IO WebSockets |

---

## 🚀 Setup & Run

### Prerequisites
- Node.js v18+
- Valkey or Redis running locally (or uses in-memory fallback automatically)

### Backend
```bash
cd backend
npm install
npm start
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

### With Docker
```bash
docker-compose up
```

### Default Login Accounts
| Role | Username | Password |
|---|---|---|
| Commander | `commander` | `commander123` |
| Soldier | `soldier1` | `soldier123` |
| Admin | `admin` | `admin123` |

---

## 📁 Project Structure

```
sentinelops/
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   ├── db.js          # PostgreSQL + in-memory fallback
│   │   │   └── valkey.js      # Valkey client + simulator
│   │   ├── services/
│   │   │   ├── tie.js         # AI Threat Intelligence Engine
│   │   │   └── valkeyService.js # GEO, Streams, PubSub, Sorted Sets
│   │   └── server.js          # Express + Socket.IO server
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── DashboardCommander.jsx
│   │   │   ├── DashboardSoldier.jsx
│   │   │   ├── DashboardAdmin.jsx
│   │   │   └── TacticalMap.jsx
│   │   ├── utils/
│   │   │   ├── crypto.js      # AES-256 encryption
│   │   │   └── offlineSync.js # Offline queue manager
│   │   └── App.jsx
│   └── package.json
└── docker-compose.yml
```

---

## 🏆 Why Valkey?

> *"SentinelOps proves that Valkey isn't just a cache — it's a tactical decision engine."*

Valkey powers **5 distinct real-time features** simultaneously in this application:
making it the backbone of the entire platform — not a supporting component.

---

**Built with ❤️ for Valkey Hackathon 2025**
