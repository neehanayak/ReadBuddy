# ReadBuddy

A lightweight Chrome extension + backend that helps students understand dense terminology in research papers via AI-powered, context-aware explanations.

## Features

- Highlight → right-click → “Explain with AI” flow
- Short, plain-English explanations with “Explain further” and “Ask follow-up”
- FastAPI backend with CORS and health checks
- Ready for RAG (Pinecone/Chroma) and multiple LLMs (OpenAI/Anthropic)
- Dockerized services and basic CI

## Project Structure
## Two‑Week Plan (Daily Goals)

Week 1 — Backend Core + RAG Pipeline  
- Day 1: Project setup  
  - Create GitHub repo, set up .env.example  
  - Scaffold repo structure (backend/, frontend/, docker-compose.yml)  
  - Setup Python virtual env + install FastAPI, Uvicorn  
  - Run “Hello World” FastAPI server
- Day 2: Backend APIs skeleton  
  - Set up routers/, services/  
  - Create /health endpoint  
  - Add .gitignore, requirements.txt  
  - CI skeleton (GitHub Actions basic test to run pytest --version)
- Day 3: LLM abstraction layer  
  - Implement LLMProvider for OpenAI  
  - Write /query endpoint (non-streaming)
- Day 4: Vector DB integration  
  - Add Pinecone or Chroma support (vectorstore.py)  
  - /ingest endpoint (upload → chunk → embed → store) with metadata
- Day 5: RAG pipeline (non-streaming)  
  - Ingest → retrieve context → call LLM → answer
- Day 6: Streaming responses  
  - Upgrade /query to stream tokens via StreamingResponse
- Day 7: Add second LLM  
  - Anthropic or local  
  - .env switch LLM_PROVIDER=anthropic|openai|local

Week 2 — Frontend + Analytics + Deployment  
- Day 8: Frontend scaffold (Next.js / Tailwind)  
- Day 9: Streaming chat UI  
- Day 10: Analytics logging (Backend → Postgres)  
- Day 11: Analytics dashboard (Frontend)  
- Day 12: Dockerization (both services + db)  
- Day 13: CI/CD (build/push images, optional deploy)  
- Day 14: Wrap-up + Docs + smoke tests

Milestones  
- End of Week 1 → RAG backend service working (local docs + OpenAI/Anthropic)  
- End of Week 2 → Full platform: streaming chat UI, analytics, Dockerized, ready to deploy

## Prerequisites

- Python 3.10+ (3.11 recommended)
- Node.js 18+ (for frontend, in Week 2)
- Docker & Docker Compose (optional, for containerized dev)
- Git

## Quickstart (Backend, Local)

1) Clone and enter repo:
```bash
git clone <your-repo-url> readbuddy
cd readbuddy/backend
Create and activate virtual environment:
bash
Copy
python -m venv venv
# macOS/Linux
source venv/bin/activate
# Windows PowerShell
# .\venv\Scripts\Activate.ps1
Install dependencies:
bash
Copy
pip install --upgrade pip
pip install -r requirements.txt
Set environment variables:
bash
Copy
cd ..
cp .env.example .env
# Open .env and fill values as needed, e.g. ALLOWED_ORIGINS for local testing
Run the API:
bash
Copy
cd backend
# Option A
python main.py
# Option B
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
Verify:
Root: http://localhost:8000/
Health: http://localhost:8000/health
Swagger: http://localhost:8000/docs
ReDoc: http://localhost:8000/redoc
Expected root response:

json
Copy
{ "message": "Hello World from ReadBuddy API!", "status": "running", "version": "1.0.0" }
Environment Variables
Copy .env.example to .env and adjust as needed:

LLM settings
LLM_PROVIDER=openai | anthropic | local
OPENAI_API_KEY
ANTHROPIC_API_KEY
Vector DB
VECTOR_DB=pinecone | chroma
PINECONE_API_KEY
PINECONE_ENVIRONMENT
PINECONE_INDEX_NAME=readbuddy
Database
DATABASE_URL=postgresql://postgres:postgres@db:5432/readbuddy
Server
BACKEND_PORT=8000
FRONTEND_PORT=3000
CORS
ALLOWED_ORIGINS=http://localhost:3000,chrome-extension://*
Run with Docker (Backend + DB + Frontend scaffold)
From repo root:

bash
Copy
docker-compose up --build
Backend: http://localhost:8000
Frontend (placeholder until Day 8): http://localhost:3000
Postgres: localhost:5432 (user: postgres, pass: postgres, db: readbuddy)
Stop:

bash
Copy
docker-compose down
CI
A basic GitHub Actions workflow is included:

Checks out the repo
Installs backend dependencies
Runs pytest --version (placeholder until tests are added)
Runs flake8 (syntax checks + warnings)
See .github/workflows/ci.yml.

Roadmap Details
LLM Abstraction: Unified interface to plug OpenAI, Anthropic, or a local model
RAG: Ingestion, chunking, embeddings, metadata (chunk number, source), retrieval
Streaming: Token-streaming endpoint for responsive UI
Analytics: Log query text, response length, latency, provider; aggregate for dashboard
Deployment: Docker images, optional push to Docker Hub, deploy to Render/Fly.io/ECS
Endpoints (Day 1)
GET / — Hello World + service status
GET /health — Health check
Will be expanded in later days to include:

POST /query — Ask question (non-streaming → streaming)
POST /ingest — Upload documents for RAG
GET /analytics/summary — Stats for dashboard
Extension Notes (Upcoming)
background.js: capture selection, context menu, send POST to backend
content script: inject floating card with explanation + buttons
chat box/modal for follow-ups; local or backend-stored memory
Contributing
Create feature branches off develop
Run flake8 and ensure CI is green
Add tests where feasible
PRs should include a brief description and screenshots/logs for UI/behavioral changes
License
MIT
