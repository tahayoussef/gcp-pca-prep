# Identity and Access Management (IAM) - Comprehensive Guide

## Cloud IAM - Introduction

### Overview
Identity and Access Management (IAM) controls **who (identity) can do what (permissions) on which resources** in Google Cloud.

**Core Principle**: Grant minimum necessary permissions (Principle of Least Privilege)

### IAM Consists Of

**1. Principal (Who)**
- Google Account (end user)
- Service Account (application/workload)
- Google Group
- Google Workspace domain
- Cloud Identity domain
- All Authenticated Users (allAuthenticatedUsers)
- All Users (allUsers - public access)

**2. Role (What permissions)**
- Collection of permissions
- Permissions define allowed actions on resources
- Format: `service.resource.verb` (e.g., `compute.instances.list`)

**3. Resource (Which resource)**
- Organization, folder, project, or service resource
- Organized hierarchically

**4. Policy (Binding)**
- Links principals to roles on a resource
- Attached to resources
- Inherited down the hierarchy

### IAM Policy Structure

```json
{
  "bindings": [
    {
      "role": "roles/storage.objectViewer",
      "members": [
        "user:alice@example.com",
        "serviceAccount:my-app@project.iam.gserviceaccount.com"
      ]
    }
  ]
}
```

---

## Cloud IAM - Understanding Service Accounts

### What Are Service Accounts?

**Definition**: Special type of account used by applications and compute workloads (not humans)

**Format**: `SERVICE_ACCOUNT_NAME@PROJECT_ID.iam.gserviceaccount.com`

**Purpose**: Enable applications to authenticate and access GCP resources securely

### Types of Service Accounts

**1. User-Managed Service Accounts**
- Created explicitly by users
- Fully controlled by user
- Custom naming

**2. Google-Managed Service Accounts**
- Created automatically by GCP services
- Example: Compute Engine default service account
- Managed by Google

**3. Default Service Accounts**
- Automatically created when enabling certain services
- **Compute Engine**: `PROJECT_NUMBER-compute@developer.gserviceaccount.com`
- **App Engine**: `PROJECT_ID@appspot.gserviceaccount.com`
- **Best Practice**: Don't use defaults; create custom service accounts

### Service Account as Principal vs. Resource

**Service Account as Principal** (identity making requests):
- Acts on behalf of applications
- Given IAM roles to access resources
- Example: VM's service account accessing Cloud Storage

**Service Account as Resource** (being accessed):
- Other principals can impersonate or manage it
- Controlled via `roles/iam.serviceAccountUser`, `roles/iam.serviceAccountTokenCreator`
- Example: User impersonating a service account

### Authentication Methods

**1. Attached Service Accounts** (Recommended)
- Service account attached to compute resource (VM, Cloud Run, GKE pod)
- Application uses Application Default Credentials (ADC)
- No explicit key management required
- **Most secure method**

**2. Workload Identity Federation** (For external workloads)
- Authenticate external workloads without service account keys
- Uses OIDC/SAML/AWS credentials
- **Preferred for CI/CD, AWS, Azure, on-prem**

**3. Service Account Keys** (Avoid when possible)
- JSON key files downloaded manually
- **Security risk**: Long-lived credentials, can be stolen
- Use only when no alternative exists
- Rotate regularly if used

**4. Service Account Impersonation**
- User/principal acts as service account temporarily
- Auditability: logs show both user and service account
- More secure than sharing keys

### Service Account Permissions

```
# Grant BigQuery access to service account (as principal)
gcloud projects add-iam-policy-binding PROJECT_ID \
  --member="serviceAccount:my-sa@PROJECT_ID.iam.gserviceaccount.com" \
  --role="roles/bigquery.dataViewer"

# Allow user to impersonate service account (SA as resource)
gcloud iam service-accounts add-iam-policy-binding my-sa@PROJECT_ID.iam.gserviceaccount.com \
  --member="user:alice@example.com" \
  --role="roles/iam.serviceAccountTokenCreator"
```

**Exam Tip**: Service accounts function both as principals (doing work) and resources (being managed/impersonated). Know the difference.

---

## Cloud IAM - Service Account Key Management

### Overview
Service account keys are credentials that allow authentication outside of GCP (e.g., on-premises, third-party clouds).

### Types of Keys

**1. User-Managed Keys**
- Created/managed by users
- Downloaded as JSON files
- Long-lived (no automatic expiration)
- **High security risk** - can be stolen, leaked, or compromised

