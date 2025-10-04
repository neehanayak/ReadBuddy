# 📚 ReadBuddy

**ReadBuddy** is a lightweight Chrome extension that helps students understand dense terminology and context-specific phrases in research papers using **AI-powered explanations**.  
Get instant, plain-English insights **without leaving the paper** — making academic reading faster and more accessible.

---

## 🎯 Problem

Students often struggle with:

- Dense academic terminology in research papers  
- Context-specific phrases that require domain knowledge  
- Constantly switching between papers and search engines  
- Loss of reading flow and comprehension  

---

## 💡 Solution

**ReadBuddy** provides fast, context-aware explanations directly in your browser:

1. Highlight any phrase in a research paper  
2. Right-click → **“Explain with AI”**  
3. Get a short, plain-English explanation instantly  
4. Choose:
   - 🧩 **Explain further** – get more detailed insight  
   - 💬 **Ask follow-up** – open a mini chat  
   - ✅ **Got it** – dismiss  

No context switching. No interruptions. Just seamless learning.

---

## ✨ Features

- ⚡ **Instant Explanations:** Highlight → right-click → understand  
- 🧠 **Plain English:** 2–3 sentence, clarity-optimized explanations  
- 🔁 **Follow-up Options:** “Explain further”, “Ask follow-up”, “Got it”  
- 🔍 **Context-Aware (RAG):** Uses document context for accuracy  
- 🤖 **Multi-LLM Support:** Works with OpenAI, Anthropic, or local models  
- 🪶 **Fast & Lightweight:** Minimal UI, maximum speed  

---

## 🏗️ Architecture

### How It Works

```text
[User highlights text in webpage]
        ↓
[Right-click → "Explain with AI"]
        ↓
[Extension captures selection + page context]
        ↓
[POST request → FastAPI Backend]
        ↓
[Backend retrieves relevant context (RAG)]
        ↓
[LLM generates explanation]
        ↓
[Response streamed back to extension]
        ↓
[Floating card appears with explanation]

┌──────────────────────────────┐
│ Explanation (2-3 sentences) │
│ [Explain further]           │
│ [Ask follow-up]             │
│ [Got it]                    │
└──────────────────────────────┘
```

## 🧰 Tech Stack

### **Frontend / Extension**
- Chrome Extension (Manifest V3)
- Vanilla JavaScript (content scripts, background service worker)
- CSS (for floating UI cards)

### **Backend**
- FastAPI (Python)
- OpenAI / Anthropic APIs
- Pinecone / ChromaDB (Vector Database for RAG)
- PostgreSQL (analytics and logging)
- Docker & Docker Compose

### **Optional Frontend Dashboard**
- Next.js
- Tailwind CSS
- Recharts (for analytics visualization)

---

## 📁 Project Structure

```plaintext
readbuddy/
├── backend/              # FastAPI backend service
│   ├── routers/          # API route handlers
│   ├── services/         # Business logic (LLM, RAG, embeddings)
│   ├── models/           # Database models
│   └── main.py           # FastAPI entry point
├── extension/            # Chrome extension
│   ├── manifest.json     # Extension configuration
│   ├── background.js     # Service worker (context menu, API calls)
│   ├── content.js        # Content script (UI injection)
│   └── popup.html        # Extension popup (optional)
├── frontend/             # Next.js dashboard (optional)
├── docker-compose.yml    # Docker orchestration
├── .env.example          # Environment variables template
└── README.md
```

# 🚀 Getting Started

## 🧩 Prerequisites
- **Python 3.10+**
- **Node.js 18+** (for frontend dashboard, optional)
- **Docker & Docker Compose** (optional)
- **OpenAI or Anthropic API key**

---

## ⚙️ Backend Setup

### 1️⃣ Clone the repository
```bash
git clone https://github.com/neehanayak/ReadBuddy.git
cd ReadBuddy
```
### 2️⃣ Set up environment variables
```bash
cp .env.example .env
# Edit .env and add your API keys
```
3️⃣ Run with Docker (recommended)
```bash
docker-compose up --build
```
4️⃣ Or run locally
```bash
cd backend
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```
✅ Verify the backend

