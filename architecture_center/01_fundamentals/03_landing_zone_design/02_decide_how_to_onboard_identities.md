# Decide How to Onboard Identities

## Overview
Identity onboarding defines how users authenticate to Google Cloud. Using **Cloud Identity** or **Google Workspace** allows you to manage the lifecycle and security of user accounts, rather than relying on unmanaged consumer Gmail accounts.

## Identity Architecture Options

### Option 1: Google as Primary Identity Provider (IdP)
Google (Cloud Identity or Workspace) acts as the authoritative source for user identities.
*   **Use Case**: No existing IdP, or a desire to start fresh with a specific user subset.
*   **Integration**: Supports direct authentication and readily integrates with third-party apps via SAML/OIDC.

### Option 2: Federation with an External IdP
Integrates Google Cloud with an existing identity system (e.g., Active Directory, Azure AD, Okta, Ping).
*   **Use Case**: Employees should use existing corporate credentials to access Google Cloud.
*   **Mechanism**: **Federation** establishes trust, allowing external identities to sign in to Google Cloud services.
*   **Benefits**: seamless user experience (SSO), centralized credential management in the existing IdP.

## Key Recommendations
*   **Avoid Consumer Accounts**: Do not use private personal accounts (Gmail) for corporate access.
*   **Consolidate**: Verify existing domains and consolidate user accounts to ensure corporate control.
*   **SSO**: Implement Single Sign-On (SSO) for a better user experience and security posture.
