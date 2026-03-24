## Heading 2
NEXUS
## Heading 2
Advanced RAG Document Intelligence Chatbot

FastAPI · Ollama (LLaMA 3) · ChromaDB · Python

## Heading 3
Overview

Nexus is a fully local, ChatGPT-style document intelligence assistant that enables users to upload files and ask contextual questions about them.
All processing runs entirely offline:
No cloud APIs
No external inference services
No data leaving your machine
Responses include document-level source citations with page references, ensuring factual reliability. If information is not present in the uploaded files, the system explicitly states that.
Powered by LLaMA 3 via Ollama for private local inference.
## Heading 3
Retrieval-Augmented Generation (RAG) Pipeline

Nexus implements a structured RAG workflow instead of relying on pretrained model memory.
Document Ingestion Pipeline
## Heading 3
When a file is uploaded:

Text extracted page-wise / slide-wise / row-wise
Chunked into ~600-character segments using LangChain splitter
Converted into embeddings via nomic-embed-text
Stored persistently inside ChromaDB
Question Answering Pipeline
## Heading 3
When a query is submitted:

Query converted into embedding
Top 15 semantic matches retrieved from vector store
Hybrid ranking applied:
70% semantic similarity
30% keyword overlap
Top 5 chunks selected as context
LLaMA 3 generates grounded response
Sources cited with document name and page number
Tokens streamed live to UI

| Format | Processing Method                    |
| ------ | ------------------------------------ |
| PDF    | Page-level extraction via pypdf      |
| DOCX   | Paragraph extraction                 |
| TXT    | Direct ingestion                     |
| CSV    | Row-to-text structured embedding     |
| PPTX   | Slide-level extraction               |
| ZIP    | Automatic archive unpack + ingestion |

## Heading 3
Retrieval Intelligence Features:

Hybrid semantic + keyword search
Duplicate chunk filtering via MD5 hashing
80-character chunk overlap for context continuity

| Component | Requirement               |
| --------- | ------------------------- |
| CPU       | 4-core Intel i5 / Ryzen 5 |
| RAM       | 8 GB                      |
| Disk      | 10 GB                     |
| GPU       | Optional                  |
| OS        | Windows / macOS / Linux   |
| Python    | 3.9+                      |

| Component | Requirement         |
| --------- | ------------------- |
| CPU       | 8-core i7 / Ryzen 7 |
| RAM       | 16–32 GB            |
| GPU       | RTX 3060 (8 GB+)    |
| Disk      | 20 GB SSD           |

| Model            | Size    | Purpose             |
| ---------------- | ------- | ------------------- |
| llama3           | ~4.7 GB | Response generation |
| nomic-embed-text | ~274 MB | Embeddings          |
## Heading 3
Installation Guide
Prerequisites
Install:
Python 3.9+
Ollama
Git
Top-k reranking before LLM inference
Chat Experience Features
Streaming token responses
Clickable document/page source citations
Conversational memory (last 3 exchanges)
Model switching (llama3, mistral, phi3, gemma)
Persistent sessions via localStorage
## Heading 2
Step 1: Create Project Folder
RAG_BOT/├── main.py
├── chat_ui.html
├── requirements.txt
└── README.md
## Heading 2
Step 2: Open Terminal
cd RAG_BOT
## Heading 2
Step 3: Create Virtual Environment
Windows:
python -m venv venv
venv\Scripts\activate
macOS/Linux:
python -m venv venv
source venv/bin/activate
## Heading 2
Step 4: Install Dependencies
pip install -r requirements.txt
If pandas fails on Windows:
pip install pandas --only-binary=all
pip install python-multipart
## Heading 2
Step 5: Download Models
ollama pull llama3
ollama pull nomic-embed-text
Step 6: Start Server
uvicorn main:app --reload
## Heading 3
Open:
http://localhost:8000
Daily Startup Commands
venv\Scripts\activate
uvicorn main:app --reload
Usage Guide
Upload Documents
Open browser interface
Drag-and-drop files
Wait for indexing confirmation
Documents appear in sidebar
## Heading 3
Multiple documents supported simultaneously.
Ask Questions
Enter query
Press Enter
View citations below answer
Continue conversation naturally
Workspace Controls
Switch models via dropdown
Remove documents individually
Clear chat history
Start new isolated session

API Endpoints
Interactive docs:
http://localhost:8000/docs
| Method | Endpoint                        | Description           |
| ------ | ------------------------------- | --------------------- |
| POST   | /session/new                    | Create session        |
| POST   | /upload                         | Upload document       |
| POST   | /upload/zip                     | Upload ZIP            |
| GET    | /chat/stream                    | Streaming response    |
| GET    | /session/{id}/documents         | List documents        |
| GET    | /session/{id}/history           | Chat history          |
| DELETE | /session/{id}/history           | Clear history         |
| DELETE | /session/{id}/document/{doc_id} | Remove document       |
| GET    | /models                         | List available models |
| GET    | /health                         | Health check          |

Project Structure
RAG_BOT/
├── main.py
├── chat_ui.html
├── requirements.txt
├── README.md
├── .gitignore
├── venv/
├── chroma_db/
└── uploads/
## Heading 3
Tech Stack
| Tool             | Role                  |
| ---------------- | --------------------- |
| FastAPI          | Backend API framework |
| Uvicorn          | ASGI server           |
| Ollama           | Local LLM runtime     |
| ChromaDB         | Vector database       |
| LangChain        | Text chunking         |
| pypdf            | PDF parsing           |
| python-docx      | DOCX parsing          |
| pandas           | CSV parsing           |
| python-pptx      | PPTX parsing          |
| python-multipart | Upload handling       |
| Pydantic         | Validation            |

## Heading 3
Troubleshooting
pandas install failure
pip install pandas --only-binary=all
Missing python-multipart
pip install python-multipart
Encoding error in UI
## Heading 3
Update:
return ui_path.read_text(encoding='utf-8')
Ollama not running
ollama serve
Slow responses

Use GPU or switch to smaller models (phi3 recommended).
ChromaDB corruption
## Heading 3
Delete folder:
Remove-Item -Recurse -Force chroma_db
Restart server afterward.
## Heading 3
Git Ignore Recommendations
Ignore
chroma_db/
uploads/
venv/
.env
__pycache__/
## Heading 3
Commit only:
main.py
chat_ui.html
requirements.txt
README.md
.gitignore

Built with FastAPI · Ollama · ChromaDB · LLaMA 3 · Python