- **API:** http://localhost:8000
- **Docs:** http://localhost:8000/docs
- **Health:** http://localhost:8000/health


## 🧩 Install Chrome Extension

1. Open **Google Chrome** and navigate to: 
```bash 
chrome://extensions/
```
2. Enable **Developer mode** (top right corner)
3. Click **Load unpacked**
4. Select the `extension/` folder from this repository

✅ The **ReadBuddy** icon will now appear in your Chrome toolbar.

## 🪄 Usage

1. Open any **research paper** or **online article**  
2. Highlight a **phrase or term** you want explained  
3. Right-click → select **“Explain with AI”**  
4. A floating card will appear with a **2–3 sentence plain-English explanation**

### 💡 Available Options
- 🧠 **Explain further** → Get a more detailed explanation  
- 💬 **Ask follow-up** → Open a mini chat for clarification  
- ✅ **Got it** → Dismiss the explanation card


## 🔧 Configuration

### 🧾 Environment Variables (`.env`)
Create a `.env` file in the root directory based on `.env.example` and fill in your API keys and configuration:

```bash
# LLM Configuration
LLM_PROVIDER=openai  # Options: openai, anthropic, local
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# Vector Database
VECTOR_DB=pinecone  # Options: pinecone, chroma
PINECONE_API_KEY=your_pinecone_api_key_here
PINECONE_ENVIRONMENT=your_pinecone_environment_here
PINECONE_INDEX_NAME=readbuddy

# Database
DATABASE_URL=postgresql://postgres:postgres@db:5432/readbuddy

# Server
BACKEND_PORT=8000
FRONTEND_PORT=3000

# CORS
ALLOWED_ORIGINS=http://localhost:3000,chrome-extension://*
```

## 📡 API Endpoints

### ✅ Current Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET    | `/`      | Root endpoint with service info |
| GET    | `/health`| Health check |

### 🧩 Planned Endpoints
| Method | Endpoint             | Description |
|--------|--------------------|-------------|
| POST   | `/query`             | Get AI explanation for highlighted text |
| POST   | `/ingest`            | Upload documents for RAG context |
| GET    | `/analytics/summary` | Retrieve usage statistics |

---

## 🧪 Development

### 🧠 Run Tests
```bash
cd backend
pytest
```
### 🧹 Linting
```bash
flake8 backend
```
---
## 🚀 Build for Production
``` bash
docker-compose -f docker-compose.prod.yml up --build
```
## 🗺️ Roadmap
- ✅ Project setup and FastAPI backend  
- 🧠 LLM abstraction layer (OpenAI, Anthropic)  
- 🔍 Vector database integration (RAG)  
- ⚡ Streaming responses  
- 🧩 Chrome extension (basic functionality)  
- 💬 Follow-up chat interface  
- 📊 Analytics dashboard  
- 📚 Multi-document context support  
- 🛰️ Offline mode (local LLMs)  
- 🦊 Firefox extension support  

---

## 🤝 Contributing
Contributions are always welcome 💙

1. **Fork** the repository  
2. **Create your branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit Changes**
```bash
git commit -m "Add some AmazingFeature"
```
4. **Push your branch**
```bash
git push origin feature/AmazingFeature
```
5. **Open a Pull Request**

--

## 📄 License
This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👥 Author
**Neeha Nayak**  
🔗 [GitHub Profile](https://github.com/neehanayak)

---

## 🙏 Acknowledgments
- Inspired by the need to make **academic research more accessible**  
- Built with ❤️ using **FastAPI**, **OpenAI**, and modern web technologies  
- Thanks to all contributors and early testers who shaped the project  

---

## 📧 Contact
For questions or feedback, please open an **issue** or contact:  
📩 *wizardingbyte@outlook.com*

---

> Made with ❤️ to help students read research papers more effectively.



