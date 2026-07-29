# System Architecture

Project: JARVIS

Version: 0.1

Status: Draft

Author: Krishna Pranay Danda

---

# 1. Purpose

This document describes the high-level architecture of JARVIS and explains how its major components interact.

The primary objective is to build a modular, scalable, secure, and maintainable AI Operating System where every subsystem has a clearly defined responsibility.

This document serves as the architectural blueprint for the entire project before implementation begins.

---

# 2. Architecture Goals

The architecture is designed with the following objectives:

- Modularity
- Scalability
- Maintainability
- Security
- Extensibility
- Local-first AI
- Low Coupling
- High Cohesion
- Replaceable Components
- Clear Separation of Responsibilities

---

# 3. High-Level Architecture

```text
                 USER
                   │
                   ▼
            React Frontend
                   │
                   ▼
          Spring Boot Backend
                   │
        ┌──────────┼────────────┐
        ▼          ▼            ▼
     Memory     Planner     Tool Manager
        │          │            │
        └──────────┼────────────┘
                   ▼
             AI Services
                   │
                   ▼
          Ollama (Qwen/Llama)
                   │
                   ▼
             PostgreSQL
```

The Spring Boot Backend acts as the central orchestrator of the system.

Every request from the user passes through the backend, which decides which modules should participate in fulfilling the request.

Individual modules never control the workflow of the application.

---

# 4. Component Responsibilities

## User

Responsibilities

- Interacts with JARVIS
- Provides requests
- Receives responses

The user communicates only with the frontend.

---

## React Frontend

Technology

- React

Responsibilities

- Chat Interface
- Dashboard
- Settings
- Authentication Screens
- Notifications
- Display Results

The frontend is responsible only for presentation and user interaction.

It does not contain business logic.

---

## Spring Boot Backend


Responsibilities

- Request Routing
- Workflow Orchestration
- Authentication
- Session Management
- Business Logic
- Module Coordination
- API Exposure
- Error Handling

The backend is the brain of JARVIS.

It coordinates every subsystem but does not perform specialized work itself.

---

## Memory Module

Responsibilities

- Store memories
- Retrieve relevant memories
- Update memories
- Delete memories
- Rank memories by relevance
- Manage long-term memory

The memory system operates independently from AI models.

Its responsibility is to provide relevant context whenever requested.

---

## Planner Module

Responsibilities

- Analyze goals
- Break goals into tasks
- Create execution plans
- Track progress
- Manage task dependencies

The Planner focuses only on planning.

It does not execute tasks.

---

## Tool Manager

Responsibilities

- Execute tools
- Open applications
- Read PDFs
- File operations
- Browser automation
- Terminal execution
- Future tool integrations

The Tool Manager provides generic capabilities rather than application-specific commands.

---

## AI Services

Responsibilities

- Prompt Construction
- Context Building
- AI Model Communication
- Response Parsing
- Model Selection
- AI Configuration

AI Services perform reasoning only.

They do not control application workflow or make business decisions.

---

## Ollama

Responsibilities

- Execute language models
- Natural language understanding
- Reasoning
- Code generation
- Text generation

Ollama acts as the inference engine responsible for executing AI models.

---

## PostgreSQL

Responsibilities

- User Information
- Conversations
- Memories
- Settings
- Logs
- Future Metadata

PostgreSQL acts as the persistent storage layer of JARVIS.

---

# 5. Request Flow

Example Request

> "Summarize my DBMS PDF and remember it."

```text
User
    │
    ▼
React Frontend
    │
    ▼
Spring Boot Backend (Core)
    │
    ▼
Tool Manager
    │
    ▼
PDF Reader
    │
    ▼
Extract Text
    │
    ▼
Memory Module
(Retrieve related memories)
    │
    ▼
AI Services
(Build prompt + context)
    │
    ▼
Ollama
    │
    ▼
Generated Summary
    │
    ▼
Memory Module
(Store summary)
    │
    ▼
Spring Boot Backend
    │
    ▼
React Frontend
    │
    ▼
User
```

### Flow Description

1. The user submits a request through the frontend.
2. The backend analyzes the request and determines the required modules.
3. The Tool Manager extracts the PDF contents.
4. The Memory Module retrieves any relevant past memories.
5. AI Services build a prompt using both the extracted text and retrieved memories.
6. Ollama generates the summary.
7. The backend stores the summary using the Memory Module.
8. The final response is returned to the user.

---

# 6. Module Communication Rules

The architecture follows an orchestration pattern.

Communication rules:

- Modules never directly control one another.
- The Core Backend coordinates every workflow.
- AI Services perform reasoning only.
- Memory only manages memories.
- Planner only creates plans.
- Tool Manager only executes tools.
- Security validates sensitive actions before execution.
- Database access should occur only through the responsible modules.

These rules minimize coupling and improve maintainability.

---

# 7. Architectural Principles

## Separation of Concerns

Each module has one clearly defined responsibility.

---

## Single Responsibility Principle

Every subsystem should have only one primary reason to change.

---

## Low Coupling

Modules communicate through well-defined interfaces.

Internal implementation details remain hidden.

---

## High Cohesion

Responsibilities within a module should be closely related.

---

## Replaceable Components

AI models, databases, and tools should be replaceable without redesigning the architecture.

---

## Orchestration

The backend coordinates workflows.

Modules execute specialized responsibilities.

---

## Local-first Design

User data should remain on the local machine whenever possible.

Cloud services should remain optional.

---

## Safety First

Potentially dangerous operations must require explicit user confirmation before execution.

---

# 8. Future Expansion

The architecture is designed for long-term evolution.

Possible future modules include:

- Voice Interface
- Vision Module
- Plugin Marketplace
- Multi-Agent System
- Workflow Engine
- Smart Home Integration
- Mobile Companion
- Cloud Synchronization
- Knowledge Graph
- Vector Database
- Personalized Learning Engine

These modules can be added without significantly modifying the existing architecture due to the modular design.

---

# 9. Summary

JARVIS follows a modular, orchestrated architecture where each subsystem performs a specialized responsibility.

The Spring Boot Backend acts as the central coordinator, while independent modules handle memory, planning, tools, AI reasoning, and persistent storage.

This architecture promotes scalability, maintainability, flexibility, and long-term evolution while ensuring that individual components remain loosely coupled and independently replaceable.
