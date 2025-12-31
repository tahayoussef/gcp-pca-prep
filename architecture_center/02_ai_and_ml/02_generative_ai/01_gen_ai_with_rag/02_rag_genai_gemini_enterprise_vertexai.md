# RAG Infrastructure using Gemini Enterprise and Vertex AI

## Overview
Fully managed RAG solution using **Gemini Enterprise** for automatic vector embedding and search, minimizing custom code.

## Architecture

### Data Ingestion Subsystem
1.  Upload data to **Cloud Storage**.
2.  **Cloud Storage** triggers **Pub/Sub** notification.
3.  **Pub/Sub** triggers **Cloud Run Functions**.
4.  **Cloud Run Functions** processes data and generates metadata (JSONL), stores in Cloud Storage.
5.  **Pub/Sub** triggers **Gemini Enterprise Managed Datastore** to parse, chunk, and auto-embed data.

### Serving Subsystem
1.  User query → **Cloud Run Frontend** → **Cloud Run Backend**.
2.  Backend sends query to **Gemini Enterprise API**.
3.  **Gemini Enterprise**:
    *   Embeds query.
    *   Performs semantic search on Managed Datastore.
    *   Augments prompt with retrieved data.
    *   Generates response with Responsible AI filters.
4.  Response → Backend → Frontend → User.

## Key Features
*   **Fully Managed**: Automatic embeddings, chunking, and search via Gemini Enterprise.
*   **Responsible AI**: Built-in safety filters.
*   **Use Cases**: Personalized recommendations, clinical assistance, legal research.
