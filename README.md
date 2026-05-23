# ◈ Cardsmith — Profile Card Generator

A full-stack app that accepts user input via a form, sends a POST request to a FastAPI backend, processes/validates the data, and returns a formatted profile card rendered on the same page.

## Project Structure

```
profilecard/
├── backend/
│   └── main.py        # FastAPI app — validation, processing, in-memory store
├── frontend/
│   └── index.html     # Single-page UI served by FastAPI
└── requirements.txt
```

## Setup & Run

### 1. Install dependencies
```bash
cd profilecard
pip install -r requirements.txt
```

### 2. Start the server
```bash
cd backend
uvicorn main:app --reload --port 8000
```

### 3. Open the app
```
http://localhost:8000
```

---

## API Reference

### POST `/api/profile`
Creates and returns a formatted profile card.

**Request body (JSON):**
```json
{
  "name":      "Aria Chen",           // required
  "username":  "aria_chen",           // required, alphanumeric + _ -
  "bio":       "Designer & explorer", // required, max 280 chars
  "role":      "Product Designer",    // optional
  "location":  "Tokyo, JP",           // optional
  "website":   "https://aria.dev",    // optional
  "image_url": "https://...",         // optional
  "tags":      "design, ux, code"     // optional, comma-separated
}
```

**Response (201):**
```json
{
  "id": "a3f9c12e4b",
  "name": "Aria Chen",
  "username": "aria_chen",
  "bio": "Designer & explorer",
  "role": "Product Designer",
  "location": "Tokyo, JP",
  "website": "https://aria.dev",
  "image_url": "https://...",
  "tags": ["design", "ux", "code"],
  "avatar_color": "#8e44ad",
  "initials": "AC",
  "created_at": "May 23, 2025",
  "card_number": 1
}
```

### GET `/api/profiles`
Returns all generated cards (most recent first).

### DELETE `/api/profile/{id}`
Removes a card by ID.

---

## Key Concepts Demonstrated
- **POST request handling** — form data serialized to JSON, sent to backend
- **Pydantic validation** — required fields, length limits, username sanitization
- **Data processing** — server derives `initials`, `avatar_color`, `card_number` from input
- **Response → UI** — backend JSON is consumed by JS to render a styled card
- **In-memory store** — cards persist for the server session (no DB needed)
