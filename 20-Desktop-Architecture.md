# 20 - Desktop Architecture

Version: 1.0

Status: Planning

---

# Desktop Overview

## Stack

Framework: Tauri v2

Frontend: Next.js (embedded via Tauri)

Language: Rust (Tauri backend)

Packaging: .msi (Windows), .AppImage (Linux)

---

# Tauri Architecture

Tauri Core (Rust)

File system access

System tray

Native notifications

Camera/mic access (permissions)

Window management

Auto-updater

Shortcut registration

WebView (Next.js frontend)

All UI rendered in webview.

---

# Desktop-Specific Features

System Tray Icon

Quick access to dashboard, timer, search.

Focus indicator icon.

Global Hotkeys

Ctrl+Shift+N: Quick note

Ctrl+Shift+F: Search

Ctrl+Shift+T: Timer toggle

Native Notifications

Study break reminders

Revision due alerts

Focus score alerts

Offline Support

Service worker caching.

Local IndexedDB for offline data.

Sync when online.

Auto-Start (optional)

Launch PAIOS on system startup.

---

# Permissions

Camera (eye tracking, presence) - explicit grant

Microphone (voice detection) - explicit grant

File system (code projects, PDFs) - user selected paths

Notifications

Keyboard/mouse monitoring - accessibility permission

All permissions are revocable from settings.

---

# Status

Complete

Next Document: 21-Testing-Strategy.md
