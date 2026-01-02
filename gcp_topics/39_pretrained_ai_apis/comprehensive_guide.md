# Pretrained AI APIs - Comprehensive Guide

## Overview
Ready-to-use machine learning models via REST/gRPC APIs. No model training required.
- **Use Case**: "Add AI features to my app without hiring data scientists".

---

## 1. Cloud Vision API
- **Capabilities**:
  - **Label Detection**: "This is a cat", "This is the Eiffel Tower".
  - **OCR (Text Detection)**: Extract text from images/PDFs.
  - **SafeSearch**: Detect adult/violent content.
  - **Face Detection**: Detect *where* faces are (bounding box) and emotions (joy, sorrow), but **NOT facial recognition** (identifying *who* it is).

## 2. Cloud Speech-to-Text (STT)
- **Use Case**: Transcribe audio to text.
- **Modes**:
  - **Synchronous**: Short audio (< 1 min).
  - **streaming**: Real-time (gRPC/Websockets).
  - **Asynchronous**: Long audio (up to 480 mins). stored in GCS.
- **Best Practices**:
  - Use **Lossless** encoding (FLAC/WAV).
  - Sample rate **16000 Hz** is ideal.

## 3. Cloud Natural Language API (NLP)
- **Capabilities**:
  - **Sentiment Analysis**: Is the review positive or negative?
    - **Score**: -1.0 (Negative) to 1.0 (Positive).
    - **Magnitude**: Strength of emotion (0.0 to +inf).
  - **Entity Analysis**: Extract proper nouns (google, New York).
  - **Content Classification**: "This article is about Sports".
  - **Syntax Analysis**: Parse sentences.

## 4. Cloud Translation API
- **Basic**: Simple text translation using NMT (Neural Machine Translation).
- **Advanced**:
  - **Glossary**: Force specific translations (e.g., "BrandName" should not be translated).
  - **Batch Translation**: Translate massive files in GCS.
  - **Adaptive Translation**: Use LLMs to adapt to style.

## 5. Cloud Video Intelligence API
- **Capabilities**:
  - Perform Vision-like tasks on **Video** files.
  - **Shot Change Detection**: "Scene changed at 05:03".
  - **Object Tracking**: Follow a car across frames.

---

## Exam Focus Areas

1.  **Vision vs Video**:
    - "Analyze a live video stream for objects". -> **Video Intelligence API (Streaming)** or **Vision API** (if extracting frames manually). Usually **Video Intelligence**.

2.  **Speech-to-Text Async**:
    - "Transcribe a 2-hour meeting recording". -> **Asynchronous Recognize**.

3.  **NLP Sentiment**:
    - "Filter out negative comments". -> Check **Sentiment Score < 0**.
    - "Identify highly emotional mixed comments". -> **Score ~ 0** but **Magnitude is High**.

4.  **PII Redaction**:
    - **DLP API** is better suited for PII redaction than NLP API, though NLP can find Entities. Stick to **DLP** for compliance/redaction compliance.
