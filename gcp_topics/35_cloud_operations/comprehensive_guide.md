# Cloud Operations (Stackdriver) - Comprehensive Guide

## Overview
Integrated suite for Logging, Monitoring, Tracing, and Profiling.
- **Legacy Name**: Stackdriver.
- **Agent**: The **Ops Agent** (Unified Logging & Monitoring) is recommended for Compute Engine VMs.

---

## 1. Cloud Logging (Log)
- **Log Router**: The central nervous system.
  - **Sink**: Rules to route logs to destinations.
  - **Destinations**:
    - **Default Bucket**: Stored for 30 days (by default).
    - **Cloud Storage**: Cheap, long-term retention (Years).
    - **BigQuery**: Analytics (SQL query logs).
    - **Pub/Sub**: Stream to external systems (Splunk, Datadog).
- **Log Exclusion**: Don't ingest noisy logs to save money.
- **Export**: Aggregate logs from entire Organization into a centralized "Audit Project".

## 2. Cloud Monitoring (Metrics)
- **Metrics**: Time-series data (CPU usage, Latency).
- **Uptime Checks**: Ping endpoints from around the world.
- **Alerting Policies**:
  - **Metric Threshold**: "CPU > 80% for 5 mins".
  - **Rate of Change**: "Error rate increased by 50%".
- **Dashboards**: Visualize metrics (GQL - Google Query Language or PromQL).

## 3. Cloud Trace (Latency)
- **Distributed Tracing**: Follow a request as it hops across microservices.
- **Use Case**: "User reported slow page load. Which internal service is the bottleneck?".
- **Automatic**: App Engine, Cloud Functions, Cloud Run (often built-in). GCE/GKE need instrumentation (OpenTelemetry).

## 4. Cloud Profiler (Code Performance)
- **Continuous Profiling**: Low-overhead sampling of production code.
- **Flame Graphs**: Visualize where CPU time or RAM is spent inside a function stack.
- **Use Case**: "Why is this function consuming 2GB of RAM?".

## 5. Cloud Debugger (Deprecated but Exam Legacy)
- **Snapshot Debugging**: Capture local variables and stack trace at a specific line of code *without stopping* the app.
- **Note**: Officially deprecated in favor of Snapshot Debugger in Firebase/IDs, but historic exams might mention it.

---

## Exam Focus Areas

1.  **Retention & Compliance**:
    - "Store logs for 7 years for audit". -> **Log Sink to Cloud Storage** (Archive class).
    - "Analyze logs with SQL". -> **Log Sink to BigQuery**.

2.  **Organization Aggregation**:
    - "Security team needs to see logs from ALL projects". -> **Aggregated Sink** at Org/Folder level exporting to a central **BigQuery** dataset or **Logging Bucket**.

3.  **Troubleshooting**:
    - "App is slow, need to find bottleneck". -> **Cloud Trace**.
    - "App is burning CPU, need to optimize code". -> **Cloud Profiler**.
    - "VM is unreachable". -> **Cloud Monitoring (Uptime Check)** or **Serial Console Output** (in Logging).
