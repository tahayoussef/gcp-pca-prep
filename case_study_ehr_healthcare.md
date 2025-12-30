# Case Study: EHR Healthcare (v6.1 - Hybrid & Compliance Focus)

## Company Overview
EHR Healthcare provides a SaaS platform for electronic health records. They are moving from a **colocation (colo)** environment to Google Cloud to fix scalability issues and outages.

## Business Requirements
*   **Reliability**: 99.9% uptime for customer-facing systems.
*   **Growth**: Rapidly onboard new insurance providers (reduce time to market).
*   **Compliance**: HIPAA, GDPR, PII protection.
*   **Insights**: Analyze global health trends from their data.

## Existing Technical Environment
*   **Legacy**: 
    *   Colocation Data Centers.
    *   **Databases**: Mix of **MySQL**, **MS SQL Server**, **Redis**, **MongoDB**.
    *   **Connectivity**: Integrations with insurance providers via on-prem lines.
*   **App Stack**: Some containerized apps (Kubernetes), some legacy.

## Key Services & Architecture Patterns
*   **Compute**:
    *   **GKE**: Target for containerized apps.
    *   **Anthos (GKE Enterprise)**: Ideally suited if they want to keep some workloads on-prem or manage the hybrid state consistently.
*   **Databases (The big migration challenge)**:
    *   MySQL -> **Cloud SQL for MySQL**.
    *   MS SQL Server -> **Cloud SQL for SQL Server**.
    *   Redis -> **Memorystore for Redis**.
    *   MongoDB -> **MongoDB Atlas** (Marketplace) or self-managed on GCE (if Atlas isn't an option in the question).
*   **Networking**:
    *   **Dedicated Interconnect**: Required for low-latency, high-throughput connection to the Colo/On-prem.
    *   **Cloud VPN**: For connecting to smaller insurance provider partners.
*   **Security & Compliance**:
    *   **Cloud DLP**: Essential for scanning/redacting PII before data hits analytics.
    *   **Cloud IAM**: Least privilege.
    *   **Google Cloud Directory Sync (GCDS)**: Sync existing Active Directory users to Cloud Identity.
*   **API Management**:
    *   **Apigee**: The standard answer for "Manage, Secure, and Monetize content APIs for external partners (insurance providers)".

## Exam Scenarios & "Gotchas"
*   **Scenario**: "How do we securely connect to insurance providers for data exchange?"
    *   **Answer**: **Apigee** (for API management) + **Cloud VPN** (for connectivity).
*   **Scenario**: "We need to analyze patient data but must strip PII first."
    *   **Answer**: Ingest -> **Dataflow** calls **Cloud DLP API** to de-identify -> Write to **BigQuery**.
*   **Scenario**: "Ensure we don't accidentally deploy non-compliant containers."
    *   **Answer**: **Binary Authorization** on GKE.
*   **Scenario**: "We need 99.9% availability for the database."
    *   **Answer**: **Cloud SQL High Availability** (Regional). It provides a standby in a different zone.
