# 06 - Learning System

## Part 8

Version: 1.0

Status: Planning

---

# Quiz Engine

## Purpose

The Quiz Engine creates, administers, and evaluates quizzes to assess learning comprehension and reinforce knowledge retention.

Quizzes are auto-generated from learning materials and can be custom-created by users.

---

# Quiz Architecture

Quiz Engine
- Question Bank
- Quiz Generator
- Quiz Administrator
- Grading Engine
- Performance Analyzer
- Feedback Provider

Quizzes serve both assessment and learning purposes.

---

# Quiz Types

Practice Quiz

Low-stakes, unlimited attempts, immediate feedback.

Topic Quiz

Covers specific topic or chapter.

Subject Quiz

Covers entire subject scope.

Revision Quiz

Based on due revision items.

Exam Simulation

Timed, scored, mimics real exam conditions.

Custom Quiz

User-defined scope and parameters.

---

# Question Types

Multiple Choice

Single correct answer from options.

Multiple Answer

Multiple correct answers from options.

True/False

Binary choice question.

Fill in the Blank

Text input for missing word/phrase.

Short Answer

Brief written response.

Matching

Match items from two columns.

Ordering

Arrange items in correct sequence.

Essay

Extended written response (AI-assisted grading).

Code Challenge

Write or complete code snippet.

Formula Entry

Mathematical expression input.

---

# Entity: question_bank

Purpose

Stores all quiz questions.

Fields

question_id

subject_id

topic

question_type

question_text

options (JSON array for MCQs)

correct_answer

explanation

difficulty (1-5)

tags

source (auto_generated, user_created, imported)

usage_count

correct_count

incorrect_count

created_at

---

# Quiz Generation

Quizzes can be generated automatically.

Generation Sources

From Notes (AI extracts questions from notes)

From Book Chapters (key concepts become questions)

From Revision Items (due items become quiz)

From Mistakes (questions related to past errors)

From Topic (all topics in subject)

From Custom Criteria (user defines scope)

---

# AI Question Generation

AI generates questions from learning materials.

Generation Process

Select Source Material

↓

AI Analyzes Content

↓

Extract Key Concepts

↓

Generate Questions

↓

Validate Questions

↓

Present to User

↓

User Accepts/Edits/Rejects

AI-generated questions improve with user feedback.

---

# Quiz Administration

Taking a quiz follows a structured flow.

Quiz Flow

Start Quiz

↓

Read Question

↓

Select/Enter Answer

↓

Confirm

↓

Next Question

↓

Complete All Questions

↓

Review Answers

↓

Submit

↓

Grading

↓

Results Displayed

---

# Quiz Timer

Quizzes can have time limits.

Timer Features

Countdown Display

Time Per Question (configurable)

Auto-Submit on Timeout

Pause (for practice quizzes only)

Time Remaining Warnings

---

# Grading Engine

Automatic grading for objective questions.

Grading Rules

Multiple Choice: Exact match

Multiple Answer: Partial credit option

True/False: Exact match

Fill Blank: Case-insensitive, trim whitespace

Matching: All pairs correct

Ordering: Exact sequence

Short Answer: AI-assisted similarity matching

Essay: AI-assisted rubric grading (optional)

---

# Scoring

Score calculation methods.

Basic Score

(Correct Answers / Total Questions) x 100

Weighted Score

Questions have different weight values.

Partial Credit

Multiple answer questions can award partial points.

Penalty Score

Incorrect answers deduct points (optional).

---

# Entity: quiz_attempts

Purpose

Records quiz attempts and results.

Fields

attempt_id

quiz_id (or generated_quiz_id)

subject_id

question_count

correct_count

incorrect_count

skipped_count

score_percent

time_taken_seconds

completed

answers (JSON array of user answers)

created_at

---

# Post-Quiz Review

After completing a quiz, users review results.

Review Features

Correct/Incorrect Indicators

Explanation for Each Question

Score Breakdown by Topic

Mistake Analysis

Recommended Next Steps

Link to Relevant Notes/Resources

---

# Quiz Analytics

Comprehensive quiz performance tracking.

Metrics

Average Score (overall and per subject)

Score Trend (improvement over time)

Weak Topics (lowest scoring areas)

Strong Topics (highest scoring areas)

Average Time Per Question

Common Mistakes

Question Difficulty Distribution

---

# Mistake Tracking

Every mistake is tracked for future learning.

Mistake Data

Question

User's Answer

Correct Answer

Topic

Date

Quiz Type

Mistakes automatically become revision items.

---

# Entity: mistakes

Purpose

Stores user mistakes for analysis.

Fields

mistake_id

question_id

subject_id

user_answer

correct_answer

topic

difficulty

quiz_type

attempt_id

created_at

Resolved (linked to revision item)

---

# Spaced Repetition Integration

Quiz performance feeds into the Revision Engine.

Integration Flow

Quiz Completed

↓

Incorrect Answers Identified

↓

Revision Items Created

↓

Scheduled for Review

↓

Future Quiz Includes Similar Questions

↓

Progress Tracked

---

# Events

Events published to Event Store

learning.quiz.generated

learning.quiz.started

learning.quiz.completed

learning.quiz.question.answered

learning.quiz.graded

learning.quiz.mistake.tracked

learning.quiz.analytics.updated

---

# Summary

The Quiz Engine provides comprehensive assessment capabilities with auto-generation, multiple question types, intelligent grading, and deep performance analytics.

Quiz results directly feed into the Revision Engine and Knowledge Graph.

---

# End of Part 8

Next

Part 9

- Flashcards System
- Card Types
- Deck Management
- Spaced Repetition for Flashcards
- Import/Export (Anki compatible)
- Flashcard Analytics
