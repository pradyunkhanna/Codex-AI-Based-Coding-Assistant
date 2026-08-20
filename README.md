# AI Codebase Assistant

An AI-powered assistant that answers natural-language questions about a codebase using retrieval-augmented generation (RAG).

## Project Structure
```
ai-codebase-assistant/
├── src/
│   ├── ingest.py        # Part 1: repo ingestion & file filtering
│   ├── chunker.py       # Part 2: code chunking
│   ├── embedder.py      # Part 3: embeddings + vector storage
│   ├── retriever.py     # Part 4: retrieval + QA pipeline
│   └── main.py           # CLI entry point
├── data/
│   └── sample_repo/     # test repo goes here (gitignored)
├── requirements.txt
└── README.md
```

## Status
- [x] Part 1: Repo Ingestion
- [x] Part 2: Chunking
- [x] Part 3: Embedding + Storage
- [x] Part 4: Retrieval + QA Pipeline
- [ ] Part 5: Interface
- [ ] Part 6: Evaluation + Polish

## Setup
```bash
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

No API key needed — embeddings and retrieval run locally via
`sentence-transformers`. The first run downloads a small (~80MB)
model, which is then cached on your machine.

(Optional: set an `OPENAI_API_KEY` environment variable if you want
written answers instead of raw retrieved code — retriever.py will
use it automatically if present, otherwise falls back to local-only.)

## Usage
```bash
# ingest + chunk only
python src/main.py --repo data/sample_repo

# ingest + chunk + embed locally + store in Chroma (run this once per repo)
python src/main.py --repo data/sample_repo --embed

# ask questions about the indexed repo (repeatable, no re-embedding needed)
python src/main.py --ask "how does authentication work?"
```
