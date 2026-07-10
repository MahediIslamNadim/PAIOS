# 04 - Unified Data Platform

## Part 2

Version: 1.0

Status: Planning

---

# Database Design Principles

Every database object follows consistent design rules.

The goal is long-term maintainability, predictable performance, and compatibility across storage engines.

---

# Naming Conventions

## Tables

Use lowercase snake_case.

Examples

users

study_sessions

knowledge_objects

knowledge_relationships

projects

tasks

calendar_events

audit_logs

event_store

embeddings

---

## Columns

Use lowercase snake_case.

Examples

created_at

updated_at

deleted_at

knowledge_id

project_id

session_duration

reading_progress

---

## Primary Keys

Every table uses

id

Type

UUID

Example

550e8400-e29b-41d4-a716-446655440000

IDs never change after creation.

---

# Foreign Keys

Every relationship uses explicit foreign keys.

Examples

knowledge_id

project_id

study_session_id

user_id

task_id

Foreign key constraints remain enabled.

---

# Required Columns

Every major table includes

id

created_at

updated_at

version

created_by

updated_by

deleted_at (nullable)

status

These columns provide consistency across modules.

---

# Soft Delete

Objects are normally soft deleted.

Example

deleted_at = NULL

↓

Active

deleted_at = timestamp

↓

Deleted

Permanent deletion requires explicit cleanup.

---

# Versioning

Each row contains

version

Every successful update increments the version.

This supports synchronization and optimistic concurrency.

---

# Status Fields

Recommended status values

active

archived

deleted

draft

pending

completed

failed

Status values should be documented for each table.

---

# JSON Columns

Flexible metadata is stored in JSON.

Examples

preferences

ai_metadata

ocr_metadata

plugin_configuration

Unknown fields should never break existing readers.

---

# Constraints

Required constraints

NOT NULL

CHECK

FOREIGN KEY

UNIQUE

DEFAULT

Constraints should protect data integrity whenever possible.

---

# Indexing Rules

Indexes should support

Primary Lookups

Foreign Keys

Search

Sorting

Recent Activity

Relationship Traversal

Unused indexes should be periodically reviewed.

---

# Transactions

Use transactions whenever operations span multiple tables.

Example

Create Study Session

↓

Insert Session

↓

Insert Evidence

↓

Update Statistics

↓

Insert Event

↓

Commit

---

# Repository Contracts

Every repository exposes

Create()

GetById()

Update()

Delete()

Search()

List()

Exists()

Count()

Repositories should not expose SQL syntax.

---

# Query Principles

Prefer

Indexed Queries

Parameterized Queries

Pagination

Batch Operations

Streaming (where appropriate)

Avoid

SELECT *

N+1 Queries

Unbounded Results

String Concatenated SQL

---

# Pagination

Large datasets use pagination.

Supported Strategies

Offset

Cursor

Keyset

The chosen strategy depends on workload.

---

# Audit Support

Important updates generate audit entries.

Examples

Knowledge Modified

Project Updated

Task Completed

Permission Changed

Plugin Installed

Audit creation should be automatic whenever practical.

---

# Repository Layer

Application

↓

Repository Interface

↓

Storage Adapter

↓

SQLite

Future adapters may replace SQLite without changing business logic.

---

# Error Handling

Repositories return structured errors.

Examples

Object Not Found

Duplicate Object

Validation Failed

Permission Denied

Conflict

Storage Failure

Errors should remain implementation-independent.

---

# Migration Safety

Schema changes use versioned migrations.

Migration Process

Validate

↓

Backup

↓

Apply Migration

↓

Verify

↓

Commit

↓

Rollback if Needed

Every migration should be reversible whenever practical.

---

# Summary

Consistent naming, versioning, constraints, repositories, and migration rules ensure that the Unified Data Platform remains maintainable and portable as PAIOS evolves.

---

# End of Part 2

Next

Part 3

- Core Entity Model
- User Schema
- Profile Schema
- Device Schema
- Workspace Schema
- Identity Relationships
