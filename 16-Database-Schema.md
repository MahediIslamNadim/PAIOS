# 16 - Database Schema Design

Version: 1.0

Status: Planning

---

# Database Schema Overview

## Purpose

This document defines the complete database schema for PAIOS.

It covers all entities across all modules with relationships, indexes, and data types.

---

# Technology

Primary Database

PostgreSQL (relational data, ACID compliance)

Vector Database

pgvector extension (embeddings, semantic search)

Cache

Redis (session cache, metrics cache)

File Storage

Local filesystem (documents, images, attachments)

---

# Schema Principles

Normalized Until Necessary

Standard normalization, denormalize only for performance.

UUID Primary Keys

All primary keys use UUID v4.

Timestamps

Every table has created_at and updated_at.

Soft Deletes

Records are soft-deleted unless data privacy requires hard delete.

JSONB for Flexible Data

Variable schema fields use JSONB.

Indexes on Foreign Keys

All foreign keys indexed.

---

# Core Tables

## users

id UUID PK

email VARCHAR(255) UNIQUE

password_hash VARCHAR(255)

name VARCHAR(255)

preferred_language VARCHAR(10) DEFAULT 'en'

timezone VARCHAR(50)

settings JSONB

email_verified BOOLEAN DEFAULT false

is_active BOOLEAN DEFAULT true

last_login_at TIMESTAMPTZ

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

deleted_at TIMESTAMPTZ

---

## learning_profile

id UUID PK

user_id UUID FK -> users.id

preferred_study_duration_minutes INT DEFAULT 45

preferred_study_time TIME

daily_goal_type VARCHAR(20)

daily_goal_value INT

revision_enabled BOOLEAN DEFAULT true

quiz_enabled BOOLEAN DEFAULT true

flashcard_daily_limit INT DEFAULT 20

ai_tutor_enabled BOOLEAN DEFAULT true

current_focus_subject_id UUID FK -> subjects.id

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

---

## subjects

id UUID PK

user_id UUID FK -> users.id

name VARCHAR(255)

description TEXT

icon VARCHAR(50)

color VARCHAR(7)

category VARCHAR(50)

status VARCHAR(20) DEFAULT 'active'

priority INT DEFAULT 3

total_study_time_seconds BIGINT DEFAULT 0

current_streak_days INT DEFAULT 0

longest_streak_days INT DEFAULT 0

last_studied_at TIMESTAMPTZ

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

deleted_at TIMESTAMPTZ

---

## courses

id UUID PK

subject_id UUID FK -> subjects.id

name VARCHAR(255)

description TEXT

provider VARCHAR(100)

level VARCHAR(20)

estimated_duration_hours DECIMAL(6,1)

total_modules INT

total_chapters INT

completion_criteria TEXT

status VARCHAR(20) DEFAULT 'not_started'

enrolled_at TIMESTAMPTZ

completed_at TIMESTAMPTZ

rating SMALLINT

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

---

## course_modules

id UUID PK

course_id UUID FK -> courses.id

name VARCHAR(255)

description TEXT

order_index INT

total_chapters INT

estimated_duration_minutes INT

status VARCHAR(20) DEFAULT 'locked'

completed_at TIMESTAMPTZ

created_at TIMESTAMPTZ

---

## course_chapters

id UUID PK

module_id UUID FK -> course_modules.id

name VARCHAR(255)

description TEXT

order_index INT

content_type VARCHAR(20)

estimated_duration_minutes INT

status VARCHAR(20) DEFAULT 'locked'

completion_score SMALLINT

completed_at TIMESTAMPTZ

created_at TIMESTAMPTZ

---

## books

id UUID PK

subject_id UUID FK -> subjects.id

title VARCHAR(255)

author VARCHAR(255)

isbn VARCHAR(20)

page_count INT

current_page INT DEFAULT 0

reading_progress_percent DECIMAL(5,2) DEFAULT 0

format VARCHAR(20)

source_path TEXT

status VARCHAR(20) DEFAULT 'unread'

priority INT DEFAULT 3

rating SMALLINT

notes_count INT DEFAULT 0

highlight_count INT DEFAULT 0

started_at TIMESTAMPTZ

finished_at TIMESTAMPTZ

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

---

## book_chapters

id UUID PK

book_id UUID FK -> books.id

title VARCHAR(255)

page_start INT

page_end INT

estimated_reading_minutes INT

