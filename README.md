# tentiq

Full-stack prototype for running campaign-based UX tests with a Lightning-payment flow:
- `backend/`: FastAPI API for campaign creation, assignment, completion tracking, and payouts.
- `frontend/`: Next.js app that fetches the current campaign and renders the campaign variant in an iframe for testers.

## Project Description

This project lets an agent create testing campaigns with multiple variants, then serves those campaigns to users one by one.  
When users complete tasks, the backend records metrics and handles payout flow logic via Lightning invoice integrations.

Main capabilities:
- Campaign creation and payment status checks (`/api/agent/*`)
- User variant assignment and task completion (`/api/user/*`)
- SDK-style event/session endpoints (`/sdk/*`)
- Frontend test-session UI that loads and advances campaigns

## Setup Instructions

### 1) Prerequisites

- Python 3.11+ (recommended)
- Node.js 18+ and npm
- PostgreSQL (local or remote)

### 2) Backend setup (`backend`)

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
cp .env.example .env
```

Set `DATABASE_URL` in `backend/.env` (example is provided in `backend/.env.example`).

Run backend:

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Backend will be available at `http://localhost:8000` and API docs at `http://localhost:8000/docs`.

### 3) Frontend setup (`frontend`)

```bash
cd frontend
npm install
npm run dev
```

Frontend will run at `http://localhost:3000`.

### 4) Running the full project

Start backend (`:8000`) and frontend (`:3000`) in separate terminals.

## Dependencies and Environment Files

### Backend dependencies

Defined in `backend/requirements.txt`:
- `fastapi`
- `uvicorn[standard]`
- `SQLAlchemy`
- `psycopg[binary]`
- `pydantic-settings`
- `aiohttp`
- `certifi`
- `nostr-sdk`

### Frontend dependencies

Defined in `frontend/package.json`:
- Runtime: `next`, `react`, `react-dom`
- Dev: `typescript`, `eslint`, `eslint-config-next`, `tailwindcss`, `@tailwindcss/postcss`, `@types/node`, `@types/react`, `@types/react-dom`

### Environment files

- `backend/.env.example` (template)
- `backend/.env` (local, create from template)
