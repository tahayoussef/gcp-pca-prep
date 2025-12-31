# Multi-Agent AI System in Google Cloud

## Overview
Illustrates a robust multi-agent architecture using **Cloud Run**, **Vertex AI Agent Engine**, and the **ADK**. It employs a **Coordinator Agent** to manage sequential or iterative flows between specialized sub-agents.

## Architecture
*   **Frontend**: Serverless Cloud Run service (e.g., Chat UI).
*   **Coordinator Agent**: Receives prompt, detects intent, and routes to specific flows.
*   **Communication**: **Agent2Agent (A2A)** protocol for interoperability.
*   **Flows**:
    *   **Sequential**: Task A -> Task A.1
    *   **Iterative Refinement**: Task B -> Quality Evaluator -> (if bad) Prompt Enhancer -> Task B (Loop).

## Use Cases
*   **Financial Advisor (Sequential)**: Data Retriever -> Financial Analyzer -> Stock Recommender -> Trade Executor.
*   **Research Assistant (Hierarchical/Loop)**: Planner -> Researcher (loops with Evaluator) -> Report Composer.
*   **Supply Chain Optimizer**: Warehouse Manager interacts with Shipment Tracker and Supplier Communicator.

## Design Considerations
*   **Security**:
    *   **Human-in-the-loop**: Essential for business-critical systems to approve/override actions.
    *   **IAM**: Least privilege per agent.
    *   **Observability**: Trace execution paths and reasoning.
*   **Region Selection**: Balance service availability, latency, and data residency/cost.
