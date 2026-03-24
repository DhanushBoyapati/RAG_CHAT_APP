# Nexus — Advanced RAG Chatbot

Local ChatGPT-style document assistant built with FastAPI + Ollama + ChromaDB.

## Quick Start

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Pull Ollama models
ollama pull llama3
ollama pull nomic-embed-text

# 3. Run
uvicorn main:app --reload

# 4. Open browser
# http://localhost:8000
```

## Features

- Upload PDF, DOCX, TXT, CSV, PPTX, ZIP
- Multi-document knowledge base per session
- Streaming responses (ChatGPT-style typing)
- Hybrid search (semantic + keyword)
- Source citations with page numbers
- Conversational memory (last 3 exchanges)
- Model selector (llama3, mistral, phi3, gemma)
- Drag-and-drop file upload
- Session-based vector storage

## API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| POST | /session/new | Create new session |
| POST | /upload | Upload a file |
| POST | /upload/zip | Upload ZIP archive |
| GET  | /chat/stream | SSE streaming chat |
| GET  | /session/{id}/documents | List documents |
| GET  | /session/{id}/history | Get chat history |
| DELETE | /session/{id}/history | Clear history |
| DELETE | /session/{id}/document/{doc_id} | Remove document |
| GET  | /models | List available Ollama models |
| GET  | /health | Health check |

## Project Structure

```
nexus/
├── main.py          ← FastAPI backend
├── chat_ui.html     ← Frontend UI
├── requirements.txt
├── chroma_db/       ← Vector DB (auto-created, git ignored)
└── uploads/         ← Temp uploads (git ignored)
```
