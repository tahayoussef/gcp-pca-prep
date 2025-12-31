# Preventative Controls (Enterprise Foundation Blueprint)

## Overview
Preventative controls act as guardrails to block non-compliant resource configurations before they can be deployed. These are primarily enforced using **Organization Policy Service**.

## Key Organization Policy Constraints
The blueprint applies these constraints at the Organization level to ensure inheritance across all folders and projects.

### Compute Guardrails
*   **Disable External IPs**: `compute.vmExternalIpAccess` - Prevents VMs from having public IP addresses (except allowed lists).
*   **Block Serial Port**: `compute.disableSerialPortAccess` - Closes a common attack vector (SSH via serial console).
*   **Clean Projects**: `compute.skipDefaultNetworkCreation` - Ensures new projects don't start with an insecure "default" VPC.
*   **Nested Virtualization**: `compute.disableNestedVirtualization` - Reduces risks associated with unmonitored nested VMs.

### IAM Guardrails
*   **No Service Account Keys**: `iam.disableServiceAccountKeyCreation` - Forces the use of safer authentication (Workload Identity) instead of downloadable keys.
*   **Managed Service Accounts**: `iam.automaticIamGrantsForDefaultServiceAccounts` - Prevents default service accounts from getting Editor rights automatically.

### Storage & Data Guardrails
*   **Block Public Access**: `storage.publicAccessPrevention` - Enforces "public access prevention" on buckets to block `allUsers`.
*   **Uniform Access**: `storage.uniformBucketLevelAccess` - Disables legacy ACLs, requiring IAM for all bucket access.
*   **SQL Security**: `sql.restrictPublicIp` - Prevents Cloud SQL instances from having public IPs.

## Infrastructure as Code (IaC) Validation
In addition to runtime policies, the blueprint uses **Pre-deployment validation** in the CI/CD pipeline.
*   **GitOps**: Changes are committed to a repo.
*   **Policy Checks**: The pipeline runs validators (e.g., `gcloud policy-intelligence`, `terraform validate`, or `checkov`) to catch violations before Terraform apply.
