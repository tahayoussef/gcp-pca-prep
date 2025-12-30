# GCP Professional Cloud Architect (PCA) - 1 Month Study Plan

## Week 1: Foundations & Core Architecture
*Goal: Master the resource hierarchy, connectivity, and core compute/storage.*

*   **Day 1: IAM & Resource Hierarchy**
    *   Organization, Folders, Projects.
    *   IAM Roles (Primitive vs Predefined vs Custom).
    *   Service Accounts & Best practices (Least Privilege).
    *   *Practice*: Set up a Shared VPC structure.
*   **Day 2: Networking Deep Dive**
    *   VPC, Subnets, Firewall Rules.
    *   Hybrid Connectivity: Cloud VPN vs Interconnect (Dedicated/Partner).
    *   Peering vs Shared VPC used cases.
*   **Day 3: Compute Options**
    *   Decision Tree: GCE vs GKE vs App Engine vs Cloud Run.
    *   When to use "Migrate for Compute Engine" (Lift & Shift).
    *   Preemptible vs Spot VMs.
*   **Day 4: Storage & Database Selection**
    *   Object Storage: GCS classes (Standard, Nearline, Coldline, Archive).
    *   Relational: Cloud SQL vs Cloud Spanner (Global scale).
    *   NoSQL: Bigtable (Time-series/IoT) vs Firestore (Mobile/Web).
    *   *Activity*: Draw a flowchart for choosing a storage option.
*   **Day 5: Load Balancing**
    *   Global (HTTP(S), SSL Proxy) vs Regional (Network LB).
    *   Internal vs External LBs.
    *   Cloud Armor integration.
*   **Day 6: Case Study Intro - EHR Healthcare**
    *   Read `case_study_ehr_healthcare.md`.
    *   Analyze: Hybrid connectivity needs, HIPAA compliance, Migration strategy.
*   **Day 7: Review & Mini-Lab**
    *   Deploy a simple 3-tier web app (GCE/MIG -> LB).

## Week 2: Data, ML, and Modernization
*Goal: Understand "Transform" technologies - Big Data, AI, and Containerization.*

*   **Day 8: GKE & Anthos**
    *   GKE Cluster architecture (Zonal vs Regional).
    *   Anthos (Hybrid/Multi-cloud management).
    *   Workload Identity.
*   **Day 9: Big Data Pipelines**
    *   Ingestion: Pub/Sub vs IoT Core (Legacy check).
    *   Processing: Dataflow (Beam) vs Dataproc (Spark/Hadoop).
    *   Choosing the right pipeline tool.
*   **Day 10: Analytics & Warehousing**
    *   BigQuery: Architecture, Slots, Partitioning/Clustering.
    *   Looker/Data Studio basics.
*   **Day 11: Machine Learning & AI**
    *   Vertex AI Overview.
    *   Pre-trained APIs (Vision, NLP, Video Intelligence).
    *   *Focus*: When to use APIs vs AutoML vs Custom Training.
*   **Day 12: Application Modernization**
    *   Strangler pattern.
    *   CI/CD: Cloud Build, Artifact Registry.
    *   App Engine versions/splitting traffic.
*   **Day 13: Case Study - Altostrat Media**
    *   Read `case_study_altostrat.md`.
    *   Analyze: Storage lifecycle for media, ML APIs for content moderation.
*   **Day 14: Case Study - Cymbal Retail**
    *   Read `case_study_cymbal_retail.md`.
    *   Analyze: Retail Search/Recommendation AI, handling scale (Black Friday).

## Week 3: Security, Reliability & Operations
*Goal: The role of the Architect - SRE principles and securing the fort.*

*   **Day 15: Advanced Security**
    *   Cloud DLP (PII redaction).
    *   KMS (Key Management) & CMEK.
    *   VPC Service Controls (Perimeter security).
*   **Day 16: Reliability & SRE**
    *   Defining SLIs, SLOs, SLAs.
    *   Error Budget.
    *   High Availability Design (Multi-zone vs Multi-region).
*   **Day 17: Operations Suite**
    *   Cloud Monitoring (Metrics, Alerts).
    *   Cloud Logging (Sinks, Exports to BQ).
    *   Cloud Trace (Latency).
*   **Day 18: Cost Optimization**
    *   Billing Exports.
    *   CUDs, SUDs.
    *   Programmatic budget alerts (Pub/Sub -> Cloud Function).
*   **Day 19: Case Study - Knight Motives**
    *   Read `case_study_knightmotives.md`.
    *   Analyze: IoT patterns, Bigtable schema design, Apigee for partners.
*   **Day 20: Compliance & Governance**
    *   Organizational Policies.
    *   Audit Logging.
*   **Day 21: Review**
    *   Cross-reference Case Studies with services learned this week.

## Week 4: Final Prep & Scenarios
*Goal: Synthesis and Exam Technique.*

*   **Day 22-24: Mock Exams (Timed)**
    *   Take practice tests.
    *   *Crucial*: Review every wrong answer. Why is the distractor wrong?
*   **Day 25: Designing Solutions (Whiteboarding)**
    *   Pick a random startup idea (e.g., "Global Ride Sharing").
    *   Sketch the architecture: LB -> GKE -> Spanner + Pub/Sub -> Dataflow -> BQ.
*   **Day 26: The "Google Way"**
    *   Review Google's philosophy: Managed services over self-managed. Global over Regional (unless compliance/latency dictates). Least Privilege.
*   **Day 27: Final Fact Check**
    *   Review `gcp_services_cheat_sheet.md`.
    *   Memorize key limits or quotas (less important now, but good to know).
*   **Day 28: Rest**
    *   Light review. Ensure readiness.
