# GCP Service Emulators - Comprehensive Guide

## Overview
**GCP Service Emulators** allow developers to run local versions of Google Cloud services. This enables **local development and testing** without needing internet access, authentication, or incurring costs.

## Key Emulators
Access via `gcloud beta emulators [service] start`.

1.  **Pub/Sub Emulator**: Simulate topics and subscriptions.
2.  **Firestore Emulator**: Simulate document database.
3.  **Datastore Emulator**: Simulate NoSQL database.
4.  **Bigtable Emulator**: Simulate wide-column store.
5.  **Spanner Emulator**: Simulate relational global database.

## Exam Focus Areas

1.  **Cost Optimization**:
    - "Developers are spending too much money spinning up Cloud Spanner instances for every unit test." -> Use **Spanner Emulator**.

2.  **Offline Development**:
    - "Team needs to work on the train/airplane without internet." -> Use **Local Emulators**.

3.  **CI/CD Speed**:
    - "Integration tests are slow because they wait for cloud resource provisioning." -> Use Emulators in the CI pipeline for faster feedback.
