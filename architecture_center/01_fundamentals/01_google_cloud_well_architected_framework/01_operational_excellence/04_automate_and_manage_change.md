# Automate and manage change

- **Foundational Elements**
    - **Change governance** (policies/approval), **Risk assessment**, **Testing/validation**, and **Controlled deployment**.

- **Adopt Infrastructure as Code (IaC)**
    - Use tools like **Terraform** to manage infrastructure declaratively.
    - **Benefits**:
        - Human-readable configurations (JSON/YAML).
        - **Consistency** and repeatability (eliminates drift).
        - Accountability and simplified troubleshooting.

- **Implement Version Control**
    - Use systems like **Git** to track changes to IaC and configurations.
    - Provides visibility, history, and **rollback** capabilities.
    - Essential for collaboration and risk mitigation.

- **Build CI/CD Pipelines**
    - Automate building, testing, and deployment.
    - Tools:
        - **Cloud Build**: Managed build service.
        - **Cloud Deploy**: diverse deployments (blue-green, traffic splitting).
    - Enables continuous integration and early bug detection.

- **Use Configuration Management Tools**
    - Tools: Puppet, Chef, Ansible, **VM Manager**.
    - Ensures resource consistency and compliance.
    - Reduces manual error risks and improves operational efficiency.

- **Automate Testing**
    - Integrate into CI/CD pipelines.
    - Types:
        - **Unit testing**: Individual functions.
        - **Integration testing**: Component interactions.
        - **End-to-end testing**: specific real-world scenarios.
    - Ensures code meets quality standards before deployment.
