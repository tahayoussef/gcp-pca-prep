# Cloud Identity-Aware Proxy (IAP) - Comprehensive Guide

## Overview
Control access to your cloud applications and VMs running on Google Cloud from the internet.
- **Core Verification**: Verifies user identity and context (Zero Trust) before allowing access.
- **No VPN Needed**: Users can access internal apps without a VPN.

---

## Two Main Modes

### 1. IAP for HTTPS Resources (Web Apps)
- **Targets**: App Engine, Cloud Run, Compute Engine (via Load Balancer).
- **Mechanism**:
  - Acts as a centralized authentication layer.
  - Checks IAM policy (`roles/iap.httpsResourceAccessor`) before forwarding request to backend.
  - **Header Injection**: Injects `x-goog-iap-jwt-assertion` header into the request. Backend can verify this JWT to know *who* the user is (email, user ID).

### 2. IAP for TCP (SSH/RDP)
- **Targets**: Compute Engine VMs.
- **Benefits**:
  - **No Public IP needed**: VM can have only private IP.
  - **No Bastion Host**: No need to manage a jump box.
- **How it works**:
  - Engineer runs `gcloud compute ssh instance-name --tunnel-through-iap`.
  - Traffic goes from Client -> Google IAP endpoint -> Google Internal Network -> VM.
  - **IAM**: Checks `roles/iap.tunnelResourceAccessor`.

---

## Context-Aware Access
- IAP integrates with **Access Context Manager**.
- **Rules**:
  - "Allow access only from Corporate Laptop".
  - "Allow access only from US IP addresses".
  - "Allow access only if Device OS is updated".

---

## Exam Focus Areas

1.  **Secure Remote Access**:
    - "How to SSH into private VM without VPN or Bastion?". -> **IAP for TCP**.

2.  **Zero Trust / BeyondCorp**:
    - "Expose internal HR app to employees working from home securely". -> **IAP**.

3.  **Authentication**:
    - "How does the backend app know who the user is?". -> **Verify the JWT token** in the `x-goog-iap-jwt-assertion` header.

4.  **Firewall**:
    - For IAP TCP to work, you must allow ingress traffic from IAP's IP range: `35.235.240.0/20` on Port 22 (SSH) or 3389 (RDP).
