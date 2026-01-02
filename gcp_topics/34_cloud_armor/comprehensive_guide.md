# Cloud Armor - Comprehensive Guide

## Overview
DDoS protection and Web Application Firewall (WAF) service.
- **Scope**: Global (Edge). Protects External Load Balancers.
- **Defense**: Protects against L3/L4 (DDoS) and L7 (Web Attacks).

---

## Tiers (Exam Critical)

| Feature | Standard | Enterprise (Managed Protection) |
| :--- | :--- | :--- |
| **Cost** | Free (L3/L4 protection provided by Google Network). Pay-per-rule for WAF. | Monthly Subscription + Data Processing fee. |
| **DDoS Protection** | L3/L4 Volumetric (Sny flood, UDP flood) - **Always On**. | **L7 DDoS** protection (Adaptive Protection). |
| **Support** | None. | **DDoS Response Team** (Human support during active attack). |
| **Bill Protection** | No. | **DDoS Bill Protection** (Credits for spike in bill due to attack). |

---

## Security Policies (WAF)
- **Rules**:
  - **Allow/Deny**: Based on IP, Geo-location, ASN.
  - **Pre-configured WAF Rules**: `sqli-v33-stable`, `xss-v33-stable` (Based on ModSecurity/OWASP).
  - **Custom Rules**: CEL (Common Expression Language). E.g., `request.headers['user-agent'].contains('BadBot')`.

---

## Adaptive Protection
- **Machine Learning**: Learns "normal" traffic patterns for your specific backend.
- **Alerting**: Detects anomalies (e.g., "High request rate from country X").
- **Signature**: Automatically generates a WAF rule to block the *specific* attack signature without blocking legit traffic.
- **Auto-Deploy**: Can be configured to automatically block the attack (Enterprise).

---

## Exam Focus Areas

1.  **Use Case Selection**:
    - "Prevent SQL Injection". -> **Cloud Armor** (WAF Rule).
    - "Protect against massive DDoS and get bill credits". -> **Cloud Armor Enterprise**.
    - "Block traffic from a specific country". -> **Cloud Armor** (Geo-match rule).
    - "Only allow access from corporate VPN IP". -> **Cloud Armor** (Allow List).

2.  **Order of Evaluation**:
    - Rules evaluated by **Priority** (0 to 2147483647).
    - First match wins.
    - **Default Rule**: Deny (or Allow) at lowest priority.

3.  **Integration**:
    - Works with **Global External HTTP(S) LB**, **TCP/SSL Proxy LB**.
    - **Hybrid**: Can protect on-prem apps if they are behind a GCP LB (Hybrid connectivity).

4.  **Logging**:
    - Armor logs are part of **Load Balancer logs**.
    - Check `jsonPayload.enforcedSecurityPolicy` to see why a request was blocked.
