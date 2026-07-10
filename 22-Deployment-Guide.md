# 22 - Deployment Guide

Version: 1.0

Status: Planning

---

# Deployment Overview

## Desktop (Primary)

Windows: .msi installer via Tauri bundler

Linux: .AppImage

Distribution: GitHub Releases, auto-update

## Backend

Local: Embedded (SQLite for single-user)

Cloud (Optional): Docker containers

PostgreSQL, Redis

NestJS API server

## CI/CD

GitHub Actions

Lint -> Test -> Build -> Release

Automated builds on tag push

---

# Status

Complete

Next Document: 23-Development-Rules.md
