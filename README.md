# FastLibra 📚

A simple in-memory book management REST API built with **FastAPI**.  
No database required — books are stored in a Python dictionary at runtime.

---

## Features

- 📖 List all books
- 🔍 Get a single book by ID
- ➕ Add a new book
- ✏️ Partially update a book (PATCH)
- 🗑️ Delete a book

---

## Requirements

- Python 3.10+
- FastAPI
- Uvicorn (for running the server)

Install dependencies:

```bash
uv sync
```

---

## Running the App

Open project folder and run these commands:

```bash
# Activate Virtual Environment
source .venv/bin/activate

# Run the project
uv run fastapi dev
```

- API base URL: <http://127.0.0.1:8000>
- Interactive docs (Swagger UI): <http://127.0.0.1:8000/docs>
- Alternative docs (ReDoc): <http://127.0.0.1:8000/redoc>

---

## Endpoints

| Method | Path          | Description            |
| ------ | ------------- | ---------------------- |
| GET    | `/`           | Welcome message        |
| GET    | `/books`      | Get all books          |
| GET    | `/books/{id}` | Get one book by ID     |
| POST   | `/books`      | Add a new book         |
| PATCH  | `/books/{id}` | Update specific fields |
| DELETE | `/books/{id}` | Delete a book          |

---

## Book Schema

```json
{
  "title": "string",
  "author": "string",
  "year": 1925,
  "genre": "string",
  "pages": 180,
  "rating": 4.4
}
```

---

## Usage Examples

### Get all books

```bash
curl http://127.0.0.1:8000/books
```

### Get a single book

```bash
curl http://127.0.0.1:8000/books/3
```

### Add a new book

```bash
curl -X POST http://127.0.0.1:8000/books \
  -H "Content-Type: application/json" \
  -d '{
    "title": "The Alchemist",
    "author": "Paulo Coelho",
    "year": 1988,
    "genre": "Fiction",
    "pages": 208,
    "rating": 4.3
  }'
```

### Update a book (partial)

```bash
curl -X PATCH http://127.0.0.1:8000/books/3 \
  -H "Content-Type: application/json" \
  -d '{"rating": 4.9, "pages": 350}'
```

### Delete a book

```bash
curl -X DELETE http://127.0.0.1:8000/books/2
```

---

## Notes

- Data is stored **in memory only** — restarting the server resets everything.
- `PATCH` updates only the fields you send (`exclude_unset=True`), so partial updates work as expected.
- New book IDs are auto-assigned as `max(existing_ids) + 1`.

---

## Possible Improvements

- Persist data with a real database (SQLite, PostgreSQL)
- Add pagination, filtering, and search
- Add authentication
- Write automated tests with `pytest` + `TestClient`

---

## License

MIT — free to use and modify.