**2. Google-Managed Keys**
- Managed automatically by Google
- Used internally by Google services
- Automatically rotated
- Cannot be downloaded
- **Preferred when applicable**

### Best Practices for Key Management

**1. Avoid Keys When Possible**
- Use attached service accounts for GCP resources
- Use Workload Identity Federation for external workloads
- Use service account impersonation for short-lived access

**2. When Keys Are Necessary**:
- **Limit permissions**: Grant least privilege to the service account
- **Rotate regularly**: Max 90 days (30 days preferred)
- **Audit usage**: Enable Data Access audit logs
- **Store securely**: Use Secret Manager, never commit to Git
- **Monitor**: Set up alerts for key creation/usage
- **Delete unused keys**: Use Recommender to identify inactive keys

**3. Detection and Prevention**:
- Organization policy: `constraints/iam.disableServiceAccountKeyCreation`
- Audit logs: Track key creation and usage
- Recommender: Identifies unused service account keys

**Key Rotation Process**:
1. Create new key
2. Deploy new key to applications
3. Verify new key works
4. Delete old key
5. Update tracking/inventory

**Exam Tip**: Service account keys are a security risk. Always prefer alternatives (attached SA, Workload Identity Federation, impersonation). If keys must be used, rotate frequently, store in Secret Manager, and audit.

---

## Cloud IAM - Permissions and Roles

### Permissions

**Format**: `service.resource.verb`

Examples:
- `compute.instances.create`
- `storage.buckets.list`
- `bigquery.datasets.get`

**Key Points**:
- Permissions are not granted directly to principals
- Permissions are bundled into roles
- Thousands of permissions exist across GCP services

### Roles

**Definition**: Collection of permissions

**Structure**: `roles/SERVICE.ROLE_NAME`

Examples:
- `roles/compute.admin`
- `roles/storage.objectViewer`
- `roles/iam.serviceAccountUser`

---

## Cloud IAM - Role Type Details

### 1. Basic Roles (Legacy - Avoid)

**Types**:
- **Viewer (`roles/viewer`)**: Read-only access to all resources
- **Editor (`roles/editor`)**: Viewer + can modify resources
- **Owner (`roles/owner`)**: Editor + manage roles and billing

**Problems**:
- **Too broad**: Grant thousands of permissions
- **Violate least privilege**: Often more access than needed
- **Legacy**: Exist for backward compatibility

**Recommendation**: Use predefined or custom roles instead

---

### 2. Predefined Roles (Recommended)

**Definition**: Fine-grained roles created and maintained by Google for specific services

**Examples**:
- `roles/compute.instanceAdmin.v1`: Manage Compute Engine instances
- `roles/storage.objectCreator`: Create/overwrite Cloud Storage objects
- `roles/bigquery.dataViewer`: Read BigQuery data

**Advantages**:
- **Least privilege**: Specific to service/function
- **Maintained by Google**: Updated as services evolve
- **Well-documented**: Clear permission sets

**Best Practice**: Start with predefined roles; create custom only when needed

---

### 3. Custom Roles

**Definition**: User-defined roles with custom permission sets

**When to Use**:
- Predefined roles grant too many permissions
- Need specific combination of permissions
- Compliance/security requirements

**Creation**:
```bash
gcloud iam roles create myCustomRole \
  --project=PROJECT_ID \
  --title="My Custom Role" \
  --permissions=compute.instances.get,compute.instances.list
```

**Limitations**:
- Can only contain permissions for a single service or related services
- Cannot include permissions outside your organization/project scope
- Maintenance burden (must update as APIs evolve)
- Launch stages: ALPHA, BETA, GA, DISABLED

**Best Practice**: Use sparingly. Audit regularly. Disable when unused.

---

## Cloud IAM - Principle of Least Privilege

### Definition
Grant only the minimum permissions necessary to perform a task - no more, no less.

### Implementation Strategies**1 **Start with minimal permissions**, add as needed (not reverse)

