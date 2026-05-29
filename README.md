# ✅ Todo REST API

A CRUD REST API built with **FastAPI** and **SQLite**, using **SQLAlchemy ORM** for database interaction. This project marks a step up from in-memory storage — all data is persisted in a real database and survives server restarts.

---

##  What Makes This Different From Previous Projects

| Feature | Previous Projects | This Project |
|---|---|---|
| Storage | In-memory Python list | SQLite database (persistent) |
| ORM | None | SQLAlchemy |
| DB Session | None | `Depends(get_db)` injection |
| Data models | Plain class / dict | SQLAlchemy `Column` models |
| Data survives restart | ❌ | ✅ |

---

##  What I Learned

- Setting up **SQLAlchemy** with FastAPI
- Creating database models with `Column` types
- Using **dependency injection** with `Depends(get_db)` for session management
- Safely handling DB sessions with `yield` and `try/finally`
- Performing real **database CRUD** — query, add, commit, delete
- Using `Annotated` for cleaner dependency typing

---

##  Getting Started

### Prerequisites

- Python 3.8+
- FastAPI
- Uvicorn
- SQLAlchemy

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/todo-api-fastapi-sqlite.git
cd todo-api-fastapi-sqlite

# Install dependencies
pip install fastapi uvicorn sqlalchemy

# Run the server
uvicorn main:app --reload
```

API runs at `http://127.0.0.1:8000`

> Interactive docs at `http://127.0.0.1:8000/docs`

The SQLite database file `todos.db` is created automatically on first run.

---

##  Data Structure

### Todo model

| Field         | Type    | Validation              | Description               |
|---------------|---------|-------------------------|---------------------------|
| `id`          | int     | Auto-generated          | Primary key               |
| `title`       | string  | min 3 characters        | Todo title                |
| `description` | string  | min 3, max 200 chars    | Todo description          |
| `priority`    | int     | 1–9                     | Priority level            |
| `complete`    | bool    | —                       | Completion status         |

---

##  API Endpoints

### GET

| Endpoint | Description |
|---|---|
| `GET /` | Fetch all todos |
| `GET /todo/{todo_id}` | Fetch a single todo by ID |

### POST

| Endpoint | Description |
|---|---|
| `POST /todo` | Create a new todo |

**Request body example:**
```json
{
  "title": "Learn SQLAlchemy",
  "description": "Study ORM models, sessions and queries",
  "priority": 8,
  "complete": false
}
```

### PUT

| Endpoint | Description |
|---|---|
| `PUT /todo/{todo_id}` | Update an existing todo by ID |

### DELETE

| Endpoint | Description |
|---|---|
| `DELETE /todo/{todo_id}` | Delete a todo by ID |

---

##  Error Responses

| Status | When |
|---|---|
| `404 Not Found` | Todo ID does not exist |
| `422 Unprocessable Entity` | Invalid or missing fields (auto-handled by FastAPI) |

---

## Project Structure

```
todo-api-fastapi-sqlite/
│
├── main.py        # All API routes and logic
├── models.py      # SQLAlchemy table model
├── database.py    # DB engine, session, and Base setup
├── todos.db       # SQLite database (auto-created)
└── README.md      # Project documentation
```

---

## Built With

- [FastAPI](https://fastapi.tiangolo.com/) — Web framework
- [SQLAlchemy](https://www.sqlalchemy.org/) — ORM and database toolkit
- [SQLite](https://www.sqlite.org/) — Lightweight persistent database
- [Pydantic](https://docs.pydantic.dev/) — Request validation
- [Uvicorn](https://www.uvicorn.org/) — ASGI server

---

## Future Improvements

- [ ] Add user authentication with JWT
- [ ] Associate todos with specific users
- [ ] Add filtering by `priority` and `complete` status
- [ ] Migrate from SQLite to PostgreSQL
- [ ] Add Alembic for schema migrations
- [ ] Write tests with `pytest` and FastAPI `TestClient`
- [ ] Containerize with Docker

---

*Built while progressing through FastAPI — first project using a real persistent database with SQLAlchemy ORM.*
