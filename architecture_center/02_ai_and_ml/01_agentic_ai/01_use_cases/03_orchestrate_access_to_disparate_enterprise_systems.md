# Orchestrate Access to Disparate Enterprise Systems

## Overview
An orchestrator agent that routes client interactions to appropriate backend systems using **Model Context Protocol (MCP)** servers as an abstraction layer.

## Architecture
*   **Channels**: Custom Frontend (Web), Ad-hoc Chat (Gemini Enterprise), or System Events (Pub/Sub).
*   **Orchestrator Agent**: Relies on **ADK** and **Cloud Run**. Manages the multi-agent system and state.
*   **Anti-Corruption Layer**: Uses **MCP Servers** to expose backend APIs as standardized tools. This isolates the agent from backend complexity and coupling.
    *   **MCP Toolbox for Databases**: For Cloud SQL access.
    *   **Custom MCP Servers**: For other backend apps.

## Use Cases
*   **Swivel-chair automation**: Automating tasks that require switching between multiple apps.
*   **Unified Interface**: Single conversational interface for legacy systems.
*   **Modernization**: Event-driven integration via Pub/Sub.
