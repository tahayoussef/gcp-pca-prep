# Identity and Access Management for Hybrid/Multicloud

## Authenticate Workforce Users in Hybrid Environment
*   **Google Cloud Identity**: Centralized identity provider for Google Cloud and on-prem (via AD sync).
*   **Active Directory Integration**: Sync AD users to Google Cloud Identity; SSO via SAML.
*   **Patterns**:
    *   **Cloud Identity + AD Sync**: One-way sync from on-prem AD to Cloud Identity.
    *   **AD Federation**: SSO; AD remains authoritative.

## Configure Active Directory for VMs
*   VMs in Google Cloud automatically join on-prem AD domain.
*   **Tools**: AD domain join scripts; Managed Service for Microsoft AD.

## Deploy Active Directory Forest
*   Deploy AD forest entirely on Compute Engine VMs (lift-and-shift AD).
*   **Use**: When migrating entire AD infrastructure to cloud.

## Patterns for Using AD in Hybrid
*   **Hybrid AD**: On-prem AD + Google Cloud Managed AD with trust relationship.
*   **Cloud-Only AD**: AD entirely in Google Cloud.
*   **Federated Identity**: SSO with external IdP (Okta, Azure AD, etc.).

## Third-Party Integration: Cohesity
*   Cohesity for hybrid data protection (backup/DR) using Cloud Storage.
