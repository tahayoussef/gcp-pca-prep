# GCP Fundamentals - Comprehensive Guide

## Accessing GCP - Console, SDK, and APIs

### Three Ways to Interact with GCP

1. **Google Cloud Console**
   - Web-based graphical user interface
   - Access at console.cloud.google.com
   - Provides visual management of all GCP resources
   - Best for: Exploration, quick configurations, visual monitoring

2. **Command-Line Interface (gcloud CLI)**
   - Part of the Google Cloud SDK
   - Programmatic access from local terminal
   - Supports scripting and automation
   - Best for: Automation, DevOps workflows, batch operations

3. **RESTful APIs and Client Libraries**
   - Programmatic access from applications
   - Available for multiple programming languages (Python, Java, Go, Node.js, etc.)
   - Best for: Application integration, custom tooling

**Exam Tip**: Know when to recommend each interface - console for learning/exploration, gcloud for automation, APIs for application integration.

---

## Google Cloud SDK and gcloud

### Overview
- **gcloud CLI**: Primary command-line tool for managing GCP resources
- Current version evolves regularly (check with `gcloud version`)
- Installed automatically in Cloud Shell; requires download for local use

### Key Features

**Installation & Authentication**
```bash
# Initialize SDK and authenticate
gcloud init

# Set default project
gcloud config set project PROJECT_ID

# Authenticate with service account
gcloud auth activate-service-account --key-file=KEY_FILE
```

**Release Levels**
- **GA (General Availability)**: Production-ready, stable commands
- **Beta**: Preview features with most functionality complete
- **Alpha**: Experimental features, may change or be removed

```bash
# Install alpha and beta components
gcloud components install alpha beta

# Use beta command
gcloud beta compute instances create ...
```

**Command Structure**
```
gcloud <component> <entity> <operation> [options]
```

Examples:
- `gcloud compute instances list`
- `gcloud sql databases create ...`
- `gcloud container clusters create ...`

### Properties and Configuration
- Properties control gcloud behavior (default region, project, etc.)
- Managed via `gcloud config` command
- Can be set globally or per-configuration profile

```bash
# Set compute region
gcloud config set compute/region us-central1

# Create named configuration
gcloud config configurations create dev-config
```

**Exam Tip**: Remember the three release levels and their stability guarantees. Alpha/Beta components require explicit installation.

---

## Cloud Shell

### Overview
- Free, browser-based terminal with pre-configured development environment
- Ephemeral VM instance (5 GB persistent disk storage in `$HOME`)
- No installation required - accessible from Google Cloud Console
- Pre-installed tools: gcloud, kubectl, terraform, docker, git, and more

### Key Characteristics

**Persistent Disk Storage**
- 5 GB persistent storage in `$HOME` directory
- Survives session termination
- Files persist across sessions
- **Important**: VM instance itself is ephemeral (recreated each session)

**Authorization**
- Automatically authenticated with your Google account
- No need to run `gcloud auth login`
- Inherits permissions from your user account

**Environment**
- Debian-based environment
- Pre-configured environment variables (PROJECT_ID, etc.)
- Automatic zone selection (closest to your location)
- Editor built-in (Cloud Shell Editor - web-based IDE)

**Session Limits**
- Sessions timeout after ~20 minutes of inactivity
- Weekly usage limits apply (to prevent abuse)
- Sessions run while web interface is active

**Safe Mode**
- Boots Cloud Shell without executing startup scripts
- Used for troubleshooting problematic startup configurations

**Exam Tip**: Cloud Shell is ideal for quick tasks, learning, and scenarios where you don't have local tools installed. Remember the 5 GB persistent `$HOME` limitation.

---

## GCP Resource Hierarchy

### Overview
Google Cloud resources are organized in a hierarchical structure that provides:
- **Logical grouping** of resources
- **Inheritance of access policies** (IAM) and organization policies
- **Centralized billing** and management

### Hierarchy Levels (Top to Bottom)

```
Organization
    └── Folder(s)
            └── Project(s)
                    └── Resources (VMs, disks, buckets, etc.)
```

### 1. Organization Resource (Root Level)

**Overview**
- Represents a company/organization
- Root node of the GCP resource hierarchy
- **Requires**: Google Workspace or Cloud Identity account
- One organization per Workspace/Cloud Identity domain

**Key Characteristics**
- Automatically provisioned when a Workspace/Cloud Identity user creates a project
- All projects created by domain users belong to the organization
- Policies set at organization level apply to all descended resources
- **Free tier** users cannot create an organization resource

