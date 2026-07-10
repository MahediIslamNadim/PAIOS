# 04 - Unified Data Platform

## Part 9

Version: 1.0

Status: Planning

---

# Multi-Modal Monitoring Data Platform (MMDP)

## Purpose

The Multi-Modal Monitoring Data Platform stores observational data collected during study sessions.

These observations help estimate focus, engagement, fatigue, and study behavior.

Observation data supports adaptive learning but does not determine truth.

---

# Design Principles

Privacy First

User Controlled

Offline First

Evidence Based

Transparent

Explainable

Non-Punitive

---

# Monitoring Sources

Webcam

Microphone

Keyboard

Mouse

Screen

OCR

Application Activity

System Activity

Future Sensors

Each source is independently configurable.

---

# Entity: monitoring_sessions

Purpose

Represents one monitoring session.

Fields

id

study_session_id

started_at

ended_at

monitoring_mode

enabled_sources

status

created_at

---

# Entity: webcam_observations

Purpose

Stores webcam-derived observations.

Fields

id

monitoring_session_id

timestamp

face_detected

face_count

head_pose

eye_direction

looking_at_screen

estimated_attention

estimated_fatigue

confidence

created_at

Images are not stored by default.

Only extracted observations are persisted.

---

# Entity: voice_observations

Purpose

Stores voice activity observations.

Fields

id

monitoring_session_id

timestamp

voice_detected

speech_duration

estimated_reading

estimated_discussion

background_noise

confidence

created_at

Audio recordings are optional and disabled by default.

---

# Entity: screen_observations

Purpose

Stores screen interaction metadata.

Fields

id

monitoring_session_id

timestamp

active_application

window_title_hash

document_type

estimated_activity

created_at

Sensitive content should not be stored unless explicitly enabled.

---

# Entity: input_observations

Purpose

Tracks keyboard and mouse activity.

Fields

id

monitoring_session_id

timestamp

keyboard_activity

mouse_activity

idle_duration

typing_speed

created_at

Raw keystrokes are never stored.

---

# Entity: ocr_observations

Purpose

Represents notebook and document OCR imports.

Fields

id

study_session_id

knowledge_object_id

source_image

ocr_engine

confidence

language

processing_time

created_at

The extracted text becomes Knowledge Objects after validation.

---

# Entity: application_activity

Purpose

Tracks applications used during study.

Fields

id

study_session_id

application_name

category

duration_seconds

focus_score

created_at

Examples

VS Code

Browser

PDF Reader

KiCad

QGroundControl

LibreOffice

Terminal

---

# Derived Metrics

Calculated Metrics

Estimated Focus Time

Estimated Deep Work

Context Switches

Break Frequency

Reading Time

Writing Time

Coding Time

Research Time

Revision Time

These metrics are estimates generated from multiple observations.

---

# Observation Confidence

Every observation includes

confidence

Range

0.0

↓

1.0

Confidence depends on

Lighting

Camera Quality

Microphone Quality

Model Accuracy

Observation Duration

Confidence should always be visible when appropriate.

---

# Privacy Controls

Users control

Camera

Microphone

OCR

Keyboard Metadata

Mouse Metadata

Application Tracking

Screen Metadata

Every monitoring source may be enabled or disabled independently.

---

# Data Retention

Policies

Delete After 7 Days

Delete After 30 Days

Archive

Never Store

Manual Only

Retention policies are configurable.

---

# AI Integration

The AI Runtime may use monitoring data to

Estimate Focus

Recommend Breaks

Detect Fatigue

Suggest Revision

Improve Planning

Recommendations must not rely on a single observation source.

---

# Events

Examples

Camera Enabled

Camera Disabled

OCR Completed

Voice Observation Recorded

Focus Updated

Fatigue Estimated

Events enter the Event Store.

---

# Performance

Indexes

study_session_id

monitoring_session_id

timestamp

created_at

Old observations may be summarized to reduce storage usage.

---

# Summary

The Multi-Modal Monitoring Data Platform provides privacy-aware observational data that supports adaptive learning.

Monitoring is transparent, configurable, and designed to assist rather than judge the user.

---

# End of Part 9

Next

Part 10

- Search Architecture
- Full-Text Search
- Semantic Search
- Hybrid Search
- Embedding Storage
- Retrieval Pipeline
