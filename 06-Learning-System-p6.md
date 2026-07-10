# 06 - Learning System

## Part 6

Version: 1.0

Status: Planning

---

# Reading Tracker & PDF Reader

## Purpose

The Reading Tracker monitors all reading activities across books, documents, and articles.

The PDF Reader provides an integrated reading experience with annotation, OCR, and AI-powered analysis.

---

# Reading Tracker Architecture

Reading Tracker
- Reading Session Manager
- Progress Calculator
- Reading Speed Analyzer
- Goal Tracker
- Reading History

Reading is a primary learning activity in PAIOS.

---

# Reading Session

A reading session tracks continuous reading.

Session Data

Start Time

End Time

Duration

Pages Read

Reading Speed (pages/hour)

Focus Score

Resource (book, PDF, article, etc.)

Annotations Created

---

# Entity: reading_sessions

Purpose

Records individual reading sessions.

Fields

session_id

book_id (or document_id)

chapter_id (optional)

page_start

page_end

total_pages_read

duration_seconds

reading_speed_pages_per_hour

focus_score

annotation_count

session_type (focused, casual, review)

completed

created_at

---

# Reading Progress Tracking

Progress tracked at multiple levels.

Book Level

Percentage complete

Pages remaining

Estimated time to finish

Chapter Level

Chapter status (unread, reading, completed)

Pages per chapter

Chapter difficulty

Daily Level

Pages read today

Reading goal progress

Streak (consecutive reading days)

---

# Reading Statistics

Comprehensive reading analytics.

Metrics

Total Pages Read

Total Reading Time

Average Reading Speed

Books Completed

Reading Streak (days)

Most Read Subjects

Reading Time Distribution

Reading Speed Trend

---

# PDF Reader Integration

Built-in PDF reader with learning features.

PDF Reader Features

Native PDF Rendering

Page Navigation (scroll, thumbnails, search)

Text Selection & Highlighting

Annotation (notes, highlights, bookmarks)

OCR (optical character recognition for scanned PDFs)

Text-to-Speech (optional)

AI Summarization

Chapter Detection (auto-detect chapters)

Bookmark Sync

---

# OCR Integration

Scanned PDFs are processed with OCR.

OCR Pipeline

PDF Page Image

↓

Text Region Detection

↓

OCR Engine (Tesseract)

↓

Text Extraction

↓

Layout Analysis

↓

Searchable Text

↓

User Can Annotate

OCR results improve over time with corrections.

---

# PDF Annotation System

Annotate PDFs with rich tools.

Annotation Types

Text Highlight (multiple colors)

Underline

Strike-through

Note (attached to position)

Bookmark (save page location)

Drawing (freehand, shapes)

Stamp (approve, review, etc.)

All annotations are searchable.

---

# Entity: pdf_annotations

Purpose

Stores PDF annotations.

Fields

annotation_id

document_id

page_number

annotation_type

coordinates (position data)

content (text, note, drawing data)

color

created_at

All annotations sync with the Knowledge Graph.

---

# Speed Reading Tools

Built-in speed reading aids.

Tools

RSVP (Rapid Serial Visual Presentation)

Focus Mode (dim non-essential areas)

Pacing Guide (visual guide line)

Word Highlighting (highlight as you read)

Reading Speed Trainer (gradually increase speed)

---

# Reading Goals

Set and track reading targets.

Goal Types

Daily Pages

Daily Minutes

Weekly Books

Monthly Pages

Goal examples

Read 20 pages daily

Read 30 minutes daily

Complete 2 books per month

---

# Read-Later System

Save articles and documents to read later.

Read-Later Features

Browser Extension (save web articles)

Share Target (from mobile/desktop)

Auto-Tagging (AI categorizes saved items)

Priority Queue (mark items as high priority)

Offline Download

Reading Progress Sync

---

# Reading Reminders

Gentle reminders to maintain reading habits.

Reminder Types

Daily Reading Goal Reminder

Streak Protection Reminder

Unread Book Reminder

Overdue Reading Session

Custom Schedule

---

# Events

Events published to Event Store

learning.reading.session.started

learning.reading.session.completed

learning.reading.page.completed

learning.reading.chapter.completed

learning.reading.book.completed

learning.reading.annotation.created

learning.reading.goal.achieved

learning.reading.speed.updated

---

# Summary

The Reading Tracker provides comprehensive monitoring of all reading activities.

The PDF Reader delivers an integrated reading experience with powerful annotation, OCR, and AI features.

Together they ensure no reading activity goes untracked.

---

# End of Part 6

Next

Part 7

- Revision Engine & Spaced Repetition
- SM-2 Algorithm
- Scheduling Logic
- Due Item Management
- Review Sessions
- Performance Tracking
