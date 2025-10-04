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

### 2️⃣ Set up environment variables
```bash
cp .env.example .env
# Edit .env and add your API keys





