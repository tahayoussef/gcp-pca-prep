# Design Self-Service Data Platform for Data Mesh

## Overview
How to design a **self-service platform** that enables domain teams to create and manage data products in a data mesh.

## Architecture
*   **IaC Templates**: Terraform/Cloud Deployment Manager templates for common data product patterns.
*   **Service Catalog**: Self-service portal for provisioning data products.
*   **CI/CD Pipelines**: Automated testing and deployment for data products.

## Platform Components

### Infrastructure Provisioning
*   **Automated Setup**: Domain teams click a button to provision BigQuery datasets, Dataflow pipelines, Pub/Sub topics.
*   **Standardized Configuration**: Pre-configured security, networking, monitoring.

### Data Product Consumption Interfaces
*   **BigQuery Views/Functions**: SQL interfaces for analytical consumption.
*   **APIs**: REST/gRPC APIs for operational consumption.
*   **Streams**: Pub/Sub topics for real-time consumption.
*   **ML Models**: Vertex AI models exposing predictions.

### Common Services
*   **Dataplex Universal Catalog**: Metadata management, data discovery.
*   **Data Observability**: Automated data quality monitoring (freshness, completeness, schema changes).
*   **Data Lineage**: Track data sources and transformations.
*   **Access Management**: Self-service IAM via IaC.

## Benefits
*   **Reduced Time-to-Market**: Domain teams can create data products quickly.
*   **Consistency**: Standardized patterns across all domains.
*   **Governance**: Automated policy enforcement at provisioning time.
