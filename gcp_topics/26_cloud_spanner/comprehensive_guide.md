# Cloud Spanner - Comprehensive Guide

## Overview
Unique database that combines **Relational Semantics** (SQL, ACID, Joins) with **NoSQL Scalability** (Horizontal write scaling).
- **Use Case**: Global Scale + Strong Consistency (Financial ledgers, Validating global inventory).
- **Constraint**: More expensive than Cloud SQL.
- **Scaling Limit**: Unlimited.

---

## TrueTime & External Consistency
- **The Magic**: Spanner uses atomic clocks and GPS receivers in data centers to keep time synchronized.
- **TrueTime API**: Returns a time interval `[earliest, latest]` guaranteed to contain the current time.
- **External Consistency**: Stronger than traditional "Strong Consistency". Guarantees that if Transaction A finishes before Transaction B starts, then A's timestamp < B's timestamp, **globally**.
- **Implication**: You can run `SELECT *` across a globally distributed database and get a consistent snapshot without locking the database.

---

## Schema Design (Exam Critical)

### 1. Interleaved Tables (Parent-Child)
- **Concept**: Physically store child rows (Orders) next to their parent row (Customer).
- **Mechanism**:
  ```sql
  CREATE TABLE Customers (`CustomerId` INT64, `Name` STRING(MAX)) PRIMARY KEY (`CustomerId`);
  CREATE TABLE Orders (`CustomerId` INT64, `OrderId` INT64, ...) 
  PRIMARY KEY (`CustomerId`, `OrderId`),
  INTERLEAVE IN PARENT Customers ON DELETE CASCADE;
  ```
- **Benefit**: **Joins are extremely fast** (Local).
- **Trade-off**: "Hot" parent row can become a hotspot if it has millions of children (e.g., "Justin Bieber" follower list).

### 2. Primary Key Hotspots
- Just like Bigtable, **avoid monotonic increasing keys** (Timestamp, Sequence).
- **Fix**: Use UUID (v4) or Bit-reverse key.

---

## Architecture & Replication
- **Regional Instance**: High availability within a region (3 zones).
- **Multi-Region Instance**:
  - **Read-Write Replicas**: In 2 regions (e.g., US-West, US-East).
  - **Witness Replica**: In 3rd region (Tie-breaker).
  - **Read-Only Replicas**: Can be anywhere (Global).
- **Availability**: **99.999%** (Five 9s) for Multi-Region.

---

## Spanner Graph (New)
- Determine graph relationships using SQL `GRAPH_TABLE`.
- Find shortest path, neighbor detection.
- **Use Case**: Fraud detection rings, Social networks.

---

## Exam Focus Areas

1.  **Cloud SQL vs Spanner**:
    - "Needs > 64TB" -> **Spanner**.
    - "Needs > 60k Write IOPS" -> **Spanner**.
    - "Global consistency" -> **Spanner**.
    - "Standard MySQL/Postgres tool compatibility" -> **Cloud SQL** (Spanner has Postgres *dialect* but not 100% driver compatibility for everything).

2.  **Performance Tuning**:
    - "High latency on writes".
    - Check **Locking**. Spanner uses **Pessimistic Locking** for Read-Write transactions.
    - Check **Hotspots**. Is everyone writing to `CustomerId=1`?

3.  **Backup/Restore**:
    - Spanner backup is consistent.
    - **Point-in-Time Recovery (PITR)** supported.
