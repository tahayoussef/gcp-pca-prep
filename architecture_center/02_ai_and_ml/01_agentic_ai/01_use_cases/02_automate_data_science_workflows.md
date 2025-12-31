# Automate Data Science Workflows

## Overview
A multi-agent system that automates complex analytics and ML tasks using a **Coordinator** pattern.

## Architecture
*   **Root Agent**: Acts as a Coordinator. Receives requests and delegates to specialized agents.
*   **Specialized Agents**:
    *   **Analytics Agent**: Generates/Runs Python code for visualization and stats.
    *   **AlloyDB Agent**: Generates PostgreSQL queries using MCP Toolbox.
    *   **BigQuery Agent**: Generates GoogleSQL queries using ADK built-in tools.
    *   **BQML Agent**: Manages ML lifecycle (create models, predict) in BigQuery.

## Key Features
*   **Agent as a Tool**: The root agent invokes other agents as if they were tools.
*   **Code/SQL Generation**: Agents autonomously write and execute code to retrieve and analyze data.
*   **Products**: Cloud Run, ADK, Vertex AI, AlloyDB, BigQuery.
