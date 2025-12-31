# Choose your Agentic AI Architecture Components

## Overview
An **agent** is an autonomous system that uses an AI model as a reasoning engine to understand intent, create plans, and execute interactions using tools.
*   **Goal**: Create an autonomous system that understands user intent and executes multi-step plans.
*   **Core Logic**: Uses AI models (reasoning) + Tools (action) + Memory (context).

## Key Architecture Components
1.  **Frontend Framework**: UI components for user interaction.
2.  **Agent Development Framework**:
    *   **ADK (Agent Development Kit)**: Recommended for Google Cloud. Open-source, modular, optimized for Gemini. Supports multi-agent states and delegation.
    *   **Genkit**: General-purpose framework for fine-grained control.
3.  **Agent Tools**: Functions/APIs enabling external actions.
    *   Must be observable and have robust error handling.
    *   Includes built-in tools (search, code interpreter) or custom function calls.
4.  **Agent Memory**:
    *   **Short-term**: Session context (e.g., chat history).
    *   **Long-term**: Vector databases or structural storage for retrieving past knowledge.
5.  **Agent Design Patterns**: Structural approaches (Single vs. Multi-agent).
6.  **Agent Runtime**: Compute environment (Cloud Run, GKE, Vertex AI Agent Engine).
7.  **AI Models & Runtime**: The underlying LLM and serving infrastructure.
