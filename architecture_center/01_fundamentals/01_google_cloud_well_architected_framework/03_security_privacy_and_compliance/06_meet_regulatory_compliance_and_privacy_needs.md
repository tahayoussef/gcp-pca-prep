# Meet regulatory, compliance, and privacy needs

- **Address Organizational Risks**
    - **Assessment**: Perform risk assessments regularly using frameworks like **Cloud Controls Matrix (CCM)** and **Threat Modeling** (OWASP).
    - **Mitigation**: Use technical controls (Cloud VPN, Cloud Interconnect), contractual protections (**CDPA**), and third-party attestations (ISO/IEC 27017).

- **Regulatory and Compliance Obligations**
    - **Compliance Resource Center**: Central hub for certifications and regulation support.
    - **Assured Workloads**: Automate compliance for specific regimes (FedRAMP, IL4) by enforcing region restrictions, key management settings, and personnel access controls.
    - **Blueprints**: Use Terraform blueprints for FedRAMP, HIPAA, etc.

- **Monitor Compliance**
    - **Access Transparency**: Logs when Google admins access your content.
    - **Network Logging**: Firewall Rules Logging, VPC Flow Logs.
    - **Security Command Center Premium**: Compliance monitoring and alerts.
    - **Key Access Justifications**: Reasons for key access requests.

- **Data Sovereignty**
    - **Operational**: Restrict resource locations (Org Policies) and limit Google personnel access based on attributes.
    - **Software**: Use Hybrid/Multicloud or **Google Distributed Cloud** to run workloads where needed.

- **Privacy Requirements**
    - **Data Residency**: Control where data is stored using Org Policies.
    - **Classification**: Use **Sensitive Data Protection** to discover/tag sensitive data (PII) and **Dataplex** for cataloging.
    - **Lock Down Access**: Use **VPC Service Controls** perimeters and MFA.
