# AIET Project: RAG Pipeline with ChromaDB

**Group 8**

A Retrieval-Augmented Generation (RAG) pipeline that ingests documents into a ChromaDB vector store, retrieves the most relevant context for a user query, and passes it to an LLM to generate the final answer.

## Overview

The project has two parts:

1. **Ingestion pipeline**: loads source documents, splits them into chunks, generates embeddings, and stores them in ChromaDB.
2. **Retrieval and answering pipeline**: embeds the user query, retrieves the top-k similar chunks from ChromaDB, builds a prompt with that context, and sends it to the LLM for inference.

## Architecture

```
            INGESTION
Documents -> Chunking -> Embeddings -> ChromaDB

            QUERY
User query -> Embed query -> ChromaDB top-k search
           -> Prompt (query + retrieved context) -> LLM -> Final answer
```

## Tech Stack

- **Language:** Python 3.<x>
- **Vector DB:** ChromaDB
- **Embedding model:** `<e.g. sentence-transformers/all-MiniLM-L6-v2>`
- **LLM:** `<e.g. OpenAI GPT-4o / Claude / Llama via Ollama>`
- **Framework (if any):** `<e.g. LangChain / LlamaIndex / none>`

## Project Structure

```
aietproject/
├── <ingest.py>          # data ingestion into ChromaDB
├── <retrieve.py>        # retrieval + LLM answering
├── <data/>              # source documents
├── <requirements.txt>
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.<x> or higher
- An API key for your LLM provider (if applicable)

### Installation

```bash
git clone https://github.com/jayaerrabelli/aietproject.git
cd aietproject
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the project root:

```
<LLM_API_KEY>=your_key_here
```

## Usage

### 1. Ingest data

```bash
python <ingest.py> --source <path/to/data>
```

This chunks the documents, embeds them, and stores them in ChromaDB (persisted at `<./chroma_db>`).

### 2. Ask a question

```bash
python <retrieve.py> --query "Your question here"
```

### Example

```
Query:  <example question>
Answer: <example answer returned by the pipeline>
```

## How It Works

- **Chunking:** documents are split into chunks of `<size>` characters with `<overlap>` overlap.
- **Retrieval:** the top `<k>` most similar chunks are fetched by vector similarity.
- **Generation:** the retrieved chunks are inserted into the prompt as context, and the LLM is instructed to answer using only that context.

## Team

Group 8

- `Murali Grandhi`
- `Kalpana Deverapalli`
- `Priya Ghuse`
- `Jayashree Errabelli`

## License

`<e.g. MIT>`
