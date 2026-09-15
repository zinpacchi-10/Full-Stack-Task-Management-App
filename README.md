# Task Management App (MERN Stack)

A full-stack Task Management application — a simplified Trello/Asana clone — built with **MongoDB, Express.js, React, and Node.js (MERN)**. Includes JWT authentication, full CRUD for tasks/projects, filtering & sorting, and a responsive UI.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React (Vite or CRA), React Router, Axios, Context API / Redux Toolkit |
| Backend | Node.js, Express.js |
| Database | MongoDB + Mongoose |
| Auth | JWT (jsonwebtoken), bcrypt for password hashing |
| Styling | Tailwind CSS / CSS Modules |
| Validation | Joi or express-validator |
| Dev Tools | Nodemon, dotenv, ESLint, Prettier |
| Testing | Jest, React Testing Library, Supertest |
| Deployment | Frontend → Vercel/Netlify, Backend → Render/Railway, DB → MongoDB Atlas |

---

## Project Structure

```
task-manager-app/
├── client/                        # React frontend
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/            # Reusable UI: Button, Modal, TaskCard, Navbar
│   │   ├── pages/                 # Login, Register, Dashboard, ProjectBoard
│   │   ├── context/ or store/     # Auth context / Redux store
│   │   ├── hooks/                 # useAuth, useFetch, useTasks
│   │   ├── services/              # Axios API calls (api.js, taskService.js)
│   │   ├── utils/                 # helpers, constants
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── .env
│   └── package.json
│
├── server/                        # Express backend
│   ├── config/
│   │   └── db.js                  # MongoDB connection
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── taskController.js
│   │   └── projectController.js
│   ├── middleware/
│   │   ├── authMiddleware.js      # JWT verification
│   │   ├── errorMiddleware.js
│   │   └── validateMiddleware.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Task.js
│   │   └── Project.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── taskRoutes.js
│   │   └── projectRoutes.js
│   ├── utils/
│   │   └── generateToken.js
│   ├── .env
│   ├── server.js
│   └── package.json
│
├── .gitignore
└── README.md
```

---

## Roadmap (Phased Build Order)

### Phase 1 — Planning & Setup
- Define core entities: `User`, `Task`, `Project` (optional grouping layer)
- Design MongoDB schemas and relationships (User → owns → Tasks/Projects)
- Set up two repos or one monorepo with `client/` and `server/` folders
- Initialize Git, `.gitignore`, base `package.json` in both folders

### Phase 2 — Backend Foundation
- Set up Express server (`server.js`), connect MongoDB via Mongoose
- Build `User` model with hashed passwords (bcrypt)
- Build `Task` model: title, description, status, priority, dueDate, owner (ref User)
- Set up environment variables (`.env`): `PORT`, `MONGO_URI`, `JWT_SECRET`

### Phase 3 — Authentication (JWT)
- `POST /api/auth/register` — hash password, create user
- `POST /api/auth/login` — verify password, issue JWT
- `authMiddleware.js` — verify JWT on protected routes
- Optional: refresh tokens, `GET /api/auth/me` for current user

### Phase 4 — Task CRUD API
- `POST /api/tasks` — create task
- `GET /api/tasks` — list tasks (with filtering/sorting query params)
- `GET /api/tasks/:id` — get single task
- `PUT /api/tasks/:id` — update task
- `DELETE /api/tasks/:id` — delete task
- Restrict all routes to authenticated, task-owning users

### Phase 5 — Filtering, Sorting & Search
- Query params: `?status=in-progress&priority=high&sortBy=dueDate&search=keyword`
- Implement filtering logic in controller using Mongoose query building
- Add pagination if task volume is expected to be large (`?page=&limit=`)

### Phase 6 — Frontend Foundation
- Set up React app (Vite recommended for faster dev builds)
- Set up React Router: `/login`, `/register`, `/dashboard`
- Build Axios instance with base URL + JWT interceptor (attach token to headers)
- Build Auth Context/Redux slice to store user + token (persist in localStorage)

### Phase 7 — Frontend Core Features
- Login/Register forms with validation
- Protected route wrapper (`PrivateRoute`) that checks auth state
- Dashboard: list tasks fetched from API
- TaskCard, TaskForm (create/edit), Modal for task details
- Filter/sort controls wired to API query params

### Phase 8 — UI/UX Polish
- Responsive layout (mobile-first, Tailwind or CSS Grid/Flexbox)
- Loading states, error boundaries, toast notifications
- Optional: drag-and-drop board view (`react-beautiful-dnd` or `@dnd-kit`) for a Trello-style board

### Phase 9 — Testing
- Backend: unit tests for controllers (Jest), integration tests for routes (Supertest)
- Frontend: component tests (React Testing Library)
- Manual QA pass across auth flow and CRUD operations

### Phase 10 — Deployment
- Backend → Render or Railway (set env vars there)
- Frontend → Vercel or Netlify (set `VITE_API_URL` env var)
- Database → MongoDB Atlas (whitelist deployment IPs)
- Add CORS config on backend to allow frontend origin

---

## Getting Started (Local Dev)

```bash
# Clone repo
git clone <your-repo-url>
cd task-manager-app

# Backend
cd server
npm install
npm run dev        # requires nodemon script in package.json

# Frontend (new terminal)
cd client
npm install
npm run dev
```

### Required Environment Variables

**server/.env**
```
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```

**client/.env**
```
VITE_API_URL=http://localhost:5000/api
```

---

## Core API Endpoints (Reference)

| Method | Endpoint | Auth Required | Description |
|---|---|---|---|
| POST | `/api/auth/register` | No | Register new user |
| POST | `/api/auth/login` | No | Login, returns JWT |
| GET | `/api/auth/me` | Yes | Get current user |
| GET | `/api/tasks` | Yes | Get all tasks (filter/sort via query) |
| POST | `/api/tasks` | Yes | Create task |
| GET | `/api/tasks/:id` | Yes | Get single task |
| PUT | `/api/tasks/:id` | Yes | Update task |
| DELETE | `/api/tasks/:id` | Yes | Delete task |

---

## Notes on Accuracy

This roadmap reflects a standard, verifiable MERN architecture pattern used widely in production apps — no invented libraries, fictional APIs, or unverified claims. Package/tool choices (Mongoose, JWT, bcrypt, Vite, Tailwind, Render/Vercel/Atlas) are real, actively maintained tools as of 2026. Confirm current versions via `npm info <package>` before locking dependencies, since minor version numbers change over time.

---

## License

MIT
