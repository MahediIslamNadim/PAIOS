# 08 - Programming Workspace

## Part 5

Version: 1.0

Status: Planning

---

# Build, Debug & Deploy

## Purpose

Build, Debug, and Deploy capabilities integrate the software development lifecycle within PAIOS.

Automated builds, interactive debugging, testing integration, and deployment pipelines streamline development workflows.

---

# Build System Integration

Integrate with existing build tools.

Supported Build Systems

npm / yarn / pnpm (Node.js)

pip / poetry / uv (Python)

cargo (Rust)

make / cmake (C/C++)

gradle / maven (Java)

dotnet build (.NET)

PlatformIO (Embedded)

Arduino CLI

Custom (user-defined)

---

# Build Manager

Manage build configurations and execution.

Build Manager Features

Run Build (with selected configuration)

Build Configurations (debug, release, test, custom)

Build Output Viewer (parse errors and warnings)

Build History (success/failure log)

Quick Build (last configuration)

Build Shortcuts (Ctrl+Shift+B)

---

# Entity: build_configurations

Purpose

Stores build configurations per project.

Fields

config_id

project_id

name (debug, release, test, custom)

build_command

arguments

environment_variables (JSON)

working_directory

pre_build_steps (JSON array)

post_build_steps (JSON array)

is_default

created_at

---

# Task Runners

Automate repetitive development tasks.

Task Types

Build

Test

Lint

Format

Clean

Deploy

Database Migration

Docker Operations

Custom Scripts

Tasks can be chained in sequences.

---

# Debugger Interface

Interactive debugging for supported languages.

Debug Features

Breakpoints (line, conditional, function)

Step Over, Step Into, Step Out

Continue, Stop, Restart

Call Stack View

Variable Inspection (watch, hover)

Expression Evaluation

Thread View

Debug Console

---

# Debugger Support

Supported debuggers per language.

Python: debugpy

Node.js: Node Inspector

C/C++: GDB, LLDB

C#: .NET Debugger

Java: Java Debugger

Go: Delve

Rust: LLDB, GDB via rust-gdb

Embedded: OpenOCD + GDB

Custom debugger configurations are supported.

---

# Testing Integration

Run and manage tests.

Test Frameworks

Python: pytest, unittest

JavaScript: Jest, Vitest, Mocha

C/C++: CTest, Google Test

Rust: cargo test

Java: JUnit

.NET: NUnit, xUnit

Go: go test

Embedded: PlatformIO test

---

# Test Runner

Execute tests with rich feedback.

Test Runner Features

Run All Tests

Run Test File

Run Single Test

Test Output Viewer

Test History

Code Coverage (if supported by framework)

Failed Test Quick Fix (navigate to error)

---

# Test Reports

Comprehensive test reporting.

Report Contents

Total Tests

Passed / Failed / Skipped

Duration

Failure Details (with stack trace)

Coverage Percentage

Test History (trend over time)

Reports are integrated with CI results when available.

---

# Deployment Automation

Deploy applications from PAIOS.

Deployment Targets

Local (run directly)

Docker (build and run container)

Cloud (push to cloud platform)

Server (SSH deploy)

Package (build package for distribution)

Firmware (flash to device - via Engineering Workspace)

---

# Entity: deployment_configs

Purpose

Stores deployment configurations.

Fields

deploy_id

project_id

name

deployment_type (local, docker, cloud, server, package, firmware)

target

build_before_deploy

commands (JSON array)

environment_variables

rollback_command

is_production

created_at

---

# CI/CD Integration

Integrate with external CI/CD systems.

Supported Systems

GitHub Actions

GitLab CI

Jenkins

CircleCI

Custom (webhook-based)

Integration Features

View Pipeline Status

Trigger Pipeline from PAIOS

View Build Logs

Deploy Artifact

---

# Events

Events published to Event Store

programming.build.started

programming.build.completed

programming.build.failed

programming.debug.session.started

programming.debug.session.ended

programming.test.run.started

programming.test.run.completed

programming.deploy.started

programming.deploy.completed

programming.deploy.failed

---

# Summary

Build, Debug, and Deploy integration provides a complete development workflow within PAIOS.

Automated builds, interactive debugging, testing, and deployment pipelines streamline the path from code to production.

---

# End of Part 5

Next

Part 6

- Code Review & Bug Tracking
- Code Review Workflow
- Inline Comments
- Review Requests
- Bug Tracker
- Issue Management
