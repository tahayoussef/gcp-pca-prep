# Monitoring and Logging

## Export Logs and Metrics

### Metric Export
*   **Use**: Export Cloud Monitoring metrics to BigQuery for long-term analysis, custom dashboards, or ML.
*   **Methods**: 
    - Log sinks to export to BigQuery, Pub/Sub, Cloud Storage.
    - Metrics scope for cross-project monitoring.

### Import Logs from Cloud Storage
*   **Use**: Re-import archived logs from Cloud Storage back to Cloud Logging for analysis.
*   **Deployment**: Cloud Function triggered by Cloud Storage object creation; reads logs and writes to Cloud Logging API.

### Stream Logs to Splunk
*   **Architecture**: Cloud Logging → Pub/Sub → Dataflow → Splunk HEC (HTTP Event Collector).
*   **Use**: Organizations using Splunk for SIEM can ingest Google Cloud logs.

## Hybrid and Multicloud Monitoring

### Patterns
*   **Centralized**: All logs/metrics sent to Google Cloud (Cloud Logging, Cloud Monitoring).
*   **Federated**: Each environment has its own monitoring; aggregated view via dashboards.

### BindPlane for On-Premises
*   **BindPlane**: Third-party agent that collects logs/metrics from on-prem servers and sends to Google Cloud.
*   **Supported Sources**: Windows, Linux, databases, network devices.
*   **Deployment**: Install BindPlane agent on-prem; configure to send to Cloud Logging/Monitoring.

### Stream Logs to Datadog
*   **Architecture**: Cloud Logging → Pub/Sub → Datadog (via Datadog integration or Dataflow).
*   **Use**: Organizations using Datadog for observability can ingest Google Cloud logs.
