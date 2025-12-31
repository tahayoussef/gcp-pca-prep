# AI and ML perspective: Operational excellence

- **Model Development Foundation**
    - **Versioning**: Code, Data, and Models must be versioned together to ensure reproducibility.
    - **Foundation**: Define clear problem statements and outcomes before coding.

- **Automate Lifecycle (MLOps)**
    - **Orchestration**: Use **Vertex AI Pipelines** for end-to-end automation (Data Prep -> Train -> Deploy).
    - **CI/CD**: Adapt CI/CD for ML (CT/CD). validate data integrity, stress test models (e.g., with **Locust**), and validate model quality *before* deployment.

- **Implement Observability**
    - **Monitoring**: Track **Training-Serving Skew** and **Prediction Drift**.
    - **Golden Dataset**: Use a validated baseline dataset to detect skew.
    - **GenAI**: Use **Human-in-the-loop (HITL)** for evaluating subjective quality (safety, grounding).

- **Culture**
    - **Collaboration**: Breaks silos between Data Scientists and Engineers.
    - **Ethics**: Embed safety and bias checks early in the process.
