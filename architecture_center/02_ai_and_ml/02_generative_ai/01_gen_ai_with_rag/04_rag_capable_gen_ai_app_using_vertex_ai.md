# RAG Infrastructure using Vertex AI and AlloyDB for PostgreSQL

## Overview
RAG implementation using **AlloyDB for PostgreSQL** with **pgvector** extension as the vector store. Includes quality evaluation subsystem.

## Architecture

### Data Ingestion Subsystem
1.  Upload data to **Cloud Storage**.
2.  **Pub/Sub** triggers **Cloud Run Job**.
3.  **Cloud Run Job**:
    *   Uses config from **AlloyDB**.
    *   Uses **Document AI** to parse/chunk data.
    *   Calls **Vertex AI Embeddings API**.
    *   Stores embeddings in **AlloyDB with pgvector extension**.

### Serving Subsystem
1.  User query → **Frontend** → **Application Backend**.
2.  Backend:
    *   Converts query to embeddings.
    *   Performs **semantic search** in AlloyDB vector store.
    *   Combines query + retrieved data = contextualized prompt.
    *   Sends to **Vertex AI LLM** (foundation or custom).
3.  Response screened by **Responsible AI filters**.
4.  Logs stored in **Cloud Logging**, analytics in **BigQuery**.

### Quality Evaluation Subsystem
*   Monitors and evaluates the quality of generated responses.

## Key Features
*   **AlloyDB as Vector Store**: ACID compliance + vector similarity.
*   **Document AI**: Advanced parsing for complex documents.
*   **Quality Evaluation**: Built-in subsystem for response quality monitoring.
