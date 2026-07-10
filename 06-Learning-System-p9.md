# 06 - Learning System

## Part 9

Version: 1.0

Status: Planning

---

# Flashcards System

## Purpose

The Flashcards System provides digital flashcards with spaced repetition for efficient memorization.

Flashcards are auto-generated from learning materials and support rich multimedia content.

---

# Flashcards Architecture

Flashcard Manager
- Card Store
- Deck Manager
- Review Controller
- Spaced Repetition Engine
- Import/Export Handler
- Analytics Tracker

Flashcards are a core memorization tool.

---

# Card Types

Basic (Front & Back)

Standard question-answer format.

Basic (with Reversed)

Both directions (term->definition and definition->term).

Cloze Deletion

Fill in the blank within a sentence.

Image Occlusion

Hide parts of an image for recall.

Type Answer

User types answer instead of self-assessment.

Audio Card

Front plays audio, user recalls.

---

# Entity: flashcards

Purpose

Stores individual flashcard data.

Fields

card_id

deck_id

card_type

front_content (text, markdown, image URL)

back_content

hint (optional)

tags

difficulty (1-5)

easiness_factor

interval_days

repetitions

next_review_date

last_review_date

last_quality

review_count

status (new, learning, reviewing, mastered, suspended)

created_at

---

# Deck Management

Flashcards are organized into decks.

Deck Structure

Subject Deck (one per subject)

├── Topic Sub-decks

├── Book Sub-decks

├── Custom Decks

└── Imported Decks (from Anki, etc.)

Nesting allows flexible organization.

---

# Entity: flashcard_decks

Purpose

Stores deck metadata.

Fields

deck_id

subject_id

name

description

card_count

new_per_day

review_limit_per_day

is_default

parent_deck_id (for nesting)

created_at

---

# Flashcard Review Flow

Open Deck

↓

See Due Cards Count

↓

Start Review

↓

View Front

↓

Think/Recall

↓

Reveal Answer

↓

Self-Assess (Again, Hard, Good, Easy)

↓

Algorithm Updates Schedule

↓

Next Card

↓

Review Complete

↓

Statistics Updated

---

# Review Buttons

Standard spaced repetition buttons.

Again (0)

Forget completely, reset interval.

Hard (2)

Recalled with difficulty, smaller interval increase.

Good (4)

Recalled correctly, standard interval.

Easy (5)

Instant recall, largest interval increase.

Button labels show next review time (e.g., "Good - 6 days").

---

# Auto-Generation

Flashcards are auto-generated from learning materials.

Generation Sources

Notes (key concepts become cards)

Book Highlights (important passages)

Quiz Mistakes (incorrect answers become cards)

AI Extraction (AI identifies flashcard-worthy content)

Import (Anki, CSV, JSON)

---

# Rich Media Support

Cards support multimedia content.

Supported Media

Text (Markdown formatted)

Images (embedded or linked)

Audio (pronunciation, examples)

LaTeX (mathematical formulas)

Code (syntax highlighted code snippets)

Diagrams (Mermaid charts, etc.)

---

# Anki Import/Export

Compatible with Anki format.

Import

.apkg files

.csv files

.txt files

Export

.apkg format

.csv format

All metadata preserved during transfer.

---

# Entity: flashcard_reviews

Purpose

Records individual flashcard reviews.

Fields

review_id

card_id

deck_id

quality (0-5)

response_time_seconds

session_id

scheduled_date

reviewed_date

created_at

---

# Flashcard Statistics

Review metrics and progress tracking.

Metrics

Cards Due Today

Cards Reviewed Today

Mature Cards (interval > 21 days)

Young Cards (interval <= 21 days)

Average Retention Rate

Average Response Time

Reviews Per Day (average)

Card Count Per Deck

---

# Daily Flashcards Workflow

Morning

Check due cards count

Review during free moments

Evening

Complete remaining due cards

Generate new cards from today's learning

Goal

Clear all due cards daily

---

# Flashcards Widget

Desktop widget for quick reviews.

Widget Features

Shows due card count

One-click review start

Quick answer (Good/Hard toggle)

Minimal distraction mode

Widget is optional and configurable.

---

# Events

Events published to Event Store

learning.flashcard.created

learning.flashcard.reviewed

learning.flashcard.mastered

learning.flashcard.deck.created

learning.flashcard.imported

learning.flashcard.exported

learning.flashcard.overdue.alert

---

# Summary

The Flashcards System provides powerful digital flashcards with spaced repetition, auto-generation from learning materials, and Anki-compatible import/export.

Cards support rich media and are integrated with the broader PAIOS learning ecosystem.

---

# End of Part 9

Next

Part 10

- Learning Analytics & Progress Tracking
- Subject Progress
- Time Analytics
- Performance Metrics
- Streak Tracking
- Reports & Insights
