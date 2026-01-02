# Cloud Dataproc - Comprehensive Guide

## Overview
Managed **Spark** and **Hadoop** service.
- **Use Case**: Lift and shift legacy Hadoop/Spark jobs to GCP.
- **Cost**: Per-second billing. Cheaper than running your own cluster permanently.

---

## Dataproc Architecture

### 1. Clusters (Standard)
- **Master Node**: YARN Resource Manager, HDFS NameNode.
- **Worker Nodes**: YARN NodeManager, HDFS DataNode.
- **Preemptible Workers**: Cheaper, short-lived nodes. Good for processing logic, not storage (Data might handle HDFS replication but risky).
  - *Exam Tip*: Don't store HDFS data on Preemptible instances alone. Keep primary workers standard, use preemptible for secondary/burst.

### 2. Workflow Templates
- Orchestrate a DAG of jobs (Hadoop, pyspark, hive).
- **Managed Cluster**: The template *creates* an ephemeral cluster, runs the jobs, and *deletes* the cluster.
- **Cluster Selector**: Runs jobs on an existing long-running cluster.

### 3. Dataproc Serverless
- Run Spark jobs without creating a cluster physically.
- Just submit code (jar/python).
- **Auto-scaling**: Google manages the infrastructure completely.

---

## Migrating to Dataproc (Exam Critical)

| Feature | On-Prem Hadoop | Cloud Dataproc |
| :--- | :--- | :--- |
| **Storage** | HDFS (Local disks) | **GCS** (Cloud Storage Connector) |
| **Compute** | Fixed cluster | **Ephemeral** (Create, Run, Delete) |
| **Scaling** | Add hardware | `gcloud dataproc clusters update ... --num-workers N` |

**Best Practice**: Move data from HDFS to **GCS**. Then you can shut down clusters when not in use.

---

## Exam Focus Areas

1.  **Storage**:
    - "Migrating Hadoop cluster. How to save costs?".
    - Answer: Use **GCS** instead of HDFS for persistent storage. Use ephemeral clusters.

2.  **Initialization Actions**:
    - "Need to install custom library (e.g., Kafka connector) on all nodes".
    - Answer: Use **Initialization Actions** (scripts stored in GCS, run on bootstrap).

3.  **High Availability**:
    - Dataproc supports **HA Mode** (3 Masters) to tolerate master failure.
    - Default is 1 Master (SPOF).

4.  **Autoscaling Policy**:
    - Define policy (YAML) to scale workers based on YARN memory availability.
    - Attach policy to cluster.
