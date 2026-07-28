# System Architecture

Project: JARVIS

Version: 0.1

Status: Draft

Author: Krishna Pranay Danda

---

# 1. Purpose

This document describes the high-level architecture of JARVIS and explains how its major components interact.

The goal is to create a modular, scalable, secure, and maintainable AI operating system where each subsystem has a clearly defined responsibility.

---

# 2. Architecture Goals

The architecture is designed to achieve the following goals:

- Modularity
- Scalability
- Maintainability
- Security
- Extensibility
- Local-first AI
- Easy replacement of components

---

# 3. High-Level Architecture

```

Then add the first architecture diagram.

```text
                 USER
                   │
                   ▼
            React Frontend
                   │
                   ▼
          Spring Boot Backend
                   │
        ┌──────────┼───────────┐
        ▼          ▼           ▼
    Memory      Planner      Tool Manager
        │          │           │
        └──────────┼───────────┘
                   ▼
             AI Services
                   │
                   ▼
          Ollama (Qwen/Llama)
                   │
                   ▼
             PostgreSQL
```


# 4. Component Responsibilities
```

Now describe every component.

Example:

## User

Initiates requests and receives responses.

The user interacts only with the frontend.

---

## React Frontend

Responsibilities

- Chat Interface
- Dashboard
- Settings
- Authentication Screens
- Notifications

The frontend does not contain business logic.

---

## Spring Boot Backend

Responsibilities

- Request Routing
- Orchestration
- Authentication
- Business Logic
- Module Coordination
- API Exposure

The backend acts as the brain of the application and coordinates communication between all subsystems.

---

## Memory Module

Responsibilities

- Store memories
- Retrieve relevant memories
- Update memories
- Delete memories
- Rank relevant memories

The memory module is independent of the AI implementation.

---

## Planner Module

Responsibilities

- Break large goals into tasks
- Create execution plans
- Track task progress
- Manage dependencies

---

## Tool Manager

Responsibilities

- Execute tools
- Manage application launching
- Read PDFs
- File operations
- Browser automation
- Terminal execution

The Tool Manager exposes generic capabilities rather than application-specific features.

---

## AI Services

Responsibilities

- Build prompts
- Build AI context
- Call AI models
- Parse responses
- Select AI models

AI Services do not make application-level decisions.

---

## Ollama

Responsibilities

- Execute language models
- Reasoning
- Code generation
- Text generation

---

## PostgreSQL

Responsibilities

- User data
- Memories
- Conversations
- Settings
- Logs
