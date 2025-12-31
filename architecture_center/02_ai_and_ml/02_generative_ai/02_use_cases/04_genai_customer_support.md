# Generate Solutions for Customer Support Questions

## Overview
**RAG-based** support desk application that retrieves relevant knowledge base resources and generates customer solutions.

## Architecture
1.  Customer submits question to support desk (runs on **GKE**).
2.  Question → **Knowledge Retriever Service**.
3.  Retriever sends prompt to **Gemini API (Vertex AI)** to identify relevant resources.
4.  **Gemini** searches support knowledge base in **Cloud Storage**.
5.  Returns IDs of relevant resources → Retriever fetches them from Cloud Storage.
6.  Question + resources → **Solution Generator Service**.
7.  Generator sends resources + prompt to **Gemini**.
8.  **Gemini** generates detailed solution (step-by-step instructions or video walkthrough).
9.  Solution provided to customer via support desk app.

## Key Features
*   **RAG Pattern**: Grounds responses in knowledge base.
*   **GKE Deployment**: Containerized services for scalability.
