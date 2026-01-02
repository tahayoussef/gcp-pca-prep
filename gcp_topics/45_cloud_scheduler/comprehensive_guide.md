# Cloud Scheduler - Comprehensive Guide

## Overview
Fully managed, serverless enterprise-grade cron job scheduler.
- **Core Function**: "Cron as a Service".
- **Targets**: HTTP/S endpoints, Pub/Sub topics, App Engine HTTP applications.

---

## Key Features

### 1. Reliability & Retries
- **At-least-once delivery**: Guarantees your job runs, but might rarely run twice. Idempotency in job handlers is recommended.
- **Retry Policy**:
  - Configurable: Max retry count, Max retry duration, Min/Max backoff.
  - **Exponential Backoff**: Prevents thundering herd if the target is down.

### 2. Integration Targets
- **Pub/Sub**: Trigger Cloud Functions or Cloud Run indirectly (Scheduler -> Pub/Sub -> Cloud Run).
- **HTTP/S**: Call any public URL or internal private endpoints (if in same VPC/using triggers).
- **App Engine**: Native integration for App Engine tasks.

### 3. Unix Cron Syntax
- Uses standard cron format: `* * * * *` (Minute Hour Day Month DayOfWeek).

---

## Exam Focus Areas

1.  **Retry Configuration**:
    - "Job triggers a Cloud Function that reads a file. If the file is locked, we want to try again later." -> Configure **Retry Policy** with backoff.

2.  **Architecture Pattern**:
    - "Need to trigger a Cloud Run Batch job every night at 2 AM." -> **Cloud Scheduler** -> **HTTP POST** (to Cloud Run jobs trigger URL).

3.  **Fan-out**:
    - "Trigger 10,000 workers every hour." -> Cloud Scheduler -> **Pub/Sub** -> 10,000 subscribers.
