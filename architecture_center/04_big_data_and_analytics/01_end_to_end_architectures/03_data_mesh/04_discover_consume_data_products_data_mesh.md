# Discover and Consume Data Products in a Data Mesh

## Overview
How data consumers **discover** and **consume** data products in a data mesh.

## Discovery
*   **Dataplex Catalog**: Search for data products by keywords, tags, domain.
*   **Metadata**: View schemas, documentation, SLOs, ownership.
*   **Data Preview**: Sample data before requesting access.

## Access Request Workflow
1.  **Consumer** searches catalog and finds desired data product.
2.  **Request Access**: Submit access request via portal.
3.  **Approval**: Domain owner or automated policy approves.
4.  **IAM Grants**: Consumer receives necessary BigQuery/API permissions.

## Consumption Methods

### Analytical Consumption
*   **BigQuery SQL**: Query authorized views directly.
*   **BI Tools**: Connect Looker, Tableau, Data Studio to BigQuery.

### Programmatic Consumption
*   **BigQuery API**: Python, Java, Node.js clients.
*   **REST APIs**: Call Cloud Endpoints/Apigee APIs.

### Streaming Consumption
*   **Pub/Sub Subscriptions**: Subscribe to event streams.
*   **Dataflow Pipelines**: Process streaming data.

### ML Consumption
*   **Vertex AI Predictions**: Call ML model endpoints.

## Data Consumption Patterns
*   **Single-Domain Consumption**: Consumer uses data from one domain.
*   **Multi-Domain Joins**: Consumer joins data from multiple domains.
*   **Aggregated Views**: Consumer creates aggregated views across domains.
