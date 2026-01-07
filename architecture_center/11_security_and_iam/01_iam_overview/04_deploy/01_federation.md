# Federation Implementation

Federation connects your external IdP to Google Cloud to automate identity management and enable Single Sign-On (SSO).

## Key Components
-   **Provisioning**: One-way sync of users and groups from IdP to Google Cloud. Changes in IdP propagate to Google.
-   **Single Sign-On (SSO)**: Google delegates authentication to the IdP via SAML. IdP enforces passwords and policies (MFA).

## Federating with Active Directory (AD)
**Tools**:
-   **Provisioning**: Google Cloud Directory Sync (GCDS) - runs on-prem, syncs LDAP to Google API.
-   **SSO**: Active Directory Federation Services (AD FS).

### Mapping Strategies
1.  **Structure**:
    -   **Single Forest**: Map to one Cloud Identity account.
    -   **Multi-Forest**: Requires one GCDS instance per forest. Can map to single or multiple Cloud Identity accounts depending on trusts.
2.  **Users**:
    -   **Map by UPN (Recommended)**: Best if UPNs are valid email addresses matching verified domains.
    -   **Map by Email**: Use `mail` attribute if UPNs are internal-only (`.local`). Requires unique, populated emails for all users.
3.  **Groups**:
    -   Sync **Security Groups** to control GCP IAM access.
    -   **Global Groups**: Sync limited to local domain if using Global Catalog.
    -   **Universal Groups**: Visible across forest.

## Federating with Azure AD (Microsoft Entra ID)
**Tools**: Google Cloud/Google Workspace Gallery App in Azure AD.

### Mapping Strategies
1.  **Structure**:
    -   **Single Tenant**: Map to one Cloud Identity account.
    -   **Multi-Tenant**: Best to use separate Cloud Identity accounts per tenant to ensure isolation.
    -   **Guest Users (B2B)**: Difficult to sync features (UPNs use `*.onmicrosoft.com` which isn't verifiable in Google).
2.  **Users**:
    -   **Map by UPN**: Standard Azure approach.
    -   **Map by Email**: Alternative if UPNs don't match verified domains.
3.  **Groups**:
    -   **Security Groups**: Mapped to Google Groups for IAM.
    -   **Mail-Enabled Groups**: Ensure email uses a verified custom domain, otherwise Azure generates `onmicrosoft.com` address which fails sync.
