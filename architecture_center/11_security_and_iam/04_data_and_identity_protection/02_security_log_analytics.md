# Security Log Analytics

Security log analytics involves collecting, aggregating, and analyzing Google Cloud logs to detect threats and audit usage.

## Workflow
1.  **Enable Logs**:
    -   **Admin Activity**: Enabled by default (free).
    -   **Data Access Logs**: Must be enabled manually (incurs costs). High volume.
    -   **Service-specific Logs**: (e.g., VPC Flow Logs, Cloud DNS logs).
    -   **Log Scoping Tool**: Use to map logs to **MITRE ATT&CK** tactics and techniques.
2.  **Route Logs**:
    -   Use **Aggregated Sinks** at the Org/Folder level to centralize logs.
    -   **Log Analytics**: Route to a Log Bucket (supports SQL).
    -   **BigQuery**: Route to a dataset for advanced analytics/BI.
    -   **3rd Party SIEM**: Route to Pub/Sub or Cloud Storage for ingestion.
    -   **Google Security Operations (Chronicle)**: Integrated ingestion for threat detection.
3.  **Analyze Logs**:
    -   **SQL**: Use for searching logs in BigQuery or Log Analytics.
    -   **YARA-L**: Used for detection rules in Chronicle.
    -   **CSA (Community Security Analytics)**: Open-source repository of pre-built SQL queries for common security questions (e.g., "detect unauthorized login attempts").
