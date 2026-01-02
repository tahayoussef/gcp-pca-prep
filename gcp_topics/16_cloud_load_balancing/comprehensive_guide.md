# Cloud Load Balancing - Comprehensive Guide

## Decision Tree (The "Holy Grail" of Exam questions)

### 1. What type of traffic?
- **HTTP(S) or HTTP/2?** -> **Application Load Balancer (ALB)** (Layer 7).
- **TCP, UDP, SSL (Non-HTTP)?** -> **Network Load Balancer (NLB)** (Layer 4).

### 2. Internal or External?
- **Public Users (Internet)** -> **External**.
- **Private VPC / On-Prem Users** -> **Internal**.

### 3. Global or Regional?
- **Distributed users, Multi-region failover** -> **Global**.
- **Compliance (Data Residency), Standard Tier Network** -> **Regional**.

### 4. Client IP & Offload (For Network LBs)?
- **Need SSL Offload?** -> **Proxy Network Load Balancer**. (Terminates connection, Client IP in header).
- **Need to see original Client IP directly?** -> **Passthrough Network Load Balancer**. (No termination, fast).

---

## Load Balancer Types

### 1. Global External Application Load Balancer (Classic & Managed)
- **Layer**: 7 (HTTP/S).
- **Scope**: Global (Anycast IP).
- **Features**: CDN, Cloud Armor (WAF), SSL Termination, Path-based routing (`/video` vs `/images`).
- **Backends**: Instance Groups (MIG), NEG (Zonal, Serverless, Internet).

### 2. Regional External Application Load Balancer
- **Layer**: 7.
- **Scope**: Regional.
- **Use Case**: Data residency compliance (traffic must stay in region).

### 3. Internal Application Load Balancer
- **Layer**: 7.
- **Scope**: Regional (Cross-region internal access possible via Global Access).
- **Use Case**: Microservices, internal web apps.
- **Envoy**: Based on Envoy proxy.

### 4. Proxy Network Load Balancer (External/Internal)
- **Layer**: 4 (TCP/SSL).
- **Architecture**: Terminates connection at LB -> Opens new connection to backend.
- **Features**: SSL Offload, TCP/SSL Proxy.
- **Note**: Backend sees LB IP, not Client IP (unless using Proxy Protocol).

### 5. Passthrough Network Load Balancer (External/Internal)
- **Layer**: 4.
- **Architecture**: Packets passed directly to backend (DSR - Direct Server Return).
- **Features**: Preserves **Client IP**. Extremely high performance.
- **Limit**: Must be **Regional**.

---

## Key Concepts

### Backend Services & Health Checks
- **Backend Service**: Logical group of backends (Instance Groups, NEGs).
- **Health Check**: Probes backends. If unhealthy, traffic stops routing there.
- **Session Affinity**:
  - **Client IP**: Stickiness based on IP hash.
  - **Generated Cookie**: (ALB only) Stickiness based on cookie.

### Negative Caching / CDN
- Enable **Cloud CDN** on Backend Service (ALB only).
- Caches content at Google Edge.

### SSL Certificates
- **Google-Managed**: Auto-renewed, free. (Requires DNS validation).
- **Self-Managed**: You upload cert/key.

---

## Exam Focus Areas

1.  **Selection Scenarios**:
    - "Web app, global users, needs WAF (Cloud Armor)". -> **Global External Application Load Balancer**.
    - "UDP game server, needs low latency, regional". -> **External Passthrough Network Load Balancer** (Regional).
    - "Internal DB, TCP traffic, needs to see original Client IP". -> **Internal Passthrough Network Load Balancer**.
    - "TLS termination for non-HTTP traffic". -> **SSL Proxy Load Balancer**.

2.  **Preserving Client IP**:
    - **Passthrough**: Yes, automatically.
    - **ALB (HTTP)**: Yes, in `X-Forwarded-For` header.
    - **Proxy NLB**: No, unless you enable PROXY protocol (and backend supports it).

3.  **Cross-Region Internal**:
    - "Internal clients in Region A need to reach Internal LB in Region B".
    - Solution: **Global Access** enabled on the Internal LB Forwarding Rule.
