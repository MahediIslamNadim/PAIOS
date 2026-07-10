# 12 - Analytics

## Part 2

Version: 1.0

Status: Planning

---

# Dashboards & Visualizations

## Purpose

Dashboards provide visual overviews of key metrics from all PAIOS modules.

Customizable layouts and chart types allow users to focus on what matters most.

---

# Dashboard Types

Main Dashboard

Cross-module overview shown on home screen.

Learning Dashboard

Study time, quiz scores, revision, streaks.

Productivity Dashboard

Focus time, tasks, goals, habits.

Coding Dashboard

Commits, languages, build status.

Research Dashboard

Papers read, experiments, citations.

Health Dashboard

Sleep, exercise, mood, energy.

Custom Dashboard

User-defined layout and metrics.

---

# Chart Types

Time Series

Line chart for trends over time.

Bar Chart

Compare values across categories.

Pie / Donut

Distribution of categories.

Heatmap

Intensity by hour/day (productivity patterns).

Radar

Multi-metric comparison (skills, subjects).

Progress Bar

Goal completion, subject progress.

Gauge

Single metric with target (focus score, daily goal).

Table

Detailed data with sort/filter.

Number Card

Single important number (streak, hours today).

---

# Dashboard Customization

Users customize their dashboards.

Customization Options

Add/Remove Widgets

Resize and Rearrange

Choose Metrics

Set Time Ranges

Choose Chart Types

Save Multiple Dashboard Configurations

Reset to Default

---

# Entity: dashboard_configs

Purpose

Stores user dashboard configurations.

Fields

config_id

name

description

layout (JSON grid definition)

widgets (JSON array of widget definitions)

is_default

is_main_dashboard

created_at

---

# Widget Components

Each widget displays one metric or chart.

Widget Types

Metric Card (single number)

Time Series Chart

Bar Chart

Pie Chart

Progress Bar

Heatmap

Recent Items List

Calendar (streak heatmap)

Goal Summary

Widgets have configurable time ranges and filters.

---

# Real-Time Widgets

Live updates for active metrics.

Real-Time Widgets

Focus Score (live update every second)

Timer (study/pomodoro countdown)

Today's Progress (vs goal)

Active Session Status

Widgets update via event bus without page refresh.

---

# Global Search in Analytics

Search across all analytics data.

Search Features

Search Metric Names

Search Dashboard Names

Search Report Titles

Search by Date Range

Search by Module

Cross-module search results.

---

# Events

Events published to Event Store

analytics.dashboard.created

analytics.dashboard.modified

analytics.widget.added

analytics.widget.removed

analytics.dashboard.reset

---

# Summary

Dashboards and Visualizations provide customizable, real-time views of all PAIOS analytics data.

Users can build personal dashboards focused on their priorities.

---

# End of Part 2

Next

Part 3

- Reports & Exports
- Scheduled Reports
- Report Templates
- Export Formats
- Data Portability
- Automated Distribution
