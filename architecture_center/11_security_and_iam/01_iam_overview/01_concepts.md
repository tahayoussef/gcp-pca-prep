# Concepts

## Overview of Google identity management
- **Google Sign-In**: Central authentication service for Google Cloud, Marketing Platform, and Ads. Relies on "Google identities".
- **Domain Model Entities**:
    - **Google Identity**: An email address (e.g., `alice@gmail.com`, `alice@example.com`) unique to a person. A person can have multiple identities.
    - **User Account**: Stores attributes and configuration for an identity. Not created on the fly; must be provisioned.
    - **Consumer Account**: Created by self-service (e.g., Gmail or custom email). Owned by the individual. Can have multiple identities (emails).
    - **Managed User Account**: Controlled by an organization via Cloud Identity or Google Workspace. Defined by a primary email involved in a domain registered to the org.
    - **Service Account**: Special account for machine users (applications, VMs). Identified by email (e.g., `...@developer.gserviceaccount.com`). No password; uses keys or IAM binding.
    - **Group**: bundles users for access control or mailing lists. Identified by email. Can contain users, other groups, and service accounts.
    - **Organizational Unit (OU)**: Hierarchical container for *users* to apply configs (licenses, 2FA). distinct from GCP resource folders.
    - **Cloud Identity / Workspace Account**: Top-level container (tenant) for users, groups, and OUs.

## Reference Architectures
- **Core Tenets**:
    - **Authoritative Source**: Single system to create/manage identities (e.g., HRIS, Active Directory).
    - **Identity Provider (IdP)**: Single system for authentication (SSO).
- **Architecture Patterns**:
    1.  **Google as IdP and Authoritative Source**:
        -   Cloud Identity/Workspace manages users.
        -   Good for: No existing on-prem infrastructure, using Workspace for collaboration.
    2.  **Google as IdP with HRIS as Authoritative Source**:
        -   HRIS provisions users to Google. Google handles auth.
        -   Good for: Existing HRIS workflows, using Workspace.
    3.  **External IdP (Federation)**:
        -   **External IDaaS (Okta, Ping, etc.)**: IDaaS is both IdP and authoritative (or connected to HRIS). Provisions to Google.
        -   **Active Directory (AD)**:
            -   **GCDS (Google Cloud Directory Sync)**: Syncs users/groups from AD to Google (one-way).
            -   **AD FS**: Handles SSO.
            -   Good for: Existing AD infrastructure, seamless Windows sign-in.
        -   **Entra ID (Azure AD)**:
            -   Entra ID provisions to Google. Entra ID handles SSO (can federate with on-prem AD).
            -   Good for: Microsoft 365/Azure customers.

## Single Sign-On (SSO)
- **Concept**: Users auth via external IdP, not Google password.
- **Protocol**: SAML 2.0. Google is Service Provider (SP), External IdP is SAML IdP.
- **Flow**:
    1.  User accesses Google service.
    2.  Redirected to IdP (with `SAMLRequest` and `RelayState`).
    3.  User authenticates at IdP.
    4.  IdP redirects back to Google Assertion Consumer Service (ACS) with `SAMLResponse` (signed assertion).
    5.  Google validates signature and logs user in.
- **Configuration**:
    -   **SAML Profiles**: Assign different SSO settings to different OUs or groups.
    -   **Certificates**: Google needs IdP's public key to verify assertion signatures.
    -   **NameID**: Maps IdP user to Google user (usually email).
- **Network**: User browser relays messages. IdP doesn't need to be exposed to internet, just reachable by user.
