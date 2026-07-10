# 04 - Unified Data Platform

## Part 1

Version: 1.0

Status: Planning

---

# Purpose

The Unified Data Platform (UDP) is the foundational data architecture of PAIOS.

It provides a unified interface for storing, retrieving, indexing, searching, relating, and versioning every piece of user knowledge.

The platform hides implementation details behind stable interfaces.

Business modules never communicate directly with storage engines.

---

# Design Goals

The platform should

Remain offline-first

Scale incrementally

Support multiple storage engines

Enable AI-native retrieval

Maintain strong consistency where required

Support future migrations

Preserve knowledge history

Optimize read performance

---

# Data Philosophy

PAIOS stores knowledge, not files.

Every stored entity is represented as structured information.

Files are treated as attachments to knowledge rather than the primary asset.

Knowledge always has higher priority than storage format.

---

# Data Architecture

Application

↓

Repository Layer

↓

Unified Data Platform

↓

Storage Adapters

↓

Physical Storage

Storage technologies are replaceable.

Business logic remains unchanged.

---

# Data Categories

Structured Data

Knowledge Objects

Relationships

Embeddings

Search Index

Events

Time-Series Metrics

Attachments

AI Cache

Audit Logs

Configuration

Each category has different storage requirements.

---

# Storage Abstraction

Applications never access databases directly.

Instead they use repositories.

Example

KnowledgeRepository

StudyRepository

ProjectRepository

TaskRepository

CalendarRepository

EmbeddingRepository

AuditRepository

Repositories expose domain-focused operations.

---

# Repository Pattern

Repositories define

Create

Read

Update

Delete

Search

Version History

Bulk Operations

Transaction Support

Implementations may differ by storage engine.

---

# Polyglot Persistence

Different data types may use different storage engines.

Examples

Relational Data

SQLite

Knowledge Graph

Graph Adapter

Embeddings

Vector Adapter

Search

FTS Adapter

Attachments

File Storage

Events

Event Store

The rest of the application interacts through common interfaces.

---

# Initial Storage Strategy (v1)

Primary Database

SQLite

Search

SQLite FTS5

Attachments

Local Filesystem

Embeddings

SQLite Vector Extension (or compatible adapter)

Events

SQLite Tables or JSON Event Store

The architecture allows replacement in future versions.

---

# Future Storage Strategy

Possible Future Technologies

PostgreSQL

Neo4j

Qdrant

Milvus

OpenSearch

S3-Compatible Storage

These are implementation details rather than architectural requirements.

---

# Data Ownership

Every module owns its data.

Examples

Learning Module

Study Sessions

Knowledge Module

Knowledge Objects

Planner

Tasks

AI Runtime

Inference Metadata

Monitoring

Observation Evidence

Other modules access data through repositories or events.

---

# Transactions

Transactions are required for operations that modify multiple related objects.

Examples

Create Knowledge Object

↓

Create Relationships

↓

Create Event

↓

Update Search Index Queue

↓

Commit

If any step fails,

the transaction should roll back whenever practical.

---

# Identifiers

Every important object receives a globally unique identifier.

Examples

Knowledge Object ID

Study Session ID

Project ID

Task ID

Embedding ID

Relationship ID

Audit Entry ID

IDs remain stable throughout the object's lifetime.

---

# Time Management

Every object stores

Created Time

Updated Time

Version

Optional Deleted Time

All timestamps should use UTC internally.

User interfaces convert to local time.

---

# Data Lifecycle

Create

↓

Validate

↓

Persist

↓

Index

↓

Link

↓

Analyze

↓

Recommend

↓

Archive

↓

Backup

↓

Restore

Each stage publishes observable events.

---

# Summary

The Unified Data Platform separates business logic from storage implementation.

Repositories provide stable interfaces while storage engines remain replaceable.

The architecture supports gradual evolution from a simple local database to a distributed multi-engine platform.

---

# End of Part 1

Next

Part 2

- SQLite Schema Strategy
- Naming Conventions
- Table Design Rules
- Primary Keys
- Foreign Keys
- Constraints
- Repository Contracts
