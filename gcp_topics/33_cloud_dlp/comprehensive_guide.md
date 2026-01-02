# Cloud Data Loss Prevention (DLP) - Comprehensive Guide

## Overview
Fully managed service to inspect, classify, and redact sensitive data (PII) from text, images, and storage.
- **Use Case**: Compliance (GDPR, HIPAA), sanitizing data for dev/test environments.
- **Scope**: Can scan GCS buckets, BigQuery tables, Datastore, or stream data (Content API).

---

## Core Concepts

### 1. InfoTypes
- **Definition**: A "detector" for a specific type of sensitive data.
- **Built-in**: over 150+ detectors (e.g., `CREDIT_CARD_NUMBER`, `US_SOCIAL_SECURITY_NUMBER`, `EMAIL_ADDRESS`, `GCP_CREDENTIALS`).
- **Custom**: You can define your own using Regex or Dictionary lists (e.g., `Start Trek Employee ID`).

### 2. Inspection vs Redaction
- **Inspection**: "Tell me what PII is in this file and where." (Returns likelihood scores and locations).
- **Redaction**: "Replace the PII with *** or a hash." (Returns the sanitized file).
  - Can be reversible (pseudonymization using Format-Preserving Encryption - FPE).
  - Can be irreversible (Masking with *).

### 3. De-identification
- **Masking**: `****-1234`.
- **Replacement**: Replace with a fixed string `[REDACTED]`.
- **Bucketing**: Replace specific age `24` with range `20-30`. (K-anonymity).
- **Crypto-Hashing**: Replace with a consistent hash (allows joining data on UserID without revealing the ID).

---

## Operations
- **Inspection Job**: Batch scan of a GCS bucket or BigQuery table.
- **InspectContent API**: Real-time scan of a text string/image sent in the request.
- **Triggers**: Schedule scans periodically.

---

## Exam Focus Areas

1.  **Compliance**:
    - "Upload PII to BigQuery but keep it compliant".
    - Answer: Use **DLP** to inspect/redact PII *before* ingestion (using Dataflow) or scan *after* ingestion (DLP Inspection Job).

2.  **Images**:
    - DLP can redact text from images (OCR + Redaction).

3.  **Cost Check**:
    - "Minimize DLP costs".
    - Answer: Use **Sampling** (don't scan 100% of rows) or limit the **InfoTypes** (only scan for Credit Cards if that's all you care about).

4.  **Templates**:
    - Use **Inspect Templates** and **De-identify Templates** to decouple configuration from the code. Create a template once, reference it in multiple jobs.
