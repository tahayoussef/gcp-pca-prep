# Best Practices for Planning and Federation

## Planning Accounts and Organizations
- **Account Consolidation**:
    -   Combine Cloud Identity (CI) and Google Workspace (GW) in a single account (same platform/APIs).
    -   Use **one** CI/GW account for all users to enforce consistent policies (password, 2FA, SSO).
    -   **Exception**: Use separate accounts for **Staging** vs. **Production** to test global configs (SSO, provisioning) safely.
- **Organization Structure**:
    -   Use **one** Organization node if possible for centralized policy management.
    -   Use **Folders** to delineate permissions and structure resources (e.g., by department).
    -   **Multiple Organizations**: Use only if strictly necessary (e.g., completely autonomous subsidiaries).
    -   **Sandbox/Experimentation**: Use a separate Organization for loose experimentation to keep production secure and clean.
- **DNS Domains**:
    -   Use disjoint domains (e.g., `example.com` vs `dev-example.com`) for different accounts to avoid conflicts.
    -   Verify domain ownership for primary and secondary domains.
- **Security**:
    -   **Super Admins**: Limit number. Don't use for daily tasks. Enforce 2FA (hardware keys best).
    -   **Admin Separation**: Don't grant super-admin access just for DNS management or specific GCP tasks. Use least privilege custom roles.
    -   **Logs**: Export audit logs (login, admin activity) to BigQuery for long-term retention and analysis.

## Best Practices for Federating
- **Mapping Identities**:
    -   **One Identity**: Use the same email address in IdP and Google (Subject NameID = Primary Email). Simplifies user experience and logging.
    -   **Source of Truth**: Treat external IdP as the authoritative source.
    -   **Provisioning**: Automate provisioning (one-way sync: IdP -> Google).
    -   **Routable Emails**: Ensure primary emails are valid/routable for notifications (budget alerts, support).
- **Consumer Accounts**:
    -   Assess existing consumer accounts (`@example.com` created by users personally) before federating.
    -   **Conflict Prevention**: Provision corporate accounts early to prevent new consumer sign-ups on corporate domains.
    -   **Consolidation**: Migrate or rename existing consumer accounts to avoid "conflicting account" state.
- **Identity Sets**:
    -   **Subset Rule**: Google identities should be a **subset** of IdP identities.
    -   **Orphaned Accounts**: Delete/suspend Google account immediately when IdP account is deleted to prevent "name squatting" (new employee inheriting old identity).
- **Single Sign-On (SSO)**:
    -   **Issuer**: Default is `google.com`. Use domain-specific issuer (`google.com/a/DOMAIN`) only if multiple accounts share one IdP tenant.
    -   **Session Length**: Set IdP session length < Google session length to ensure re-authentication.
    -   **Super Admins**: Exempt from enforced SSO (so they can fix IdP breakages). Enforce Google 2FA on them instead.
- **Service Accounts**:
    -   Preferred: Use OAuth 2.0/OIDC for apps acting on behalf of users.
    -   Use GCP Service Accounts for machine-to-machine.
    -   **Domain-Wide Delegation**: Use sparingly. Requires a dedicated CI/GW user to impersonate.