**Benefits**
- Central visibility and control over all resources
- Organization-wide IAM roles
- Organization-level billing
- Centralized audit logging

### 2. Folder Resource (Optional)

**Overview**
- Additional grouping mechanism between organization and projects
- **Requires**: Organization resource must exist first
- Can contain projects and other folders (nested structure)

**Use Cases**
- Map to departments, teams, or environments
- Example: `Production`, `Development`, `Team-A`, `Team-B`
- Isolate resources with different compliance requirements
- Apply policies to groups of projects

**Key Characteristics**
- Folders can be nested (sub-folders within folders)
- IAM policies and organization policies inherit down the hierarchy
- Useful for large organizations with multiple teams/departments

### 3. Project Resource

**Overview**
- **Fundamental organizing entity** in GCP
- All resources must belong to a project
- Serves as a namespace (resource names unique within project)

**Project Identifiers**
- **Project Name**: Human-readable, user-provided (changeable)
- **Project ID**: Globally unique, user-provided or auto-generated (immutable after creation)
- **Project Number**: Automatically assigned by GCP (immutable)

**Key Characteristics**
- Projects cannot access other projects' resources by default
  - Exception: Shared VPC and VPC Peering
- Each project associates with **one billing account**
- Multiple projects can share the same billing account
- Project ID is permanent - deletion doesn't free the ID for reuse

**Resource Scope**
- Resources within a project can communicate easily (same internal network)
- Subject to regional/zonal restrictions
- Project serves as default context for gcloud commands

**Exam Tip**: Understand project vs. project ID vs. project number distinction. Remember that deleted project IDs cannot be reused.

---

## Project Name, ID, and Number

### Detailed Breakdown

| Identifier | Description | Mutability | Uniqueness | Example |
|------------|-------------|------------|------------|---------|
| **Project Name** | Human-friendly display name | Changeable | No (can duplicate) | "My Production App" |
| **Project ID** | Permanent unique identifier | **Immutable** after creation | Global (across all GCP) | `my-prod-app-123456` |
| **Project Number** | Auto-generated numeric ID | Immutable | Global | `123456789012` |

### When to Use Each

- **Project Name**: Display in UI, human communication
- **Project ID**: gcloud commands, API calls, resource URIs, configurations
- **Project Number**: Service accounts, internal GCP references, some API calls

```bash
# Get project details
gcloud projects describe PROJECT_ID

# List all projects
gcloud projects list
```

**Exam Tip**: Project ID is immutable and globally unique. Once a project is deleted, its ID can never be reused - plan IDs carefully.

---

## Governance and Compliance with Organization Policies

### Overview
- **Organization Policy Service**: Centralized control over organization's cloud resources
- Complements IAM (controls **who** can do things; org policies control **what** can be done)
- Applied at organization, folder, or project level

### Key Concepts

**1. Constraints**
- Define restrictions on resource configuration
- Two types:
  - **List constraints**: Allow or deny specific values (e.g., allowed regions)
  - **Boolean constraints**: Enforce or don't enforce a behavior (e.g., require OS Login)

**2. Policies**
- Apply constraints to resources
- Inherit down the hierarchy (organization → folder → project)
- Can be overridden at lower levels (if parent allows)

**3. Common Use Cases**
- **Restrict resource locations**: Enforce data residency (e.g., EU only)
- **Disable service usage**: Prevent specific APIs from being enabled
- **Require uniform access controls**: Enforce uniform bucket-level access for Cloud Storage
- **VM restrictions**: Require shielded VMs, disable serial port access
- **Domain restrictions**: Limit resource sharing to specific domains

### Managed Constraints
- Pre-defined by Google
- Cover common compliance scenarios
- Examples:
  - `constraints/compute.vmExternalIpAccess`: Control external IPs on VMs
  - `constraints/gcp.resourceLocations`: Restrict resource regions
  - `constraints/iam.allowedPolicyMemberDomains`: Limit IAM member domains

### Custom Constraints
- Define your own constraints using Common Expression Language (CEL)
- Greater flexibility for organization-specific requirements

### Dry-Run Mode
- Test policies before enforcement
- See what would be blocked without actually blocking it
- Critical for validating policies before production rollout

### Conditional Organization Policies
- Apply policies based on conditions (e.g., resource tags, time of day)
- Use CEL expressions for complex logic

### Inheritance and Hierarchy
- Policies inherit from parent to child
- Child policy can be **more restrictive** than parent
- If parent **denies** something, child typically cannot override
- **Merge**: List constraints combine (union or intersection based on policy)

