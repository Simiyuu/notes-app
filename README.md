# NoteKeeper

A full-stack web application for creating and managing personal notes, built with Node.js, Express, and MySQL.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML, CSS, JavaScript |
| Backend | Node.js + Express |
| Database | MySQL via phpMyAdmin |
| Runtime | Node.js |

---

## Features

- User registration with username, email and password
- Secure login and logout
- Create, view and delete personal notes
- Server-side session storage in MySQL — no cookies used
- Each user can only access their own notes
- Data persists in MySQL and is visible in phpMyAdmin

---

## Project Structure

```
notes-app/
├── server.js          # Express backend, API routes, DB connection
├── package.json       # Project dependencies
└── public/
      ├── index.html   # App structure and markup
      ├── styles.css   # All styling and CSS variables
      └── app.js       # Frontend logic, API calls, auth handling
```

---

## Database Structure

Three tables are created automatically on server start:

**users** — stores registered accounts
| Column | Type |
|--------|------|
| id | VARCHAR(36) PRIMARY KEY |
| username | VARCHAR(100) UNIQUE |
| email | VARCHAR(255) UNIQUE |
| password | VARCHAR(100) |
| created_at | TIMESTAMP |

**sessions** — stores active login tokens (no cookies)
| Column | Type |
|--------|------|
| token | VARCHAR(36) PRIMARY KEY |
| user_id | VARCHAR(36) FOREIGN KEY |
| created_at | TIMESTAMP |

**notes** — stores user notes
| Column | Type |
|--------|------|
| id | VARCHAR(36) PRIMARY KEY |
| user_id | VARCHAR(36) FOREIGN KEY |
| title | VARCHAR(255) |
| content | TEXT |
| created_at | TIMESTAMP |

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org) installed
- [XAMPP](https://www.apachefriends.org) installed with Apache and MySQL running

### Installation

1. Clone the repository
```bash
git clone https://github.com/YOURUSERNAME/notes-app.git
cd notes-app
```

2. Install dependencies
```bash
npm install
```

3. Start XAMPP and make sure Apache and MySQL are running

4. Start the server
```bash
node server.js
```

5. Open your browser and go to
```
http://localhost:3000
```

The database and all tables are created automatically on first run.

---

## Session Management

This application does not use cookies for session storage. On login the server generates a unique token, stores it in the MySQL `sessions` table, and returns it to the client. The client stores it in `localStorage` and sends it as an `Authorization` header on every request. The server validates the token against the database on each protected route. Logging out deletes the token from the database immediately.

---

## API Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | /api/register | Register a new user | No |
| POST | /api/login | Login and receive token | No |
| POST | /api/logout | Logout and delete token | Yes |
| GET | /api/notes | Get all notes for user | Yes |
| POST | /api/notes | Create a new note | Yes |
| DELETE | /api/notes/:id | Delete a note | Yes |

---

## Unit

BIT3208 — Advanced Web Design and Development