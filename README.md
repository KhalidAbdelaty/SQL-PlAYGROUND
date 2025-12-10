# SQL Playground

**Ever accidentally dropped a production table? Yeah, me too. That's why I built this.**

SQL Playground is a full-stack web application where you can write, execute, and experiment with SQL queries in a completely isolated environment. Break things. Learn from mistakes. No consequences.

![Status](https://img.shields.io/badge/Status-Live-brightgreen) ![React](https://img.shields.io/badge/React-18-blue) ![FastAPI](https://img.shields.io/badge/FastAPI-0.104-green) ![SQL Server](https://img.shields.io/badge/SQL%20Server-2019+-red)

---

## Screenshots

### Login
![Login Page](images/login.png)

### The Playground
![SQL Playground](images/portal_sandbox.png)

---

## Why I Built This

I wanted a place where I could test complex queries without sweating. Where beginners could learn SQL without the fear of breaking something important. Where instructors could give students their own databases without any setup headaches.

So I built it.

Every user gets their own isolated SQL Server database. You can CREATE, DROP, TRUNCATE—whatever you want. It's your sandbox. When you're done, it cleans itself up.

---

## What's Inside

**The Editor** — Monaco (the same one VS Code uses) with SQL syntax highlighting, IntelliSense, and keyboard shortcuts that actually work.

**Schema Browser** — Click a table, drag it into the editor, see its structure. No more guessing column names.

**Query History** — Every query you run is saved. One click to re-run. One click to copy.

**Results Grid** — Sort, filter, paginate. Export to CSV or JSON when you need to.

**Saved Queries** — Save your go-to queries. Tag them. Star your favorites. Access them with `Ctrl+Shift+O`.

**Query Caching** — Run the same SELECT twice? The second one's instant. You'll see a little "cached" badge when it happens.

---

## Keyboard Shortcuts

| Shortcut | What it does |
|----------|--------------|
| `Ctrl + Enter` | Run query |
| `Ctrl + Shift + F` | Format SQL |
| `Ctrl + Shift + Q` | Save query |
| `Ctrl + Shift + O` | Open saved queries |
| `Ctrl + Shift + H` | Show all shortcuts |
| `Ctrl + K` | Clear editor |
| `Esc` | Close any dialog |

---

## Tech Stack

**Frontend:** React 18, Vite, Monaco Editor, AG Grid, TailwindCSS, Framer Motion

**Backend:** FastAPI, SQL Server, SQLite (for auth), pyodbc, JWT, bcrypt

I chose each piece deliberately. FastAPI because it's fast and the auto-generated docs are genuinely useful. Monaco because it's what developers actually use. AG Grid because it handles large datasets without breaking a sweat.

---

## Getting Started

### You'll Need
- Python 3.8+
- Node.js 16+
- SQL Server 2019+
- ODBC Driver 17 for SQL Server

### Setup

**1. Clone it:**
```bash
git clone https://github.com/KhalidAbdelaty/SQL-PlAYGROUND.git
cd SQL-PlAYGROUND
```

**2. Backend:**
```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

Create `backend/.env`:
```env
DB_SERVER=YOUR_SERVER_NAME
DB_DATABASE=master
DB_TRUSTED_CONNECTION=yes
DB_DRIVER=ODBC Driver 17 for SQL Server

JWT_SECRET=your-secret-key-here
ADMIN_SETUP_KEY=your-setup-key-here

HOST=0.0.0.0
PORT=8000
CORS_ORIGINS=http://localhost:5173
```

**3. Frontend:**
```bash
cd ../frontend
npm install
```

Create `frontend/.env`:
```env
VITE_API_URL=http://localhost:8000
VITE_WS_URL=ws://localhost:8000
```

**4. Run it:**
```bash
# Terminal 1
cd backend && python run.py

# Terminal 2
cd frontend && npm run dev
```

**5. Open:** http://localhost:5173

---

## Security

This isn't a toy. I built real security into it:

- **Dangerous query detection** — DROP, TRUNCATE, DELETE on large tables? You'll get a confirmation dialog.
- **Sandbox isolation** — Users can't see or touch each other's databases.
- **Rate limiting** — 60 requests per minute. No abuse.
- **Session management** — 8 hour expiry. Extend it if you need to.
- **Password hashing** — bcrypt with salt. Industry standard.
- **Database size limits** — 100MB per sandbox. Keeps things fair.

---

## Architecture

```
Frontend (React)
    │
    │ HTTPS
    ▼
Backend (FastAPI)
    │
    ├──► SQL Server (user queries)
    │
    └──► SQLite (auth, sessions, saved queries)
```

Simple. Each layer does one thing well.

---

## API

The backend exposes a clean REST API. Full documentation at `/docs` when you run the server.

**Auth:** Login, register, logout, extend session

**Queries:** Execute, format, history, saved queries

**Schema:** List databases, get table structures

---

## What's Next

Done:
- [x] Query caching
- [x] Saved queries with tags
- [x] Keyboard shortcuts
- [x] Mobile responsive
- [x] Toast notifications

Coming:
- [ ] Query execution plan visualization
- [ ] Collaborative sharing
- [ ] Database diagrams
- [ ] PostgreSQL and MySQL support

---

## Contributing

Found a bug? Have an idea? Open an issue or submit a PR. I read everything.

---

## About Me

I'm **Khalid Abdelaty**, a Data Engineer who likes building tools that solve real problems. This project came from my own frustration with not having a safe place to experiment with SQL.

[LinkedIn](https://www.linkedin.com/in/khalidabdelaty/)

---

<div align="center">
  <sub>Built by Khalid Abdelaty · 2025</sub>
</div>
