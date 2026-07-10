# 17 - API Architecture

Version: 1.0

Status: Planning

---

# API Overview

## Design Principles

RESTful by Default

REST for CRUD operations.

GraphQL for Complex Queries

GraphQL for dashboards and analytics queries.

Event-Driven for Real-Time

WebSocket / SSE for live updates.

Versioned

All APIs are versioned (v1, v2, etc.).

Secure

JWT authentication, role-based access.

Documented

OpenAPI/Swagger specification.

---

# API Structure

Base URL: /api/v1

## Core Endpoints

Authentication

POST /auth/register

POST /auth/login

POST /auth/refresh

POST /auth/logout

Learning Module

GET/POST/PUT/DELETE /subjects

GET/POST/PUT/DELETE /courses

GET/POST/PUT/DELETE /books

GET/POST /study-sessions

GET/POST/PUT/DELETE /notes

GET/POST /revision-items

GET/POST /quizzes

GET/POST/PUT/DELETE /flashcards

Engineering Module

GET/POST/PUT/DELETE /projects

GET/POST /flight-controllers

GET/POST/PUT/DELETE /components

GET/POST /experiments

Programming Module

GET/POST/PUT/DELETE /repositories

GET/POST /commits

GET/POST/PUT /issues

Productivity Module

GET/POST/PUT /plans

GET/POST/PUT/DELETE /goals

GET/POST/PUT/DELETE /habits

GET/POST /journal-entries

Analytics Module

GET /analytics/dashboard

GET /analytics/reports

GET /analytics/insights

Monitoring (all optional)

POST /monitoring/focus

GET /monitoring/stats

Admin

GET/PUT /admin/settings

GET /admin/health

---

# Authentication

JWT-based authentication.

Access Token: 15-minute expiry

Refresh Token: 7-day expiry, rotate on use

Rate Limiting: 100 req/min per user

---

# Response Format

Standard envelope:

{

"success": true,

"data": {},

"meta": { "page": 1, "total": 100 },

"error": null

}

---

# WebSocket Events

Real-time events via WebSocket.

Connection: /ws

Events: focus.update, session.update, notification, analytics.realtime

---

# Status

Complete

Next Document: 18-Frontend-Architecture.md
