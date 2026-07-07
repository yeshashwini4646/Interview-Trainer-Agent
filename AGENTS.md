# AI Agent Guide for Interview-Trainer-Agent

## Purpose
Help AI coding agents understand this repository quickly so they can make safe, useful changes without needing to infer project structure from scratch.

## Project overview
Interview-Trainer-Agent is an AI-powered interview coaching platform with:
- `backend/` — FastAPI application, auth, interview sessions, AI agents, and vector retrieval
- `frontend/` — Streamlit UI that calls the backend via a thin HTTP client
- `data/` — seed and sample question data
- `vector_db/` — persisted ChromaDB collections
- `docs/` — architecture and API docs
- `tests/` — pytest test suite

## Key commands
Use these commands when building, running, or testing:
- Install dependencies: `pip install -e ".[dev]"`
- Run backend: `uvicorn backend.main:app --reload --port 8000`
- Run frontend: `streamlit run frontend/app.py`
- Initialize database: `python -m backend.db.init_db`
- Run tests: `pytest tests/ -v`
- Docker compose: `docker compose up --build`

## Important files and directories
- `backend/main.py` — FastAPI app startup and RAG index builder
- `backend/api/v1/router.py` — API route registration
- `backend/agents/` — AI agents, Granite wrapper, embeddings, vector store
- `backend/core/` — app configuration, dependency injection, security, logging
- `backend/models/` — SQLAlchemy ORM models
- `backend/schemas/` — Pydantic request/response schemas
- `backend/services/` — business logic layer coordinating models and agents
- `frontend/app.py` — Streamlit app shell and navigation
- `frontend/api_client.py` — HTTP client used by the frontend
- `tests/` — test coverage for API endpoints, agents, RAG, resume parser, sessions

## Architecture notes
- The backend uses FastAPI with a single HTTP API at `api/v1`.
- The frontend is Streamlit-based and consumes backend APIs via `frontend/api_client.py`.
- The AI layer is built around IBM Watsonx Granite and ChromaDB.
- `backend/agents/watsonx_client.py` manages singleton Granite/embedding clients.
- `GraniteService` centralizes prompt formatting and JSON extraction.
- The RAG vector store is built on startup and persisted under `vector_db/`.

## Environment variables
The repo expects these env vars at runtime:
- `OPENAI_API_KEY` or underlying model credentials
- `SECRET_KEY`
- `DATABASE_URL`
- `VECTOR_DB_PATH`
- `API_BASE_URL`
- `WATSONX_API_KEY`, `WATSONX_PROJECT_ID`, `WATSONX_URL` (for Watsonx integration)

## Guidance for agents
- Prefer existing docs rather than duplicating them. See `README.md` and `docs/architecture.md`.
- Preserve the FastAPI / Streamlit separation when adding features.
- Keep AI prompt logic in `backend/agents/` and business logic in `backend/services/`.
- Do not assume a node/frontend build system; this is a Python-only repo.
- Keep test coverage in mind when changing behavior: use `tests/` and pytest fixtures.

## Useful references
- `README.md` — project overview, quick start, env vars
- `docs/architecture.md` — architecture and AI layer design
