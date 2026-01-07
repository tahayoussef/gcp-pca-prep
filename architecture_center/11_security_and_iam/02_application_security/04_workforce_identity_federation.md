# Workforce Identity Federation

Workforce Identity Federation allows you to grant external identities (partners, contractors, employees in non-Google IdPs) access to Google Cloud resources using their existing credentials, without creating Google user accounts or syncing directories.

## Key Concepts
-   **Syncless**: No need to use GCDS to sync users to Cloud Identity. Google interprets the external token directly.
-   **Supported Protocols**: SAML 2.0 and OpenID Connect (OIDC). Supports Azure AD, Okta, AD FS, etc.
-   **Workforce Identity Pools**: Containers for managing groups of external identities.
    -   **Providers**: definition of the IdP relationship within a pool.
-   **Attribute Mapping**: Maps attributes from the IdP assertion (claims) to Google Cloud attributes (e.g., `google.subject`, `attribute.department`) for use in IAM policies.

## Use Cases
-   **B2B/Partners**: Grant temporary access to partners without managing extended lifecycles.
-   **Partial Migration**: Use existing IdP for auth while gradually adopting Google Cloud.

## Comparison
-   **Workforce Identity Federation**: For *humans* (users, groups).
-   **Workload Identity Federation**: For *software workloads* (applications, CI/CD pipelines, AWS Lambda).
