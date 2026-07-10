# 03 - System Architecture

## Part 2

---

# Monorepo Architecture

PAIOS uses a modular monorepo architecture.

The repository is organized by responsibility rather than by technology.

Every directory has a single purpose.

The repository should remain understandable even after years of development.

---

# Repository Structure

```

Personal-AI-Operating-System/

│

├── apps/

│ ├── desktop/

│ ├── web/

│ └── docs/

│

├── packages/

│ ├── ui/

│ ├── shared/

│ ├── auth/

│ ├── learning/

│ ├── knowledge/

│ ├── ai/

│ ├── monitoring/

│ ├── analytics/

│ ├── planner/

│ ├── research/

│ ├── engineering/

│ ├── programming/

│ ├── database/

│ ├── search/

│ ├── events/

│ └── types/

│

├── services/

│ ├── ai-gateway/

│ ├── sync/

│ ├── embedding/

│ ├── search-index/

│ ├── backup/

│ ├── notification/

│ └── scheduler/

│

├── assets/

├── scripts/

├── tools/

├── docs/

├── tests/

├── configs/

└── .github/

```

---

# Applications

## Desktop

Primary application.

Responsibilities

Dashboard

Study

Research

Programming

Engineering

Knowledge

Planner

Settings

Desktop-specific integrations

---

## Web

Optional companion.

Responsibilities

Read-only dashboard

Cloud synchronization

Reports

Remote access

Limited editing

---

## Documentation

Contains

Architecture

API

Database

AI

Developer Guides

Standards

Decision Records

Documentation is treated as part of the product.

---

# Packages

Packages contain reusable modules.

Each package should have one responsibility.

Example

packages/learning

Contains

Study Sessions

Subjects

Courses

Books

Revision

Flashcards

Quiz

Learning Analytics

No UI code should exist here unless explicitly designed as reusable components.

---

# Shared Package

Contains reusable utilities.

Examples

Logger

Date Utilities

Validation

Constants

Error Handling

Configuration

Shared Types

Never place business logic inside shared.

---

# AI Package

Contains

Prompt Templates

Context Builder

Memory Interface

Model Abstraction

AI Utilities

Embeddings

Token Management

The package should not depend on a specific AI provider.

---

# Database Package

Contains

Schema

Migrations

Repositories

Queries

Database Utilities

Seed Data

The rest of the application should interact through repositories or services rather than raw SQL.

---

# Services

Services execute long-running or background operations.

Examples

Embedding Generation

Search Index Updates

Cloud Synchronization

Scheduled Revision

Daily Reports

Notification Delivery

Backup

Each service should be independently deployable in the future if needed.

---

# Naming Convention

Directories

lowercase-with-dashes

Files

kebab-case.ts

Components

PascalCase.tsx

Variables

camelCase

Classes

PascalCase

Constants

UPPER_CASE

Events

dot.notation

Example

study.session.started

learning.topic.mastered

knowledge.object.created

ai.recommendation.generated

---

# Module Structure

Every package follows the same structure.

```

learning/

│

├── domain/

├── application/

├── infrastructure/

├── presentation/

├── events/

├── tests/

├── docs/

└── index.ts

```

Consistency is more important than creativity.

---

# Module Responsibilities

Every module must clearly define

Purpose

Inputs

Outputs

Events Published

Events Consumed

Dependencies

Owner

Documentation

Tests

Future Extensions

---

# Dependency Rules

A module may depend only on

Shared

Contracts

Events

Public Interfaces

A module must never import another module's internal implementation.

---

# Forbidden Dependencies

Learning

must never directly access

AI internals.

Research

must never directly modify

Knowledge Graph storage.

Monitoring

must never directly update

Dashboard.

Instead, modules communicate through services or events.

---

# Configuration

Configuration should be centralized.

Examples

Database

AI Models

Storage

Feature Flags

Paths

Logging

Environment Variables

Secrets

No hardcoded configuration inside modules.

---

# Summary

The repository is organized to support

Independent modules

Clear ownership

Simple navigation

Long-term maintenance

AI-assisted development

---

# End of Part 2

Next

Part 3

- Request Lifecycle
- Event Bus Architecture
- Communication Flow
- AI Gateway
- Plugin System
- Background Workers
