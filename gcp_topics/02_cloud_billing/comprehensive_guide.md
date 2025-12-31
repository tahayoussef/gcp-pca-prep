# Cloud Billing - Comprehensive Guide

## Cloud Billing - Introduction

### Overview
Cloud Billing is Google Cloud's cost tracking and payment system that:
- Defines **who pays** for GCP resources
- Tracks usage costs across all linked projects
- Manages payment methods and billing information
- Enables cost analysis, budgets, and alerts

### Cloud Billing Account

**Definition**: A Google Cloud resource that tracks all costs incurred by GCP usage in projects linked to it.

**Key Characteristics**:
- Managed in Google Cloud Console
- Connected to a **Google Payments Profile** (payment instrument)
- Operates in a **single currency** (cannot mix currencies)
- Generates a **single invoice** per billing account (except with split invoicing)
- Projects can only be linked to **one billing account at a time**
- Multiple projects can share the same billing account

**Billing Account Types**:
1. **Self-serve**: Online signup, credit card payment, invoiced monthly
2. **Invoiced**: Billed monthly or annually, payment by check/wire transfer, requires credit check

### Google Payments Profile

**Definition**: Google-level resource (not GCP-specific) that processes payments across all Google services.

**Key Characteristics**:
- Managed at payments.google.com
- Handles payments for all Google products (Ads, Cloud, Fi, etc.)
- Stores payment instruments (credit cards, debit cards, bank accounts)
- Contains billing contact information (name, address, tax ID)
- Functions as document center for invoices and payment history

**Relationship to Cloud Billing**:
```
Google Payments Profile
    └── Cloud Billing Account(s)
            └── Project(s)
                    └── Resources (charged to billing account)
```

**Exam Tip**: Understand the separation - Payments Profile is Google-wide; Billing Account is GCP-specific. One payments profile can have multiple billing accounts.

---

## Cloud Billing - Exports

### Overview
Billing data export enables automated export of detailed cost and usage data to:
- **BigQuery**: For SQL analysis and custom reporting
- **Cloud Storage (JSON)**: For custom processing
- **File export**: CSV download for spreadsheet analysis

### BigQuery Export

**Purpose**: Export granular billing data to BigQuery for detailed cost analysis

**What's Exported**:
- **Standard Usage Cost Data**: Detailed usage, costs, credits, and taxes
- **Detailed Usage Cost Data**: Even more granular (includes SKU-level pricing)
- **Pricing Data**: List prices for all GCP services
- **Cost breakdown by**: Project, service, SKU, location, labels, and more

**Setup**:
1. Create a BigQuery dataset (for billing export)
2. Enable billing export in Cloud Billing settings
3. Specify the target dataset
4. Data begins exporting automatically (throughout the day)

**Key Features**:
- Data updates **multiple times per day** (near real-time)
- Historical data from export enablement forward (not retroactive)
- Supports **cost attribution** using labels and tags
- Enables complex SQL queries for custom analysis

**Timing Recommendation**: Enable export **when creating billing account** to capture complete cost history

**Common Use Cases**:
- Chargeback/showback models (allocating costs to teams)
- Custom cost dashboards (Looker Studio, Data Studio)
- Anomaly detection and cost forecasting
- Granular cost optimization analysis

### Limitations
- Export is **not retroactive** - only captures data from enablement forward
- Slight delay between resource usage and data availability in BigQuery
- BigQuery storage and query costs apply (minimal for most use cases)

**Exam Tip**: BigQuery export is the primary method for detailed cost analysis. Enable early to capture full cost history. Use Standard export for most cases; Detailed for SKU-level analysis.

---

## Cloud Billing - Resource Labels

### Overview
Labels are **key-value pairs** attached to GCP resources to categorize and track costs at a granular level.

### Key Concepts

**Label Structure**:
- **Key**: Descriptor (e.g., `environment`, `team`, `cost-center`)
- **Value**: Specific value (e.g., `production`, `data-eng`, `eng-001`)
- Format: Lowercase letters, numbers, hyphens, underscores
- Example: `environment:production`, `team:data-engineering`

**Label vs. Tag**:
- **Labels**: User-defined key-value pairs for organization and billing
- **Tags**: Network tags (for firewall rules) or resource tags (for conditional IAM/org policies)
- **Don't confuse**: Labels are for cost tracking; tags are for access/network control

