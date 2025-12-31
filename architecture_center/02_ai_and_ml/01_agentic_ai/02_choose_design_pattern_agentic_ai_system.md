# Choose a Design Pattern for Agentic AI

## Overview
Design patterns define how agents are organized, how they collaborate, and how the AI model orchestrates tasks.

## Design Patterns

### Single-Agent System
*   **Description**: One model + tools + system prompt.
*   **Use Case**: Multi-step tasks with defined tools (e.g., research assistant).
*   **Pros/Cons**: Simple to start, but performance degrades with complexity.
*   **ReAct Pattern**: "Reason and Act" loop (Thought -> Action -> Observation) for dynamic planning.

### Multi-Agent Systems
Orchestrates specialized agents to solve complex problems.

1.  **Sequential Pattern**
    *   **Flow**: Linear execution (Agent A -> Agent B -> Agent C).
    *   **Use Case**: Structured, repeatable pipelines (e.g., Data Extract -> Clean -> Load).
    *   **Pros**: Low latency/cost (no dynamic orchestration). **Cons**: Rigid.

2.  **Parallel Pattern** (Concurrent)
    *   **Flow**: Fan-out to multiple agents, fan-in to synthesize results.
    *   **Use Case**: Gathering diverse perspectives (e.g., Sentiment + Keyword + Urgency analysis simultaneously).
    *   **Pros**: Reduced latency. **Cons**: Higher resource usage/cost.

3.  **Loop Pattern**
    *   **Flow**: Repeats until an exit condition is met (Quality check or Max iterations).
    *   **Use Case**: Iterative refinement (e.g., Generate -> Critique -> Refine).
    *   **Risk**: Potential infinite loops if exit condition fails.

4.  **Coordinator Pattern**
    *   **Flow**: Central "Coordinator" agent analyzes request and dynamically routes to specialized agents.
    *   **Use Case**: Adaptive routing (e.g., Customer Service routing to Refund vs. Tech Support agent).
    *   **Pros**: Flexible. **Cons**: High token usage/latency due to orchestration overhead.

5.  **Hierarchical Task Decomposition**
    *   **Flow**: Root agent breaks complex task into sub-tasks, delegates to sub-agents (Tree structure).
    *   **Use Case**: Ambiguous, high-complexity problems (e.g., complex research project).

6.  **Swarm Pattern**
    *   **Flow**: All-to-all collaboration without a central supervisor. Dispatcher routes initially.
    *   **Use Case**: Brainstorming / Debate (e.g., Product design with Engineer, Marketer, Finance agents).
    *   **Cons**: Highest complexity and cost; risk of non-convergence.
