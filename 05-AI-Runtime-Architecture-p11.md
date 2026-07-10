# 05 - AI Runtime Architecture

## Part 11

Version: 1.0

Status: Planning

---

# MCP Session Manager & Resource Discovery

## Purpose

The MCP Session Manager governs the lifecycle, state, and persistence of all AI agent sessions within PAIOS.

The Resource Discovery Protocol enables agents to dynamically discover, access, and interact with platform resources.

---

# Session Manager Architecture

Session Manager
- Session Factory
- Session Store
- Session State Machine
- Session Validator
- Session Scheduler
- Session Monitor

Each component operates independently.

---

# Session Factory

Creates new sessions.

Responsibilities

Generate Unique Session ID

Set Initial State

Assign Permission Scope

Configure Timeout

Attach Agent Context

Initialize Resource Access List

Initialize Tool Access List

Publish session.created Event

---

# Session Store

Persists session data.

Storage

Active Sessions -> In-Memory Cache

Inactive Sessions -> Database

Archived Sessions -> Long-Term Storage

The store supports fast lookup.

---

# Entity: active_sessions

Purpose

Tracks currently active sessions.

Fields

session_id

agent_id

permission_scope

resource_access_list

tool_access_list

created_at

last_active_at

timeout_seconds

state

metadata

Active sessions expire after timeout.

---

# Session State Machine

States

Created

Authenticating

Active

Idle

Suspended

Expired

Closed

Failed

Transitions are logged for auditing.

---

# State Transitions

Created -> Authenticating (on session start)

Authenticating -> Active (on success)

Authenticating -> Failed (on failure)

Active -> Idle (on inactivity)

Idle -> Active (on activity)

Active -> Suspended (on policy violation)

Suspended -> Active (on resolution)

Active -> Expired (on timeout)

Any -> Closed (on session end)

---

# Session Validation

Every request validates

Session Exists

Session Not Expired

Session Not Suspended

Permission Scope Still Valid

Resource Still Accessible

Tool Still Available

Invalid sessions receive immediate rejection.

---

# Session Timeout

Configurable timeout policies.

Types

Inactivity Timeout (default: 30 minutes)

Absolute Timeout (default: 24 hours)

Extended Session (user-approved long tasks)

Timeouts prevent resource leaks.

---

# Session Scheduler

Background service managing session lifecycle.

Tasks

Check Expired Sessions

Cleanup Stale Resources

Archive Old Sessions

Send Expiry Warnings

Refresh Permission Tokens

The scheduler runs periodically.

---

# Session Monitor

Tracks session health.

Metrics

Active Session Count

Session Duration

Request Count Per Session

Error Count Per Session

Idle Time

Resource Usage

Suspicious Activity

---

# Resource Discovery Protocol

Purpose

Enables agents to discover available resources dynamically.

Resources are not hardcoded.

Agents query available resources at runtime.

---

# Resource Types

System Resources

Knowledge Graph

User Profile

Settings

Notifications

Search Index

File System

Knowledge Resources

Books

Notes

Projects

Flashcards

Quizzes

Study Sessions

Documents

Research Papers

AI Resources

AI Memory

Digital Twin

Learning History

Recommendations

Predictions

External Resources

Connected Services

Plugin Data

MCP Connectors

Hardware Interfaces

---

# Resource Discovery Flow

Agent

↓

Resource Discovery Request

↓

MCP Gateway

↓

Permission Check

↓

Resource Manager

↓

Available Resources Response

↓

Agent Selects Resource

↓

Access Request

↓

Permission Validation

↓

Resource Access Granted

---

# Resource Metadata

Each resource provides

Resource ID

Resource Name

Resource Type

Schema

Access Level Required

Supported Operations

Estimated Size

Depends On

Tags

Description

---

# Resource Access Levels

Public

Accessible to all authenticated agents.

Protected

Requires specific permission.

Private

Belongs to specific user or session.

System

Internal system resources, not agent accessible.

Audit Only

Read-only historical data.

---

# Resource Caching

Frequently accessed resources are cached.

Cache Layers

L1: In-Memory (fast, small)

L2: Redis (medium, configurable TTL)

L3: Database (slow, persistent)

Cache invalidation follows resource update events.

---

# Resource Access Control

Each resource access requires

Permission Check

Rate Limit Check

Resource Availability

Operation Validity

Access is logged for auditing.

---

# Resource Events

Events published to Event Store

resource.discovered

resource.accessed

resource.cached

resource.invalidated

resource.unavailable

resource.permission.denied

---

# Summary

The MCP Session Manager ensures secure, stateful, and observable AI agent interactions.

The Resource Discovery Protocol enables dynamic, permission-controlled access to all platform resources.

Together they form the foundation for flexible and secure AI-platform communication.

---

# End of Part 11

Next

Part 12

- MCP Tool Registry
- Tool Registration & Versioning
- Tool Execution Lifecycle
- MCP Security Model
- Authentication & Authorization
- Input/Output Validation
