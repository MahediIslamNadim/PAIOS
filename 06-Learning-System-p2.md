# 06 - Learning System

## Part 2

Version: 1.0

Status: Planning

---

# Learning Manager Core & Subject Management

## Purpose

The Learning Manager is the central orchestrator of all learning activities within PAIOS.

Subject Management provides the hierarchical structure for organizing all learning resources.

---

# Learning Manager Architecture

Learning Manager
- Subject Manager
- Session Orchestrator
- Revision Scheduler
- Progress Tracker
- Goal Manager
- Recommendation Integrator

The Learning Manager coordinates all sub-components.

---

# Learning Manager Responsibilities

Subject & Course Organization

Study Session Scheduling

Progress Tracking

Goal Management

Recommendation Integration

Event Publishing

Cross-Module Coordination

---

# Entity: learning_profile

Purpose

Stores user-level learning configuration and state.

Fields

profile_id

user_id

preferred_study_duration_minutes

preferred_study_time

daily_goal_type (time, sessions, topics)

daily_goal_value

revision_enabled

quiz_enabled

flashcard_daily_limit

ai_tutor_enabled

current_focus_subject_id

created_at

updated_at

---

# Subject Management

Subjects are the top-level organizational unit.

Subject Examples

Mathematics

Physics

Programming

Electronics

Drone Engineering

Embedded Systems

AI & Machine Learning

Research Methodology

Each subject is independent with its own resources.

---

# Entity: subjects

Purpose

Stores subject definitions.

Fields

subject_id

name

description

icon

color

category (academic, professional, personal, research)

status (active, paused, completed, archived)

priority (1-5)

total_study_time_seconds

current_streak_days

longest_streak_days

last_studied_at

created_at

updated_at

---

# Subject Hierarchy

Subject

├── Courses (structured curriculum)

│   ├── Modules

│   └── Chapters

├── Books (reading material)

│   ├── Chapters

│   └── Topics

├── Topics (standalone learning units)

├── Study Sessions (time-based learning records)

├── Notes (subject-specific notes)

├── Quizzes (assessment records)

└── Flashcards (review items)

---

# Subject Status Flow

Active

Currently being studied.

Paused

Temporarily on hold.

Completed

Learning goals achieved.

Archived

No longer active, history preserved.

Users can reactivate paused or archived subjects.

---

# Learning Goals

Goals define what the user wants to achieve.

Goal Types

Time Based (study X hours per week)

Session Based (complete X sessions per week)

Topic Based (master X topics per month)

Course Based (complete course by date)

Exam Based (prepare for exam on date)

Skill Based (reach skill level by date)

---

# Entity: learning_goals

Purpose

Stores learning goals per subject.

Fields

goal_id

subject_id

goal_type

target_value

current_value

unit (hours, sessions, topics, percent)

start_date

target_date

completed_date

status (active, achieved, missed, cancelled)

notes

created_at

---

# Goal Tracking Flow

Goal Created

↓

Progress Updated (per study session)

↓

Progress Check (daily/weekly)

↓

On Track -> Continue

↓

Behind -> AI Suggests Adjustment

↓

Achieved -> Celebrate + New Goal

↓

Missed -> Analyze + Reschedule

---

# Subject Dashboard

Each subject has a dedicated dashboard.

Dashboard Sections

Overview (progress, streak, next review)

Resources (books, courses, topics)

Recent Sessions (last 5 study sessions)

Upcoming Revision (due items)

Performance (quiz scores, mastery level)

AI Recommendations (personalized suggestions)

---

# Subject Quick Actions

Start Study Session

Add Resource (book, course, topic)

Review Due Items

Take Quiz

View Notes

Edit Goals

---

# Subject Search & Filter

Search across all subjects.

Filters

Status (active, paused, completed, archived)

Category

Priority

Last Studied (recent, older)

Performance (high, medium, low)

---

# Bulk Operations

Archive multiple subjects

Export subject data

Reset subject progress

Transfer resources between subjects

---

# Events

Events published to Event Store

learning.subject.created

learning.subject.updated

learning.subject.archived

learning.subject.completed

learning.goal.created

learning.goal.achieved

learning.goal.missed

learning.profile.updated

---

# Summary

The Learning Manager provides centralized orchestration for all learning activities.

Subject Management organizes learning into clear hierarchical structures with goals, progress tracking, and AI-enhanced recommendations.

---

# End of Part 2

Next

Part 3

- Course Management
- Book Management
- Topic Management
- Resource Organization
- Curriculum Planning
