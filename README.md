# AI Interview Trainer

End-to-end AI-powered interview coaching platform built with **FastAPI** (backend) and **Streamlit** (frontend).

---

## Features

- 🎤 **AI Question Generation** — context-aware questions tailored to role, difficulty, and topic
- 🤖 **AI Answer Evaluation** — structured feedback with score, strengths, improvements, and model answer
- 📊 **Session History** — review past sessions and track progress over time
- 🔐 **JWT Auth** — secure register/login flow
- 🗄️ **Vector Store** — ChromaDB-backed similarity search for question retrieval

---

## Project Structure

```
Interview-Trainer-Agent/
├── backend/                   # FastAPI application
│   ├── main.py                # App entry point
│   ├── core/                  # Config, security, logging, DI
│   ├── api/v1/endpoints/      # Route handlers (auth, sessions, questions, feedback)
│   ├── agents/                # LLM agents + vector store
│   ├── services/              # Business logic layer
│   ├── models/                # SQLAlchemy ORM models
│   ├── schemas/               # Pydantic request/response schemas
│   └── db/                    # Engine, session factory, init script
│
├── frontend/                  # Streamlit application
│   ├── app.py                 # Entry point / navigation shell
│   ├── api_client.py          # HTTP client for backend API
│   ├── state.py               # st.session_state helpers
│   ├── components.py          # Reusable UI widgets
│   └── pages/                 # One file per page (home, practice, history, settings)
│
├── data/                      # Seed/reference data
├── vector_db/                 # Persisted ChromaDB collections
├── docs/                      # Architecture docs, ADRs
└── tests/                     # Pytest test suite
```

---

## Quick Start

### 1. Install dependencies

```bash
pip install -e ".[dev]"
```

### 2. Configure environment

```bash
cp .env.example .env
# Edit .env — set OPENAI_API_KEY at minimum
```

### 3. Initialise the database

```bash
python -m backend.db.init_db
```

### 4. Start the backend

```bash
uvicorn backend.main:app --reload --port 8000
```

### 5. Start the frontend

```bash
streamlit run frontend/app.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

---

## Running Tests

```bash
pytest tests/ -v
```

---

## Docker Compose

```bash
docker compose up --build
```

---

## Environment Variables

| Variable | Default | Description |
|---|---|---|
| `OPENAI_API_KEY` | — | Your OpenAI API key |
| `LLM_MODEL` | `gpt-4o-mini` | Model to use for generation |
| `SECRET_KEY` | `changeme` | JWT signing secret |
| `DATABASE_URL` | SQLite local file | SQLAlchemy connection string |
| `VECTOR_DB_PATH` | `vector_db` | ChromaDB persistence path |
| `API_BASE_URL` | `http://localhost:8000/api/v1` | Frontend → backend URL |
