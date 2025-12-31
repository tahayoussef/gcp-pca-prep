# Cymbal Bank Application Architecture

## Overview
**Cymbal Bank** is the reference application demonstrating the Enterprise Developer Platform Blueprint in action. It's a microservices-based banking app.

## Tenants
*   Cymbal Bank is deployed as a single tenant on the platform.
*   Demonstrates multi-tenant platform capabilities with real-world example.

## Applications
*   **Frontend**: Web UI for customers.
*   **Backend Services**: Account management, transaction processing, balance calculation.
*   **Database**: AlloyDB for PostgreSQL for transactional data.

## Database Structure
*   Microservices architecture with separate data stores per service where applicable.
*   Demonstrates distributed service patterns.
