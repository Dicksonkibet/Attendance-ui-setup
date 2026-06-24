# AttendTrack

A lightweight, browser-based attendance management system for schools, training centers, and small organizations. Sign up, create classes, enroll students, take attendance in a couple of clicks, and review attendance trends — all running entirely client-side.

## Features

- **Authentication** — Email/password sign up and sign in, with a live password-strength indicator and session-based login state.
- **Dashboard** — At-a-glance stats (total classes, enrolled students, sessions logged, average attendance rate) plus a feed of recent sessions and quick-action shortcuts.
- **Class management** — Create, edit, search, and delete classes, each showing live enrollment counts.
- **Student management** — Add, edit, search, and delete students; assign each student to a class and filter the roster by class.
- **Take Attendance** — Pick a class and date to generate a roster, mark each student Present / Late / Absent (defaults to Present), with one-click "mark all" actions, then save the session.
- **Reports** — Browse all attendance sessions with date/class filters and per-session detail view, or switch to a per-student summary showing total sessions, present/absent/late counts, and attendance rate.
- **Responsive UI** — Collapsible sidebar navigation with a mobile-friendly top bar and overlay menu.

## Tech Stack

- **HTML5** — semantic, multi-page structure (no SPA framework or bundler)
- **CSS3** — custom design system using CSS variables (colors, spacing, radii, typography), Inter + Space Grotesk fonts via Google Fonts
- **Vanilla JavaScript (ES6+)** — no frameworks, no build step, no external JS dependencies
- **Browser storage** — `localStorage` for persisted data, `sessionStorage` for the active login session

There is no backend server or database — the entire application runs in the browser.

## Project Structure

```
attendance-system/
├── index.html           # Sign in / Sign up page
├── dashboard.html        # Overview / stats dashboard
├── classes.html          # Class management
├── students.html         # Student management
├── attendance.html       # Take attendance
├── reports.html          # Session & student reports
├── css/
│   ├── auth.css          # Styles for the sign in / sign up page
│   └── app.css           # Shared app styles (sidebar, cards, tables, etc.)
└── js/
    ├── auth.js            # Sign up / sign in logic, password strength
    ├── app.js             # Session guard, nav state, shared data helpers, toasts
    ├── dashboard.js        # Dashboard stats and recent sessions
    ├── classes.js          # Class CRUD
    ├── students.js         # Student CRUD
    ├── attendance.js       # Attendance-taking workflow
    └── reports.js          # Session and student reporting/filtering
```

## Getting Started

No installation, build step, or server is required.

1. Download or clone this repository.
2. Open `index.html` directly in a modern browser (Chrome, Firefox, Edge, or Safari), **or** serve the folder with any static file server, for example:
   ```bash
   npx serve .
   # or
   python3 -m http.server 8000
   ```
3. Create an account from the **Create Account** tab, then sign in.

> Serving the folder over `http://localhost` (rather than opening the file directly via `file://`) is recommended for the most consistent behavior across browsers.

## Usage

1. **Sign up / Sign in** on the landing page.
2. **Create a class** from the Classes page (e.g. "Grade 10 — Mathematics").
3. **Add students** from the Students page and assign each one to a class.
4. **Take attendance** by selecting a class and date, marking each student, and saving the session.
5. **Review reports** by session or by student, with date-range and class filters.

## Data & Storage Notes

All application data is stored locally in the browser:

- Registered users are stored under a single `localStorage` key.
- Each signed-in user's classes, students, and attendance sessions are stored under per-user keys (scoped by user ID), so different accounts in the same browser don't see each other's data.
- The active login session lives in `sessionStorage` and is cleared on logout or when the browser tab/session ends.

**Limitations to be aware of:**

- Data is stored only in the current browser on the current device — it is not synced across devices or browsers and will be lost if site data/storage is cleared.
- This is a front-end demo/prototype data layer, not a secure backend: credentials and records are stored in plain form in browser storage rather than in a database with proper hashing and access controls. Do not use this as-is to store real, sensitive, or production student data.
- There is no automated backup or export feature for the underlying data.

## Browser Support

Works in any modern evergreen browser (Chrome, Firefox, Edge, Safari) with `localStorage`/`sessionStorage` support and JavaScript enabled.

## Roadmap Ideas

- Server-side persistence with a real database and authentication (hashed passwords, sessions/JWT)
- CSV/Excel export of attendance reports
- Bulk student import
- Email/SMS notifications for absences
- Multi-user roles (admin, teacher) within one organization

## License
Licensed under the Apache License, Version 2.0 — see the LICENSE file for details.
