# Implement security by design

- **Principle Overview**
    - **Secure by Default**: System settings are secure out-of-the-box (no user action needed).
    - **Secure by Design**: Proactively embedding security throughout the development lifecycle (threat modeling, reviews).

- **Choose Secure System Components**
    - Use reliable libraries and frameworks.
    - Use **Assured Open Source Software** for secured OSS packages.
    - Scan for vulnerabilities with third-party tools.

- **Build a Layered Security Approach (Defense in Depth)**
    - Implement security at every layer (Edge, Network, Identity, Compute, Data).
    - Perform **Risk Assessments** (e.g., using CSA Cloud Controls Matrix).
    - Use **Threat Modeling** (e.g., OWASP method) to identify gaps.
    - Understand the **Shared Responsibility Model** (IaaS vs PaaS vs SaaS).

- **Use Hardened and Attested Infrastructure**
    - **Images**: Use **Container-Optimized OS (COS)** or curated/hardened images.
    - **Shielded VM**: Boot security, integrity monitoring (vTPM).
    - **OS Login**: Manage SSH access via IAM (no SSH key management needed).
    - **Org Policies**: Restrict IP allocation, locations, and service account keys.
    - **GKE**: Use Node Auto-Upgrades and **Distroless Images** to reduce attack surface.

- **Encrypt Data**
    - **At Rest**: Encrypted by default. Use **CMEK** (Customer-Managed Encryption Keys) with **Cloud KMS** or **Cloud EKM** (External Key Manager) for compliance.
    - **In Transit**: Encrypted by default (VM-to-VM). Use **TLS/mTLS** for app traffic.
    - **In Use**: Use **Confidential Computing** (Confidential VMs) to encrypt data in memory.
