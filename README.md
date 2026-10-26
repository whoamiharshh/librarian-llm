# librarian-llm

A small learning project for search and retrieval-augmented generation (RAG) with [Typesense](https://typesense.org), [LangChain](https://python.langchain.com) and [Groq](https://groq.com).

All the work happens in [`typesense.ipynb`](typesense.ipynb), in two parts:

1. **Book search.** Creates a `books_latest` collection in Typesense, imports 500 books from `books_catalog_500.json`, and runs keyword searches sorted by rating.
2. **RAG.** Splits `test.txt` into chunks, embeds them with a Hugging Face sentence-transformer, stores them in Typesense as vectors, and finds the chunks closest to a question.

```
test.txt ─► chunk ─► embed ─► Typesense ─► similarity search ─► (Groq LLM answer, coming next)
```

## Setup

You need Python 3.14 and a [Typesense Cloud](https://cloud.typesense.org) cluster (or a local Typesense server).

```bash
git clone https://github.com/whoamiharshh/librarian-llm.git
cd librarian-llm
python -m venv .venv
.venv\Scripts\activate        # Windows
# source .venv/bin/activate   # macOS / Linux
pip install -r requirements.txt
```

Copy `.env.example` to `.env` and fill in your own values:

```
TYPESENSE_HOST=xxxxxxxx-1.a1.typesense.net
TYPESENSE_API_KEY=your-typesense-admin-key
GROQ_API_KEY=your-groq-api-key
```

`.env` is in `.gitignore`, so your keys stay on your machine.

## Run

Open `typesense.ipynb` and run the cells in order. Run cells 2, 3 and 9 **only once**: they create collections or upload data, and running them again gives an "already exists" error or duplicate documents.

## Data

- `books_catalog_500.json` is a synthetic catalog. The books, authors and ratings are made up.
- `test.txt` is a short sample text about artificial intelligence, used for the RAG demo.
