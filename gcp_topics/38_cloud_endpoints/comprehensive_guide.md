# Cloud Endpoints - Comprehensive Guide

## Overview
Manage, secure, and monitor your APIs.
- **Core Function**: Acts as an API Gateway for gRPC and REST APIs.
- **Proxy**: Uses **Extensible Service Proxy (ESP)** or **ESPv2** (Envoy-based) sidecar to intercept traffic.

---

## Architecture

### 1. ESPv2 (Extensible Service Proxy)
- **What is it?**: A high-performance, Envoy-based proxy.
- **Where does it run?**:
  - **Sidecar**: Next to your application container (Cloud Run, GKE, Kubernetes).
  - **Gateway**: Standalone (Compute Engine).
- **Function**: Intercepts all incoming requests, checks **Service Control** (Auth, Quota), and if allowed, forwards to backend.

### 2. Service Management
- **Configuration**: Uses **OpenAPI Specification** (Swagger) or gRPC Service Configuration.
- **Role**: Stores the API definition, quotas, and auth rules.

### 3. Service Control
- **Runtime Checks**: The "brain" that ESP calls to answer:
  - "Is this API Key valid?"
  - "Does this user have quota left?"
- **Telemetry**: Reports logs and metrics to Cloud Operations.

---

## Features

### Authentication vs Identification
- **Identification (API Key)**:
  - "Which **Project** is calling me?"
  - Used for **Quotas** and **Billing**.
  - **Not secure** for user auth (vulnerable to MITM if not over HTTPS, and keys can be stolen).
- **Authentication (AuthN)**:
  - "Which **User** is calling me?"
  - Supports: **Firebase Auth**, **Auth0**, **Google ID Tokens** (Service Accounts).
  - mechanism: Validates **JWT** (JSON Web Token) signed by the provider.

### Quotas & Rate Limiting
- Defined in OpenAPI spec using `x-google-quota`.
- **Metric**: "Read Requests".
- **Limit**: "1000 requests per minute per Project".
- **Tiering**: Can define different tiers (Free, Gold, Platinum).

---

## Developer Workflow
1.  **Define API**: Write `openapi.yaml`.
2.  **Deploy Config**: `gcloud endpoints services deploy openapi.yaml`.
3.  **Deploy Backend**: Deploy your app code + ESPv2 container (sidecar).
4.  **Consuming**: Clients allow send requests to the ESPv2 IP/URL.

---

## Exam Focus Areas

1.  **Endpoints vs Apigee**:
    - **Cloud Endpoints**: Lightweight, focused on GCP backends (GKE, Cloud Run, App Engine). Low cost/Free (pay for Service Control calls). Good for "Internal" or "Simple External" APIs.
    - **Apigee**: Enterprise-grade. Monetization, Developer Portals, Legacy Soap transformation, Hybrid deployment. High cost.

2.  **Performance**:
    - **ESPv2** caches checks locally to reduce latency (calls Service Control asynchronously).

3.  **Transcoding**:
    - Cloud Endpoints can translate **REST (JSON)** to **gRPC** automatically. Allows you to write a high-performance gRPC backend but expose it to web clients as JSON.

4.  **OpenAPI Extensions**:
    - `x-google-backend`: Direct traffic to a specific backend address (e.g. Cloud Function URL).
    - `x-google-management`: Enable quotas.
