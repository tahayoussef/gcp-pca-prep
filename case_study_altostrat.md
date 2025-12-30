# Case Study: Altostrat Media (v6.1 - Gen AI Focus)

## Company Overview
Altostrat Media is a legacy media company aiming to modernize its content platform and enhance customer experience using Google Cloud's **generative AI** services. They want to position themselves as an AI-driven leader in media.

## Solution Concept
To transform their business, Altostrat is building a new system to:
1.  **Automate Content Analysis**: Use AI to tag, summarize, and moderate uploaded video/audio.
2.  **Personalize User Experience**: Use Gen AI to recommend content and enable "natural language" search/interaction.
3.  **Modernize Operations**: Move from on-prem ingestion to a scalable, hybrid cloud architecture.

## Business Requirements
*   **Modernization**: Replace legacy on-prem ingestion with a cloud-native, scalable pipeline.
*   **Innovation**: Differentiate with Gen AI features (summaries, chat-based search).
*   **Automation**: Reduce manual effort in metadata tagging and content moderation.
*   **Market Position**: Establish Altostrat as a technical leader.
*   **Trust/Safety**: ensure AI outputs are "auditable" and "explainable", and content is filtered for toxicity.

## Technical Requirements
*   **Deep Content Analysis**: System must extract metadata, entities, and sentiment from media.
*   **Ingestion Pipeline**: High-bandwidth secure connectivity to ingest massive media files from legacy on-prem storage.
*   **Scalability**: Compute must scale for bursty transcoding/analysis jobs.
*   **Storage Lifecycle**: Optimize costs for petabytes of media (Hot -> Cold -> Archive).
*   **Observability**: Unified monitoring for the hybrid environment.

## Existing Technical Environment
*   **Compute**: **Google Kubernetes Engine (GKE)** involves microservices for content.
*   **Storage**: **Cloud Storage** for raw media.
*   **Analytics**: **BigQuery** for viewer data.
*   **Legacy**: On-premises data center handling initial ingestion and archival.

## Key Services & Architecture Patterns
*   **Compute**:
    *   **GKE**: For the core application microservices.
    *   **Cloud Run / Cloud Functions**: Event-driven processing. Triggered when a new file hits GCS.
    *   **Dataproc**: For large-scale text/log preprocessing (stemming, tokenization) if needed before AI.
*   **AI/ML (The Core Focus)**:
    *   **Vertex AI**: The unified platform.
    *   **Video Intelligence API**: For extracting metadata/labels from video.
    *   **Natural Language API**: For sentiment analysis and entity extraction from transcripts.
    *   **Generative AI (LLMs)**: For creating summaries and "chat with content" features.
*   **Data & Storage**:
    *   **Cloud Storage**: Use **Lifecycle management** to move old videos to archival classes.
    *   **BigQuery**: Store analytics. Use **BigQuery ML** for simple classification models on structured data.
*   **Networking**:
    *   **Dedicated Interconnect**: The likely answer for "High Speed" ingestion from on-prem.
    *   **Cloud VPN**: Backup connectivity.

## Exam Scenarios & "Gotchas"
*   **Scenario**: "We need to filter inappropriate content automatically."
    *   **Answer**: Use **Video Intelligence API** (content moderation features) or Vertex AI vision models.
*   **Scenario**: "Ensure we don't overspend on storage for old videos."
    *   **Answer**: Configure **GCS Object Lifecycle Management** rules (e.g., Move to Coldline after 30 days).
*   **Scenario**: "How do we trigger the analysis immediately after upload?"
    *   **Answer**: **Eventarc** (or Cloud Storage notification) triggering a **Cloud Run Function**.
*   **Scenario**: "The AI Results must be explainable."
    *   **Answer**: Use **Vertex AI Explainable AI** features on your models.
