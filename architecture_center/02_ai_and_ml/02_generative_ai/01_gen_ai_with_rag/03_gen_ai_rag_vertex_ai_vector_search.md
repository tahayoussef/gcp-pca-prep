# RAG Infrastructure using Vertex AI and Vector Search

## Overview
Custom RAG implementation using **Vertex AI Vector Search** for high-performance similarity search.

## Architecture

### Data Ingestion Subsystem
1.  Upload data to **Cloud Storage**.
2.  **Pub/Sub** triggers **Cloud Run Function**.
3.  **Cloud Run Function**:
    *   Parses, chunks data.
    *   Calls **Vertex AI Embeddings API** to create embeddings.
    *   Builds/updates **Vector Search Index**.
4.  Index supports **streaming updates** for new data.

### Serving Subsystem
1.  User query → **Cloud Run Frontend** → **Cloud Run Backend**.
2.  Backend:
    *   Converts query to embeddings (using same model/params as ingestion).
    *   Performs **vector-similarity search** on Vector Search Index.
    *   Constructs augmented prompt (query + grounding data).
    *   Sends to **Vertex AI LLM**.
3.  LLM generates response with **Responsible AI filters**.
4.  Response → Backend → Frontend → User.

## Key Features
*   **High Performance**: Optimized for large-scale vector search.
*   **Configurable**: Choose embedding models (text/multimodal).
*   **Prompt Optimizer**: Vertex AI tool to improve prompts at scale.
