# 🎸 BandMate

> A web platform for bands to manage practice sessions, song lists, and collaboration.

BandMate helps musicians stay organized by centralizing everything a band needs — from scheduling rehearsals to sharing sheet music and storing recordings — in one place.

---

## ✨ Key Features

- **Band Management** — Create a band, invite members, and manage roles
- **Practice Scheduling** — Plan and track rehearsal sessions with calendar views
- **Song List Management** — Maintain a shared setlist with status tracking per song
- **Material Sharing** — Upload and access tabs, sheet music, and MR (music reference) files
- **Rehearsal Recordings** — Store practice recordings and attach notes per session

---

## 🛠 Tech Stack

| Layer      | Technology              |
|------------|-------------------------|
| Frontend   | Next.js + React         |
| Backend    | Node.js + Express       |
| Database   | MongoDB                 |
| File Storage | Local / Cloud Storage |

---

## 📁 Repository Structure

```
bandmate/
├── client/                  # Next.js frontend
│   ├── components/          # Reusable React components
│   ├── pages/               # Next.js page routes
│   ├── styles/              # Global and module CSS
│   └── public/              # Static assets
│
├── server/                  # Node.js + Express backend
│   ├── controllers/         # Route handler logic
│   ├── models/              # Mongoose data models
│   ├── routes/              # API route definitions
│   └── middleware/          # Auth and error handling
│
├── docs/                    # Project documentation
│   ├── system-architecture.md
│   ├── api-spec.md
│   ├── database-design.md
│   └── wireframe.md
│
├── .env.example             # Environment variable template
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- MongoDB (local or Atlas)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/bandmate.git
cd bandmate

# Install server dependencies
cd server && npm install

# Install client dependencies
cd ../client && npm install
```

### Running the App

```bash
# Start the backend server
cd server && npm run dev

# Start the frontend (in a new terminal)
cd client && npm run dev
```

The app will be available at `http://localhost:3000`.

---

## 👥 Team

This project was developed as part of a university Software Engineering course.

---

## 📄 License

MIT
