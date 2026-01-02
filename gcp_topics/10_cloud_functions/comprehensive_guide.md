# Cloud Functions - Comprehensive Guide

## Cloud Functions - Introduction

### Overview
Serverless execution environment for building and connecting cloud services.
- **Microservices**: Single-purpose functions.
- **Zero Management**: No servers to provision/manage.
- **Auto-Scale**: Scales to 0.

---

## Cloud Functions Generations: 1st Gen vs 2nd Gen

### 1st Gen (Legacy)
- **Architecture**: Proprietary Google environment.
- **Concurrency**: Process 1 request per instance.
- **Timeout**: Max 9 minutes.
- **Observability**: Basic Cloud Build logs.

### 2nd Gen (Recommended / Default)
- **Architecture**: Built on **Cloud Run** and **Eventarc**.
- **Concurrency**: Supports **Concurrent requests** (up to 1000 per instance).
- **Timeout**:
  - **HTTP Functions**: Max **60 minutes**.
  - **Event Functions**: Max 9 minutes.
- **Features**: Traffic splitting, larger instances (up to 32GB RAM), longer timeouts, custom build steps.
- **Triggering**: Uses Eventarc (Audit Logs, 90+ GCP services).

---

## Triggers

### 1. HTTP Triggers
- Function receives an HTTP(S) request.
- **Use Case**: Webhooks, lightweight APIs.
- **Invocations**: Synchronous.

### 2. Event-Driven Triggers
- **Cloud Storage**: Trigger on file upload (`google.storage.object.finalize`).
- **Pub/Sub**: Trigger on message publish.
- **Firestore**: Trigger on document create/write.
- **Eventarc (2nd Gen only)**: Trigger on *any* Audit Log event (e.g., "BigQuery Job Completed").

---

## Runtimes & Dependencies
- **Languages**: Node.js, Python, Go, Java, .NET, Ruby, PHP.
- **Dependencies**: Add `requirements.txt` (Python) or `package.json` (Node.js). Dependencies are installed during the **Build** phase (Cloud Build).

---

## Securing Cloud Functions

### 1. Public Access (Unauthenticated)
- Run `gcloud functions add-iam-policy-binding` with `member=allUsers` and `role=roles/cloudfunctions.invoker` (1st Gen) or `roles/run.invoker` (2nd Gen).

### 2. Private Access (Authenticated)
- **Identity**: Caller must provide OIDC ID Token in `Authorization: Bearer <token>` header.
- **Service-to-Service**: Use Service Accounts.
- **VPC Access**:
  - **Egress**: Access private resources (Cloud SQL) via **Serverless VPC Access Connector**.
  - **Ingress**: Restrict using "Allow internal traffic only".

---

## Exam Focus Areas

1.  **Gen 1 vs Gen 2**:
    - **Scenario**: "Process needs to run for 45 minutes". -> **2nd Gen (HTTP)** (Max 60 min).
    - **Scenario**: "Need to handle 100 concurrent requests on a single warm instance to save money". -> **2nd Gen** (Concurrency).

2.  **Triggers**:
    - **Scenario**: "Trigger function when a specific BigQuery error occurs". -> **Eventarc** (Audit Logs).
    - **Scenario**: "Process file immediately after upload". -> **Cloud Storage trigger**.

3.  **Idempotency**:
    - Important!: Functions triggers (especially Pub/Sub) offer **At-Least-Once** delivery.
    - Your code **MUST be idempotent** (safe to run multiple times with same input).
    - **Retries**: Can enable "Retry on failure". If code is not idempotent, retries can corrupt data.
