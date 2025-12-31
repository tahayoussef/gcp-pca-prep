# Implement shift-left security

- **Adopt Preventive Security Controls**
    - Implement checks early (in IaC).
    - **Infrastructure as Code (IaC)**: Use **Policy Controller** or **OPA** to enforce constraints in CI/CD.
    - **Org Policies**: Enforce guardrails (e.g., restrict locations).
    - **VPC Service Controls**: Define security perimeters.

- **Automate Secure Application Releases**
    - Use CI/CD pipelines (e.g., **Cloud Build**, **Cloud Deploy**) to remove manual errors.
    - Adopt **SLSA** framework for supply chain security.
    - **Binary Authorization**: Require attestations (signatures) for container images before deployment to GKE/Cloud Run.

- **Scan for Vulnerabilities**
    - **Artifact Analysis**: Automatically scans container images in Artifact Registry for known vulnerabilities and CVEs.
    - Blocks deployment of non-compliant images.

- **Monitor Application Code**
    - **Web Security Scanner**: Dynamic analysis (DAST) for running apps (XSS, injection).
    - **Security Command Center**: Continuously monitor security posture and compliance.
