# Security Command Center (SCC) - Comprehensive Guide

## Overview
Centralized dashboard for security and risk management across the entire Organization.
- **Scope**: Organization-level visibility (can also be activated at Project level).
- **Core Function**: Asset Discovery, Threat Detection, Vulnerability Scanning.

---

## Tiers (Exam Critical)

| Feature | Standard Tier | Premium Tier |
| :--- | :--- | :--- |
| **Cost** | Free (for Org-level). | Pay-per-use / Subscription. |
| **Asset Discovery** | Yes (Cloud Asset Inventory). | Yes. |
| **Security Health Analytics** | Basic findings (public buckets, open firewalls). | **Advanced** findings (cross-site scripting, compliance violation). |
| **Threat Detection** | None. | **Event Threat Detection** (ETD) & **Container Threat Detection** (CTD). E.g., Coin mining, brute force. |
| **Web Security Scanner** | No. | **Managed** scans for App Engine, GKE, Compute Engine. |
| **Compliance** | No. | **Compliance Mapping** (CIS, PCI-DSS, NIST, ISO). |

---

## Key Components

### 1. Security Health Analytics (SHA)
- **Misconfigurations**: "Port 22 open to world", "Bucket is public", "MFA not enabled".
- **Action**: Generates a **Finding**.

### 2. Event Threat Detection (ETD)
- **Log Analysis**: Analyzes Cloud Logging (VPC Flow Logs, Cloud Audit Logs) to find threats.
- **Threats**:
  - **Malware**: Bad IP communication.
  - **Coin Mining**: High CPU + suspicious domain.
  - **Leakage**: BigQuery data exfiltration.

### 3. Web Security Scanner
- **Active Scanning**: Crawls your public web apps (App Engine, GKE, Compute) to find OWASP Top 10 vulns (XSS, Flash Injection, Mixed Content).
- **Note**: Modifies state (it crawls forms). Be careful with production data.

### 4. Container Threat Detection
- **Runtime Analysis**: Analyzes system calls (syscalls) on the GKE node kernel.
- **Threats**: "Reverse Shell", "Unexpected Child Process".

---

## Remediation
- **Manual**: Click "Fix" in console (guides you).
- **Automated**: Findings are published to **Platform Logs** or **Pub/Sub**.
  - **Pattern**: SCC -> Pub/Sub -> Cloud Functions -> Fix the issue (e.g., Close the firewall).

---

## Exam Focus Areas

1.  **Tier Selection**:
    - "Need to detect cryptocurrency mining". -> **Premium Tier** (Event Threat Detection).
    - "Need to check if buckets are public". -> **Standard Tier**.

2.  **Compliance**:
    - "Need to verify CIS conformance". -> **Premium Tier**.

3.  **Automation**:
    - "Automatically remediate open firewalls". -> **SCC Export to Pub/Sub** -> Cloud Function.

4.  **Scope**:
    - SCC is best enabled at the **Organization Level** for complete visibility.
