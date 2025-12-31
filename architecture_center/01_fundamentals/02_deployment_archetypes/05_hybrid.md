# Google Cloud hybrid deployment archetype

- **Overview**
    - Application spans **Google Cloud and On-premises** environments.

- **Use Cases**
    - **Disaster Recovery**: On-prem app with a backup/DR site in Google Cloud.
    - **Dev/Test**: Develop on-prem, deploy to cloud (or vice versa).
    - **Cloud Bursting**: Handle peak loads by bursting to the cloud.
    - **Augmentation**: Keep legacy app on-prem but use Cloud for **AI/ML**, **BigQuery**, or storage.
    - **Tiered/Split-stack**: Frontend in Cloud (CDN, DDoS protection), Backend on-premises.

- **Design Considerations**
    - **Connectivity**: Critical need for reliable **Interconnect** (Dedicated/Partner) or VPN.
    - **Complexity**: High operational complexity to manage consistency across environments.
    - **Security**: Unified security posture is challenging.
