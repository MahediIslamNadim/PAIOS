# 03 - System Architecture

## Part 8

Version: 1.0

Status: Planning

---

# Multi-Modal Cognitive Observation System (MCOS)

## Purpose

The Multi-Modal Cognitive Observation System (MCOS) observes optional signals during learning sessions to improve recommendations.

It estimates attention, engagement, fatigue, and study behavior using multiple evidence sources.

The system is designed to assist learning.

It is not designed for surveillance or discipline.

---

# Design Principles

MCOS follows five principles.

Permission First

Privacy First

Evidence Based

User Controlled

Graceful Degradation

If a sensor is unavailable or disabled, the platform continues functioning with remaining signals.

---

# Observation Sources

Optional Sensors

Webcam

Microphone

Keyboard

Mouse

Screen Activity

Clipboard

Window Focus

Document Activity

OCR

Digital Pen (Future)

Wearables (Future)

Each source can be independently enabled or disabled.

---

# Observation Pipeline

Raw Signal

↓

Signal Validation

↓

Feature Extraction

↓

Noise Filtering

↓

Evidence Generation

↓

Learning Intelligence Engine

↓

Recommendation

Raw sensor data should be processed locally whenever possible.

---

# Webcam Pipeline

Camera Frame

↓

Face Detection

↓

Head Pose Estimation

↓

Eye Region Detection

↓

Blink Detection

↓

Attention Features

↓

Evidence Object

↓

Delete Frame

The system should avoid retaining raw frames by default.

---

# Eye Attention Estimation

Possible Indicators

Screen Direction

Face Orientation

Blink Frequency

Attention Stability

Session Continuity

The engine estimates attention rather than making definitive claims.

Outputs should be presented as probabilities or trends.

---

# Face Presence

The system estimates whether the user is present.

States

Present

Temporarily Away

Unknown

Camera Disabled

No assumptions should be made when evidence is insufficient.

---

# Fatigue Estimation

Potential Signals

Blink Rate

Head Movement

Typing Slowdown

Long Continuous Sessions

Reduced Interaction

Recent Break History

Fatigue estimates should trigger suggestions rather than conclusions.

---

# Voice Pipeline

Microphone

↓

Voice Activity Detection

↓

Speech Segmentation

↓

Optional Speech Recognition

↓

Evidence Generation

↓

Learning Analytics

Voice recording is optional.

Speech transcripts should only be stored if the user enables this feature.

---

# Voice Study Detection

Possible Observations

Reading Aloud

Question Asking

Self Explanation

Silent Study

Discussion

The engine uses these observations to improve learning analytics.

---

# Screen Activity Analysis

Potential Signals

Active Window

Reading Time

Coding Time

PDF Interaction

Browser Usage

Window Switching

Idle Time

The engine records interaction patterns rather than detailed screen contents by default.

---

# Keyboard Analysis

Possible Metrics

Typing Activity

Typing Consistency

Long Idle Periods

Shortcut Usage

Writing Sessions

No keystroke content should be stored unless explicitly required by a user-enabled feature.

---

# Mouse Analysis

Possible Metrics

Pointer Activity

Scrolling

Selection

Interaction Density

Navigation Patterns

Mouse activity contributes only weak evidence and should not dominate conclusions.

---

# OCR Integration

Images

Notebook Pages

Whiteboard Photos

Scanned Documents

↓

OCR

↓

Text Extraction

↓

Formula Detection

↓

Knowledge Object

↓

Evidence Graph

Manual review should always be available before permanent storage.

---

# Multi-Modal Fusion

Evidence from multiple sources is combined.

Example

Study Session

+

Book Reading

+

Keyboard Activity

+

PDF Progress

+

Optional Webcam

+

Quiz

↓

Learning Evidence

↓

Recommendation

No single signal should determine the outcome.

---

# Privacy Rules

The user chooses which sensors are enabled.

Camera

Microphone

Keyboard

Mouse

OCR

Screen Analysis

Each permission is independent.

The user may revoke permissions at any time.

---

# Data Retention

Default Behavior

Raw Video

Not Stored

Raw Audio

Not Stored

Extracted Features

Stored if enabled

Learning Evidence

Stored

Knowledge Objects

Stored

The platform should prefer derived information over raw recordings.

---

# Dashboard

MCOS exposes trends.

Examples

Focus Trend

Attention Estimate

Session Continuity

Break Balance

Reading Pattern

Coding Pattern

Learning Mode

The dashboard should avoid overstating certainty.

---

# Summary

MCOS provides optional observational evidence that complements study activity.

Its purpose is to help the Learning Intelligence Engine generate better recommendations while respecting user privacy and maintaining transparency.

---

# End of Part 8

Next

Part 9

- Knowledge Processing Pipeline
- OCR Intelligence
- Document Intelligence
- Handwritten Mathematics Recognition
- PDF Intelligence
- Multi-Source Knowledge Extraction
