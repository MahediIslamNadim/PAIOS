# 06 - Learning System

## Part 3

Version: 1.0

Status: Planning

---

# Course & Book Management

## Purpose

Course Management handles structured curricula with defined modules, chapters, and completion criteria.

Book Management organizes reading materials, tracks progress chapter-by-chapter, and integrates with the Reading Tracker and PDF Reader.

---

# Course Management Architecture

Course Manager
- Course Store
- Module Organizer
- Chapter Sequencer
- Completion Validator
- Progress Tracker
- Curriculum Planner

Courses provide structured learning paths.

---

# Entity: courses

Purpose

Stores course definitions.

Fields

course_id

subject_id

name

description

provider (university, platform, self-created)

level (beginner, intermediate, advanced, expert)

estimated_duration_hours

total_modules

total_chapters

completion_criteria

certificate_available

status (not_started, in_progress, completed)

enrolled_at

completed_at

rating

created_at

---

# Entity: course_modules

Purpose

Breaks courses into logical modules.

Fields

module_id

course_id

name

description

order_index

total_chapters

estimated_duration_minutes

status (locked, available, in_progress, completed)

completed_at

---

# Entity: course_chapters

Purpose

Individual chapters within course modules.

Fields

chapter_id

module_id

name

description

order_index

content_type (text, video, interactive, quiz)

estimated_duration_minutes

status (locked, available, in_progress, completed, reviewed)

completion_score (0-100)

completed_at

---

# Course Enrollment Flow

Discover Course

↓

View Details

↓

Enroll

↓

Curriculum Loaded

↓

First Module Unlocked

↓

Complete Chapter

↓

Next Chapter Unlocked

↓

Module Complete

↓

Next Module Unlocked

↓

Course Complete

↓

Certificate (optional)

---

# Prerequisite System

Courses and modules can have prerequisites.

Prerequisite Types

Course Prerequisite (complete another course first)

Module Prerequisite (complete previous module)

Topic Prerequisite (master specific topic)

Score Prerequisite (achieve minimum quiz score)

Locked items show prerequisite requirements.

---

# Curriculum Planner

Plan learning paths across multiple courses.

Planner Features

Recommend Course Sequence

Estimated Completion Timeline

Weekly Time Commitment

Prerequisite Validation

Alternative Path Suggestions

AI-Generated Custom Curriculum

---

# Book Management Architecture

Book Manager
- Book Store
- Chapter Organizer
- Reading Progress Tracker
- Annotation Manager
- Bookmark Manager

Books are core learning resources.

---

# Entity: books

Purpose

Stores book metadata and reading state.

Fields

book_id

subject_id

title

author

isbn

page_count

current_page

reading_progress_percent

format (pdf, physical, ebook, audio)

source_path (file path or URL)

cover_image

status (unread, reading, finished, reference)

priority (1-5)

rating

notes_count

highlight_count

started_at

finished_at

created_at

---

# Entity: book_chapters

Purpose

Individual chapters within a book.

Fields

chapter_id

book_id

title

page_start

page_end

estimated_reading_minutes

status (unread, reading, completed, reviewed)

notes_count

highlight_count

completed_at

---

# Chapter Completion Flow

User Reads Chapter

↓

Mark as Read (manual)

↓

OR Auto-Detect (PDF page tracking)

↓

Progress Updated

↓

Notes Auto-Saved

↓

Knowledge Graph Updated

↓

Revision Scheduled

↓

Next Chapter Unlocked

---

# Multiple Reading Formats

PDF Reader (Integrated)

Native PDF viewer with annotation support.

Physical Books (Manual Tracking)

Manual page tracking with timer.

E-Books (Future)

EPUB/MOBI support.

Audiobooks (Future)

Sync with audio playback.

Web Articles (Integrated)

Read-later and tracking.

---

# Annotations & Highlights

Users can annotate books.

Annotation Types

Highlight (selected text)

Note (user comment on selection)

Bookmark (page marker)

Question (mark for later review)

Summary (chapter summary)

---

# Entity: annotations

Purpose

Stores user annotations on books.

Fields

annotation_id

book_id

chapter_id

annotation_type (highlight, note, bookmark, question, summary)

page_number

selected_text

user_note

color

tags

created_at

---

# Book Collection Management

Organize books into collections.

Collection Types

Currently Reading

Want to Read

Completed

Reference

Favorites

Custom Collections

Books can belong to multiple collections.

---

# Reading Goals

Set reading targets.

Goal Types

Pages Per Day

Chapters Per Week

Books Per Month

Minutes Per Day

Goals are tracked and displayed on dashboard.

---

# Events

Events published to Event Store

learning.course.enrolled

learning.course.module.completed

learning.course.chapter.completed

learning.course.completed

learning.book.added

learning.book.chapter.completed

learning.book.completed

learning.annotation.created

learning.bookmark.added

---

# Summary

Course Management provides structured learning paths with prerequisites and progress tracking.

Book Management organizes reading materials with chapter-level tracking, annotations, and multiple format support.

Both systems feed into the Knowledge Graph and AI Recommendation Engine.

---

# End of Part 3

Next

Part 4

- Study Sessions & Timer
- Session Types
- Focus Tracking
- Break Management
- Session Analytics
- Pomodoro Integration
