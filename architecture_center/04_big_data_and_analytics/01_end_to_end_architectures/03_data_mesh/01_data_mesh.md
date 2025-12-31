# Data Mesh Architecture and Functions

## Overview
**Data Mesh** is a decentralized data architecture paradigm that treats data as a product owned by domain teams.

## Four Principles
1.  **Domain-Oriented Ownership**: Data owned and managed by domain teams (not centralized data team).
2.  **Data as a Product**: Each domain treats their data as a product with clear ownership, SLOs, quality standards.
3.  **Self-Service Data Infrastructure**: Platform team provides tools/infrastructure for domain teams to build data products easily.
4.  **Federated Computational Governance**: Centralized governance policies enforced through automation (not manual processes).

## Key Functions

### Data Producer Teams
*   **Domain Experts**: Own business logic data (e.g., sales, marketing, customer service).
*   **Build Data Products**: Create datasets, APIs, or streams for consumption.
*   **Ensure Quality**: SLAs on freshness, accuracy,completeness.

### Data Consumer Teams
*   **Discover Data Products**: Use data catalog (Dataplex) to find products.
*   **Request Access**: Self-service access request workflows.
*   **Consume Data**: Via SQL, APIs, streaming, ML models.

### Central Data Governance Team
*   **Define Policies**: Data classification, retention, access policies.
*   **Enforce Compliance**: Automated policy enforcement.

### Platform Team
*   **Infrastructure as Code (IaC)**: Provide templates for data products.
*   **Common Services**: Dataplex Catalog, data observability, CI/CD.
*   **Enable Self-Service**: Reduce friction for domain teams.

## Google Cloud Implementation
*   **Dataplex**: Data discovery, governance, metadata management.
*   **BigQuery**: Data warehousing for each domain.
*   **Pub/Sub**: Event streaming between domains.
*   **Cloud Build**: CI/CD for data pipelines.
