# 11 - Monitoring

## Part 4

Version: 1.0

Status: Planning

---

# Focus & Fatigue Detection

## Purpose

Focus Detection combines monitoring signals into a real-time focus score.

Fatigue Detection identifies signs of mental fatigue and suggests breaks to prevent burnout.

---

# Focus Score Calculation

Composite score from multiple signals.

Score Factors (weighted)

Gaze on Screen (30%) - from eye tracking

Keyboard Activity (20%) - active typing

Mouse Activity (10%) - active usage

Reading Detection (15%) - reading behavior

Presence (10%) - user at desk

Application Context (10%) - work app vs distraction

Time Into Session (5%) - diminishing after 90 min

Score: 0 (distracted) to 100 (fully focused)

---

# Focus Zones

Categorized focus levels.

Zones

Deep Focus (80-100)

Optimal state, uninterrupted work.

Focused (60-79)

Good focus, minor distractions.

Light Focus (40-59)

Some distractions, routine tasks.

Distracted (20-39)

Low focus, frequent interruptions.

Away (0-19)

User not present or disengaged.

---

# Entity: focus_records

Purpose

Stores focus score snapshots.

Fields

record_id

timestamp

focus_score

focus_zone

session_id

gaze_score

keyboard_score

mouse_score

reading_score

presence_score

duration_seconds

created_at

---

# Fatigue Detection

Detect signs of mental fatigue.

Fatigue Indicators

Blink Rate Increase (fatigue indicator)

Gaze Stability Decrease (wandering eyes)

Typing Speed Decrease (slower typing)

Typing Error Increase (more corrections)

Longer Pauses Between Actions

Yawning (if camera detects)

Session Duration (over 90 min continuous)

---

# Fatigue Level

Fatigue Score (0-100)

None (0-20): Normal, alert

Mild (20-40): Slight fatigue, continue

Moderate (40-60): Noticeable fatigue, break recommended

Significant (60-80): High fatigue, break needed

Severe (80-100): Critical fatigue, stop and rest

---

# Break Recommendations

AI recommends optimal break timing.

Break Triggers

Focus Score Below Threshold for 5+ min

Fatigue Level Moderate or Higher

Session Duration Exceeds 90 min

Eye Strain Detected (low blink rate -> then high)

Time Since Last Break > 2 hours

Recommended Break Type

Short Break (5 min): Stand, stretch, eyes

Movement Break (10 min): Walk, exercise

Rest Break (15+ min): Complete rest, nap if severe

---

# Burnout Prevention

Long-term fatigue trend analysis.

Burnout Risk Factors

Sustained low focus over days/weeks

Increasing fatigue baseline

Decreasing daily activity

Skipping breaks consistently

Declining energy levels

Sleep disruption patterns

Burnout alerts are shown with prevention suggestions.

---

# Focus History

View focus patterns over time.

Focus Timeline

Real-time focus graph during sessions

Daily focus summary

Weekly focus trends

Focus by activity type

Focus by time of day

Focus history is available in Monitoring Dashboard and Analytics.

---

# Events

Events published to Event Store

monitoring.focus.score.updated

monitoring.focus.zone.changed

monitoring.fatigue.detected

monitoring.fatigue.level.increased

monitoring.break.recommended

monitoring.burnout.risk.detected

---

# Summary

Focus Detection combines multiple signals into a real-time focus score.

Fatigue Detection helps prevent burnout with timely break recommendations.

---

# End of Part 4

Next

Part 5

- Privacy & Permissions
- Permission Model
- Granular Controls
- Data Retention
- Transparency
- User Rights
