# Scalable BigQuery Backup Automation

## Overview
Automated backup solution for **BigQuery** tables using **snapshots** or **Cloud Storage exports** at scale.

## Backup Methods

### 1. BigQuery Table Snapshots
*   **Native Feature**: Built-in BigQuery table snapshots.
*   **Pros**: Fast, incremental, no data movement.
*   **Cons**: 7-day retention limit; same region only.

### 2. Export to Cloud Storage
*   **Export**: Export table to Avro/Parquet/CSV files in Cloud Storage.
*   **Pros**: Long-term retention, cross-region backups, cost-effective storage.
*   **Cons**: Slower restore, requires re-import.

## Architecture
*   **Cloud Scheduler**: Triggers backup jobs on schedule.
*   **Cloud Functions** or **Workflows**: Orchestrates backup operations.
*   **BigQuery API**: Creates snapshots or exports.
*   **Cloud Storage**: Stores exported data.
*   **Metadata Tracking**: Firestore/BigQuery table to track backups.

## Backup Policies
*   **Tag-Based**: Tag tables with backup policy (daily, weekly, monthly).
*   **Automated Discovery**: Scan BigQuery datasets for tables matching criteria.
*   **Retention**: Automatically delete old backups based on retention policy.

## Design Considerations
*   **Security**: Encrypt exports with CMEK; restrict access to backups.
*   **Reliability**: Retry logic for failed backups.
*   **Cost**: Snapshots cheaper for short-term; exports cheaper for long-term.
*   **Performance**: Parallel backups for large datasets.

## Restore Process
*   **Snapshots**: Restore via BigQuery console/API (fast).
*   **Exports**: Load from Cloud Storage back into BigQuery.
