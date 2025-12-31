# Enterprise Foundations Blueprint

## Overview
The **Enterprise Foundations Blueprint** (formerly Security Foundations Blueprint) provides a comprehensive, opinionated guide and deployable Terraform code (`terraform-example-foundation`) for setting up a production-ready Google Cloud environment. It is designed to meet the needs of security-conscious enterprises.

## Core Components
The blueprint is built around several key architectural decisions:

1.  **Identity**: Synchronize with an external IdP; use groups for access; enforce MFA.
2.  **Organization Structure**: A single Organization with a folder hierarchy based on environments (Dev, Non-Prod, Prod).
3.  **Networking**: Strictly controlled network paths using Shared VPCs, private IPs, and centralized gateways (Hub-and-Spoke).
4.  **Security**: "Secure by default" with predefined Organization Policies, centralized logging, and threat detection.
5.  **DevOps**: Infrastructure as Code (IaC) managed via GitOps (Cloud Build + Terraform).

## Usages
*   **Starting Point**: Deploy the full Terraform reference implementation to bootstrap a new layout.
*   **Compliance Benchmark**: Compare an existing environment against these Google-recommended best practices.

## Blueprint Modules
The blueprint is divided into several detailed guides:
*   [Authentication and Authorization](02_authentication_and_authorization.md)
*   [Organization Structure](03_organization_structure.md)
*   [Networking](04_networking.md)
*   [Detective Controls](05_detective_controls.md)
