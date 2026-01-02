# Memorystore - Comprehensive Guide

## Overview
Fully managed in-memory data store service.
- **Engines**: Redis (most common) and Memcached.
- **Use Case**: Caching (reduce DB load), Session Store, Gaming Leaderboards, Pub/Sub (Redis).

---

## Memorystore for Redis
- **Persistence**: RDB Snapshots (Optional). Data survives restart (if enabled).
- **Architecture**:
  - **Basic Tier**: Single node. No HA. Ephemeral IP.
  - **Standard Tier**: Primary + Replica. (Multi-zone HA).
  - **Cluster (New)**: Scalable sharded cluster (TB scale).
- **Scaling**:
  - **Scale Up**: Increase capacity (starts maintenance).
  - **Read Replicas**: Supported in Standard Tier (up to 5 replicas).

## Memorystore for Memcached
- **Persistence**: None. (Pure cache).
- **Architecture**: Multi-threaded. Auto-discovery endpoint.
- **Scaling**: Horizontal scaling (add nodes).

---

## Exam Focus Areas

1.  **Selection**:
    - "Migrating legacy app using Memcached". -> **Memorystore for Memcached**.
    - "Need persistent session store". -> **Memorystore for Redis**.
    - "Complex data structures (Sets, Lists)". -> **Memorystore for Redis**.

2.  **High Availability**:
    - "Zero downtime scaling". -> Redis Standard Tier allows scaling with minimal downtime, but connection reset happens.

3.  **Networking**:
    - Access via **Private Service Access** (Peering).
    - Cannot access directly from Internet (Public IP). Need **VPN** or **Proxy** (e.g. Nutcracker/Twemproxy on GCE) for external access.