**Exam Tip**: Org policies control **what resources can be configured**, while IAM controls **who can configure them**. Both are needed for comprehensive governance.

---

## Organization-Level Roles

### Overview
- IAM roles granted at the organization level
- Apply to all resources within the organization
- Used for centralized administration and governance

### Common Organization-Level Roles

**1. Organization Admin (`roles/resourcemanager.organizationAdmin`)**
- Full control over the organization resource
- Can set organization policies
- Can grant IAM roles to others
- **Does NOT** have automatic access to all projects (separation of duties)
- Typically assigned to small group of trusted administrators

**2. Organization Policy Administrator (`roles/orgpolicy.policyAdmin`)**
- Create, update, delete organization policies
- Does not grant rights to other resources
- Focused solely on policy management

**3. Organization Viewer (`roles/resourcemanager.organizationViewer`)**
- Read-only access to organization structure
- View organization, folders, and projects (but not resources within)
- Useful for auditors and read-only administrators

**4. Folder Admin (`roles/resourcemanager.folderAdmin`)**
- Full control over específic folder(s)
- Can create, update, delete folders
- Manage IAM policies on folders

**5. Folder Creator (`roles/resourcemanager.folderCreator`)**
- Permission to create folders
- Does not grant management rights to existing folders
- Often granted to team leads or department admins

**6. Project Creator (`roles/resourcemanager.projectCreator`)**
- Create new projects
- Automatically becomes owner of created projects
- Organization policy can restrict where projects can be created

**7. Billing Account Administrator (`roles/billing.admin`)**
- Manage billing accounts
- Link/unlink projects to billing accounts
- View billing data and set budgets

**8. Billing Account User (`roles/billing.user`)**
- Link projects to billing accounts
- Does not grant ability to view/manage billing data
- Typically combined with Project Creator for delegated project creation

**Key Principles**
- **Separation of Duties**: Organization Admin ≠ automatic project access
- **Least Privilege**: Grant narrowest roles needed
- **Inheritance**: Roles at organization level apply to all descended resources
- **Groups**: Assign roles to groups, not individual users (easier management)

**Exam Tip**: Organization Admin does NOT automatically grant access to all resources - it's for managing the organization structure and policies, not resources. Billing Account User + Project Creator allows delegated project creation.

---

## Exam Focus Areas

### Critical Concepts to Remember

1. **Three access methods**: Console (UI), gcloud (CLI), APIs (programmatic)

2. **gcloud release levels**: GA (stable), Beta (preview), Alpha (experimental)

3. **Cloud Shell characteristics**:
   - 5 GB persistent `$HOME`
   - Ephemeral VM
   - Pre-authenticated
   - Pre-installed tools

4. **Resource Hierarchy**:
   ```
   Organization (requires Workspace/Cloud Identity)
       └── Folders (optional)
           └── Projects (required)
               └── Resources (VMs, buckets, etc.)
   ```

5. **Project Identifiers**:
   - Name: Changeable, not unique
   - ID: **Immutable**, globally unique, **cannot be reused**
   - Number: Auto-generated, immutable

6. **Organization Policies vs. IAM**:
   - Org Policies: **What** can be configured
   - IAM: **Who** can configure

7. **Policy Inheritance**: Flows down (org → folder → project → resource)

8. **Organization Admin**: Controls org structure, NOT automatic access to projects

9. **Free tier limitations**: Cannot create organization resource

10. **Billing**: One billing account per project, many projects per billing account

### Common Exam Scenarios

- **Scenario**: Company wants to ensure VMs only created in specific regions
  - **Solution**: Organization Policy with `constraints/gcp.resourceLocations`

- **Scenario**: Department leads need to create projects but not manage billing
  - **Solution**: Grant `roles/resourcemanager.projectCreator` + `roles/billing.user`

- **Scenario**: Need central visibility into all company resources
  - **Solution**: Set up Organization resource (requires Workspace/Cloud Identity)

- **Scenario**: Isolate teams but maintain central governance
  - **Solution**: Use folder structure with policies at organization/folder levels

- **Scenario**: Quick testing without local tool installation
  - **Solution**: Use Cloud Shell (5 GB persistent storage, pre-configured)

---

## Related GCP Services

- **Resource Manager API**: Programmatic management of organizations, folders, projects
- **Asset Inventory**: Track and query resource metadata across the hierarchy
- **Cloud Identity**: User/group management for organizations without Workspace
- **Cloud Billing API**: Programmatic billing management
- **IAM**: Access control (complements org policies)
