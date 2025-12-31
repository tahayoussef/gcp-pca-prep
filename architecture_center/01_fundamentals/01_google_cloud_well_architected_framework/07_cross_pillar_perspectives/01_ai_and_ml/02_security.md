# AI and ML perspective: Security

- **Data Governance**
    - **Tools**: Use **Dataplex Universal Catalog** for data discovery, lineage, and governing data access.
    - **Protection**: Use **Sensitive Data Protection (DLP)** to scan and de-identify PII in training data.

- **Secure Pipelines**
    - **Artifacts**: Protect model weights and code in **Cloud Storage** (Encrypted with **Cloud KMS**) and **Vertex AI Model Registry**.
    - **Access Control**: Use **IAM** with Least Privilege. Use dedicated Service Accounts for pipelines.
    - **Supply Chain**: Verify container images and dependencies (SLSA guidelines).

- **Secure Environment**
    - **Compute**: Use **Shielded VMs** or **Confidential Computing** (Confidential VMs) to protect data/code during training usage.
    - **Network**: Use **Private Service Connect** and Private IPs to keep training traffic off the public internet.

- **GenAI Security**
    - **Threats**: Guard against **Prompt Injection**, **Data Poisoning**, and Model Theft.
    - **Defense**: Validate inputs, sanitize outputs, and monitor for abuse.
