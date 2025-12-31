# Build Data Products in a Data Mesh

## Overview
How domain teams build and expose **data products** for consumption in a data mesh.

## Create Domain Data Warehouse
*   **BigQuery Dataset**: Each domain has its own BigQuery dataset for domain data.
*   **ETL/ELT Pipelines**: Dataflow, Dataproc, or dbt for transformations.
*   **Data Quality Checks**: Automated validation rules.

## Define Consumption Interfaces

### SQL Interfaces
*   **Authorized Views**: BigQuery views that provide curated data access.
*   **Authorized Functions**: User-defined functions for computed data.
*   **Direct Read APIs**: BigQuery Storage API for programmatic access.

### Streaming Interfaces
*   **Pub/Sub Topics**: Real-time event streams.
*   **Change Data Capture (CDC)**: Stream table changes.

### API Interfaces
*   **Cloud Endpoints/Apigee**: RESTful APIs wrapping BigQuery.
*   **Cloud Functions**: Serverless APIs.

### ML Models
*   **Vertex AI Models**: Expose predictions as a data product.

### Looker Blocks
*   **Pre-built Dashboards**: Looker blocks for common domain queries.

## Expose to Consumers
*   **Register in Dataplex Catalog**: Make data product discoverable.
*   **Define Schemas & Documentation**: Clear contracts for consumers.
*   **Set Access Controls**: IAM policies for authorized consumers.
*   **Establish SLOs**: Latency, freshness, availability guarantees.

## Data Location Considerations
*   **Cross-Region Access**: Use BigQuery's multi-region datasets for global access.
*   **Data Locality**: Keep data close to consumers for performance.
