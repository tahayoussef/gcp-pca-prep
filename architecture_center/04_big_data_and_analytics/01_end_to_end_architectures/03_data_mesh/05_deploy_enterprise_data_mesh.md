# Deploy Enterprise Data Mesh

## Overview
Enterprise-ready **data mesh** blueprint with security controls, multi-project organization, and automated deployment.

## Architecture
*   **Multi-Folder Organization**: Separate folders for platform, producers, consumers, common services.
*   **Projects**: Isolated projects per domain and environment (dev, prod).
*   **Networking**: VPC Service Controls, Private Service Connect.

## Key Architectural Decisions
*   **Decentralized Data Ownership**: Domains own their data products.
*   **Centralized Platform**: Common infrastructure managed by platform team.
*   **Federated Governance**: Policies defined centrally, enforced automatically.

## Identity & Access (IAM)
*   **Groups**: Data engineer, data analyst, data consumer groups.
*   **Service Accounts**: For automated pipelines.
*   **Least Privilege**: Minimal permissions per role.

## Deployment

### Interactive Deployment
*   **Service Catalog**: Self-service UI for provisioning data products.
*   **Terraform Templates**: Pre-built IaC modules.

### Artifact Pipelines
*   **CI/CD**: Cloud Build pipelines for data product deployment.
*   **GitOps**: Configuration in version control.

## Security Controls
*   **VPC Service Controls**: Data perimeters.
*   **CMEK**: Customer-managed encryption.
*   **Sensitive Data Protection**: PII detection and de-identification.
*   **Audit Logging**: Comprehensive access logs.

## Workflows
*   **Producer Workflow**: Create data product → Deploy infrastructure → Publish to catalog.
*   **Consumer Workflow**: Discover data product → Request access → Consume via approved interface.
