# Authentication and Authorization (Enterprise Foundation Blueprint)

## Overview
This section of the Enterprise Foundation Blueprint outlines how to manage identities and access control using **Cloud Identity** and **Identity and Access Management (IAM)**. The goal is to ensure only authorized users access Google Cloud resources and that access is managed centrally and securely.

## Key Recommendations

### External Identity Provider (IdP)
*   **Federation**: Federate Cloud Identity with your existing IdP (e.g., Active Directory, Azure AD, Okta). Use **Single Sign-On (SSO)** so users sign in with their corporate credentials.
*   **Source of Truth**: Keep the external IdP as the source of truth for user identities. Use Google Cloud Directory Sync (GCDS) or similar tools to provision users.
*   **MFA**: Enforce **Multi-Factor Authentication (MFA)** at your IdP, preferably with phishing-resistant keys (FIDO/Titan).

### Groups for Access Control
*   **Group-Based Access**: Grant IAM roles to **Google Groups**, not individual users. This simplifies management and auditing.
*   **Functional Groups**: Create groups based on job function (e.g., `grp-gcp-network-viewer`, `grp-gcp-security-reviewer`).
*   **Predefined Roles**: Avoid Basic roles (Owner/Editor/Viewer). Use **Predefined roles** (e.g., Network Viewer, Security Reviewer) for least privilege.

### Super Admin Accounts
*   **Break-Glass**: Super admin accounts bypass SSO (for emergency access).
*   **Security**: Enforce **2-Step Verification (2SV)** with security keys directly in Cloud Identity for these accounts.
*   **Recovery**: Disable self-recovery for super admins; rely on a documented internal process.

### Consumer Account Consolidation
*   **Problem**: Employees using personal accounts (consumer Gmail) for work creates security risks.
*   **Remediation**: Consolidate these into the managed Cloud Identity organization. Block access to consumer accounts if possible.

## Administrative Controls
*   **Session Length**: Enforce session limits for Google Cloud services.
*   **Audit Logs**: Share Cloud Identity audit logs with Google Cloud for centralized monitoring.
*   **Group Security**: Restrict who can add members to groups (prevent external members).