### Use Cases

**1. Cost Allocation**
- Attribute costs to teams, departments, or projects
- Enable chargeback/showback models
- Example: `cost-center:engineering`, `cost-center:marketing`

**2. Environment Separation**
- Identify development vs. production resources
- Example: `environment:dev`, `environment:prod`, `environment:staging`

**3. Application/Owner Tracking**
- Track resources by application or owner
- Example: `application:web-app`, `owner:john-doe`

**4. Compliance and Governance**
- Identify regulated workloads
- Example: `compliance:pci-dss`, `data-classification:confidential`

### Cost Analysis with Labels

**In BigQuery Billing Export**:
- Labels appear as `labels` column (array of key-value pairs)
- Query costs grouped by labels:
  ```sql
  SELECT
    labels.value AS team,
    SUM(cost) AS total_cost
  FROM `project.dataset.gcp_billing_export`
  CROSS JOIN UNNEST(labels) AS labels
  WHERE labels.key = 'team'
  GROUP BY team
  ORDER BY total_cost DESC
  ```

**In Cloud Console**:
- Filter billing reports by labels
- Create custom cost breakdowns by label values
- Set budget alerts based on label-filtered costs

### Best Practices

1. **Establish naming conventions** early (consistent key names)
2. **Mandatory labels** for critical resources (environment, team, cost-center)
3. **Automate label application** via Terraform, Deployment Manager, or org policies
4. **Audit label coverage** - ensure resources are properly labeled
5. **Limit label keys** - too many keys create confusion (10-15 standard keys recommended)

**Supported Resources**:
- Compute Engine (VMs, disks, images)
- GKE clusters and node pools
- Cloud Storage buckets
- BigQuery datasets and tables
- Pub/Sub topics and subscriptions
- Most GCP services (check service documentation)

**Exam Tip**: Labels enable granular cost tracking and allocation. They're forwarded to billing data automatically. Remember they're different from network tags and resource tags used for access control.

---

## Cloud Billing - Billing Account Access

### Overview
Cloud Billing uses **IAM roles** to control who can view and manage billing accounts and which projects can be linked to billing accounts.

### Cloud Billing IAM Roles

#### 1. Billing Account Creator (`roles/billing.creator`)
**Granted at**: Organization level
**Permissions**:
- Create new billing accounts

**Use Case**: Allow users to create new billing accounts (typically limited to finance/admin)

**Note**: This role does NOT grant access to existing billing accounts

---

#### 2. Billing Account Administrator (`roles/billing.admin`)
**Granted at**: Billing account
**Permissions**:
- View and manage all aspects of billing accounts
- Link/unlink projects to billing account
- Manage billing account IAM policies
- View and export cost data
- Update payment information
- Close/reopen billing accounts
- Set up budget alerts

**Use Case**: Full billing management (typically finance team)

**Critical Note**: This is the most powerful billing role

---

#### 3. Billing Account User (`roles/billing.user`)
**Granted at**: Billing account
**Permissions**:
- **Link projects** to the billing account
- View billing account details (but NOT cost data)

**Does NOT Grant**:
- View cost/usage data
- Manage billing account settings
- Update payment information

**Use Case**: Combined with `Project Creator` role to enable delegated project creation

**Common Pattern**:
```
User has:
- roles/billing.user (on billing account)
- roles/resourcemanager.projectCreator (at org/folder level)

Result: User can create projects AND link them to billing account
```

**Exam Tip**: This is a **key exam concept**. Billing Account User + Project Creator = delegated project creation with billing.

---

#### 4. Billing Account Viewer (`roles/billing.viewer`)
**Granted at**: Billing account
**Permissions**:
- View billing account details
- View all cost and usage data
- View payment information (read-only)

**Does NOT Grant**:
- Link/unlink projects
- Modify billing settings
- Update payment information

**Use Case**: Finance team members who need to view costs but not make changes, auditors

---

#### 5. Billing Account Costs Manager (`roles/billing.costsManager`)
**Granted at**: Billing account
**Permissions**:
- View and manage cost-related features:
  - Budget alerts
  - Billing exports
  - Cost analysis and reporting
- Does NOT include project linking or payment management

**Use Case**: Cost engineers, FinOps teams who manage budgets and cost tracking

---

