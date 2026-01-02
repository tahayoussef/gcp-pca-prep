# Cloud Dataflow - Comprehensive Guide

## Overview
Serverless, fully managed data processing service.
- **Engine**: Runs **Apache Beam** pipelines.
- **Unified Model**: Same code for **Batch** and **Streaming**.
- **Serverless**: Auto-scales workers (Horizontal Autoscaling) and Dynamic Work Rebalancing.

---

## Apache Beam Concepts

### 1. PCollection
- Distributed dataset (immutable).
- Passed between steps.
- **Bounded**: Batch data (start and end).
- **Unbounded**: Streaming data (infinite).

### 2. PTransform
- Operations on PCollections (Map, Filter, GroupByKey, Combine).
- **ParDo**: Parallel processing of each element (e.g., parsing JSON).

### 3. Windowing (Exam Critical for Streaming)
How to group infinite data into finite chunks for aggregation.
- **Fixed Window**: Disjoint time intervals (e.g., 10:00-10:05, 10:05-10:10).
- **Sliding Window**: Overlapping intervals (e.g., Every 1 min, calculate valid for 5 mins).
- **Session Window**: Defined by gaps in data. (e.g., User is active, then stops for 30 mins -> Session closed). Good for User Activity.

### 4. Watermarks, Triggers, and Late Data
- **Watermark**: "The system's guess of when all data up to time T has arrived."
- **Trigger**: Determines when to emit results (e.g., "Emit when watermark passes window end" or "Emit every minute").
- **Late Data**: Data arriving after watermark. You can define "Allowed Lateness" (e.g., 1 hour). Data arriving later than that is dropped.

---

## Flex Templates (Ops Focus)
- **Templates**: Pre-packaged pipelines.
- **Flex Templates**: Docker-based. You package your code and dependencies into a Docker image.
- **Benefit**: Allows users to launch pipelines via Console/API without setting up a Java/Python environment. Separation of "Builder" (Dev) and "Runner" (Ops).

---

## Features

- **Streaming Engine**: Moves state and shuffle out of worker VMs into a specialized backend service. Smoother scaling, checking, and updates.
- **Dataflow Prime**: Optimized, resource-efficient variant. Vertical autoscaling tailored to steps.
- **Dataflow Shuffle**: External shuffle service for batch (faster than worker-based shuffle).

---

## Exam Focus Areas

1.  **Windowing Selection**:
    - "Calculate average requests per minute, every minute". -> **Fixed Window**.
    - "Calculate running average of last 5 minutes, updated every 10 seconds". -> **Sliding Window**.
    - "Group user clicks into specific browsing sessions". -> **Session Window**.

2.  **Updating Pipelines**:
    - **Update**: You can update a streaming pipeline in-flight (using `--update` flag).
    - **Requirement**: Job names must match, and structure must be compatible.

3.  **Handling Late Data**:
    - "Data arrives late due to network status".
    - Solution: Set **Allowed Lateness**. If critical to capture ALL data eventually, output late data to a "Side Output" (Dead Letter) for manual reprocessing.

4.  **Error Handling**:
    - "One bad record crashes the pipeline".
    - Solution: `try/catch` block in ParDo. Log error or send to **Dead Letter Queue (Pub/Sub)**. Do NOT let it fail the worker (Dataflow will retry indefinitely = "Stuck Pipeline").
