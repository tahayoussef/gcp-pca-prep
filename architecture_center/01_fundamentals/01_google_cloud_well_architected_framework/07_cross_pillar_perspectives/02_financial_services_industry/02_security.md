# FSI perspective: Security

- **Security by Design**
    - **Compliance**: Embed controls for **PCI DSS**, **GLBA**, etc. early in the lifecycle.
    - **Perimeters**: Use **VPC Service Controls** to prevent data exfiltration.
    - **IaC**: Define security configurations as code (Terraform) and scan with **SAST** in CI/CD.

- **Zero Trust**
    - **Verification**: continuous verification of user and device trust (**Chrome Enterprise Premium** + **IAM**).
    - **Network**: Use **Private Service Connect** to access services privately without public internet exposure. **Identity-Aware Proxy (IAP)** for application-level access control.

- **Regulatory Compliance**
    - **Assured Workloads**: Use **Assured Workloads** to enforce data residency and compliance regimes (FedRAMP, CJIS) automatically.
    - **Data Protection**: Use **Cloud DLP** to discover and classify sensitive financial data.
    - **Audit**: Enable **Cloud Audit Logs** for comprehensive tracking of admin activities.
