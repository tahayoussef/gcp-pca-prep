# Identity and Access Governance Patterns

## Overview
Best practices for identity and access management (IAM) governance on Google Cloud.

## Key Patterns

### 1. Discover Unused Accounts & Permissions
*   **IAM Recommender**: Provides recommendations to remove excess permissions.
*   **Policy Analyzer**: Identify who has access to resources.

### 2. User Access Requests
*   **Google Groups**: Users request group membership; approvers grant access via group membership.
*   **Self-Service**: Reduces admin burden.

### 3. Time-Bound Access
*   **Conditional Role Bindings**: Grant access with expiration time.
*   **Group Membership Expiration**: Auto-remove users from groups after period.

### 4. Log Lifecycle Events
*   **Cloud Audit Logs**: Track IAM policy changes, group membership changes.
*   **Alerting**: Set up alerts for privileged access.

### 5. Access Certification
*   **Regular Reviews**: Use Policy Analyzer to audit access periodically.
*   **Revoke Unnecessary Access**: Remove unused permissions.

### 6. Manage Privileged Access
*   **Service Account Impersonation**: Users impersonate service accounts for privileged operations (instead of direct permissions).
*   **Audit Logs**: Track all impersonation events.

## Tools
*   **IAM Recommender**, **Policy Analyzer**, **Cloud Audit Logs**, **Google Groups**.
