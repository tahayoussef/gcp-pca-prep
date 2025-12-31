# Google Cloud multicloud deployment archetype

- **Overview**
    - Application uses **Google Cloud and at least one other cloud provider** (AWS, Azure, etc.).

- **Use Cases**
    - **Disaster Recovery**: Primary in GCP, DR in another cloud (or vice versa).
    - **Best of Breed**: Application in another cloud uses specific GCP services (e.g., **BigQuery** analytics, **Vertex AI**) for data processing.
    - **Avoid Vendor Lock-in**: Strategic decision to distribute workloads.

- **Design Considerations**
    - **Connectivity**: Use **Cross-Cloud Interconnect** for high-bandwidth links.
    - **Cost**: High. Egress fees between clouds, redundant storage, underutilized resources.
    - **Complexity**: Requires expertise in multiple platforms. Security governance is difficult.
    - **Management**: Use tools like **Terraform** or **GKE attached clusters** (Anthos) to unifty management.
