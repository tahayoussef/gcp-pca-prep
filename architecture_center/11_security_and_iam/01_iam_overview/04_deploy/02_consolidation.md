# Account Consolidation

Consolidation involves migrating existing "consumer" accounts (created by employees using corporate email) into managed Cloud Identity/Workspace accounts to ensure corporate control and security.

## Account States
1.  **Consumer Account**: Personal Google account created by user with corporate email (e.g., `user@company.com`). User owns data.
2.  **Unmanaged Account**: A consumer account that falls under a verified domain in Cloud Identity. Still user-controlled until transfer.
3.  **Managed Account**: Account fully controlled by the organization.
4.  **Conflicting Account**: Occurs when Admin creates a managed account with the same email as an existing unmanaged account.
    -   **Ballot Screen**: User prompted to choose between managed account (new, empty) and consumer account (needs renaming) on login.

## Migration Process
1.  **Verify Domain**: Adding/verifying domain in Cloud Identity automatically surfaces unmanaged accounts in the **Transfer Tool**.
2.  **Invite Users**: Send transfer requests via Transfer Tool.
3.  **User Action**:
    -   **Accept**: Account becomes managed. Data (Drive, etc.) is preserved and transferred to org control.
    -   **Decline/Ignore**: Account remains unmanaged. Admin cannot force transfer of data.
    -   **Rename**: User changes email to private address -> becomes standard consumer account (data stays with user).
4.  **Resolving Conflicts**:
    -   Avoid pre-provisioning users who have unmanaged accounts (unless necessary only for SSO and you accept the conflict).
    -   If conflict exists, user must rename their consumer account side to resolve it (`user%company.com@gtempaccount.com`).

## Reconciling Orphaned Accounts
After migration, some managed accounts may not match the External IdP identity (e.g., if user used an alias).
-   **Identify**: Compare Cloud Identity user list (CSV export) with IdP user list.
-   **Fix**: Rename the managed account to match the IdP UPN/Email.
-   **Obsolete Accounts**: Suspend or delete if no longer needed.

## Best Practices
-   **Communication**: Announce migration plans early so users don't reject the transfer request out of confusion.
-   **Batches**: Migrate in small batches (start with 10).
-   **DNS**: Do not change MX records until all consumer accounts are migrated to ensure they keep receiving email.
