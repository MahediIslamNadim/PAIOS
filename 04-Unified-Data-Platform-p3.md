# 04 - Unified Data Platform

## Part 3

Version: 1.0

Status: Planning

---

# Core Identity Model

## Purpose

The Core Identity Model defines the foundational entities that identify users, devices, workspaces, and execution contexts.

These entities serve as the root of nearly every relationship within the Unified Data Platform.

---

# Identity Hierarchy

User

↓

Profile

↓

Workspace

↓

Projects

↓

Knowledge

↓

Study

↓

Tasks

↓

Events

Every object can be traced back to a user and a workspace.

---

# Entity: users

Purpose

Represents a unique human user.

Fields

id

display_name

username

email (optional)

avatar_path

language

timezone

status

created_at

updated_at

version

Notes

The user record contains only identity information.

Learning data belongs elsewhere.

---

# Entity: user_profiles

Purpose

Stores user-specific preferences and profile information.

Fields

id

user_id

theme

preferred_ai_provider

preferred_language

study_preferences

notification_preferences

privacy_preferences

accessibility_preferences

created_at

updated_at

version

Large preference objects are stored as JSON.

---

# Entity: devices

Purpose

Represents physical devices.

Examples

Laptop

Desktop

Tablet

Phone

Fields

id

user_id

device_name

device_type

operating_system

app_version

last_seen_at

status

created_at

updated_at

Devices support synchronization and audit history.

---

# Entity: workspaces

Purpose

Separates independent environments.

Examples

Personal Study

University

Research

Drone Engineering

Company

Fields

id

user_id

name

description

icon

color

status

created_at

updated_at

version

Every knowledge object belongs to a workspace.

---

# Entity: workspace_members

Future Support

Multiple users

Roles

Owner

Editor

Viewer

Guest

Version 1 may support only a single owner.

The schema remains future-compatible.

---

# Entity: sessions

Purpose

Tracks application sessions.

Fields

id

user_id

device_id

started_at

ended_at

duration

exit_reason

application_version

Useful for diagnostics and analytics.

---

# Entity Relationships

User

1

↓

Many

Profiles

User

1

↓

Many

Devices

User

1

↓

Many

Workspaces

Workspace

1

↓

Many

Projects

Workspace

1

↓

Many

Knowledge Objects

Workspace

1

↓

Many

Study Sessions

---

# Identity Rules

Every workspace has one owner.

Every device belongs to one user.

Every profile belongs to one user.

Objects cannot exist without ownership.

Ownership changes require explicit migration.

---

# Multi-Workspace Isolation

Workspaces isolate

Knowledge

Projects

Tasks

AI Memory

Automation

Plugins (optional)

Search Index (logical)

Isolation prevents accidental cross-project contamination.

---

# Default Workspace

On first launch

Create

Personal Workspace

This workspace becomes the default unless changed.

---

# Identity Events

Examples

User Created

Workspace Created

Workspace Renamed

Device Registered

Profile Updated

Workspace Archived

These events enter the Event Store.

---

# Security Considerations

Workspace permissions are validated before access.

Future collaboration features should use role-based access control.

---

# Summary

The Core Identity Model separates identity, preferences, devices, and workspaces.

This separation improves scalability, synchronization, privacy, and future collaboration support.

---

# End of Part 3

Next

Part 4

- Knowledge Object Schema
- Knowledge Types
- Metadata Model
- Relationship Model
- Knowledge Versioning