status VARCHAR(20) DEFAULT 'unread'

notes_count INT DEFAULT 0

highlight_count INT DEFAULT 0

completed_at TIMESTAMPTZ

created_at TIMESTAMPTZ

---

## study_sessions

id UUID PK

user_id UUID FK -> users.id

subject_id UUID FK -> subjects.id

resource_type VARCHAR(30)

resource_id UUID

session_type VARCHAR(30)

start_time TIMESTAMPTZ

end_time TIMESTAMPTZ

duration_seconds INT

effective_duration_seconds INT

focus_score SMALLINT

energy_level SMALLINT

note_count INT DEFAULT 0

quiz_score DECIMAL(5,2)

tags JSONB

status VARCHAR(20)

created_at TIMESTAMPTZ

INDEX idx_study_sessions_user_date (user_id, start_time)

INDEX idx_study_sessions_subject (subject_id)

---

## notes

id UUID PK

user_id UUID FK -> users.id

subject_id UUID FK -> subjects.id

note_type VARCHAR(30)

title VARCHAR(255)

content TEXT

plain_text_content TEXT

resource_type VARCHAR(30)

resource_id UUID

tags JSONB

importance SMALLINT DEFAULT 3

ai_summary TEXT

character_count INT

word_count INT

is_archived BOOLEAN DEFAULT false

is_favorite BOOLEAN DEFAULT false

source_url TEXT

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

deleted_at TIMESTAMPTZ

FULLTEXT INDEX idx_notes_search (plain_text_content)

---

## revision_items

id UUID PK

user_id UUID FK -> users.id

subject_id UUID FK -> subjects.id

resource_type VARCHAR(30)

resource_id UUID

easiness_factor DECIMAL(4,2) DEFAULT 2.5

interval_days INT DEFAULT 0

repetitions INT DEFAULT 0

next_review_date DATE

last_review_date DATE

last_quality SMALLINT

review_count INT DEFAULT 0

status VARCHAR(20) DEFAULT 'new'

created_at TIMESTAMPTZ

INDEX idx_revision_due (user_id, next_review_date, status)

---

## quiz_attempts

id UUID PK

user_id UUID FK -> users.id

subject_id UUID FK -> subjects.id

quiz_id UUID

question_count INT

correct_count INT

incorrect_count INT

skipped_count INT

score_percent DECIMAL(5,2)

time_taken_seconds INT

answers JSONB

completed BOOLEAN DEFAULT true

created_at TIMESTAMPTZ

---

## flashcards

id UUID PK

user_id UUID FK -> users.id

deck_id UUID FK -> flashcard_decks.id

card_type VARCHAR(20)

front_content TEXT

back_content TEXT

hint TEXT

tags JSONB

difficulty SMALLINT DEFAULT 3

easiness_factor DECIMAL(4,2) DEFAULT 2.5

interval_days INT DEFAULT 0

repetitions INT DEFAULT 0

next_review_date DATE

last_review_date DATE

last_quality SMALLINT

review_count INT DEFAULT 0

status VARCHAR(20) DEFAULT 'new'

created_at TIMESTAMPTZ

INDEX idx_flashcard_due (user_id, next_review_date, status)

---

## flashcard_decks

id UUID PK

user_id UUID FK -> users.id

subject_id UUID FK -> subjects.id

name VARCHAR(255)

description TEXT

card_count INT DEFAULT 0

new_per_day INT DEFAULT 20

review_limit_per_day INT DEFAULT 100

is_default BOOLEAN DEFAULT false

parent_deck_id UUID FK -> flashcard_decks.id

created_at TIMESTAMPTZ

---

## research_papers

id UUID PK

user_id UUID FK -> users.id

title VARCHAR(500)

authors JSONB

abstract TEXT

publication VARCHAR(200)

year SMALLINT

doi VARCHAR(100)

arxiv_id VARCHAR(20)

pdf_url TEXT

local_file_path TEXT

pages INT

keywords JSONB

collections JSONB

status VARCHAR(20) DEFAULT 'unread'

rating SMALLINT

importance SMALLINT

reading_progress_percent DECIMAL(5,2) DEFAULT 0

notes_count INT DEFAULT 0

highlight_count INT DEFAULT 0

citation_count INT DEFAULT 0

created_at TIMESTAMPTZ

updated_at TIMESTAMPTZ

FULLTEXT INDEX idx_papers_search (title, abstract)

