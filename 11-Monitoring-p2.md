# 11 - Monitoring

## Part 2

Version: 1.0

Status: Planning

---

# Eye Tracking & Presence Detection

## Purpose

Eye Tracking estimates gaze direction and attention level using computer vision.

Presence Detection determines whether the user is physically present at their desk.

Both features are entirely optional and processed locally.

---

# Eye Tracking Technology

Method: Camera-based facial landmark detection.

Technology Options

MediaPipe Face Mesh (Google, cross-platform)

OpenCV + Dlib (traditional, lightweight)

ONNX Model (custom, optimized)

All processing happens on-device. No video leaves the computer.

---

# Eye Tracking Output

Gaze Direction

Looking at screen: center, left, right, top, bottom

Looking away: off-screen, distracted

Eyelid State

Open, partially closed, closed

Blink Rate

Blinks per minute (fatigue indicator)

Pupil Detection (if supported)

Relative pupil position

---

# Attention Estimation

Combine signals to estimate attention.

Attention Signals

Gaze on screen (primary)

Gaze stability (not rapidly shifting)

Facial orientation (facing screen)

Blink rate (normal range)

Attention Score

0-100 based on gaze and stability.

Integrated into Focus Score.

---

# Presence Detection

Detect if user is present at the desk.

Presence States

Present: user detected facing screen

Away: no face detected for N seconds

Just Returned: transition from away to present

Unknown: camera unavailable

Detection is used for:

Auto-pause study timer

Lock screen (optional)

Log idle time

---

# Presence Detection Methods

Camera-Based (Primary)

Face detection via MediaPipe/OpenCV.

Keyboard/Mouse (Secondary)

Recent input activity.

Combined

Both signals for accuracy.

---

# Configuration Options

Enable/Disable

Eye Tracking: on/off

Presence Detection: on/off

Sensitivity

Gaze threshold (percentage of time looking at screen)

Away timeout (seconds before marking away)

Visual Feedback

Show gaze indicator (dot on screen) - optional

Show presence status (dashboard widget)

---

# Privacy Protections

No Video Recordings

Raw camera frames are never saved.

No Cloud Upload

Processing is 100% local.

Temporary Memory

Frames are processed and discarded immediately.

Clear Indicator

Camera active indicator always visible.

Pause Button

One-click pause all camera monitoring.

---

# Events

Events published to Event Store

monitoring.eye.calibrated

monitoring.gaze.screen

monitoring.gaze.away

monitoring.blink.detected

monitoring.presence.detected

monitoring.presence.away

monitoring.presence.returned

---

# Summary

Eye Tracking and Presence Detection provide attention awareness with strong privacy protections.

All processing is local and opt-in with granular controls.

---

# End of Part 2

Next

Part 3

- Activity Monitoring
- Keyboard Activity
- Mouse Activity
- Voice Detection
- Reading Detection
- Aggregated Activity Score
