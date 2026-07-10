# 18 - Frontend Architecture

Version: 1.0

Status: Planning

---

# Frontend Overview

## Stack

Framework: Next.js 14+ (App Router)

UI Library: React 18+

Language: TypeScript

Styling: TailwindCSS

Components: shadcn/ui (Radix primitives)

State: Zustand (client state) + React Query (server state)

Forms: React Hook Form + Zod

Charts: Recharts

Desktop: Tauri (Next.js as frontend)

---

# Directory Structure

src/

├── app/ (Next.js App Router pages)

│   ├── (auth)/ login, register

│   ├── (dashboard)/ main dashboard

│   ├── learning/ subjects, courses, books, notes, revision, quizzes, flashcards

│   ├── engineering/ projects, flight-controller, components, experiments

│   ├── programming/ repositories, issues, commits

│   ├── research/ papers, citations, experiments

│   ├── productivity/ planner, goals, habits, journal

│   ├── monitoring/ dashboard, settings

│   ├── analytics/ dashboards, reports

│   ├── health/ sleep, exercise, mood

│   ├── career/ portfolio, cv, interviews

│   ├── startup/ ideas, roadmap, feedback

│   └── settings/ profile, preferences, permissions

├── components/ (shared components)

│   ├── ui/ (shadcn/ui components)

│   ├── layout/ headers, sidebars, navigation

│   ├── charts/ reusable chart components

│   └── forms/ form components

├── lib/ (utilities)

│   ├── api/ API client functions

│   ├── hooks/ custom React hooks

│   ├── stores/ Zustand stores

│   ├── utils/ helper functions

│   └── validations/ Zod schemas

└── types/ TypeScript type definitions

---

# State Management

Server State: React Query (TanStack Query) for all API data.

Client State: Zustand for UI state (theme, sidebar, active module).

Real-Time: WebSocket connection via Zustand store.

---

# Component Library

shadcn/ui with custom theme.

All components server-side rendered where possible.

Dark/light mode support.

Responsive design (desktop-first, tablet support).

---

# Performance

Next.js App Router for route-level code splitting.

Static generation for dashboard pages.

Incremental Static Regeneration for analytics.

Image optimization via next/image.

---

# Status

Complete

Next Document: 19-Backend-Architecture.md