---

## references (citations)

id UUID PK

user_id UUID FK -> users.id

cite_key VARCHAR(100) UNIQUE

reference_type VARCHAR(30)

title VARCHAR(500)

authors JSONB

year SMALLINT

journal VARCHAR(200)

volume VARCHAR(20)

issue VARCHAR(20)

pages VARCHAR(30)

doi VARCHAR(100)

url TEXT

arxiv_id VARCHAR(20)

isbn VARCHAR(20)

publisher VARCHAR(200)

keywords JSONB

attachments JSONB

created_at TIMESTAMPTZ

---

## engineering_projects

id UUID PK

user_id UUID FK -> users.id

name VARCHAR(255)

description TEXT

project_type VARCHAR(30)

status VARCHAR(20) DEFAULT 'planning'

difficulty VARCHAR(20)

current_phase VARCHAR(50)

github_repository TEXT

hardware_platform VARCHAR(100)

microcontroller VARCHAR(100)

start_date DATE

target_completion_date DATE

completed_date DATE

tags JSONB

created_at TIMESTAMPTZ

---

## flight_controllers

id UUID PK

project_id UUID FK -> engineering_projects.id

name VARCHAR(255)

platform VARCHAR(30)

firmware_version VARCHAR(20)

board_type VARCHAR(100)

microcontroller VARCHAR(100)

sensor_config JSONB

pid_parameters JSONB

calibration_data JSONB

rc_config JSONB

telemetry_config JSONB

safety_config JSONB

last_flashed TIMESTAMPTZ

created_at TIMESTAMPTZ

---

## components (inventory)

id UUID PK

user_id UUID FK -> users.id

category VARCHAR(50)

subcategory VARCHAR(50)

part_number VARCHAR(100)

manufacturer VARCHAR(100)

description TEXT

package VARCHAR(50)

specifications JSONB

datasheet_url TEXT

supplier VARCHAR(100)

supplier_part_number VARCHAR(100)

unit_cost DECIMAL(10,2)

currency VARCHAR(3)

quantity_on_hand INT DEFAULT 0

minimum_stock_level INT DEFAULT 0

location VARCHAR(100)

notes TEXT

tags JSONB

created_at TIMESTAMPTZ

INDEX idx_components_search (part_number, manufacturer)

---

## firmware_projects

id UUID PK

project_id UUID FK -> engineering_projects.id

name VARCHAR(255)

platform VARCHAR(30)

microcontroller VARCHAR(100)

build_system VARCHAR(30)

source_path TEXT

target_board VARCHAR(100)

firmware_version VARCHAR(20)

build_status VARCHAR(20)

hex_path TEXT

last_build_time TIMESTAMPTZ

last_flash_time TIMESTAMPTZ

created_at TIMESTAMPTZ

---

## programming_projects

id UUID PK

user_id UUID FK -> users.id

name VARCHAR(255)

description TEXT

language VARCHAR(50)

framework VARCHAR(100)

project_type VARCHAR(30)

repository_url TEXT

local_path TEXT

build_system VARCHAR(30)

status VARCHAR(20) DEFAULT 'active'

total_commits INT DEFAULT 0

total_branches INT DEFAULT 0

total_issues_open INT DEFAULT 0

total_issues_closed INT DEFAULT 0

last_commit_at TIMESTAMPTZ

created_at TIMESTAMPTZ

---

## git_repositories

id UUID PK

project_id UUID FK -> programming_projects.id

local_path TEXT

remote_url TEXT

current_branch VARCHAR(100)

total_commits INT DEFAULT 0

total_branches INT DEFAULT 0

total_tags INT DEFAULT 0

last_fetch_at TIMESTAMPTZ

last_push_at TIMESTAMPTZ

status VARCHAR(20) DEFAULT 'clean'

created_at TIMESTAMPTZ

---

## issues

id UUID PK

project_id UUID FK -> programming_projects.id

title VARCHAR(255)

description TEXT

type VARCHAR(20)

priority VARCHAR(10)

severity VARCHAR(10)

status VARCHAR(20)

assignee_id UUID FK -> users.id

labels JSONB

milestone_id UUID

due_date DATE

estimated_hours DECIMAL(6,1)

actual_hours DECIMAL(6,1)

linked_commits JSONB

linked_pull_requests JSONB

created_at TIMESTAMPTZ

closed_at TIMESTAMPTZ

---

## plans

