# Cloud Storage - Comprehensive Guide

## Overview
Object storage service (unlimited capacity, global accessibility).
- **Objects**: Immutable data. Puts/Gets.
- **Buckets**: Containers for objects. Global namespace.
- **Consistency**: **Strong global consistency** for all operations (including list-after-write).

---

## Storage Classes (Exam Critical)

| Class | Use Case | Availability | Min Duration | Access Fee |
| :--- | :--- | :--- | :--- | :--- |
| **Standard** | "Hot" data, frequently accessed (Websites, Streaming). | 99.99% (Multi-region) | None | None |
| **Nearline** | Accessed once a month (Backups, Long-tail content). | 99.9% | 30 days | Yes (Low) |
| **Coldline** | Accessed once a quarter (Disaster Recovery). | 99.9% | 90 days | Yes (Med) |
| **Archive** | Accessed once a year (Regulatory archive, Tape replacement). | 99.9% | 365 days | Yes (High) |

**Autoclass**:
- Automatically transitions objects between classes based on access patterns.
- Simplifies management but incurs a management fee. Good for unpredictable workloads.

---

## Lifecycle Management
Rules to automate actions on objects.
- **Conditions**: Age, CreatedBefore, IsLive, NumNewerVersions, MatchesStorageClass.
- **Actions**:
  - **SetStorageClass**: Move from Standard -> Nearline -> Archive.
  - **Delete**: Permanently delete (or move to Soft Delete).
  - **AbortIncompleteMultipartUpload**: Clean up failed uploads.

---

## Security & Access Control

### 1. IAM
- **Uniform Bucket-Level Access**: Recommended. Apply IAM roles (Storage Object Viewer/Admin) at the bucket level. Disables ACLs.
- **ACLs (Legacy)**: Fine-grained per-object access. Avoid unless strictly necessary.

### 2. Signed URLs
- Grant time-limited access to a specific object for a user **without a Google Account**.
- **Use Case**: "Allow user to upload their avatar directly to GCS".
- **Operation**: Generate URL with your Service Account key. User PUTs to that URL.

### 3. Bucket Lock (Retention Policy)
- **Compliance WORM** (Write Once, Read Many).
- **Retention Period**: Objects cannot be deleted/overwritten until age > Retention Period.
- **Lock**: Once locked, the policy cannot be removed or reduced (only extended). Critical for legal holds/SEC compliance.

### 4. Encryption
- **Google-Managed (Default)**: Always on.
- **CMEK (Customer-Managed)**: You manage Key in Cloud KMS.
- **CSEK (Customer-Supplied)**: You keep the key, send it with every API call. Google never sees the key.

---

## Object Versioning
- Keeps history of object overwrites/deletes.
- **Use Case**: Protection against accidental deletion.
- **Cost**: You pay for storage of *every* version.
- **Best Practice**: Pair with Lifecycle Policy to delete non-current versions after X days.

---

## Exam Focus Areas

1.  **Class Selection**:
    - **Scenario**: "Data accessed for 1 week, then never again". -> **Standard** (no retrieval fee, no min duration penalty).
    - **Scenario**: "Compliance data retrievable within milliseconds, stored for 5 years". -> **Archive** (lowest storage cost, instant access time - unlike AWS Glacier Deep Archive which takes hours).

2.  **Uploads**:
    - **Scenario**: "Upload 500GB file". -> **Resumable Upload**.
    - **Scenario**: "Upload massive number of small files". -> **Parallel Composite Upload**.

3.  **Data Consistency**:
    - Cloud Storage provides **Strong Global Consistency**. If you upload a file and immediately `LIST` the bucket, you will see it (unlike eventual consistency systems).

4.  **Directory Structure**:
    - "Flat namespace". Folders are simulated by logic (slashes in filenames).
    - Renaming a "folder" is expensive (copy + delete of all objects).
