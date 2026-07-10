# 19 - Backend Architecture

Version: 1.0

Status: Planning

---

# Backend Overview

## Stack

Framework: NestJS

Language: TypeScript

ORM: Prisma

Database: PostgreSQL + pgvector

Cache: Redis

Validation: class-validator + class-transformer

Auth: JWT + Passport

API: REST (primary) + GraphQL (analytics)

Documentation: Swagger/OpenAPI

---

# Directory Structure

src/

├── modules/

│   ├── auth/ authentication, authorization

│   ├── users/ user management

│   ├── learning/ subjects, courses, books, sessions, notes, revision, quizzes, flashcards

│   ├── engineering/ projects, flight-controller, components, experiments, firmware

│   ├── programming/ repositories, commits, issues, analytics

│   ├── research/ papers, citations, experiments, datasets

│   ├── productivity/ plans, goals, habits, journal

│   ├── monitoring/ focus, presence, activity, fatigue

│   ├── analytics/ dashboards, reports, insights, predictions

│   ├── health/ sleep, exercise, mood

│   ├── career/ portfolio, cv, interviews

│   ├── startup/ ideas, roadmap, feedback

│   └── admin/ system configuration

├── common/

│   ├── guards/ auth guards, role guards

│   ├── interceptors/ logging, transformation

│   ├── filters/ exception filters

│   ├── pipes/ validation pipes

│   └── decorators/ custom decorators

├── config/ configuration files

└── prisma/ Prisma schema and migrations

---

# Module Structure (NestJS)

Each module follows:

module.ts (NestJS module definition)

controller.ts (REST endpoints)

service.ts (business logic)

dto/ (data transfer objects)

entity/ (database entities - Prisma)

---

# Key Patterns

Repository Pattern

Prisma service per module.

Dependency Injection

NestJS DI for all services.

Event-Driven

EventEmitter for internal module communication.

CQRS (Future)

For complex analytics queries.

---

# Authentication

JWT access + refresh tokens.

Passport strategies (JWT, local).

Role-based guard (user, admin).

Rate limiting per endpoint.

---

# API Documentation

Swagger at /api/docs.

Auto-generated from NestJS decorators.

---

# Status

Complete

Next Document: 20-Desktop-Architecture.md
