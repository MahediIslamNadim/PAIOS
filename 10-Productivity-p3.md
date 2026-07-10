# 10 - Productivity

## Part 3

Version: 1.0

Status: Planning

---

# Goals & Habits

## Purpose

Goals provide direction and motivation for all activities within PAIOS.

Habits build consistent routines that support goal achievement through small daily actions.

---

# Goal Framework

Goals are organized hierarchically.

Goal Hierarchy

Life Vision (long-term, 5-10 years)

├── Annual Goals

│   ├── Quarterly Objectives

│   │   ├── Monthly Milestones

│   │   │   ├── Weekly Tasks

│   │   │   └── Daily Actions

---

# Goal Types

Learning Goal

"Complete Python for Data Science course"

Project Goal

"Build and test autonomous drone"

Health Goal

"Exercise 4 times per week"

Career Goal

"Get promoted to senior engineer"

Skill Goal

"Master STM32 development"

Habit Goal

"Study for 30 minutes daily"

---

# Entity: goals

Purpose

Stores goal definitions.

Fields

goal_id

parent_goal_id

title

description

goal_type

category

start_date

target_date

completed_date

status (draft, active, in_progress, achieved, missed, abandoned)

progress_percent

key_results (JSON array - OKRs)

metrics (JSON array)

tags

created_at

---

# OKR Support

Objectives and Key Results framework.

Structure

Objective (qualitative, ambitious)

Key Result 1 (quantitative, measurable)

Key Result 2

Key Result 3

Progress is tracked per key result.

---

# AI Goal Recommendations

AI suggests goals based on user patterns.

Recommendation Sources

Learning History (skills partially learned)

Project Patterns (incomplete projects)

Skill Gaps (missing prerequisites)

Time Availability (unused time blocks)

Peer Benchmarks (optional, aggregated)

---

# Habit Tracker

Build and maintain daily habits.

Habit Features

Create Habit

Set Frequency (daily, weekdays, weekly, custom)

Set Time of Day

Track Completion

Streak Counter

Reminder Notifications

Habit Notes

---

# Entity: habits

Purpose

Stores habit definitions.

Fields

habit_id

name

description

frequency (daily, weekdays, custom)

frequency_detail (e.g., 3 times per week)

preferred_time

category (learning, health, productivity, etc.)

streak_current

streak_longest

total_completions

completion_dates (JSON array)

reminder_enabled

reminder_time

status (active, paused, archived)

created_at

---

# Habit Streaks

Track consistency with streaks.

Streak Types

Daily Streak (consecutive days)

Weekly Streak (consecutive weeks)

Perfect Month (every day in month)

Streak features

Current count

Longest count

Streak history

Streak milestones (7, 30, 60, 90, 365 days)

---

# Habit Reminders

Gentle reminders to maintain habits.

Reminder Options

Time-Based (specific time daily)

Context-Based (after completing another habit)

Location-Based (when arriving at location - future)

Smart Reminders (AI suggests best time based on schedule)

---

# Goal-Habit Connection

Link habits to goals for progress tracking.

Connection Example

Goal: "Run 10K in 3 months"

Habit: "Run for 20 minutes every morning"

Each habit completion contributes to goal progress.

---

# Events

Events published to Event Store

productivity.goal.created

productivity.goal.updated

productivity.goal.achieved

productivity.goal.missed

productivity.habit.completed

productivity.habit.streak.updated

productivity.habit.milestone.reached

---

# Summary

Goals provide direction and motivation while Habits build consistent daily routines.

AI recommendations help users set achievable goals and maintain productive habits.

---

# End of Part 3

Next

Part 4

- Journal & Decision Journal
- Journal Types
- Prompts & Templates
- Decision Journal
- Outcome Tracking
- AI Journal Analysis
