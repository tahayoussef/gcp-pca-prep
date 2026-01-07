# Sensitive Data Protection (DLP)

Sensitive Data Protection (formerly Cloud DLP) helps you discover, classify, and protect sensitive data (PII) at scale.

## Transformation Types
-   **`recordTransformations`**: Used for structured/tabular data. Applies the same transformation to an entire field/column (e.g., hashing an SSN column). Most cost-effective when the data type is already known.
-   **`infoTypeTransformations`**: Used for unstructured text. Inspects the text to find sensitive data (infoTypes) and transforms only the findings (e.g., finding an SSN within a sentence and redacting it).

## De-identification Methods
-   **Redaction**: Deletes the sensitive value entirely.
-   **Masking**: Replaces the value with fixed characters (e.g., `####`).
-   **One-way Tokenization (Hashing)**: Replaces data with a secure hash (HMAC-SHA-256). Deterministic but non-reversible; useful for joining datasets without exposing values.
-   **Two-way Tokenization (Encryption)**: Reversible encryption that preserves referential integrity.
    -   **Deterministic Encryption (DE)**: Replaces data with a base64-encoded encrypted string. Does NOT preserve length/character set. Preferred for security.
    -   **Format-Preserving Encryption (FPE-FFX)**: Preserves the original character set and length. Essential for **legacy system compatibility**.

## Re-identification
Authorized users can reverse two-way tokenization (re-identify) using the same encryption keys (Cloud KMS) and templates used during de-identification.