#### 6. Project Billing Manager (`roles/billing.projectManager`)
**Granted at**: Project level
**Permissions**:
- Link/unlink the project to/from a billing account
- View billing information for the project

**Use Case**: Project owners who need to manage billing for their specific project only

---

#### 7. Project Billing Costs Manager (`roles/billing.projectCostsManager`)
**Granted at**: Project level
**Permissions**:
- View cost information **for the project only**
- Set up project-level budgets

**Does NOT Grant**:
- View costs for other projects
- Access billing account settings

**Use Case**: Project teams who need visibility into their project costs

---

### Access Control Patterns

**1. Centralized Billing Management**
```
Finance Team → roles/billing.admin (on billing account)
```

**2. Delegated Project Creation**
```
Developers → roles/billing.user (on billing account)
             + roles/resourcemanager.projectCreator (at org level)
```

**3. Cost Visibility for Project Teams**
```
Project Team → roles/billing.projectCostsManager (on project)
```

**4. Read-Only Auditing**
```
Auditors → roles/billing.viewer (on billing account)
```

### Separation of Concerns

**Key Principle**: Separate **billing management** from **project management**

| Need | Required Roles |
|------|---------------|
| Create projects with billing | `billing.user` + `projectCreator` |
| Manage existing billing account | `billing.admin` |
| View all costs | `billing.viewer` |
| Create billing accounts | `billing.creator` (org level) |
| View project costs only | `billing.projectCostsManager` (project level) |

**Exam Tip**: Understand the difference between billing account-level and project-level roles. `billing.user` is commonly combined with `projectCreator` for delegated project creation - this is a frequent exam scenario.

---

## Exam Focus Areas

### Critical Concepts to Remember

1. **Billing Account Characteristics**:
   - Single currency per billing account
   - Connected to Google Payments Profile
   - One billing account per project
   - Multiple projects per billing account

2. **Billing Exports**:
   - **BigQuery**: Primary method for detailed cost analysis
   - Enable early (not retroactive)
   - Near real-time updates throughout the day
   - Standard vs. Detailed usage exports

3. **Resource Labels**:
   - Key-value pairs (not tags)
   - Enable granular cost tracking
   - Appear in billing export data
   - Use for chargeback/showback models

4. **IAM Roles Matrix**:

   | Role | View Costs | Link Projects | Manage Billing | Create Billing Account |
   |------|------------|---------------|----------------|----------------------|
   | `billing.admin` | ✓ | ✓ | ✓ | ✗ |
   | `billing.user` | ✗ | ✓ | ✗ | ✗ |
   | `billing.viewer` | ✓ | ✗ | ✗ | ✗ |
   | `billing.creator` | ✗ | ✗ | ✗ | ✓ (org level) |
   | `billing.costsManager` | ✓ | ✗ | Partial (budgets) | ✗ |
   | `billing.projectManager` | ✓ (project) | ✓ (project) | ✗ | ✗ |

5. **Delegated Project Creation**:
   ```
   Grant users:
   - roles/billing.user (on billing account)
   - roles/resourcemanager.projectCreator (at org/folder)
   
   Result: Users can create projects and link to billing
   ```

### Common Exam Scenarios

- **Scenario**: Enable detailed cost analysis for FinOps team
  - **Solution**: Set up BigQuery billing export, grant `billing.costsManager` or `billing.viewer`

- **Scenario**: Allow developers to create projects without full billing access
  - **Solution**: Grant `billing.user` + `projectCreator` roles

- **Scenario**: Track costs by team for chargeback
  - **Solution**: Use resource labels (e.g., `team:data`, `team:web`) and query BigQuery export

- **Scenario**: Prevent a project from accruing costs
  - **Solution**: Unlink project from billing account (project remains, but chargeable services stop)

- **Scenario**: Audit all billing costs without modification ability
  - **Solution**: Grant `roles/billing.viewer` to auditors

- **Scenario**: Department manager needs to see costs for their projects only
  - **Solution**: Grant `roles/billing.projectCostsManager` on their projects

---

## Related Services

- **Cloud Billing Budget API**: Create programmatic budget alerts
- **Recommender API**: Cost optimization recommendations
- **Cloud Asset Inventory**: Track resource metadata including labels
- **Looker Studio**: Visualize billing data from BigQuery export
- **Cost Management Tools**: Billing Reports, Cost Table, Cost Breakdown