id UUID PK

user_id UUID FK -> users.id

plan_type VARCHAR(20)

date_range_start DATE

date_range_end DATE

title VARCHAR(255)

description TEXT

priorities JSONB

tasks JSONB

time_blocks JSONB

notes TEXT

status VARCHAR(20) DEFAULT 'draft'

created_at TIMESTAMPTZ

---

## goals

id UUID PK

user_id UUID FK -> users.id

parent_goal_id UUID FK -> goals.id

title VARCHAR(255)

description TEXT

goal_type VARCHAR(30)

category VARCHAR(50)

start_date DATE

target_date DATE

completed_date DATE

status VARCHAR(20) DEFAULT 'active'

progress_percent DECIMAL(5,2) DEFAULT 0

key_results JSONB

metrics JSONB

tags JSONB

created_at TIMESTAMPTZ

---

## habits

id UUID PK

user_id UUID FK -> users.id

name VARCHAR(255)

description TEXT

frequency VARCHAR(20)

frequency_detail VARCHAR(50)

preferred_time TIME

category VARCHAR(50)

streak_current INT DEFAULT 0

streak_longest INT DEFAULT 0

total_completions INT DEFAULT 0

completion_dates JSONB

reminder_enabled BOOLEAN DEFAULT false

reminder_time TIME

status VARCHAR(20) DEFAULT 'active'

created_at TIMESTAMPTZ

---

## journal_entries

id UUID PK

user_id UUID FK -> users.id

journal_type VARCHAR(30)

date DATE

title VARCHAR(255)

content TEXT

mood SMALLINT

energy_level SMALLINT

tags JSONB

prompt_used TEXT

linked_goals JSONB

linked_tasks JSONB

is_favorite BOOLEAN DEFAULT false

created_at TIMESTAMPTZ

---

## focus_records

id UUID PK

user_id UUID FK -> users.id

timestamp TIMESTAMPTZ

focus_score SMALLINT

focus_zone VARCHAR(20)

session_id UUID

gaze_score SMALLINT

keyboard_score SMALLINT

mouse_score SMALLINT

reading_score SMALLINT

presence_score SMALLINT

duration_seconds INT

created_at TIMESTAMPTZ

INDEX idx_focus_user_time (user_id, timestamp)

---

## health_records

id UUID PK

user_id UUID FK -> users.id

date DATE UNIQUE

sleep_hours DECIMAL(4,1)

sleep_quality SMALLINT

water_intake_glasses SMALLINT

exercise_minutes INT

exercise_type VARCHAR(50)

mood SMALLINT

energy_level SMALLINT

stress_level SMALLINT

notes TEXT

created_at TIMESTAMPTZ

---

## knowledge_graph_edges

id UUID PK

source_id UUID

source_type VARCHAR(50)

target_id UUID

target_type VARCHAR(50)

relationship_type VARCHAR(50)

weight DECIMAL(5,2) DEFAULT 1.0

metadata JSONB

created_at TIMESTAMPTZ

INDEX idx_kg_source (source_id, source_type)

INDEX idx_kg_target (target_id, target_type)

---

## events (event store)

id UUID PK

event_type VARCHAR(100)

source_module VARCHAR(50)

source_id UUID

aggregate_type VARCHAR(50)

aggregate_id UUID

payload JSONB

metadata JSONB

occurred_at TIMESTAMPTZ

INDEX idx_events_type_time (event_type, occurred_at)

INDEX idx_events_aggregate (aggregate_type, aggregate_id)

---

## ai_interactions

id UUID PK

user_id UUID FK -> users.id

session_id UUID

interaction_type VARCHAR(30)

model_id VARCHAR(100)

prompt_tokens INT

completion_tokens INT

total_tokens INT

cost DECIMAL(10,6)

latency_ms INT

user_rating SMALLINT

helpful BOOLEAN

created_at TIMESTAMPTZ

---

## audit_log

id UUID PK

timestamp TIMESTAMPTZ

session_id UUID

agent_id UUID

user_id UUID

action_type VARCHAR(50)

resource_type VARCHAR(50)

resource_id UUID

action_details JSONB

ip_address VARCHAR(45)

status VARCHAR(20)

checksum VARCHAR(64)

INDEX idx_audit_time (timestamp)

INDEX idx_audit_user (user_id)

---

# End of Database Schema

Status

Complete

Next Document

17-API-Architecture.md
