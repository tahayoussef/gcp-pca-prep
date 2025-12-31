# Decide the Security

## Overview
Security in a landing zone involves a layered defense strategy (Defense in Depth), defining how to control access, protect data, and monitor threats across the resource hierarchy.

## Key Decision Points

### Service Account Management
*   **Risk**: Persistent keys for service accounts are a common attack vector.
*   **Strategy**: Limit key creation. Use **Workload Identity Federation** for external workloads instead of static keys. Use IAM to restrict who can create keys.

### Data Exfiltration Protection
*   **Tool**: **VPC Service Controls**.
*   **Function**: Creates a service perimeter around resources (like Cloud Storage buckets, BigQuery datasets).
*   **Benefit**: Prevents data from being copied to unauthorized external resources or accessed from unauthorized locations, even with valid credentials.

### Continuous Monitoring
*   **Tool**: **Security Command Center (SCC)**.
*   **Function**: continuously scans for misconfigurations (compliance drift) and active threats.
*   **Standard**: Align with **CIS Benchmarks** for Google Cloud.

### Log Aggregation
*   **Strategy**: Use **Aggregated Log Sinks** to route audit logs from all projects/folders to a central security project (e.g., into BigQuery or a storage bucket) for analysis and retention.

### Encryption
*   **At Rest**: Google encrypts data by default. For strict compliance, use **Customer-Managed Encryption Keys (CMEK)** via Cloud KMS.
*   **In Transit**: Google encrypts network traffic by default. Use TLS for application-layer encryption.

### Access Transparency
*   **Controls**: Enable **Access Transparency** to view logs of Google Support's access to your content (when support tickets are raised). Use **Access Approval** to require explicit approval before Google personnel can access data.
