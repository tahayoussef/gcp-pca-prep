# Generate Content for Personalized Marketing Campaigns

## Overview
Uses Gen AI to generate personalized multimedia assets (audio, video, text) for targeted marketing based on user data insights.

## Architecture

### Data Ingestion Flow
1.  User data from various sources → **BigQuery**.
2.  **Dataflow** processes data to derive insights (demographics, interests, purchasing patterns).
3.  **Eventarc** triggers **Cloud Run** service.
4.  **Cloud Run** sends insights + prompt to **Gemini API (Vertex AI)**.
5.  Gemini generates personalized audio/video/text content.
6.  Content uploaded to **Cloud Storage** bucket.

### Serving Flow
*   Web portal retrieves user-specific content from Cloud Storage.
*   Personalized marketing content displayed to users.

## Key Features
*   **Personalized Media Generation**: Automatically create audio, video, and text for each user.
*   **Feedback Loop**: Can incorporate marketing impact data for continuous improvement.
*   **Human-in-the-loop**: Human review before uploading to ensure branding/safety.
