# 11 - Monitoring

## Part 3

Version: 1.0

Status: Planning

---

# Activity Monitoring

## Purpose

Activity Monitoring tracks keyboard, mouse, and voice activity to infer user engagement and context.

Reading Detection identifies when the user is reading on-screen content.

---

# Keyboard Activity Monitoring

Track keyboard usage patterns.

Tracked Metrics

Key Press Count

Keys Per Minute (typing speed)

Active Typing Duration

Pause Duration Between Typing

Application Context (which app is active)

Non-Tracked Data

Individual key content (passwords, messages)

What is typed (only patterns)

Content of typed text

---

# Mouse Activity Monitoring

Track mouse usage patterns.

Tracked Metrics

Movement Distance

Click Count

Scroll Events

Click Speed

Active vs Idle Time

Application Context

Non-Tracked Data

Screen position (not stored)

Click targets (not recorded)

---

# Voice Activity Detection

Detect voice presence without recording speech.

Detection Method

Microphone energy level analysis

Voice Activity vs Noise

Metrics

Voice Presence (binary)

Voice Duration

Voice Frequency (how often)

Non-Tracked Data

Speech content (not recorded or transcribed)

Speaker identity (not identified)

Conversation content (not analyzed)

Voice detection is OPT-IN only.

---

# Entity: activity_logs

Purpose

Stores aggregated activity metrics.

Fields

log_id

timestamp

activity_type (keyboard, mouse, voice, reading)

intensity (0-100)

duration_seconds

application (active app, if available)

is_active (boolean)

session_id

---

# Reading Detection

Detect when user is reading on-screen.

Detection Signals

Eye Movement Pattern (horizontal scanning)

Scroll Pattern (consistent, paced)

Mouse Inactivity (no clicking during reading)

Application Type (PDF reader, browser, document editor)

Face Orientation (facing screen)

Reading detection enables:

Auto-tracking reading time

Suggesting breaks after long reading

Logging reading as learning activity

---

# Aggregated Activity Score

Combine activity signals into a single score.

Score Components

Keyboard Activity (30%)

Mouse Activity (20%)

Voice Activity (10%)

Eye/Gaze on Screen (30%)

Presence (10%)

Weighting is configurable per user.

---

# Privacy Settings

Granular activity monitoring controls.

Control Options

Per-Sensor Enable/Disable

Keyboard Monitoring (on/off)

Mouse Monitoring (on/off)

Voice Detection (on/off)

Reading Detection (on/off)

Per-Session Pause

Quick toggle from status bar

---

# Events

Events published to Event Store

monitoring.keyboard.active

monitoring.keyboard.idle

monitoring.mouse.active

monitoring.mouse.idle

monitoring.voice.detected

monitoring.reading.detected

monitoring.activity.score.updated

---

# Summary

Activity Monitoring tracks engagement patterns without storing sensitive content.

All metrics are aggregated and privacy-preserving.

---

# End of Part 3

Next

Part 4

- Focus & Fatigue Detection
- Focus Score Calculation
- Focus Zones
- Fatigue Detection
- Break Recommendations
- Burnout Prevention
