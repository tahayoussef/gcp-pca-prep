# Firebase & Cloud Firestore - Comprehensive Guide

## Overview
**NoSQL Document Database** that scales automatically. Serverless.
- **Data Model**: Documents organized into Collections. (Schema-less).
- **Strong Consistency**: Always strongly consistent (unlike eventual consistency of many NoSQL DBs).
- **ACID Transactions**: Supported across multiple documents.

---

## Firestore Modes (Exam Critical)

You must choose one mode per project. You cannot mix them.

| Feature | Native Mode | Datastore Mode |
| :--- | :--- | :--- |
| **Primary Use Case** | Mobile/Web Apps (Real-time updates) | Server-side Backend (High throughput) |
| **Real-time Sync** | **Yes** (Listeners push updates to client) | No |
| **Offline Support** | **Yes** (Mobile SDK caches data) | No |
| **Scalability** | Millions of connections | Massive write throughput |
| **Client Libraries** | Mobile (iOS/Android) + Web + Server | Server-side only (Python, Java, Go) |
| **Write Limit** | **1 write per second per document** | Unlimited (but same per-entity limit applies) |

**Decision Tree**:
- "Need real-time chat app" -> **Native Mode**.
- "Need offline sync for field workers" -> **Native Mode**.
- "Migrating legacy App Engine Datastore app" -> **Datastore Mode**.
- "High-throughput ingestion from IoT sensors (no real-time client needed)" -> **Datastore Mode** (or Bigtable if *very* high).

---

## Firebase Realtime Database
- **Legacy** product.
- **Data Model**: One giant JSON tree (not collections/documents).
- **Cons**: Write contention on huge trees. Harder to scale.
- **Use Case**: Simple real-time presence (Who is online?) or legacy apps. **Prefer Firestore** for almost everything else.

---

## Exam Focus Areas

1.  **Hotspots**:
    - Like Bigtable, avoid sequential keys if write rate is massive (500/500 rule: 500 writes/sec to a collection).
    - **Indexing**: Firestore automatically indexes *every* field.
    - **Write Limit**: You cannot update the *same document* more than 1/sec. (Physics limit of replication). If you need a counter that increments 1000/sec, use **Distributed Counters** (Shard the counter into N sub-counters).

2.  **Transactions**:
    - Supported.
    - "Update inventory count safely" -> Use Transaction.

3.  **Composite Indexes**:
    - Queries on multiple fields (e.g., `WHERE age > 20 AND city = 'NY'`) require a **Composite Index**.
    - `index.yaml` or created via Console error link.
