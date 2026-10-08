# 🎓 Smart Campus Connect

<p align="center">
  <img src="assets/smart_campus_banner.jpg" alt="Smart Campus Connect Banner" width="100%">
</p>

> **A unified student lifecycle management platform for academic tracking, campus navigation, event discovery, and peer connections.**

[![Python](https://img.shields.io/badge/Python-3.13+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5+-3178C6.svg)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3+-38B2AC.svg)](https://tailwindcss.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Overview

Smart Campus Connect is a full-stack campus management platform built for students, faculty, and administrators. It combines academic tracking, campus navigation, event discovery, study room booking, and social features into one unified application.

### Key Features

| Module | Features |
|--------|----------|
| **Authentication** | JWT-based auth, role-based access (Student/Faculty/Admin), CPUT email validation |
| **Courses** | Course CRUD, enrollment, credit tracking, department/semester organization |
| **Events** | Event discovery, registration, categories (Workshop/Career/Social/Academic), attendee tracking |
| **Study Rooms** | Room search by building/capacity/equipment, real-time availability, booking system |
| **Dashboard** | Personalized stats, quick actions, recent activity feed |
| **Profile** | Account settings, role display, notification preferences |

---

## Tech Stack

### Backend
- **Framework:** FastAPI (Python 3.13+)
- **Database:** In-memory repositories (Repository Pattern) — easily swappable for PostgreSQL/MySQL
- **Auth:** JWT tokens with secure password hashing
- **Patterns:** Factory, Builder, Singleton, Prototype, Abstract Factory, Repository Pattern
- **API Docs:** Auto-generated Swagger UI (`/docs`) & ReDoc (`/redoc`)

### Frontend
- **Framework:** React 18 + TypeScript + Vite
- **Styling:** Tailwind CSS (dark mode support)
- **Routing:** React Router v6
- **State:** React Context + Hooks
- **HTTP:** Axios with interceptors
- **Icons:** Lucide React

---

## Quick Start

### Prerequisites
- Python 3.13+
- Node.js 18+ (for frontend)
- Git

### 1. Clone & Setup Backend
```bash
git clone <your-repo-url>
cd smart-campus-connect
pip install -r requirements.txt
```

### 2. Start Backend API
```bash
uvicorn src.api.main:app --reload --host 127.0.0.1 --port 8000
```
- API: http://127.0.0.1:8000
- Swagger UI: http://127.0.0.1:8000/docs
- Health: http://127.0.0.1:8000/health

### 3. Start Frontend (New Terminal)
```bash
cd frontend
npm install
npm run dev
```
- UI: http://localhost:5173

---

## Project Structure

```
smart-campus-connect/
├── src/
│   ├── api/
│   │   ├── main.py              # FastAPI app entry point
│   │   ├── models/schemas.py    # Pydantic models
│   │   └── routes/              # API endpoints
│   │       ├── users.py         # Auth & user management
│   │       ├── courses.py       # Course CRUD & enrollment
│   │       ├── assignments.py   # Assignments & grading
│   │       └── bookings.py      # Study room bookings
│   ├── creational_patterns/     # Design pattern implementations
│   ├── domain/                  # Domain models (User, Course, etc.)
│   ├── factories/               # Repository factory
│   ├── repositories/            # Repository interfaces & implementations
│   └── services/                # Business logic layer
├── frontend/                    # React + TypeScript + Vite app
│   ├── src/
│   │   ├── components/          # Shared components (Layout)
│   │   ├── context/             # React Context (Auth)
│   │   ├── pages/               # Page components
│   │   │   ├── AuthPage.tsx     # Login/Register
│   │   │   ├── DashboardPage.tsx
│   │   │   ├── CoursesPage.tsx
│   │   │   ├── EventsPage.tsx
│   │   │   ├── RoomsPage.tsx
│   │   │   └── ProfilePage.tsx
│   │   └── services/api.ts      # Axios API client
│   └── ...
├── tests/                       # Unit tests (65 tests passing)
├── docs/                        # Architecture & design docs
├── requirements.txt             # Python dependencies
└── README.md
```

---

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/users/register` | Register new user |
| POST | `/api/users/login` | Login & get JWT token |
| GET | `/api/users/me` | Get current user (requires Bearer token) |
| GET | `/api/users/{user_id}` | Get user by ID |
| GET | `/api/users/` | List all users |

### Courses
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/courses/` | Create course (Faculty/Admin) |
| GET | `/api/courses/` | List all courses |
| GET | `/api/courses/{id}` | Get course details |
| POST | `/api/courses/{id}/enroll/{student_id}` | Enroll student |

### Events
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/events/` | List events |
| POST | `/api/events/` | Create event |
| POST | `/api/events/{id}/register` | Register for event |

### Study Rooms & Bookings
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/bookings/rooms` | List all rooms |
| GET | `/api/bookings/rooms/available` | List available rooms |
| POST | `/api/bookings/` | Create booking |
| GET | `/api/bookings/` | List user bookings |
| DELETE | `/api/bookings/{id}` | Cancel booking |

---

## Design Patterns Implemented

This project demonstrates **six creational design patterns** in `src/creational_patterns/`:

| Pattern | File | Purpose |
|---------|------|---------|
| Simple Factory | `simple_factory.py` | Creates User objects (Student, Faculty, Admin) |
| Factory Method | `factory_method.py` | Creates Payment Processors (Credit Card, PayPal) |
| Abstract Factory | `abstract_factory.py` | Creates UI component families (Windows/MacOS) |
| Builder | `builder.py` | Builds complex Assignment objects |
| Prototype | `prototype.py` | Clones Notification templates |
| Singleton | `singleton.py` | Single DatabaseConnection instance |

**Repository Pattern** in `src/repositories/` with:
- Abstract interfaces for each entity
- In-memory implementations (production-ready)
- Factory for storage backend selection
- Stubs for future PostgreSQL/MySQL backends

---

## Testing

```bash
# Run all tests (65 tests)
python -m unittest discover tests -v

# Or with pytest
python -m pytest -v
```

All tests pass covering:
- Creational design patterns
- Repository implementations
- Service layer business logic
- API endpoints

---

## Development

### Adding a New Storage Backend
1. Implement repository interfaces in `src/repositories/`
2. Register in `src/factories/repository_factory.py`
3. Update `storage_type` in service initialization

### Frontend Development
```bash
cd frontend
npm run dev          # Start dev server
npm run build        # Production build
npm run preview      # Preview production build
```

---

## Deployment

### Backend (Production)
```bash
# Using Gunicorn + Uvicorn workers
gunicorn src.api.main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000

# Or Docker
docker build -t smart-campus-connect .
docker run -p 8000:8000 smart-campus-connect
```

### Frontend (Production)
```bash
cd frontend
npm run build
# Serve dist/ with nginx, Vercel, Netlify, etc.
```

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

## Author

**Divyanshu Tiwari**  
*Entrepreneurship Development*

---

## Contributors

- **Ayush3038** — Collaborator

---

## Acknowledgments

- Built as part of the Smart Campus Connect academic project
- Design patterns implementation inspired by Gang of Four patterns
- Repository pattern for clean architecture