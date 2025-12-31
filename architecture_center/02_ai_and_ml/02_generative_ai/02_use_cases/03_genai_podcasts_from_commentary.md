# Generate Podcasts from Audio Files

## Overview
Uses Gen AI to generate podcast scripts from audio commentary (e.g., sports event highlights).

## Architecture
1.  User uploads audio files to **Cloud Storage**.
2.  **Eventarc** triggers **Cloud Run**.
3.  **Cloud Run** sends audio to **Speech-to-Text**.
4.  **Speech-to-Text** produces time-stamped transcripts.
5.  Transcripts + prompt sent to **Gemini API (Vertex AI)** (e.g., "generate 15-min podcast script about highlights").
6.  **Gemini** generates draft podcast script.
7.  **Cloud Run** sends draft to user for review/editing.
8.  User finalizes script → sent to **Text-to-Speech**.
9.  **Text-to-Speech** produces final podcast audio.

## Key Services
*   **Speech-to-Text**: Audio transcription.
*   **Gemini**: Script generation.
*   **Text-to-Speech**: Synthetic speech from text.
