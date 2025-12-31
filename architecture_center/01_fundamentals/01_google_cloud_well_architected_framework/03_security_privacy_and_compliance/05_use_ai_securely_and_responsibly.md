# Use AI securely and responsibly

- **Secure Usage Recommendations**
    - **Design**: Contextualize AI risks within business processes.
    - **Data Security**: Apply strong foundations (IAM, encryption) to AI data.
    - **Pipeline Security**: Secure code/model artifacts, use **SLSA** guidelines, tracking lineage.
    - **Input Protection**: monitoring prompts and inputs (Generative AI).

- **AI Governance**
    - **Fairness**: Use **Vertex AI** evaluation metrics (bias detection).
    - **Explainability**: Use **Vertex Explainable AI** (feature attribution).
    - **Data Lineage**: Track data origin and transformations using **Dataplex**.
    - **Accountability**: Log key events (**Cloud Logging**) and analyze errors (**Error Reporting**).
    - **Privacy**: Implement **Differential Privacy** (add noise) during training (e.g., in BigQuery).
