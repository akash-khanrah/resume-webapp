# 💙 Neon 3D Portfolio — React × FastAPI × MySQL

A stylish **blue-black 3D** portfolio web app that works on **mobile, tablet, laptop & computer**.

## ✨ Features

| Section | What it does |
|---|---|
| 🏠 **Home** | Typing animation, 3D tilt code card, stats strip, social links |
| 👨‍💻 **About** | Story, language chips (Python 🐍 JS ⚡ SQL 🐬…), animated skill bars |
| 🚀 **Projects** | Your real files only — drop in `backend/uploads/projects/`, auto-listed (multi-file, anytime) |
| 📄 **Resume** | Owner's PDF resume only — inline viewer + **Download** (backend-managed, seen-only) |
| 🎪 **Fun Zone** | Joke / Fact / Quote machine + fake “Hack Me” terminal 😂 |
| 📩 **Contact** | Email + GitHub + LinkedIn cards, **SMS-style form → saved to MySQL** 🐬 |
| 🤖 **AI Face** | Live avatar that **changes every 2 minutes** with countdown ⏳ |

Plus: matrix code-rain background, cursor glow, floating Hire-Me button, toasts, confetti 🎉.

## 🗂️ Project structure

```
portfolio-app/
├── backend/            # FastAPI + MySQL (SQLite fallback for preview)
│   ├── main.py         # ★ edit PROFILE / PROJECTS / RESUME here
│   ├── database.py     # MySQL via env, else local SQLite
│   ├── models.py       # contact_messages table
│   └── requirements.txt
├── frontend/           # React + Vite (no UI libs, pure neon CSS)
│   └── src/
│       ├── config.js   # ★ edit your name/links here (instant UI update)
│       ├── App.jsx
│       ├── components/ # MatrixRain, AIFace, FunZone
│       └── index.css   # blue-black 3D theme
└── README.md
```

## 🚀 Run it (2 terminals)

**Terminal 1 — backend (port 8000):**
```bash
cd portfolio-app/backend
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```
API docs: http://localhost:8000/docs

**Terminal 2 — frontend (port 5173):**
```bash
cd portfolio-app/frontend
npm install
npm run dev
```
Open: http://localhost:5173

> The Vite dev server proxies `/api/*` → FastAPI, so no CORS hassle.

## 📄 Resume PDF (backend only, seen-only on site)

The PDF lives **only in backend** at `backend/uploads/resume.pdf`. The website shows it **seen-only** (inline viewer + download) — no upload buttons on the public site. 2 ways to set it:

1. **Send it here:** attach your PDF in chat and I'll place it for you.
2. **Manually:** copy your file to `portfolio-app/backend/uploads/resume.pdf` and refresh.

Public API: `GET /api/resume/pdf` (view) • `GET /api/resume/pdf-info` (file info).

## 📁 Project files (any type, backend only, seen-only)

Drop **any file type** — images 🖼️, videos 🎬, audio 🎵, PDF 📄, ZIP 📦, code 💻 — into `backend/uploads/projects/` and it appears automatically in the site's **Projects → 📁 Project Files** gallery (images preview, videos/audio play inline, others open/download). No upload buttons on the public site — backend only.

Public API: `GET /api/projects/files` (list) • `GET /api/projects/files/{name}` (view/download).

## 💣 Mine Game

Neon Minesweeper in the **Game** section: Easy 8×8, Medium 10×10, Hard 12×12, timer, flags (right-click or Flag-mode on mobile), first-click safety, funny win/lose messages. Pure React — no backend needed.

## 🚀 Start Page (opens first)

The site now has **3 pages**: ① 🚀 start screen (opens first — clean welcome + Start Website button only, Enter ⏎ works too) ② main portfolio ③ offline status page. Pressing Start enters the site — if the API is down you'll land on the status page with retry + offline options instead.

## 📡 Page 3 — Offline / Status page

The **offline page opens** with a live 🕐 clock (works fully offline), status rows, auto re-check every 10s, a Retry button, and shortcuts to the site / 💣 Mine Game (playable offline!). Click the navbar 🟢/🔴 badge or the footer Status link anytime to view it. An auto offline banner appears on top of the main page when the API is down — click it to open the status page.

## 📱 App interface (mobile + installable)

The website works like a **mobile app**: bottom navigation bar on phones (Home • Projects • Resume • Game • Contact with live active state), standalone display mode, theme colors and a PWA manifest — phones offer **"Add to Home Screen"** for a fullscreen app feel. 📲

## 🔐 Admin login + SMS inbox (new page)

**Login only** (no signup, admin only). Click the navbar 🟢/🔴 **API badge** or the footer Admin link → the **login page** opens → after login you see **all SMS-style messages** with Refresh + Delete. Pressing **Back/Site = automatic logout** 🔒.

- Defaults: username `admin` • password `akash123` • API key `akash-portfolio-key-2026`
- Change via env: `ADMIN_USERNAME` / `ADMIN_PASSWORD` / `ADMIN_API_KEY`
- Endpoints: `POST /api/auth/login` • `GET /api/contact/messages?x_api_key=...` 🔐 • `DELETE /api/contact/messages/{id}` 🔐

## 🐬 MySQL (auto-connect + auto-fallback, zero red errors)

Your settings are **baked in as defaults**: host `localhost` • user `root` • password `akash007` • database `proatfulio` • table `contacts`.

- MySQL running? Backend **creates the database + table automatically** and uses it. 🐬
- MySQL down? It **falls back to SQLite** (`backend/portfolio.db`) with a warning — never crashes. 🛟
- Override anytime via env: `MYSQL_HOST` / `MYSQL_PORT` / `MYSQL_USER` / `MYSQL_PASSWORD` / `MYSQL_DB`, or full `DATABASE_URL="mysql+pymysql://user:pass@host:port/db"`.
- View messages (after admin login): `GET /api/contact/messages?x_api_key=...` 🔐

Without these vars, messages save to `backend/portfolio.db` (SQLite) — same API, zero setup. ✅

## ✏️ Make it YOURS (2 minutes)

1. `frontend/src/config.js` → name, email, phone, GitHub, LinkedIn.
2. `backend/main.py` → `PROFILE`, `PROJECTS`, `RESUME` dicts (same data, for API).
3. Restart both servers. Done! 🎉

## 🌐 Single-server deploy (optional)

```bash
cd portfolio-app/frontend && npm run build
cd ../backend && uvicorn main:app --host 0.0.0.0 --port 8000
```
FastAPI auto-serves `frontend/dist` at `/` — one port hosts everything.

---
Built with React ⚛️ + FastAPI 🐍 + MySQL 🐬 • No bugs, only features 🐛✨
