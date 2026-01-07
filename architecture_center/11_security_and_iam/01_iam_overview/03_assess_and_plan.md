# Assess and Plan Onboarding

## Overview
Before deploying Cloud Identity or Google Workspace:
-   **Understand Domain Model**: Identities, accounts, organizations.
-   **Architecture**: Choose between **Google as IdP** or **External IdP**.
-   **Existing Accounts**: Assess if employees are already using Google services with consumer accounts.

## Assess Existing User Accounts
Employees may be using unmanaged accounts, posing security and compliance risks.

### Types of Accounts to Investigate
1.  **Consumer Accounts** (`user@example.com`):
    -   **Description**: Personal accounts created by matching corporate email.
    -   **Risks**: No lifecycle control (former employees retain access), no security policy enforcement (MFA), data ownership issues.
    -   **Handling**:
        -   **Matching IdP Identity**: Migrate to Cloud Identity/Google Workspace.
        -   **No Match**: Investigate (alias mismatch? former employee?).
2.  **Gmail Accounts** (`user@gmail.com`):
    -   **Description**: Personal Gmail used for work.
    -   **Risks**: No affiliation with organization, total lack of control.
    -   **Handling**: Revoke access to corporate resources, provision new managed account, asking user to transfer data manually if needed.
3.  **Managed Accounts** (No IdP Match):
    -   **Description**: Accounts manually created by admin but not in external IdP.
    -   **Handling**: Reconcile (fix email mismatch, delete if obsolete).

## Select an Onboarding Plan
Choose a plan based on your target architecture and existing account state.

### Plan 1: No Federation (Google as IdP)
-   **Use Case**: No external IdP.
-   **Steps**:
    1.  Set up Cloud Identity/Workspace accounts.
    2.  Migrate existing consumer accounts (to avoid conflicts).
    3.  Create remaining users (Admin Console, CSV, or GAM).

### Plan 2: Federation, No Consolidation
-   **Use Case**: External IdP, but **no** existing consumer accounts to migrate.
-   **Steps**:
    1.  Set up accounts.
    2.  Configure Federation (SSO + Provisioning).
    3.  Provision all users from IdP.

### Plan 3: Federation with Consolidation (Complex but Fast SSO)
-   **Use Case**: External IdP + **existing** consumer accounts. Want SSO immediately.
-   **Steps**:
    1.  Configure Federation **safely** (prevent IdP from creating/deleting conflicting users).
    2.  Provision **new** users only via IdP.
    3.  Migrate consumer accounts to managed accounts.
    4.  Remove "safe" restrictions and fully sync IdP.
-   **Pros**: Immediate SSO coverage.
-   **Cons**: Complex initial configuration.

### Plan 4: Delayed Federation
-   **Use Case**: External IdP + **existing** consumer accounts. Simplify setup.
-   **Steps**:
    1.  Migrate all consumer accounts to managed accounts first.
    2.  Set up Federation (SSO + Provisioning) *after* consolidation.
-   **Pros**: Simpler federation setup.
-   **Cons**: Delayed SSO; double management of users during migration.

## Safe Federation for Consolidation
To use **Plan 3**, you must configure the IdP to **allow SSO** for existing consumer accounts but **prevent auto-provisioning** (which causes conflicts) or **deletion** (data loss) until migration is done.

### Strategies by IdP
-   **Azure AD (Entra ID)**:
    -   **Two Apps**: One for SSO (assigned to all), one for Provisioning (assigned only to new users).
    -   **Disable Creation**: Configure provisioning to update/suspend but **not create** users.
-   **Active Directory (GCDS)**:
    -   **Disable Creation**: Configure GCDS to not create new users.
    -   **Manual Group**: Sync only a specific group excluding consumer account holders.
-   **Okta**:
    -   **Disable Creation**: Uncheck "Create Users" in provisioning settings.
    -   **Two Apps**: Similar to Azure AD approach.
