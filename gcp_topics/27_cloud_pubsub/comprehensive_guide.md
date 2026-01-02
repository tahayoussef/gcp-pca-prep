# Cloud Pub/Sub - Comprehensive Guide

## Overview
Global, asynchronous messaging service.
- **Pattern**: Publisher -> Topic -> Subscription -> Subscriber.
- **Decoupling**: Decouples senders from receivers.
- **Global**: Topic is global (One endpoint anywhere in the world).
- **Delivery**: At-least-once (Duplicates possible).

---

## Subscription Types (Exam Critical)

| Feature | Pull | Push | BigQuery Export |
| :--- | :--- | :--- | :--- |
| **Mechanic** | Subscriber asks "Any mail?" | Pub/Sub posts to HTTPS endpoint | Pub/Sub writes directly to BQ |
| **Flow Control** | Subscriber controls rate | Pub/Sub pushes fast (Subscriber must handle) | Managed |
| **Use Case** | High throughput, batch processing, Dataflow | Webhooks, Cloud Functions, App Engine | Analytics, easy archiving |

---

## Key Features

### 1. Message Ordering
- Default: **No ordering** (Parallel delivery).
- **Ordering Keys**: If you publish with an `OrderingKey` (e.g., `UserID`), Pub/Sub guarantees messages *for that key* are delivered in order.
- **Trade-off**: If one message fails (subscriber doesn't Ack), subsequent messages for that key are blocked (Head-of-Line Blocking).

### 2. Schemas
- Enforce structure (Avro or Protocol Buffers) on the Topic.
- **Benefit**: Rejects "bad" messages at the Publisher level (Publisher gets 400 error). Prevents garbage data from entering pipeline.

### 3. Dead Letter Topic (DLQ)
- If Subscriber fails to Ack message after X attempts, move it to a Dead Letter Topic.
- Allows pipeline to continue processing (skip poison pill), while you debug the bad message later.

### 4. Exactly-Once Delivery
- Pub/Sub standard is **At-Least-Once**.
- **Exactly-Once**: Enabled on Subscription. Requires Subscriber to support it (Enable `exactly_once_delivery` and use `AckID` correctly).

---

## Exam Focus Areas

1.  **Architecture**:
    - "Decouple microservices". -> **Pub/Sub**.
    - "Ingest IoT data globally". -> **Pub/Sub**.
    - "Handle massive spike in traffic without crashing backend". -> **Pub/Sub** (Buffer).

2.  **Order**:
    - "Need strict order for financial transactions". -> Use **Ordering Key**.
    - "One message failing blocks everything". -> Too broad ordering key. Use granular key.

3.  **Push vs Pull**:
    - "Cloud Run service needs to process messages". -> **Push** subscription (invokes the service).
    - "Dataflow pipeline". -> **Pull** (Dataflow automatically handles Pull).

4.  **Retention**:
    - Unacknowledged messages retained for **7 days** (default/max).
    - You can also "Seek" (Replay) to a timestamp if `RetainAckedMessages` is enabled.
