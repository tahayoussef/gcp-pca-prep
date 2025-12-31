# Operations for Developer Platform and Applications

## Overview
Common automated and manual operations for managing the platform and applications.

## Common Automated Operations
Automated via **webhook triggers** (API-driven from source control or developer portal):

### Platform Operations
*   **Add Tenant**: Admin submits form → automated trigger creates tenant resources.
*   **Add Application**: Developer submits form → automated trigger creates app resources.

### Application Development
*   **Build/Deploy to Dev**: Developer commits code → auto-build and deploy (CI/CD).
*   **Deploy YAML Config Changes**: Developer commits config → auto-deploy.
*   **Deploy Infra Changes**: Developer commits Terraform → auto plan/apply.

### Promotion
*   **Promote to Nonprod/Prod**: Operator merges branches → automated rollout.
*   **Promote Infra Changes**: Operator merges Terraform changes → automated rollout.

## Common Manual Operations
*   **Platform Upgrades**: GKE version upgrades, service mesh updates.
*   **Security Patching**: Apply security patches to nodes/control planes.
*   **Incident Response**: Manual intervention for production issues.
*   **Resource Quota Adjustments**: Modify quotas based on demand.
