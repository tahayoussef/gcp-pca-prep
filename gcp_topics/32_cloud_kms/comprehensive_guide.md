# Cloud Key Management Service (KMS) - Comprehensive Guide

## Overview
Managed service for creating and managing cryptographic keys.
- **Location**: Global, Regional, or Multi-Region.
- **Hierarchy**: Project -> Location -> KeyRing -> Key -> KeyVersion.
- **Operations**: Encrypt, Decrypt, Sign.

---

## Encryption Types

### 1. Google-Managed Keys (Default)
- **Automatic**: Keys are owned and managed by Google.
- **Rotation**: Automatic.
- **Use Case**: General purpose storage (buckets, disks).

### 2. Customer-Managed Encryption Keys (CMEK)
- **Concept**: *You* create/manage the key in KMS, but *Google Services* (GCS, BigQuery, Compute Engine) use it to encrypt data.
- **Control**: You can disable/revoke the key to instantly lock out data access ("Crypto-shredding").
- **Rotation**: You define the rotation schedule.
- **Use Case**: Compliance "We must control the keys".

### 3. Customer-Supplied Encryption Keys (CSEK)
- **Concept**: You generate the raw key material on-premise and pass it to GCP in the API call.
- **Storage**: GCP *never* stores the key. It is used in RAM to decrypt/encrypt and then discarded.
- **Downside**: If you lose the key, the data is lost forever. Limited service support (Compute Engine Disks, GCS).
- **Use Case**: Extreme security ("GCP must never know the key").

### 4. Cloud External Key Manager (EKM)
- **Concept**: Keys are stored *outside* GCP (e.g., Thales, Fortanix). GCP calls out to external system to sign/unwrap.
- **Use Case**: Regulatory "Hold Your Own Key" (HYOK) where keys cannot sit in a cloud provider.

---

## Envelope Encryption (Exam Critical)
KMS does not encrypt large data (GBs) directly. It uses Envelope Encryption.
1.  **DEK (Data Encryption Key)**: Encrypts the actual data chunk. (Generated locally by service).
2.  **KEK (Key Encryption Key)**: The KMS Master Key. Encrypts the *DEK*.
3.  **Storage**: The encrypted data + the encrypted DEK (wrapped DEK) are stored together.
4.  **Decryption**: Service sends wrapped DEK to KMS -> KMS decrypts it with KEK -> Returns plaintext DEK -> Service decrypts data.

---

## Key Hierarchy
- **KeyRing**: Logical grouping of keys for IAM permissions. (e.g., "Finance-Keys").
- **Key**: The named resource (e.g., "Salary-DB-Key"). configuration (Rotation period).
- **KeyVersion**: The actual cryptographic material. (v1, v2, v3).

---

## Exam Focus Areas

1.  **Rotation**:
    - "Compliance requires rotation every 90 days". -> Configure **Automatic Rotation** on the Key.
    - **Note**: Rotation creates a new `Primary` version (v2). Old data encrypted with v1 can still be decrypted (KMS keeps v1 active for decryption). New data uses v2.

2.  **Permissions**:
    - Separation of Duties.
    - **Security Team**: `roles/cloudkms.admin` (Manage keys).
    - **Service Account**: `roles/cloudkms.cryptoKeyEncrypterDecrypter` (Use keys).
    - **Constraint**: `Organization Policy` can restrict which projects can use CMEK.

3.  **Location**:
    - KeyRing must be in the **same location** as the data (usually).
    - E.g., GCS bucket in `us-east1` needs KMS key in `us-east1`.
