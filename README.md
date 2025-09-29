# RAG
A minimal Retrieval-Augmented Generation (RAG) implementation designed for experimentation and as a foundation for future projects.
This notebook demonstrates how to combine document embeddings, a vector store, and LLM APIs to build a simple yet effective retrieval-based question-answering pipeline.

## Features
- Supports Youtube videos (subtitles scrapping), Wikipedia pages, PDF and TXT as data sources.
- Embedding generation using SentenceTransformers.
- Vector storage and retrieval with FAISS or a manual cosine similarity implementation (for small datasets).
- Integration with multiple LLM APIs (e.g. Gemini, Mistral, Groq).
- Includes preprocessing steps for text cleaning and chunking.
- Flexible design — intended as a starting point for larger RAG/AI projects.

## FAISS vs Manual Implementation
For small datasets, a manual cosine similarity search over embeddings is often sufficient and easy to implement. However, this approach does not scale well when the number of documents ans pages grows, since it requires computing similarities against all vectors at query time.

By contrast, FAISS provides an efficient and optimized vector database that supports fast similarity search, even for large-scale collections. It uses advanced indexing structures and is widely adopted in production-grade retrieval systems. In this project, FAISS is the recommended option when dealing with more than a few hundred chunks.

## Chunking strategy
Too large chunks may overwhelm the LLM with irrelevant text, while too small chunks risk losing context. In this project, text is split into sentence-based chunks that balance semantic coherence and retrieval granularity. I tried to group 10 sentences for each chunk to keep a good context, this number can be changed for futrther experiments. I thought about implementing sliding windows to make more combinations of sentences in a chunk and get rid of border sentences but consequently it would create redundancy in the retrievation of the top similar chunks.
