# ReadBuddy

ReadBuddy is a lightweight Chrome extension that helps students understand dense terminology and context-specific phrases in research papers. Highlight any phrase and instantly get a short, plain-English explanation — without leaving the paper. You can then choose to “Explain further,” “Ask follow-up,” or mark “Got it.”

## Why ReadBuddy?

Reading primary literature is hard. Jargon, acronyms, and field-specific phrases slow you down and break your focus. ReadBuddy keeps you in the flow by explaining terms right where you’re reading.

## What it does

- Highlight → right-click → “Explain with AI”
- 2–3 sentence plain-English explanations
- “Explain further” for more detail
- “Ask follow-up” to open a small chat (only when you need it)
- “Got it” to dismiss and keep reading

## How it works (at a glance)

1. You highlight a phrase on a webpage
2. Right-click → “Explain with AI”
3. The extension sends your selection (and page context) to the backend
4. The backend asks an AI model and returns a short explanation
5. A small floating card appears near your selection with the explanation and actions

## Project goals

- Make research papers more approachable for students
- Keep the experience fast and minimal
- Provide helpful context when needed (without forcing you to leave the page)
- Support follow-up questions only when you want them

## What’s under the hood (high level)

- Chrome Extension (content script + background)
- Backend API (FastAPI) to call the AI model
- Option to use retrieval-augmented generation (RAG) for better context (later)
- Support for multiple AI providers

## Status

- Core flow: highlight → explain → follow-up actions
- Backend: health checks and basic endpoints
- UI: small floating card near your selection

## Roadmap

- Better context via RAG (e.g., Pinecone/Chroma)
- Streaming responses for faster-feeling answers
- Analytics dashboard (usage, latency, etc.)
- Optional Next.js dashboard
- Add screenshots and demo GIFs

## Screenshots / Demo

(You can add images here later.)
- Screenshot of the floating explanation card
- Demo GIF of highlight → explain → follow-up

## Contributing

Ideas, issues, and pull requests are welcome. The goal is to keep this tool simple, fast, and genuinely useful for students.

---

> Made with ❤️ to help students read research papers more effectively