**2. Use role recommendations** (Google's ML-based suggestions for permission removal)

**3. Use denial policies** to enforce restrictions

**4. Time-bound access** for temporary needs

**5. Conditional IAM** for context-based access

**6. Regular audits** - remove unused permissions

**Example Scenario**:
- **Bad**: Grant `roles/editor` to developer who only needs to read logs
- **Good**: Grant `roles/logging.viewer`

**Exam Tip**: Least privilege is a core IAM principle. Exam scenarios often have overly permissive roles - identify and recommend minimal roles.

---

## Cloud IAM - Least Privilege via Environment Separation

### Strategy
Separate environments (dev, staging, prod) into different projects/folders with distinct IAM policies.

**Benefits**:
- **Risk isolation**: Mistakes in dev don't affect prod
- **Granular control**: Different permissions per environment
- **Compliance**: Stricter controls for production
- **Auditability**: Clear separation of duties

**Implementation**:
```
Organization
  └── Folder: Development
      └── Project: dev-app-1 (developers have Editor)
  └── Folder: Production
      └── Project: prod-app-1 (developers have Viewer only)
```

**Access Patterns**:
- **Dev**: Developers have `Editor` role
- **Staging**: Developers have limited write access
- **Prod**: Developers have `Viewer` only; changes via CI/CD

**Exam Tip**: Environment separation (different projects) is a best practice for least privilege and blast radius reduction.

---

## Cloud IAM - Groups

### Overview
Google Groups allow batch IAM management by assigning roles to groups instead of individual users.

**Benefits**:
- **Scalability**: Add/remove users from group (not each resource)
- **Consistency**: Ensure all team members have same access
- **Auditability**: Clear group membership tracking
- **Flexibility**: Nest groups for complex org structures

### Best Practices

**1. Use groups for all user access** (never grant roles to individual users)

**2. Naming convention**: `gcp-[environment]-[role]@example.com`
   - `gcp-prod-viewers@example.com`
   - `gcp-dev-editors@example.com`

**3. Synchronize with corporate directory** (Google Workspace, Cloud Identity)

**4. Regular review**: Audit group membership quarterly

**Example**:
```bash
# Grant role to group (not individual users)
gcloud projects add-iam-policy-binding PROJECT_ID \
  --member="group:data-engineers@example.com" \
  --role="roles/bigquery.dataEditor"
```

**Exam Tip**: Always recommend groups over individual user grants for scalability and maintainability.

---

## Cloud IAM - IAM Conditions

### Overview
IAM Conditions allow **conditional access based on attributes** (time, IP, resource type, etc.).

**Format**: Common Expression Language (CEL)

### Condition Attributes

**1. Date/Time**
```
request.time < timestamp("2024-12-31T23:59:59Z")
```

**2. Resource Attributes**
```
resource.name.startsWith("projects/_/buckets/prod-")
```

**3. Request Attributes**
```
resource.service == "compute.googleapis.com"
```

**4. Principal Attributes**
```
principal.email.endsWith("@example.com")
```

### Use Cases

**Temporary Access**:
```
Grant role only until specific date:
request.time < timestamp("2024-06-01T00:00:00Z")
```

**IP-Based Access**:
```
Grant access only from corporate network:
origin.ip in ["203.0.113.0/24"]
```

**Resource-Specific Access**:
```
Grant access only to production resources:
resource.name.startsWith("projects/_/buckets/prod-")
```

**Time-of-Day Restrictions**:
```
Grant access only during business hours:
request.time.getHours("America/New_York") >= 9 &&
request.time.getHours("America/New_York") < 17
```

**Exam Tip**: IAM Conditions enable fine-grained, contextual access control beyond standard role bindings.

---

## Cloud IAM - Federated Authentication

### Overview
Identity federation allows external identities (AWS, Azure AD, GitHub, Okta, etc.) to access GCP resources **without creating corresponding Google identities**.

### Workload Identity Federation

**Purpose**: Eliminate service account keys for external workloads

**How It Works**:
1. External workload authenticates with its own IdP (AWS, Azure, GitHub, etc.)
2. Receives credential/token from IdP
3. Exchanges token with GCP Security Token Service (STS)
4. Receives short-lived GCP access token
5. Accesses GCP resources

**Components**:
- **Workload Identity Pool**: Container for external identities
- **Workload Identity Provider**: Bridge to external IdP (AWS, Azure AD, OIDC, SAML)
- **Attribute Mapping**: Map external claims to GCP attributes
- **Attribute Conditions**: Filter which external identities can access GCP

**Supported Identity Providers**:
- AWS
- Azure AD (Microsoft Entra ID)
- OIDC providers (GitHub, GitLab, Okta,Terraform Cloud, etc.)
- SAML providers
- Kubernetes (GKE Workload Identity)

**Access Methods**:
1. **Direct Resource Access**: External identity → GCP resource directly
2. **Service Account Impersonation**: External identity → Service Account → GCP resource (more common)

**Example Use Case**: GitHub Actions authenticating to GCP without service account keys

**Benefits**:
- **No long-lived keys**: Eliminates key management burden
- **Auditability**: Logs show external identity (not just service account)
- **Least privilege**: Fine-grained control via attribute conditions
- **Security**: Short-lived tokens, automatic rotation

**Exam Tip**: Workload Identity Federation is the secure, keyless way to authenticate external workloads (CI/CD, multi-cloud, on-prem). Always prefer it over service account keys.

---

## Cloud IAM - gcloud Commands

### Common IAM Commands

**View IAM Policy**:
```bash
# Project level
gcloud projects get-iam-policy PROJECT_ID

# Service account level
gcloud iam service-accounts get-iam-policy SA_EMAIL
```

**Add IAM Binding**:
```bash
gcloud projects add-iam-policy-binding PROJECT_ID \
  --member="user:alice@example.com" \
  --role="roles/viewer"
```

**Remove IAM Binding**:
```bash
gcloud projects remove-iam-policy-binding PROJECT_ID \
  --member="user:alice@example.com" \
  --role="roles/viewer"
```

**Create Service Account**:
```bash
gcloud iam service-accounts create SA_NAME \
  --display-name="My Service Account"
```

**Create Service Account Key** (avoid if possible):
```bash
gcloud iam service-accounts keys create key.json \
  --iam-account=SA_EMAIL
```

**List Service Accounts**:
```bash
gcloud iam service-accounts list
```

**Impersonate Service Account**:
```bash
gcloud compute instances list \
  --impersonate-service-account=SA_EMAIL
```

**Create Custom Role**:
```bash
gcloud iam roles create ROLE_ID \
  --project=PROJECT_ID \
  --file=role-definition.yaml
```

---

## Exam Focus Areas

### Critical Concepts

1. **IAM Components**: Principal (who) + Role (what) + Resource (which) = Policy

2. **Role Types**:
   - **Basic**: Legacy, too broad, avoid
   - **Predefined**: Use first
   - **Custom**: Use when predefined insufficient

3. **Service Accounts**:
   - Authentication for applications, not users
   - As principal: Gets IAM roles to access resources
   - As resource: Users can impersonate/manage
   - **Keys are security risks** - use alternatives

4. **Alternatives to SA Keys** (priority order):
   - Attached service accounts (GCP resources)
   - Workload Identity Federation (external workloads)
   - Service account impersonation (temporary access)
   - Service account keys (last resort)

5. **Least Privilege**:
   - Grant minimum necessary permissions
   - Use groups, not individual users
   - Separate environments (dev/prod)
   - Use role recommendations
   - Implement IAM Conditions

6. **Policy Inheritance**:
   - Flows down hierarchy (org → folder → project → resource)
   - Child cannot reduce parent grant (can only add or restrict via deny policies)
   - Use for broad grants (e.g., entire folder)

7. **IAM Conditions**:
   - Contextual access (time, IP, resource attributes)
   - Uses CEL expressions
   - Adds fine-grained control beyond roles

8. **Workload Identity Federation**:
   - Keyless authentication for external workloads
   - Eliminates service account key management
   - Supports AWS, Azure, OIDC, SAML
   - **Always prefer over service account keys**

### Common Exam Scenarios

- **Scenario**: Application on AWS needs GCP access
  - **Solution**: Workload Identity Federation with AWS provider (not service account keys)

- **Scenario**: Developer needs temp elevated access for incident
  - **Solution**: Service account impersonation (not permanent role grant)

- **Scenario**: Grant access to all team members efficiently
  - **Solution**: Use Google Group with IAM role binding (not individual grants)

- **Scenario**: Restrict access to production resources during business hours only
  - **Solution**: IAM Condition with time-based CEL expression

- **Scenario**: Minimize blast radius if credentials compromised
  - **Solution**: Least privilege + separate projects + avoid service account keys

- **Scenario**: Service account keys were leaked to GitHub
  - **Solution**: Immediately disable/delete key, rotate, audit access logs, investigate

---

## Related Services

- **Secret Manager**: Secure storage for service account keys (if must use)
- **Cloud Identity**: User/group management without Google Workspace
- **Cloud Asset Inventory**: Track IAM policies across organization
- **Policy Analyzer**: Understand who has access to what
- **IAM Recommender**: ML-based suggestions for permission removal
- **Access Approval**: Require admin approval for Google support access
- **VPC Service Controls**: Perimeter-based data exfiltration protection
