# Administer Interactive Learning

## Overview
A single-agent system that assesses user knowledge and generates personalized learning experiences (e.g., coding quizzes).

## Architecture
*   **User Interface**: Quiz App hosted on **Cloud Run**.
*   **AI Agent**: Uses **Vertex AI (Gemini)** to interpret input and call tools (Start Quiz, Evaluate Answer, Generate Question).
*   **Memory & State**:
    *   **Session History**: Stored in **Vertex AI Agent Engine Sessions** for current quiz progress.
    *   **Long-term Memory**: Stored in **Memory Bank** to personalized future sessions based on past performance.

## Key Components
*   **Cloud Run**: Hosts the application.
*   **ADK**: Used to build the agent.
*   **Vertex AI**: Model serving and agent engine.
