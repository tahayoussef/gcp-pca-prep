# Secured BigQuery Data Warehouse

## Overview
Enterprise-grade secure **BigQuery** data warehouse for confidential data with comprehensive security controls.

## Key Security Controls

### Data Ingestion
*   **VPC Service Controls**: Perimeter around BigQuery to prevent data exfiltration.
*   **Private Connectivity**: Private Service Connect/VPN for data import.

### Encryption
*   **Client-Side Encryption**: Encrypt data before sending to Google Cloud.
*   **Column-Level Encryption**: Encrypt sensitive columns using AEAD functions.
*   **CMEK**: Customer Managed Encryption Keys via Cloud KMS.

### Access Control
*   **IAM Roles**: Fine-grained access control (data analyst, data engineer, security analyst groups).
*   **Column-Level Access Control**: Restrict access to specific columns.
*   **Dynamic Data Masking**: Mask sensitive data for unauthorized users.

### Data De-Identification
*   **Sensitive Data Protection**: Detect and de-identify PII.
*   **Tokenization**: Replace sensitive values with tokens.

### Monitoring & Compliance
*   **Cloud Logging**: Audit all data access.
*   **Access Transparency**: Logs of Google support access.
*   **Organizational Policies**: Enforce security policies.

## Organization Structure
*   **Folders**: Separate projects for data platform, producers, consumers, common services.
*   **Projects**: Isolated environments for different teams/purposes.
