# Case Study: Cymbal Retail (v6.1 - Retail/AI Focus)

## Company Overview
Cymbal Retail is a rapidly growing online retailer stuggling with **manual processes**, **fragmented data**, and **high support costs**. Their goal is to become an AI-first retailer to streamline operations and boost sales.

## Solution Concept
1.  **Catalog Enrichment**: Use Gen AI to automatically write product descriptions, generate attributes, and create image variations.
2.  **Conversational Commerce**: Deploy "Virtual Agents" to help users shop via chat.
3.  **Modernization**: Break down data silos and migrate to a unified cloud platform.

## Business Requirements
*   **Automate Catalog**: Reduce manual effort/errors in updating product info.
*   **Improve Discovery**: Better search/recommendations to drive conversion.
*   **Human-in-the-Loop (HITL)**: Associates must approve/reject AI-generated content before it goes live.
*   **Scale**: Handle peak events (Black Friday) without downtime.
*   **Security**: Protect PII (Customer Data).

## Existing Technical Environment
*   **Hybrid**: Mix of on-prem and cloud.
*   **Databases**: Heterogeneous mix of **MySQL**, **Microsoft SQL Server**, **Redis**, and **MongoDB**.
*   **Applications**: Custom web app, IVR (Interactive Voice Response) system for support.
*   **Containerization**: Some apps already on Kubernetes.

## Key Services & Architecture Patterns
*   **AI for Retail**:
    *   **Vertex AI Search for Retail (Discovery AI)**: The go-to answer for "Better Search" or "Recommendations" in retail.
    *   **Contact Center AI (CCAI)**: To modernize the IVR/Call Center.
    *   **Generative AI**: For "Attribute Generation" and "Image Generation" (creating variations of product photos).
*   **Database Migration**:
    *   **Database Migration Service (DMS)**: For moving MySQL/PostgreSQL to Cloud SQL.
    *   Move **MongoDB** to **MongoDB Atlas** on GCP.
    *   Move **Redis** to **Memorystore**.
*   **Compute**:
    *   **GKE**: For the main e-commerce platform (scalability).
*   **DevOps**:
    *   **Human-in-the-Loop UI**: Likely a custom internal app (App Engine/Cloud Run) that fetches AI results and asks for human approval.

## Exam Scenarios & "Gotchas"
*   **Scenario**: "We need to fix our product search; it returns irrelevant results."
    *   **Answer**: **Discovery AI (Vertex AI Search for Retail)**. Do NOT build a custom model if a specialized API exists.
*   **Scenario**: "We need to generate product descriptions from raw specs, but humans must check them."
    *   **Answer**: Use **Vertex AI (PaLM API)** to generate text -> Review UI -> Update Database.
*   **Scenario**: "How do we handle the Black Friday traffic spike?"
    *   **Answer**: **GKE Autoscaling** (Horizontal Pod Autoscaler) + **Global Load Balancing** (Cloud CDN to cache images).
*   **Scenario**: "Migrate the legacy SQL Server database with minimal downtime."
    *   **Answer**: Use **Cloud SQL for SQL Server** with an external master replication setup or DMS if supported (check DMS support matrix, SQL Server support is newer).
