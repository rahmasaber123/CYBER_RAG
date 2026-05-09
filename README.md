# CyberAG

CyberAG is a Hybrid Retrieval-Augmented Generation (RAG) system designed for complex cybersecurity PDFs such as the NIST Cybersecurity Framework (CSF) 2.0.

Unlike traditional dense-only RAG pipelines, CyberAG combines lexical retrieval, semantic search, reranking, metadata-aware retrieval, and semantic caching to improve retrieval precision and grounded answer generation for technical cybersecurity documents.


# System Architecture

![CyberAG Architecture]([assets/architecture.png](https://github.com/rahmasaber123/CYBER_RAG/blob/main/Screenshot%202026-05-09%20204402.png?raw=true))


                    # System Architecture

```text
                    ┌────────────────────┐
                    │   NIST PDF Input   │
                    └─────────┬──────────┘
                              │
                              ▼
                 ┌────────────────────────┐
                 │ PDF Parsing Layer      │
                 │ LlamaParse / PyPDF     │
                 └─────────┬──────────────┘
                           │
                           ▼
                 ┌────────────────────────┐
                 │ Chunking Pipeline      │
                 │ Metadata Extraction    │
                 │ Synthetic Questions    │
                 └─────────┬──────────────┘
                           │
          ┌────────────────┴────────────────┐
          ▼                                 ▼
 ┌─────────────────┐              ┌─────────────────┐
 │ BM25 Index      │              │ Chroma VectorDB │
 │ Sparse Retrieval│              │ Dense Retrieval │
 └────────┬────────┘              └────────┬────────┘
          │                                │
          └──────────────┬─────────────────┘
                         ▼
              ┌──────────────────┐
              │ RRF Fusion       │
              └────────┬─────────┘
                       ▼
            ┌──────────────────────┐
            │ Metadata Boosting    │
            └─────────┬────────────┘
                      ▼
            ┌──────────────────────┐
            │ Cross-Encoder        │
            │ Reranking            │
            └─────────┬────────────┘
                      ▼
            ┌──────────────────────┐
            │ Grounded LLM         │
            │ Synthesis            │
            └─────────┬────────────┘
                      ▼
            ┌──────────────────────┐
            │ Structured Response  │
            │ + Citations          │
            │ + Confidence         │
            └──────────────────────┘
```

## Architecture Overview

The system uses a hybrid Retrieval-Augmented Generation (RAG) pipeline
designed for cybersecurity documents based on the NIST Cybersecurity
Framework 2.0.

### Core Components

- PDF parsing using LlamaParse / PyPDF
- Metadata-aware chunking pipeline
- Synthetic question generation for semantic recall improvement
- Hybrid retrieval:
  - BM25 sparse retrieval
  - Chroma vector semantic retrieval
- Reciprocal Rank Fusion (RRF)
- Metadata boosting
- Cross-encoder reranking
- Grounded LLM synthesis
- Structured responses with citations and confidence scoring

### Key Features

- Multilingual retrieval support
- Reduced hallucinations through grounded generation
- Semantic caching for lower latency
- Production-style observability and modular design
- Optimized retrieval for cybersecurity terminology and identifiers
            
# Features

- Hybrid Retrieval Architecture
- BM25 Exact Keyword Retrieval
- Semantic Vector Search with ChromaDB
- Reciprocal Rank Fusion (RRF)
- Flashrank Reranking
- Metadata-aware Retrieval
- Multilingual Retrieval Support
- Semantic Cache
- Q/A Generation per Node
- Grounded GPT-based Answer Generation

---

# Why CyberAG?

Traditional dense retrieval struggles with highly technical cybersecurity documents containing:

- complex identifiers
- hierarchical structures
- repeated governance terminology
- semantically similar sections

Examples:
- GV.SC-07
- PR.AA-05
- DE.AE-08

CyberAG improves retrieval quality by combining:
- lexical precision
- semantic understanding
- reranking
- metadata filtering

instead of relying only on embeddings.

---

# Architecture

User Query
→ BM25 Retrieval
→ Semantic Search
→ Reciprocal Rank Fusion (RRF)
→ Flashrank Reranking
→ Context Selection
→ GPT-4o-mini Response

---

# Tech Stack

- Python
- LlamaIndex
- ChromaDB
- Sentence Transformers
- BM25
- Flashrank
- GPT-4o-mini
- Ollama
- Jupyter Notebook

---

# Semantic Q/A Generation

During ingestion, each chunk generates synthetic Q/A pairs to improve:
- semantic recall
- paraphrase matching
- cybersecurity query understanding

This helps the retriever match user intent more effectively than embedding raw chunk text alone.

---

# Semantic Cache

CyberAG includes embedding-based semantic caching.

Repeated or semantically similar queries can reuse previously grounded responses instead of repeating:
- retrieval
- reranking
- generation

This reduces:
- latency
- API cost
- redundant computation

---

# Multilingual Retrieval

CyberAG supports multilingual querying.

Example:
- English cybersecurity PDF
- Arabic user query
- English retrieval
- Arabic grounded answer generation

---

# Example Queries

- What is GV.SC-07?
- Under GOVERN, how is risk appetite communicated?
- How should organizations monitor third-party vendors?
- كيف يدير الإطار مخاطر سلسلة التوريد؟

---

# Project Goal

This project explores how retrieval engineering can significantly improve RAG quality for technical cybersecurity documents.

One of the main findings:

Improving retrieval architecture can matter more than upgrading the LLM itself.



# Author
Rahma Saber 
 AI Engineering
