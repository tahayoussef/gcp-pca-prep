# Container & Artifact Registry - Comprehensive Guide

## Overview

### Evolution
- **Container Registry (GCR)**: Legacy service. Stores images in Cloud Storage buckets. Domain: `gcr.io`.
- **Artifact Registry (AR)**: Modern, Evolution of GCR. Stores container images + language packages (Maven, npm, Python). Domain: `pkg.dev`.

**Recommendation**: New projects should use **Artifact Registry**. Existing projects should migrate.

---

## Artifact Registry Features

### 1. Multi-Format Support
Unlike GCR (containers only), AR supports:
- **Docker/OCI**
- **Maven/Gradle** (Java)
- **npm** (Node.js)
- **Python** (PyPI)
- **Apt/Yum** (OS packages)
- **Go Modules**

### 2. Repository Modes

**Standard Repository**:
- Stores your private packages/images.

**Remote Repository** (Caching Proxy):
- Caches artifacts from upstream public sources (Docker Hub, Maven Central, PyPI).
- **Benefit**:
  - **Reliability**: If Docker Hub goes down, you still have cached images.
  - **Performance**: Faster pulls (within Google network).
  - **Security**: Scan cached images for vulnerabilities.

**Virtual Repository**:
- A single endpoint that aggregates multiple repositories (Standard + Remote).
- **Benefit**: Client configures one URL, pulls from local, then falls back to remote.

### 3. Security & Governance
- **Vulnerability Scanning**: Automatically scan images for CVEs (Container Analysis).
- **Binary Authorization**: Enforce policy that only trusted/scanned images can be deployed.
- **Customer Managed Encryption Keys (CMEK)**: Encrypt repositories with your own Cloud KMS keys.
- **VPC Service Controls**: Protect data exfiltration.

---

## Migration: GCR -> Artifact Registry

### Key Differences (Exam Focus)

| Feature | Container Registry (Legacy) | Artifact Registry (Modern) |
| :--- | :--- | :--- |
| **Backing Store** | Cloud Storage Bucket (user visible) | Managed storage (hidden, abstracted) |
| **Permissions** | Bucket-level IAM (Coarse) | Repository-level IAM (Fine-grained) |
| **Locations** | Multi-region only (us, eu, asia) | **Regional** (us-central1) or Multi-regional |
| **Domain** | `gcr.io` | `LOCATION-docker.pkg.dev` |
| **Protocol** | Docker only | Docker, Maven, npm, Python, etc. |

### Migration Strategy
**Redirection (gcr.io)**:
- You can enable redirection: requests to `gcr.io` automatically map to Artifact Registry.
- Allows transparent migration without changing CI/CD pipelines immediately.
- `gcr.io/my-project/image` -> `us-docker.pkg.dev/my-project/gcr.io/image`.

---

## Authentication

### Docker Auth
Recommended Method:
```bash
gcloud auth configure-docker \
    us-central1-docker.pkg.dev
```
Updates `~/.docker/config.json` to use `gcloud` credential helper (short-lived tokens).

### Service Accounts
Use **Workload Identity Federation** (for external CI/CD like GitHub Actions) or **Service Account Keys** (if absolutely necessary) to authenticate.

---

## Exam Focus Areas

1.  **IAM Granularity**:
    - Scenario: "Need to grant Team A read/write access to ONLY their images, but Team B cannot see them".
    - Solution: Use **Artifact Registry**. Create separate repositories for Team A and Team B. Grant IAM roles on the **Repository** level. (GCR cannot do this as it's bucket-level).

2.  **Latency/Cost**:
    - Scenario: "GKE cluster in us-central1 needs low latency pulls".
    - Solution: Create **Artifact Registry** repository in **us-central1** (Regionally co-located).

3.  **Supply Chain Security**:
    - Scenario: "Prevent dependency on public Docker Hub availability".
    - Solution: Use **Artifact Registry Remote Repository** to cache Docker Hub images.
    - Scenario: "Ensure developers only pull approved packages".
    - Solution: Use **Virtual Repository** balancing internal approved packages + cached remote packages.
