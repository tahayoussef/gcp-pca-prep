# Deployment Methodology

## Overview
Automated CI/CD pipelines and deployment strategy for infrastructure and applications.

## Repositories & Ownership
*   **infra**: Platform infrastructure (Platform Developer → Platform Admin approval)
*   **eab-infra**: Terraform modules for multi-tenant infrastructure
*   **fleet-scope**: Fleet team scopes and namespaces
*   **app-factory**: Application repo creation
*   **app-template**: Base code for new apps
*   **app-code**: Application source code (App Developer → App Operator approval)
*   **config-policy**: GKE cluster policies (Config Sync)
*   **terraform-modules**: Reusable Terraform modules

## Deployment Pipelines

### Foundation Infrastructure Pipeline
*   Entry point for resource deployments (from Enterprise Foundation Blueprint).
*   Creates:
    *   Multi-tenant infrastructure
    *   Fleet-scope pipeline
    *   Application factory

### Multi-Tenant Infrastructure Pipeline
*   Creates shared infrastructure for all tenants.

### Fleet-Scope Pipeline
*   Creates namespaces and RBAC role bindings.

### Application Factory
*   Creates application CI/CD pipelines.

### Application CI/CD Pipeline
*   **Continuous Integration**: Build and test on code commit.
*   **Continuous Deployment**: Deploy to dev → nonprod → prod via branch merges.

## Principles
*   **Automation**: Builds security, auditability, traceability, repeatability into deployments.
*   **Separation of Responsibilities**: Different teams, different permissions.
*   **Least Privilege**: Minimal permissions for each role.
