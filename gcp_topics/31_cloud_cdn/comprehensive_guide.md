# Cloud CDN - Comprehensive Guide

## Overview
Content Delivery Network using Google's global edge points of presence (PoPs).
- **Integration**: Activated on the **Backend Service** of an **External HTTP(S) Load Balancer**.
- **Origin**: Can be Compute Engine, GKE, Cloud Storage, or Custom Origin (On-Prem/AWS).

---

## Caching Concepts

### 1. Cache Keys
Determines what makes a request unique.
- **Default**: Full URL (Hostname + Path + Query String).
- **Customization**:
  - **Ignore Query Strings**: Useful if query strings are random (e.g., `?session_id=...` that doesn't change content).
  - **Include Headers/Cookies**: Cache different versions for different user locales or device types.

### 2. Cache Invalidation
- Process of forcibly removing content from cache.
- **Method**: `gcloud compute url-maps invalidate-cdn-cache`.
- **Latency**: Takes a few minutes to propagate globally.
- **Rate Limit**: One invalidation per minute (roughly).

### 3. Signed URLs & Cookies
- **Use Case**: Serve private content (Pay-per-view video) via CDN.
- **Mechanism**: App generates a URL with a signature (HMAC). CDN validates signature before serving.
  - **Signed URL**: Access to a specific file.
  - **Signed Cookie**: Access to a path prefix (e.g., `/premium/*`) for a duration.

---

## Exam Focus Areas

1.  **Optimization**:
    - "Improve cache hit ratio for static assets with random query parameters".
    - Answer: **Customize Cache Key** to ignore query strings.

2.  **Security**:
    - "Serve private content with global performance".
    - Answer: **Cloud CDN with Signed URLs**.

3.  **Invalidation**:
    - "Update a file immediately globally".
    - Answer: **Invalidate** the path (expensive/limited) or **Versioning** (best practice: rename file `v2.jpg`).

4.  **Backend**:
    - Cloud CDN *must* be attached to an **External HTTP(S) Load Balancer**. It does not work with Internal LBs or Network LBs.
