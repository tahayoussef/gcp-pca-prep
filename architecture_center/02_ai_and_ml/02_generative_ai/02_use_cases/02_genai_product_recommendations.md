# Generate Personalized Product Recommendations

## Overview
Uses Gen AI to generate personalized product recommendations based on clickstream data and user behavior.

## Architecture

### Data Ingestion
1.  Clickstream data (page views, clicks, purchases) → **Dataflow**.
2.  **Dataflow** derives user profiles/preferences and creates vector embeddings.
3.  Data + embeddings stored in **BigQuery**.

### Serving Flow
1.  Customer visits **Cloud Run** storefront.
2.  Storefront → **Cloud Run** recommender service.
3.  Recommender performs **vector similarity search** in BigQuery.
4.  Retrieves user profile/preferences → sent to **Gemini API (Vertex AI)** with prompt.
5.  Gemini generates personalized product recommendations.
6.  Recommendations displayed on storefront.

## Optimization
*   **Caching** (Memorystore or Cloud CDN) between storefront and recommender service for cost/performance.
