# Organization Structure (Enterprise Foundation Blueprint)

## Overview
The blueprint defines a structured resource hierarchy to manage ownership, access control, and cost allocation. It uses **Folders** to group resources by environment and **Projects** to isolate specific functions and workloads.

## Folder Structure
The hierarchy is rooted in the **Organization** node, ensuring central visibility.

*   **`bootstrap`**: Contains resources for the CI/CD pipeline and Terraform state.
*   **`common`**: Holds shared resources like secrets, centralized logs, and security tools.
*   **`networking`**: Dedicated for network hub resources and Shared VPC host projects.
*   **`development` / `nonproduction` / `production`**: Environment-specific folders to enforce distinct policies (e.g., stricter access in Prod).

## Project Strategy
Projects are used as security boundaries. Key projects include:

*   **Host Projects** (`prj-net-*-svpc`): Contain the VPC networks.
*   **Service Projects** (`prj-{env}-{workload}`): Where application resources live, attached to the host project.
*   **Centralized Security**:
    *   `prj-c-logging`: Aggregates audit logs.
    *   `prj-c-scc`: Hosting Security Command Center configuration.
    *   `prj-c-kms`: Centralized Key Management Service.

## Governance
*   **Labels**: Apply consistent metadata (e.g., `environment`, `application`, `billingcode`) to all projects for reporting.
*   **Essential Contacts**: Configure groups to receive Google Cloud notifications (e.g., billing alerts, security notifications) ensuring they don't go to unmonitored individuals.
