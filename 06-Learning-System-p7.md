# 06 - Learning System

## Part 7

Version: 1.0

Status: Planning

---

# Revision Engine & Spaced Repetition

## Purpose

The Revision Engine implements scientifically-proven spaced repetition algorithms to optimize long-term memory retention.

It determines exactly when each piece of knowledge should be reviewed for maximum learning efficiency.

---

# Revision Architecture

Revision Engine
- Scheduler
- Algorithm Processor (SM-2)
- Due Item Manager
- Review Session Manager
- Performance Tracker
- Analytics Integrator

Revision is automated but user-controlled.

---

# Core Algorithm: SM-2

Based on the SuperMemo SM-2 algorithm with enhancements.

Algorithm Factors

Easiness Factor (EF) starts at 2.5

Interval grows with each successful review

Quality of recall (0-5) determines next interval

Minimum interval: 1 day

Maximum interval: configurable (default 365 days)

---

# Quality Ratings

User rates recall quality on each review.

0 - Complete blackout (total forget)

1 - Incorrect, but answer felt familiar

2 - Incorrect, but answer seemed easy to recall

3 - Correct with serious difficulty

4 - Correct after hesitation

5 - Perfect recall, instant response

Ratings 0-2 reset the interval.

---

# Interval Calculation

Based on SM-2 formula.

First Review

1 day

Second Review

6 days (if quality >= 3)

Subsequent Reviews

Interval = previous_interval x EF (if quality >= 3)

Reset

If quality < 3, interval resets to 1 day.

---

# Easiness Factor Update

EF is updated after each review.

Formula

EF' = EF + (0.1 - (5 - q) x (0.08 + (5 - q) x 0.02))

Where q = quality rating (0-5)

EF minimum: 1.3

Higher EF = slower interval growth (less frequent review).

---

# Entity: revision_items

Purpose

Items scheduled for spaced repetition review.

Fields

item_id

subject_id

resource_type (note, flashcard, quiz_question, topic, concept)

resource_id

easiness_factor

interval_days

repetitions (consecutive successful reviews)

next_review_date

last_review_date

last_quality

review_count

status (new, learning, reviewing, mastered, suspended)

created_at

---

# Revision Scheduler

Determines which items are due for review.

Scheduling Logic

For each item:

Due = next_review_date <= today

Overdue = next_review_date < today - grace_period

New items are introduced before fully reviewed items.

Daily limit on new items prevents overload.

---

# Daily Revision Limit

Configurable limits to prevent overload.

Default Limits

New Items Per Day: 20

Review Items Per Day: 100

Total Daily Reviews: 120

Users can adjust limits based on available time.

---

# Review Session Flow

Open Revision Queue

↓

View Due Items (sorted by urgency)

↓

Review Item

↓

Self-Assess Quality (0-5)

↓

Algorithm Updates Schedule

↓

Next Item

↓

Session Complete

↓

Statistics Updated

---

# Review Session Types

Quick Review

5-10 minute review of most urgent items.

Full Review

Complete all due items (estimated time shown).

Topic Review

Review specific topic or subject.

Exam Prep

Intensive review before exam (custom schedule).

Custom Review

User-defined review scope.

---

# Due Item Prioritization

Items are sorted by priority.

Priority Factors

Overdue Days (more overdue = higher priority)

Exam Proximity (items related to upcoming exams)

Mastery Level (low mastery = higher priority)

Subject Priority (user-defined subject priority)

Item Age (older items = higher priority)

---

# Revision Reminders

Notifications for due reviews.

Reminder Types

Daily Due Items Summary (morning)

Due Item Alert (when items become due)

Overdue Warning (if items are overdue)

Streak Protection (reminder to maintain streak)

Review scheduling respects user preferences.

---

# Entity: revision_history

Purpose

Records individual review attempts.

Fields

history_id

item_id

scheduled_date

reviewed_date

quality_rating

response_time_seconds

session_id

status (completed, skipped, rescheduled)

created_at

---

# Review Performance Analytics

Metrics tracked per item and overall.

Item Level

Review Count

Average Quality

Interval History

Mastery Trend

Overall

Total Reviews

Average Quality

Retention Rate

Overdue Items

Mastery Distribution

---

# Automated Revision Integration

Revision items are auto-generated from learning activities.

Auto-Generation Sources

Notes (AI extracts key concepts)

Quiz Answers (incorrect answers become revision items)

Flashcard Reviews (inherently revision items)

Book Highlights (important passages)

Study Session Summary (key takeaways)

Mistakes (errors made during practice)

---

# Exam Mode

Special revision mode for exam preparation.

Exam Mode Features

Higher Review Frequency

Focus on Weak Areas

Simulated Test Conditions

Progress Toward Exam Date

Estimated Readiness Score

---

# Mastery Tracking

Items progress through mastery levels.

Levels

New (just added)

Learning (first few reviews)

Reviewing (stable intervals)

Mastered (long intervals, high EF)

Re-Learning (if quality drops)

Mastery is displayed per subject and overall.

---

# Events

Events published to Event Store

learning.revision.item.created

learning.revision.item.due

learning.revision.item.reviewed

learning.revision.item.mastered

learning.revision.item.rescheduled

learning.revision.session.started

learning.revision.session.completed

learning.revision.overdue.alert

---

# Summary

The Revision Engine implements spaced repetition (SM-2) for optimal long-term memory retention.

Items are auto-generated from learning activities and scheduled at scientifically-determined intervals.

---

# End of Part 7

Next

Part 8

- Quiz Engine
- Quiz Types
- Question Types
- Quiz Generation
- Grading & Scoring
- Performance Analytics
