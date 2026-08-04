# Weave — Comprehensive System Architecture

> **Version:** 4.0 (Unified Documentation)  
> **Date:** July 28, 2026  
> **System Evolution:** V1 (Siloed Agents) → V2 (Agentic OS with Runtime) → V3 (Unified SDK, Artifact Store, Memory Bus, Policy API, Observability, Tenant Agents, Marketplace) → V4 (Current: 28 Tools, Enhanced Subsystems, Full Integration)

---

## Table of Contents

1. [System Overview](#1-system-overview)
2. [System Evolution History](#2-system-evolution-history)
3. [Architectural Principles](#3-architectural-principles)
4. [Technology Stack](#4-technology-stack)
5. [Project Structure](#5-project-structure)
6. [V3 Runtime Engine](#6-v3-runtime-engine)
7. [V3 Tool SDK & Implementations](#7-v3-tool-sdk--implementations)
8. [V3 Artifact Store](#8-v3-artifact-store)
9. [V3 Memory Bus API](#9-v3-memory-bus-api)
10. [V3 Policy API](#10-v3-policy-api)
11. [V3 Observability](#11-v3-observability)
12. [V3 Tenant Agents](#12-v3-tenant-agents)
13. [V3 Marketplace](#13-v3-marketplace)
14. [V3 Workflow Composer](#14-v3-workflow-composer)
15. [V3 Event System & Telemetry](#15-v3-event-system--telemetry)
16. [V3 WebSocket Streaming](#16-v3-websocket-streaming)
17. [V3 Skills System](#17-v3-skills-system)
18. [V3 Background Tasks & Scheduler](#18-v3-background-tasks--scheduler)
19. [V3 Package System](#19-v3-package-system)
20. [V3 Console Interface](#20-v3-console-interface)
21. [V3 URL Routing & API Map](#21-v3-url-routing--api-map)
22. [V3 Data Models](#22-v3-data-models)
23. [Module Reference](#23-module-reference)
24. [Agent Verticals](#24-agent-verticals)
25. [System Flow](#25-system-flow)
26. [Infrastructure & Deployment](#26-infrastructure--deployment)
27. [Test Suite](#27-test-suite)
28. [Known Issues & Roadmap](#28-known-issues--roadmap)

---

## 1. System Overview

Weave is a **Multi-Tenant Agentic Operating System** designed to host and orchestrate a fleet of autonomous AI agents across diverse business domains. It implements a **Kernel-Agent-Memory** architecture pattern where:

- The **Kernel** provides shared infrastructure (routing, authentication, billing, backup, runtime engine).
- **Agent Verticals** are isolated, domain-specific Django applications.
- **BrainBox** is a unified memory substrate enabling cross-agent intelligence.
- **V3 Enhancements** add production-grade SDK tooling, persistent artifact management, dedicated memory bus API, formal policy administration API, comprehensive observability, tenant-scoped agent configuration, and a marketplace for agent sharing.

### Core Features

**V1 Foundation:**
- **Multi-Tenancy**: Strict data isolation at the database level per organization.
- **Human-in-the-Loop (HITL)**: Configurable autonomy via an Approval Queue.
- **Unified Memory**: Shared Event Store, Semantic Memory, Knowledge Graph, and Inference Layer.
- **Modular Design**: Pluggable agent architecture via Django apps.
- **Async Execution**: Background task processing via Celery + Redis.
- **Real-Time**: WebSocket support via Django Channels / Daphne.

**V2 Additions:**
- **Shared Runtime Engine**: Central execution engine shared by all agents.
- **Dynamic Tool Registry**: Capability-based tool discovery and management.
- **Workflow Composer**: Multi-agent DAG orchestration with NL-to-workflow conversion.
- **Enhanced BrainBox Integration**: Deep runtime memory integration.

**V3 Additions:**
- **Tool SDK**: JSON Schema validation, health monitoring, telemetry emission.
- **Artifact Store**: Persistent file artifacts with versioning and checksums.
- **Memory Bus API**: Dedicated write/read/semantic-search API for memory records.
- **Policy Admin API**: REST CRUD for configurable policy rules.
- **Observability**: Dashboard, metrics aggregation, tool health reports, alert engine.
- **Tenant Agents**: Per-tenant agent configuration with publish to marketplace.
- **Marketplace**: Package listings, ratings, installation tracking.
- **28 Concrete Tools**: Comprehensive tool implementations across domains.
- **Event System**: 27 canonical event types with durable pub/sub.
- **Telemetry**: Per-tenant and per-agent execution metrics with aggregation.
- **WebSocket Streaming**: Real-time event streaming via Django Channels.
- **Skills System**: Declarative reusable skills with registry.
- **Background Tasks**: Managed async task execution with scheduler.
- **Package System**: Agent package management and loading.
- **Console Interface**: Interactive agent console for debugging.

---

## 2. System Evolution History

### V1: Siloed Agents (Original)

**Architecture:** Each agent was an independent Django application with embedded logic, hard-coded tool functions, and isolated memory stores. Agents could not share context or coordinate.

**Key Characteristics:**
- Independent agent apps with no shared runtime
- Hard-coded tool functions within each agent's logic
- Basic state persistence per agent
- Linear execution of predefined scripts
- No centralized safety or policy layer
- No unified memory substrate
- No multi-agent orchestration

**Limitations:**
- Memory fragmentation — each agent maintained its own context
- No cross-agent intelligence transfer
- Duplicate infrastructure for each new agent
- No standardized tool interface
- No configurable autonomy modes

### V2: Agentic OS with Runtime

**Architecture:** Introduced a shared `AgentRuntime` engine, dynamic `ToolRegistry`, and `WorkflowComposer` for multi-agent orchestration. BrainBox became the unified memory substrate.

**Key Additions:**
- `AgentRuntime` — central execution engine shared by all agents
- `ToolRegistry` — dynamic tool discovery by capabilities
- `WorkflowComposer` — multi-agent DAG orchestration
- `BrainBox` — unified memory (Event Store, Semantic Memory, Knowledge Graph, Inference Layer)
- `SafetyLayer` — centralized intent validation
- `Planner` → `Reasoner` → `ToolRunner` pipeline
- Real-time `EventStream` telemetry
- HITL `ApprovalQueue` integration

### V3: Unified Platform (Current Base)

**Architecture:** V3 builds on V2 by adding production-grade SDK tooling, persistent artifact management, a dedicated memory bus API, a formal policy administration API, comprehensive observability, tenant-scoped agent configuration, and a marketplace for agent sharing.

**Key Additions:**
- **Tool SDK** (`ToolSchema`, `ToolHealthMonitor`, `ToolTelemetryEmitter`)
- **Artifact Store** (`ArtifactManager`) with versioning
- **Memory Bus API** (`MemoryBus`) with legacy BrainBox mirroring
- **Policy Admin API** (`PolicyRuleModel`) with REST CRUD
- **Observability** — Dashboard, metrics, health, alerts
- **Tenant Agents** (`TenantAgentModel`) with publish toggle
- **Marketplace** — Package listings, ratings, installation
- **14 Original Tools** — email, crm, browser, database, slack, whatsapp, github, excel, pdf, calendar, search, payments, maps, ocr

### V4: Enhanced Ecosystem (Current State)

**Architecture:** V4 expands V3 with additional tools, enhanced subsystems, and improved developer experience.

**Key Additions:**
- **14 Additional Tools** — calculator, compliance_checker, enrichment_api, newsletter_tools, notification, report, scraper, sentiment_analyzer, seo_tool, social_media_tool, telemetry_tool, ticket_tool, and more (total 28 tools)
- **Intent Canonicalizer** — New runtime module for intent normalization
- **Enhanced Skills System** — Full CRUD API with extensive skill definitions
- **Background Scheduler** — Advanced task scheduling and management
- **Enhanced Package System** — Improved package loading and management
- **Console Interface** — Interactive debugging and management console
- **Enhanced Streaming** — Additional execution streaming capabilities
- **Additional Models** — Plugin, Skill, RuntimeEvent, EventSubscription, EventDelivery, PackageInstallation, WorkspaceModel, RuntimeSessionModel, MarketplaceRating

---

## 3. Architectural Principles

### 3.1 Kernel-Agent-Memory Triad

```
┌─────────────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                               │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  Next.js Frontend (frontend/)                                │  │
│  │  Dashboard | Agent Fleet | Memory Bank | Inbox | Settings    │  │
│  └──────────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  WebSocket (Django Channels / Daphne)                        │  │
│  │  RuntimeEventConsumer — real-time event streaming            │  │
│  └──────────────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────┤
│                    API LAYER (REST)                                 │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌─────────┐ │
│  │Artifacts │ │  Memory  │ │  Policy  │ │Observab. │ │Marketpl.│ │
│  │  CRUD    │ │  CRUD    │ │  CRUD    │ │Metrics   │ │Ratings  │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └─────────┘ │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────┐ │
│  │Tenant    │ │  Skills  │ │  Events  │ │ Agent Verticals      │ │
│  │Agents    │ │  API     │ │  Stream  │ │ (Monica, Finance...) │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────────┘ │
├─────────────────────────────────────────────────────────────────────┤
│                    RUNTIME LAYER (Kernel)                           │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  AgentRuntime — Central Execution Engine                     │  │
│  │  Safety → Policy → Session → Context → Plan → Execute → Mem │  │
│  └──────────────────────────────────────────────────────────────┘  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────┐ │
│  │ Planner  │ │ToolRunner│ │ Reasoner │ │ ContextBuilder       │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────────┘ │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────┐ │
│  │ Safety   │ │  Policy  │ │  Session │ │ WorkspaceManager     │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────────┘ │
├─────────────────────────────────────────────────────────────────────┤
│                    MEMORY & STORAGE LAYER                           │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  BrainBox — Unified Memory Substrate                         │  │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐  │  │
│  │  │  Event   │ │ Semantic │ │Knowledge │ │  Inference   │  │  │
│  │  │  Store   │ │  Memory  │ │  Graph   │ │    Layer     │  │  │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────────┘  │  │
│  └──────────────────────────────────────────────────────────────┘  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────┐ │
│  │ Artifact │ │ Memory   │ │ Workspace│ │ KnowledgeBase (RAG)  │ │
│  │  Store   │ │  Bus     │ │  Files   │ │ (pgvector chunks)    │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────────┘ │
├─────────────────────────────────────────────────────────────────────┤
│                    INFRASTRUCTURE LAYER                             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────┐ │
│  │PostgreSQL│ │  Redis   │ │  Celery  │ │  Daphne (ASGI)       │ │
│  │ +pgvector│ │  Broker  │ │  Workers │ │  WebSocket           │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────────┘ │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────┐ │
│  │  Docker  │ │  Caddy   │ │  Sentry  │ │  WhiteNoise (Static) │ │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

### 3.2 Design Goals

- **Isolation**: Tenants cannot access each other's data or agent memory.
- **Reusability**: New agents inherit authentication, billing, backup, and memory without reimplementation.
- **Observability**: Every agent action is logged, auditable, and traceable.
- **Safety**: HITL gates prevent unsafe autonomous actions in high-stakes domains.
- **Extensibility**: Plugin system, package management, and marketplace for third-party extensions.
- **Performance**: Segregated task queues, background scheduling, and efficient resource utilization.

---

## 4. Technology Stack

| Layer | Technology | Purpose |
|---|---|---|
| Backend Framework | Django 5.0+ / Django REST Framework | API, ORM, Auth, Admin |
| ASGI Server | Daphne | WebSocket + HTTP |
| Task Queue | Celery + Redis | Background execution |
| Database | PostgreSQL 15+ with pgvector | Primary data + vector embeddings |
| Frontend | Next.js 15+ / React 19 / TypeScript | Agent management dashboard |
| AI/LLM | Groq API (Llama 3), DeepL (translation), ElevenLabs (voice) | Intelligence layer |
| Containerization | Docker + Docker Compose | Deployment |
| Reverse Proxy | Caddy | TLS, static files |
| Error Tracking | Sentry | Production monitoring |
| Static Files | WhiteNoise | CDN-ready serving |
| Browser Automation | Playwright | Web scraping and interaction |
| Vector Store | pgvector | Semantic memory embeddings |

---

## 5. Project Structure

```
Weave/
├── agentictools/                    # Django project root (Kernel)
│   ├── runtime/                     # V2 + V3 + V4 Runtime Engine (18 modules)
│   │   ├── runtime.py               # AgentRuntime orchestrator
│   │   ├── planner.py               # Planner, TaskNode, TaskPlan
│   │   ├── tool_runner.py           # ToolRunner, ToolResult
│   │   ├── memory.py                # RuntimeMemory
│   │   ├── reasoner.py              # Reasoner
│   │   ├── event_stream.py          # EventStream
│   │   ├── safety.py                # SafetyLayer
│   │   ├── session.py               # SessionManager
│   │   ├── policy.py                # PolicyEngine
│   │   ├── context_builder.py       # ContextBuilder
│   │   ├── workspace.py             # TaskWorkspace, WorkspaceManager
│   │   ├── dag.py                   # DAGWorkflowEngine
│   │   ├── model_providers.py       # ModelRouter
│   │   ├── artifacts.py             # ArtifactManager (V3)
│   │   ├── memory_bus.py            # MemoryBus (V3)
│   │   ├── tenant_agent.py          # TenantAgentConfig, TenantAgentRunner (V3)
│   │   └── intent_canonicalizer.py  # IntentCanonicalizer (V4)
│   ├── tools/                       # V2 + V3 + V4 Tool SDK
│   │   ├── base.py                  # BaseTool, ToolResult
│   │   ├── sdk.py                   # ToolSchema, ToolTelemetryEmitter, ToolHealthMonitor (V3)
│   │   ├── registry.py              # ToolRegistry
│   │   ├── manifest.py              # AgentManifest
│   │   ├── context.py               # ContextBuilder
│   │   └── implementations/         # 28 concrete tools (V4)
│   │       ├── email_tool.py
│   │       ├── crm_tool.py
│   │       ├── browser_tool.py
│   │       ├── database_tool.py
│   │       ├── slack_tool.py
│   │       ├── whatsapp_tool.py
│   │       ├── github_tool.py
│   │       ├── excel_tool.py
│   │       ├── pdf_tool.py
│   │       ├── calendar_tool.py
│   │       ├── search_tool.py
│   │       ├── payments_tool.py
│   │       ├── maps_tool.py
│   │       ├── ocr_tool.py
│   │       ├── calculator_tool.py
│   │       ├── compliance_checker_tool.py
│   │       ├── enrichment_api_tool.py
│   │       ├── newsletter_tools.py
│   │       ├── notification_tool.py
│   │       ├── report_tool.py
│   │       ├── scraper_tool.py
│   │       ├── sentiment_analyzer_tool.py
│   │       ├── seo_tool.py
│   │       ├── social_media_tool.py
│   │       ├── telemetry_tool.py
│   │       └── ticket_tool.py
│   ├── views/                       # V3 + V4 REST API Views
│   │   ├── artifacts.py             # Artifact CRUD + download + version
│   │   ├── memory.py                # Memory CRUD + search
│   │   ├── policy.py                # Policy rule CRUD
│   │   ├── observability.py         # Dashboard, metrics, health, alerts
│   │   ├── tenant_agents.py         # Tenant agent CRUD + publish
│   │   ├── marketplace.py           # Marketplace listings + ratings
│   │   ├── workflows.py             # Workflow CRUD + execute
│   │   ├── runtime.py               # Runtime execute + status
│   │   ├── tools.py                 # Tool list + execute
│   │   ├── plans.py                 # Plan CRUD
│   │   ├── background_tasks.py      # Background task management
│   │   └── plugins.py               # Plugin management
│   ├── workflow/                    # V2 Workflow Composer
│   │   └── composer.py              # WorkflowComposer, Workflow, WorkflowStep
│   ├── events/                      # V3 Event System
│   │   ├── types.py                 # RuntimeEventTypes (27 constants)
│   │   ├── envelope.py              # EventEnvelope dataclass
│   │   └── bus.py                   # EventBus (pub/sub + DB persistence)
│   ├── telemetry/                   # V3 Telemetry
│   │   └── telemetry.py             # TelemetryCollector, MetricAggregator
│   ├── streaming/                   # V3 + V4 WebSocket
│   │   ├── consumers.py             # RuntimeEventConsumer
│   │   ├── consumers_execution.py   # Execution streaming (V4)
│   │   └── streamer.py              # Stream utilities
│   ├── skills/                      # V3 + V4 Skills System
│   │   ├── registry.py              # SkillRegistry
│   │   ├── skill.py                 # Skill dataclass
│   │   ├── definitions.py           # Extensive skill definitions (V4)
│   │   ├── views.py                 # Skills CRUD API
│   │   └── urls.py                  # Skills URL routing
│   ├── background/                  # V3 + V4 Background Tasks
│   │   └── scheduler.py             # BackgroundTaskManager (V4)
│   ├── packages/                    # V3 + V4 Package System
│   │   ├── manager.py               # PackageManager
│   │   ├── loader.py                # PackageLoader
│   │   └── manifest.py              # PackageManifest
│   ├── console/                     # V4 Console Interface
│   │   └── console.py               # AgentConsole
│   ├── models.py                    # V3 + V4 Data Models (15 models)
│   ├── api_urls.py                  # V3 + V4 URL routing
│   ├── settings.py                  # Django settings
│   ├── celery.py                    # Celery config
│   └── utils/                       # Shared kernel utilities
├── agents/                          # Agent fleet (self-contained Django apps)
│   ├── monica/                      # Customer Service
│   ├── marketer/                    # Marketing & CRM
│   ├── businessfinder/              # Market Intelligence
│   ├── governance/                  # Compliance & Procurement
│   ├── finance/                     # Financial Analysis
│   ├── maintenance/                 # Predictive IoT Maintenance
│   └── risk_detection/              # Security Monitoring
├── brainbox/                        # V2 Unified Memory Substrate
│   ├── models.py                    # BrainBoxEvent, BrainBoxMemory, BrainBoxEntity, etc.
│   ├── views.py, serializers.py, urls.py
│   └── tasks/                       # Memory indexing tasks
├── core/                            # V2 Orchestration Layer
│   ├── models.py                    # ApprovalQueue, KnowledgeBase, TaskLog, Notification
│   ├── views.py, serializers.py, urls.py
│   ├── logic/                       # IntentManager, SystemHealth
│   └── tasks.py                     # Periodic Celery tasks
├── accounts/                        # V1 Multi-Tenancy & Identity
│   ├── models.py                    # Tenant, UserProfile, UniversalUser, etc.
│   ├── views.py, serializers.py, urls.py
│   ├── authentication.py            # JWT + API Key auth
│   ├── services/                    # Business logic
│   └── tasks.py                     # Async account tasks
├── billing/                         # V1 Monetization (delegates to Pluggedspace Payments Platform)
├── backup/                          # V1 Resilience (automated backup/recovery)
├── frontend/                        # Next.js 15+ Dashboard (React 19, TypeScript, TailwindCSS)
├── documentation/
│   ├── COMPREHENSIVE_SYSTEM_ARCHITECTURE.md  # This file
│   ├── system_usage_documentation.md # End-user dashboard guide
│   ├── api_endpoints.md             # API endpoint documentation
│   ├── WHATSUP.md                   # Status & known issues
│   └── academic_paper.md            # Research paper
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── manage.py
```

---

## 6. V3 Runtime Engine

### 6.1 AgentRuntime (`agentictools/runtime/runtime.py`)

The central execution engine shared by all agents. Orchestrates the full lifecycle:

```
execute(intent)
  │
  ├─ 1. Safety Check (SafetyLayer.check)
  ├─ 2. Policy Evaluation (PolicyEngine.evaluate)
  │      └─ If requires_approval → propose_action() → return approval_required
  ├─ 3. Session Management (SessionManager)
  │      └─ Create or resume session + workspace
  ├─ 4. Context Building (ContextBuilder.build)
  ├─ 5. Planning (Planner.plan)
  ├─ 6. Tool Execution (ToolRunner.execute_plan)
  ├─ 7. Memory Storage (RuntimeMemory.store)
  ├─ 8. Session Close (if auto_close_session)
  └─ 9. Event Emission (EventStream.emit)
```

**Key Methods:**
- `execute(intent)` — Main entry point. Returns `{'status': 'success'|'blocked'|'approval_required'|'partial_failure', ...}`
- `propose_action(action_type, payload, reasoning, confidence)` — Queues HITL approval via `IntentManager`
- `get_status()` — Returns runtime state for monitoring

### 6.2 Planner (`agentictools/runtime/planner.py`)

Converts intents into executable task graphs (DAGs).

**Classes:**
- `TaskNode` — Single step: `node_id`, `action`, `parameters`, `dependencies`, `status`
- `TaskPlan` — DAG of `TaskNode`s: `get_ready_nodes()`, `to_dict()`, `from_dict()`
- `Planner` — `plan()` (LLM-based for complex goals, fallback to single-node), `resume_plan()`, `_persist_plan()`

### 6.3 ToolRunner (`agentictools/runtime/tool_runner.py`)

Executes tool calls with permission checks, logging, and memory storage.

**Classes:**
- `ToolResult` — Standardized result: `success`, `data`, `error`, `duration`
- `ToolRunner` — `execute_tool(tool_name, parameters, context, simulation)`, `execute_plan(plan, simulation)`

**Auto-Artifact Creation:** When a tool returns `file_content` + `file_name` in its result data, `ToolRunner` automatically creates an `Artifact` via `ArtifactManager`.

### 6.4 SessionManager (`agentictools/runtime/session.py`)

Manages runtime sessions with variable storage and metrics.

**Key Methods:**
- `create_session(agent_id, workspace_id, memory_scope, tool_scope)` → `RuntimeSession`
- `resume_session(session_id)` → `RuntimeSession`
- `get_session(session_id)` → `RuntimeSession`
- `close_session(session_id)`

**RuntimeSession Features:**
- `set_variable(key, value)` / `get_variable(key)` — Session-scoped variables
- `record_metric(key, value)` — Execution metrics
- `status` lifecycle: `active` → `closed`

### 6.5 ContextBuilder (`agentictools/runtime/context_builder.py`)

Assembles context snapshots for LLM prompts with token budgeting.

**Key Methods:**
- `build(intent)` → `ContextSnapshot` with `assembled_prompt`, `estimated_tokens`, `audit_trail`

### 6.6 PolicyEngine (`agentictools/runtime/policy.py`)

Evaluates tenant-configurable policy rules against agent actions.

**Key Methods:**
- `evaluate(agent, action, context)` → `PolicyDecision` with `allowed`, `requires_approval`, `approver_role`, `reason`

### 6.7 SafetyLayer (`agentictools/runtime/safety.py`)

System-level safety checks before any execution.

**Key Methods:**
- `check(action_type, payload)` → `bool`
- `assess_risk(action_type, payload)` → `'low'|'medium'|'high'`

### 6.8 WorkspaceManager (`agentictools/runtime/workspace.py`)

Manages per-task workspaces with file isolation and path traversal protection.

**Classes:**
- `TaskWorkspace` — Per-task workspace: `add_file()`, `add_log()`, `add_timeline_event()`, `add_memory()`, `snapshot()`, `restore()`, `save()`, `load()`
- `WorkspaceManager` — `create_workspace()`, `get_workspace()`, `list_workspaces()`

**Security:** Path traversal attacks are rejected with `PermissionError`.

### 6.9 DAGWorkflowEngine (`agentictools/runtime/dag.py`)

Executes DAG-based task plans with dependency resolution.

### 6.10 ModelRouter (`agentictools/runtime/model_providers.py`)

Routes LLM requests to configured providers with fallback support.

### 6.11 IntentCanonicalizer (`agentictools/runtime/intent_canonicalizer.py`) [V4]

Normalizes and canonicalizes incoming intents for consistent processing.

**Key Methods:**
- `canonicalize(intent)` → `CanonicalIntent` with standardized format
- `validate(intent)` → `bool` with validation errors

---

## 7. V3 Tool SDK & Implementations

### 7.1 BaseTool (`agentictools/tools/base.py`)

Abstract base class for all tools. Every tool **must** implement `_execute(**kwargs) -> ToolResult`.

**Class-level metadata:**
- `name`, `description`, `version`, `permissions` (capability strings)
- `parameters` (JSON Schema), `input_schema`, `output_schema`
- `cost_estimate`, `latency_estimate`, `risk_level`

**Key Methods:**
- `execute(**kwargs)` — Calls `_execute()`, tracks `execution_count`, `success_count`, `failure_count`, emits telemetry
- `health_check()` — Optional; returns custom health details dict

### 7.2 ToolSchema (`agentictools/tools/sdk.py`)

Input/output validation using JSON Schema.

**Key Methods:**
- `validate_input(tool, params, strict=False)` → `bool` or raises `ToolSchemaError`
- `describe(tool)` → `dict` with `name`, `version`, `input_schema`, `output_schema`

**Modes:**
- **Strict** (`strict=True`): Raises `ToolSchemaError` on invalid input
- **Lenient** (`strict=False`): Returns `False` on invalid input

### 7.3 ToolTelemetryEmitter (`agentictools/tools/sdk.py`)

Emits telemetry events for tool execution lifecycle.

### 7.4 ToolHealthMonitor (`agentictools/tools/sdk.py`)

Probes tools and returns health status.

**Key Methods:**
- `check_tool(tool)` → `ToolHealth` with `status` (`healthy`|`degraded`|`unhealthy`), `latency_ms`, `details`
- `check_all()` → `dict` with `overall`, `summary` (`total`, `healthy`, `degraded`, `unhealthy`), `tools`

**Health Criteria:**
- 100% success rate → `healthy`
- < 100% but > 0% → `degraded`
- 0% success rate → `unhealthy`
- Tools with `health_check()` method use its return as `details`

### 7.5 ToolRegistry (`agentictools/tools/registry.py`)

Central registry for tool discovery and management.

**Key Methods:**
- `register(tool_class)` — Register a tool class
- `get(name, tenant)` — Get tenant-scoped tool instance
- `get_for_agent(agent_id, tenant)` — Get tools for a specific agent
- `list_all()` — List all registered tools
- `discover(capabilities)` — Discover tools by capability strings

### 7.6 AgentManifest (`agentictools/tools/manifest.py`)

Declares which tools and capabilities an agent requires.

### 7.7 Concrete Tool Implementations (28 tools) [V4]

| Tool | File | Capabilities |
|---|---|---|
| `email` | `email_tool.py` | `email.send`, `email.read`, `email.list` |
| `crm` | `crm_tool.py` | `crm.read`, `crm.write`, `crm.search` |
| `browser` | `browser_tool.py` | `browser.read`, `browser.screenshot` |
| `database` | `database_tool.py` | `database.query`, `database.schema` |
| `slack` | `slack_tool.py` | `slack.send`, `slack.read` |
| `whatsapp` | `whatsapp_tool.py` | `whatsapp.send`, `whatsapp.read` |
| `github` | `github_tool.py` | `github.repo`, `github.pr`, `github.issue` |
| `excel` | `excel_tool.py` | `excel.read`, `excel.write` |
| `pdf` | `pdf_tool.py` | `pdf.read`, `pdf.extract` |
| `calendar` | `calendar_tool.py` | `calendar.read`, `calendar.write` |
| `search` | `search_tool.py` | `search.web`, `search.news` |
| `payments` | `payments_tool.py` | `payments.charge`, `payments.refund` |
| `maps` | `maps_tool.py` | `maps.geocode`, `maps.distance` |
| `ocr` | `ocr_tool.py` | `ocr.extract` |
| `calculator` | `calculator_tool.py` | `calculator.calculate`, `calculator.evaluate` |
| `compliance_checker` | `compliance_checker_tool.py` | `compliance.check`, `compliance.validate` |
| `enrichment_api` | `enrichment_api_tool.py` | `enrichment.data`, `enrichment.contact` |
| `newsletter_tools` | `newsletter_tools.py` | `newsletter.create`, `newsletter.send`, `newsletter.schedule` |
| `notification` | `notification_tool.py` | `notification.send`, `notification.notify` |
| `report` | `report_tool.py` | `report.generate`, `report.export` |
| `scraper` | `scraper_tool.py` | `scraper.scrape`, `scraper.extract` |
| `sentiment_analyzer` | `sentiment_analyzer_tool.py` | `sentiment.analyze`, `sentiment.score` |
| `seo_tool` | `seo_tool.py` | `seo.analyze`, `seo.audit` |
| `social_media_tool` | `social_media_tool.py` | `social.post`, `social.analyze` |
| `telemetry_tool` | `telemetry_tool.py` | `telemetry.collect`, `telemetry.report` |
| `ticket_tool` | `ticket_tool.py` | `ticket.create`, `ticket.update`, `ticket.resolve` |

---

## 8. V3 Artifact Store

### 8.1 ArtifactManager (`agentictools/runtime/artifacts.py`)

Manages persistent artifacts with file storage, checksums, and versioning.

**Key Methods:**
- `create(name, artifact_type, content, workspace, agent, metadata)` → `Artifact`
- `get(artifact_id)` → `Artifact`
- `list(tenant, artifact_type, agent, workspace)` → `QuerySet`
- `delete(artifact_id)` → `bool`
- `version(artifact_id, new_content)` → `Artifact` (new version)
- `create_version(original_artifact_id, content)` → `Artifact` (increments version)

**Features:**
- Automatic checksum computation (SHA-256)
- File persistence to `media/artifacts/<tenant_id>/<agent>/<uuid>_<name>`
- Version tracking (increments on each `version()` call)
- Workspace association via `WorkspaceModel`

### 8.2 Artifact REST API (`agentictools/views/artifacts.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/artifacts/` | GET | List artifacts (filterable by `type`, `agent`, `workspace`) |
| `/api/agentictools/artifacts/` | POST | Create artifact |
| `/api/agentictools/artifacts/<uuid:artifact_id>/` | GET | Retrieve artifact |
| `/api/agentictools/artifacts/<uuid:artifact_id>/` | DELETE | Delete artifact |
| `/api/agentictools/artifacts/<uuid:artifact_id>/download/` | GET | Download artifact file |
| `/api/agentictools/artifacts/<uuid:artifact_id>/version/` | POST | Create new version |

### 8.3 Artifact Model (`agentictools/models.py`)

```
Artifact:
  artifact_id (UUIDField, primary_key)
  tenant (ForeignKey → Tenant)
  name (CharField)
  artifact_type (CharField: pdf, word, excel, csv, markdown, html, json, sql, image, audio, video, presentation, zip, text, binary)
  content (JSONField)
  storage_path (FilePathField, nullable)
  checksum (CharField, nullable)
  version (IntegerField, default=1)
  workspace (ForeignKey → WorkspaceModel, nullable)
  agent (CharField, nullable)
  metadata (JSONField, default=dict)
  created_at (DateTimeField, auto_now_add)
  updated_at (DateTimeField, auto_now)
```

---

## 9. V3 Memory Bus API

### 9.1 MemoryBus (`agentictools/runtime/memory_bus.py`)

A dedicated memory bus for writing, reading, and searching memory records. Mirrors to BrainBoxMemory for legacy compatibility.

**Key Methods:**
- `write(memory_type, content, agent, workspace_id, source_ref, metadata)` → `MemoryRecord`
- `read(memory_type, agent, workspace_id, limit)` → `List[MemoryRecord]`
- `search_semantic(query, agent, limit)` → `List[MemoryRecord]`

**Memory Types:** `semantic`, `episode`, `execution`, `preference`, `workspace`, `tool`, `workflow`, `entity`, `inference`

**Legacy Mirroring:** Each `MemoryRecord` creates a corresponding `BrainBoxMemory` entry with `brainbox_ref` set to `memory:<memory_id>`.

### 9.2 Memory REST API (`agentictools/views/memory.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/memory/` | GET | List memory records (filterable by `type`, `agent`, `workspace`) |
| `/api/agentictools/memory/` | POST | Create memory record |
| `/api/agentictools/memory/<uuid:memory_id>/` | GET | Retrieve memory record |
| `/api/agentictools/memory/<uuid:memory_id>/` | DELETE | Delete memory record |
| `/api/agentictools/memory/search/` | GET | Search memory by query string |

### 9.3 MemoryRecord Model (`agentictools/models.py`)

```
MemoryRecord:
  memory_id (UUIDField, primary_key)
  tenant (ForeignKey → Tenant)
  memory_type (CharField: semantic, episode, execution, preference, workspace, tool, workflow, entity, inference)
  content (TextField)
  agent (CharField)
  workspace_id (CharField, nullable)
  source_ref (CharField, nullable)
  brainbox_ref (CharField, nullable)  # Legacy BrainBoxMemory reference
  metadata (JSONField, default=dict)
  created_at (DateTimeField, auto_now_add)
```

---

## 10. V3 Policy API

### 10.1 PolicyEngine (`agentictools/runtime/policy.py`)

Evaluates tenant-configurable policy rules against agent actions.

**Key Methods:**
- `evaluate(agent, action, context)` → `PolicyDecision`

**PolicyDecision:**
- `allowed` (bool)
- `requires_approval` (bool)
- `approver_role` (str)
- `reason` (str)

### 10.2 PolicyRuleModel (`agentictools/models.py`)

```
PolicyRuleModel:
  id (AutoField, primary_key)
  tenant (ForeignKey → Tenant)
  agent_pattern (CharField, default='*')  # Glob pattern for agent matching
  action_pattern (CharField, default='*')  # Glob pattern for action matching
  constraint_type (CharField: max_amount, rate_limit, time_window, require_approval, deny, allow, confidence_threshold)
  constraint_value (JSONField, default=dict)
  requires_approval_from (CharField, blank)
  is_active (BooleanField, default=True)
  priority (IntegerField, default=0)
  created_at (DateTimeField, auto_now_add)
  updated_at (DateTimeField, auto_now)
```

### 10.3 Policy REST API (`agentictools/views/policy.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/policy/` | GET | List policy rules |
| `/api/agentictools/policy/` | POST | Create policy rule |
| `/api/agentictools/policy/<int:rule_id>/` | GET | Retrieve policy rule |
| `/api/agentictools/policy/<int:rule_id>/` | PUT | Update policy rule |
| `/api/agentictools/policy/<int:rule_id>/` | DELETE | Delete policy rule |
| `/api/agentictools/policy/evaluate/` | POST | Evaluate a policy |
| `/api/agentictools/policy/<int:pk>/activate/` | POST | Activate a policy |

---

## 11. V3 Observability

### 11.1 Observability Views (`agentictools/views/observability.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/dashboard/` | GET | Dashboard summary (total executions, active agents, pending approvals, recent alerts) |
| `/api/agentictools/metrics/summary/` | GET | Metrics summary (executions, tools, agents, costs) |
| `/api/agentictools/metrics/agents/` | GET | Per-agent metrics |
| `/api/agentictools/metrics/tools/` | GET | Per-tool metrics |
| `/api/agentictools/metrics/sessions/` | GET | Session metrics |
| `/api/agentictools/metrics/health/` | GET | Tool health report from `ToolHealthMonitor.check_all()` |
| `/api/agentictools/metrics/alerts/` | GET | Active alerts from `_evaluate_alerts()` |
| `/api/agentictools/telemetry/agents/<str:agent_id>/` | GET | Agent-specific telemetry stats |

### 11.2 Alert Engine (`_evaluate_alerts`)

Evaluates tenant health and returns alerts:

| Alert Code | Condition | Level |
|---|---|---|
| `NO_ACTIVITY_24H` | No `ToolExecution` records in 24 hours | `warn` |
| `HIGH_FAILURE_RATE` | > 20% failure rate in last 100 executions | `warn` |
| `HIGH_APPROVAL_PENDING` | > 10 pending approvals older than 1 hour | `warn` |

### 11.3 Overall Status (`_overall_status`)

- `healthy` — No alerts
- `degraded` — Any `warn` level alerts
- `critical` — Any `error` level alerts

### 11.4 Telemetry System (`agentictools/telemetry/`)

**TelemetryCollector:**
- `record_execution(tenant, agent, tool, duration, success, cost)` — Records a tool execution
- `get_tenant_metrics(tenant, since)` — Returns aggregated metrics for a tenant
- `get_agent_metrics(tenant, agent, since)` — Returns aggregated metrics for an agent

**MetricAggregator:**
- `aggregate_hourly()` — Hourly aggregation of execution metrics
- `aggregate_by_agent()` — Per-agent aggregation
- `aggregate_by_tool()` — Per-tool aggregation

### 11.5 Event System (`agentictools/events/`)

**RuntimeEventTypes** (27 constants):
- `INTENT_RECEIVED`, `PLANNING_STARTED`, `PLAN_GENERATED`, `TOOL_STARTED`, `TOOL_FINISHED`, `TOOL_FAILED`
- `MEMORY_WRITTEN`, `MEMORY_READ`, `KNOWLEDGE_QUERIED`
- `APPROVAL_REQUESTED`, `APPROVAL_GRANTED`, `APPROVAL_DENIED`
- `RUNTIME_BLOCKED`, `RUNTIME_ERROR`, `WORKFLOW_COMPLETED`, `WORKFLOW_FAILED`
- `SESSION_CREATED`, `SESSION_CLOSED`, `WORKSPACE_CREATED`, `ARTIFACT_CREATED`
- `AGENT_THINKING`, `AGENT_ACTION`, `AGENT_ERROR`
- `SYSTEM_STARTUP`, `SYSTEM_SHUTDOWN`, `SYSTEM_WARNING`, `SYSTEM_ERROR`

**EventBus:**
- `publish(event_type, payload, tenant, source, agent, metadata)` — Publishes an event
- `subscribe(handler_path, event_type)` — Subscribes a handler
- Events are persisted to `BrainBoxEvent` and broadcast via WebSocket

---

## 12. V3 Tenant Agents

### 12.1 TenantAgentModel (`agentictools/models.py`)

```
TenantAgentModel:
  agent_id (UUIDField, primary_key, default=uuid4)
  tenant (ForeignKey → Tenant)
  name (CharField)
  description (TextField, blank)
  agent_type (CharField: reactive, proactive, hybrid)
  skill_ids (JSONField, default=list)
  tool_scope (JSONField, default=list)
  trigger_words (JSONField, default=list)
  memory_types (JSONField, default=list)
  system_prompt (TextField, blank)
  persona_name (CharField, blank)
  manifest_yaml (TextField, blank)
  is_published (BooleanField, default=False)
  is_active (BooleanField, default=True)
  metadata (JSONField, default=dict)
  created_at (DateTimeField, auto_now_add)
  updated_at (DateTimeField, auto_now)
```

### 12.2 TenantAgentConfig (`agentictools/runtime/tenant_agent.py`)

Maps database model to runtime configuration.

**Key Methods:**
- `from_db(agent_model)` → `TenantAgentConfig`
- `to_manifest_dict()` → `dict` (for marketplace listing)

### 12.3 TenantAgentRunner (`agentictools/runtime/tenant_agent.py`)

Loads and runs tenant agents.

**Key Methods:**
- `from_db(agent_id, tenant)` → `TenantAgentRunner`
- Raises `ValueError` if agent not found

### 12.4 Tenant Agents REST API (`agentictools/views/tenant_agents.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/tenant-agents/` | GET | List tenant agents |
| `/api/agentictools/tenant-agents/` | POST | Create tenant agent |
| `/api/agentictools/tenant-agents/<uuid:agent_id>/` | GET | Retrieve tenant agent |
| `/api/agentictools/tenant-agents/<uuid:agent_id>/` | PUT | Update tenant agent |
| `/api/agentictools/tenant-agents/<uuid:agent_id>/` | DELETE | Delete tenant agent |
| `/api/agentictools/tenant-agents/<uuid:agent_id>/publish/` | POST | Toggle publish status |
| `/api/agentictools/system-agents/<uuid:agent_id>/test/` | POST | Test an agent |

---

## 13. V3 Marketplace

### 13.1 MarketplaceRating Model (`agentictools/models.py`)

```
MarketplaceRating:
  id (AutoField, primary_key)
  tenant (ForeignKey → Tenant)
  package_id (CharField)
  rating (PositiveSmallIntegerField, help_text="1-5 stars")
  review (TextField, blank)
  created_at (DateTimeField, auto_now_add)
  updated_at (DateTimeField, auto_now)
  
  Meta: unique_together = (tenant, package_id)
```

### 13.2 Marketplace Views (`agentictools/views/marketplace.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/marketplace/` | GET | List marketplace packages (published agents + ratings) |
| `/api/agentictools/marketplace/installed/` | GET | List installed packages for tenant |
| `/api/agentictools/marketplace/<str:package_id>/` | GET | Get package details |
| `/api/agentictools/marketplace/<str:package_id>/install/` | POST | Install a package |
| `/api/agentictools/marketplace/<str:package_id>/uninstall/` | POST | Uninstall a package |
| `/api/agentictools/marketplace/<str:package_id>/rate/` | POST | Rate a package |

**Helper Functions:**
- `_get_ratings(package_id)` → `{'average': float, 'count': int}`
- `_agent_to_package_listing(agent, tenant)` → `dict` with `package_type`, `name`, `average_rating`, `is_installed`

---

## 14. V3 Workflow Composer

### 14.1 Workflow Composer (`agentictools/workflow/composer.py`)

Enables multi-agent orchestration by chaining agents together in a DAG.

**Classes:**
- `WorkflowStep` — Single step: `step_id`, `agent_id`, `action`, `parameters`, `depends_on`, `status`
- `Workflow` — Multi-agent DAG: `get_ready_steps()`, `to_dict()`
- `WorkflowComposer` — `compose_from_natural_language(description)` → `Workflow`, `execute(workflow, simulation)`
- `WorkflowOrchestrator` — `orchestrate(workflow)` — Executes steps respecting dependencies

**Key Features:**
- NL to Workflow: Converts "Find suppliers, verify them, add to CRM" into structured steps
- Simulation mode for dry-run validation
- Workspace assignment per workflow
- Status tracking: `pending` → `running` → `completed` | `failed`

### 14.2 WorkflowModel (`agentictools/models.py`)

```
WorkflowModel:
  id (AutoField, primary_key)
  tenant (ForeignKey → Tenant)
  workflow_id (CharField, db_index=True)
  goal (TextField)
  steps (JSONField, default=list)
  workflow_data (JSONField, default=dict, blank=True)
  status (CharField, default='pending')
  created_at (DateTimeField, auto_now_add)
  updated_at (DateTimeField, auto_now=True)
  completed_at (DateTimeField, null=True, blank=True)
```

### 14.3 Workflow REST API (`agentictools/views/workflows.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/workflows/` | GET | List workflows |
| `/api/agentictools/workflows/create/` | POST | Create a workflow |
| `/api/agentictools/workflows/<str:workflow_id>/` | GET | Get workflow details |
| `/api/agentictools/workflows/<str:workflow_id>/execute/` | POST | Execute a workflow |

---

## 15. V3 Event System & Telemetry

### 15.1 Event System (`agentictools/events/`)

Three-file event system:

| File | Contents |
|---|---|
| `types.py` | `RuntimeEventTypes` — 27 canonical event constants (dataclass with `value` and `description`) |
| `envelope.py` | `EventEnvelope` — Standard event wrapper: `event_type`, `payload`, `tenant_id`, `source`, `agent`, `metadata`, `timestamp`, `event_id` |
| `bus.py` | `EventBus` — Durable pub/sub: `publish()` persists to `BrainBoxEvent` + broadcasts via WebSocket; `subscribe()` registers dotted-path handlers |

### 15.2 Telemetry (`agentictools/telemetry/`)

| File | Contents |
|---|---|
| `telemetry.py` | `TelemetryCollector` — Per-tenant metrics: `record_execution()`, `get_tenant_metrics()`, `get_agent_metrics()`; `MetricAggregator` — Time-series aggregation: `aggregate_hourly()`, `aggregate_by_agent()`, `aggregate_by_tool()` |

---

## 16. V3 WebSocket Streaming

### 16.1 WebSocket Consumer (`agentictools/streaming/consumers.py`)

**RuntimeEventConsumer** (Django Channels `AsyncWebsocketConsumer`):
- JWT authentication via query string `token` parameter
- Subscribe/unsubscribe protocol for event types
- Channel-layer group broadcasting
- `broadcast_event()` — Synchronous helper bridging `EventBus` to WebSocket clients

**Protocol:**
```json
// Subscribe
{"type": "subscribe", "event_types": ["TOOL_STARTED", "TOOL_FINISHED"]}

// Unsubscribe
{"type": "unsubscribe", "event_types": ["TOOL_STARTED"]}

// Server event
{"type": "runtime_event", "event_type": "TOOL_STARTED", "payload": {...}, "timestamp": "..."}
```

### 16.2 Execution Streaming (`agentictools/streaming/consumers_execution.py`) [V4]

Additional streaming capabilities for execution events and real-time progress updates.

---

## 17. V3 Skills System

### 17.1 Skills (`agentictools/skills/`)

Declarative skill system for reusable agent capabilities.

**Classes:**
- `Skill` — Dataclass: `name`, `description`, `inputs`, `outputs`, `handler`
- `SkillRegistry` — `register(skill)`, `get(name)`, `list_all()`, `find_by_capability()`

**Concrete Skills (from definitions.py):**
Extensive skill definitions including:
- `WebsiteAuditor` — Analyzes website HTML for technographics
- `SEOAnalyzer` — Analyzes SEO metadata and page structure
- `InvoiceExtractor` — Extracts structured data from invoices
- `LeadGenerator` — Generates leads from search results
- `VendorVerifier` — Verifies vendor credentials and compliance
- And many more defined in `definitions.py` (24KB file)

### 17.2 Skills REST API (`agentictools/skills/views.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/skills/` | GET | List all skills (registry + DB) |
| `/api/agentictools/skills/<str:skill_id>/` | GET | Get skill details |

### 17.3 Skill Model (`agentictools/models.py`)

```
Skill:
  tenant (ForeignKey → Tenant)
  name (CharField)
  description (TextField)
  permissions (JSONField, default=list)
  triggers (JSONField, default=list)
  tools (JSONField, default=list, help_text="List of tool names used by this skill")
  prompt_template (TextField, blank=True)
  output_schema (JSONField, null=True, blank=True)
  is_active (BooleanField, default=True)
  created_at (DateTimeField, auto_now_add)
  
  Meta: unique_together = (tenant, name)
```

---

## 18. V3 Background Tasks & Scheduler

### 18.1 Background Task Manager (`agentictools/background/scheduler.py`) [V4]

Advanced task scheduling and management system.

**Classes:**
- `BackgroundTaskManager` — Manages background task lifecycle
- `ScheduledTask` — Represents a scheduled task with cron-like scheduling

**Key Methods:**
- `schedule_task(task_func, schedule, kwargs)` — Schedule a background task
- `cancel_task(task_id)` — Cancel a scheduled task
- `list_tasks()` — List all scheduled tasks
- `get_task_status(task_id)` — Get task execution status

### 18.2 Background Tasks REST API (`agentictools/views/background_tasks.py`)

| Endpoint | Method | Description |
|---|---|---|
| `/api/agentictools/background-tasks/` | GET | List background tasks |
| `/api/agentictools/background-tasks/<str:task_id>/` | GET | Get task details |
| `/api/agentictools/background-tasks/<str:task_id>/cancel/` | POST | Cancel a background task |

---

## 19. V3 Package System

### 19.1 Package Manager (`agentictools/packages/manager.py`)

Agent package management and loading system.

**Classes:**
- `PackageManager` — Manages package installation, loading, and lifecycle
- `PackageLoader` — Loads package manifests and dependencies
- `PackageManifest` — Represents package metadata and configuration

**Key Methods:**
- `install_package(package_id, source)` — Install a package
- `uninstall_package(package_id)` — Uninstall a package
- `load_package(package_id)` — Load a package into runtime
- `list_packages()` — List all installed packages
- `get_package_manifest(package_id)` — Get package metadata

### 19.2 Package Installation Model (`agentictools/models.py`)

```
PackageInstallation:
  tenant (ForeignKey → Tenant, null=True, blank=True)
  package_id (CharField, db_index=True)
  name (CharField)
  version (CharField)
  package_type (CharField, default='official')
  manifest (JSONField, default=dict)
  source_path (CharField, blank=True)
  status (CharField: installed, enabled, disabled, failed)
  is_enabled (BooleanField, default=False)
  installed_at (DateTimeField, auto_now_add)
  updated_at (DateTimeField, auto_now=True)
  
  Meta: unique_together = (tenant, package_id)
```

---

## 20. V3 Console Interface

### 20.1 Agent Console (`agentictools/console/console.py`) [V4]

Interactive console for agent debugging and management.

**Classes:**
- `AgentConsole` — Interactive console with REPL-like interface

**Key Methods:**
- `start()` — Start the console interface
- `execute_command(command)` — Execute a console command
- `list_agents()` — List all available agents
- `inspect_agent(agent_id)` — Inspect agent configuration and state
- `test_agent(agent_id, input)` — Test an agent with input

**Commands:**
- `list` — List agents
- `inspect <agent_id>` — Inspect agent
- `test <agent_id> <input>` — Test agent
- `status` — Show system status
- `help` — Show help

---

## 21. V3 URL Routing & API Map

### 21.1 V3 API URLs (`agentictools/api_urls.py`)

All V3 endpoints are under `/api/agentictools/`:

| URL Pattern | View | Name |
|---|---|---|
| `tools/` | `ToolListView` | `tool-list` |
| `tools/execute/` | `ToolExecuteView` | `tool-execute` |
| `plans/` | `PlanCreateView` | `plan-create` |
| `plans/<int:pk>/` | `PlanDetailView` | `plan-detail` |
| `background-tasks/` | `BackgroundTaskListView` | `background-task-list` |
| `background-tasks/<str:task_id>/` | `BackgroundTaskDetailView` | `background-task-detail` |
| `background-tasks/<str:task_id>/cancel/` | `BackgroundTaskCancelView` | `background-task-cancel` |
| `plugins/` | `PluginListView` | `plugin-list` |
| `plugins/install/` | `PluginInstallView` | `plugin-install` |
| `plugins/toggle/` | `PluginToggleView` | `plugin-toggle` |
| `artifacts/` | `ArtifactListView` | `artifact-list` |
| `artifacts/<uuid:artifact_id>/` | `ArtifactDetailView` | `artifact-detail` |
| `artifacts/<uuid:artifact_id>/download/` | `ArtifactDownloadView` | `artifact-download` |
| `artifacts/<uuid:artifact_id>/version/` | `ArtifactVersionView` | `artifact-version` |
| `memory/` | `MemoryListView` | `memory-list` |
| `memory/<uuid:memory_id>/` | `MemoryDetailView` | `memory-detail` |
| `memory/search/` | `MemorySearchView` | `memory-search` |
| `policies/` | `PolicyListView` | `policy-list` |
| `policies/evaluate/` | `PolicyEvaluateView` | `policy-evaluate` |
| `policies/<int:pk>/` | `PolicyDetailView` | `policy-detail` |
| `policies/<int:pk>/activate/` | `PolicyActivateView` | `policy-activate` |
| `metrics/` | `MetricsSummaryView` | `metrics-summary` |
| `metrics/agents/` | `MetricsAgentsView` | `metrics-agents` |
| `metrics/tools/` | `MetricsToolsView` | `metrics-tools` |
| `metrics/sessions/` | `MetricsSessionsView` | `metrics-sessions` |
| `metrics/health/` | `MetricsHealthView` | `metrics-health` |
| `dashboard/` | `DashboardView` | `dashboard` |
| `telemetry/agents/<str:agent_id>/` | `AgentTelemetryView` | `telemetry-agent-stats` |
| `tenant-agents/` | `TenantAgentListView` | `tenant-agent-list` |
| `tenant-agents/<uuid:agent_id>/` | `TenantAgentDetailView` | `tenant-agent-detail` |
| `tenant-agents/<uuid:agent_id>/publish/` | `TenantAgentPublishView` | `tenant-agent-publish` |
| `tenant-agents/<uuid:agent_id>/test/` | `TenantAgentTestView` | `tenant-agent-test` |
| `marketplace/` | `MarketplaceListView` | `marketplace-list` |
| `marketplace/installed/` | `MarketplaceInstalledView` | `marketplace-installed` |
| `marketplace/<str:package_id>/` | `MarketplaceDetailView` | `marketplace-detail` |
| `marketplace/<str:package_id>/install/` | `MarketplaceInstallView` | `marketplace-install` |
| `marketplace/<str:package_id>/uninstall/` | `MarketplaceUninstallView` | `marketplace-uninstall` |
| `marketplace/<str:package_id>/rate/` | `MarketplaceRateView` | `marketplace-rate` |
| `skills/` | `include('agentictools.skills.urls')` | `skills` |
| `workflows/` | `WorkflowListView` | `workflow-list` |
| `workflows/create/` | `WorkflowCreateView` | `workflow-create` |
| `workflows/<str:workflow_id>/` | `WorkflowDetailView` | `workflow-detail` |
| `workflows/<str:workflow_id>/execute/` | `WorkflowExecuteView` | `workflow-execute` |
| `runtime/execute/<str:agent_id>/` | `RuntimeExecuteView` | `runtime-execute` |
| `runtime/status/<str:agent_id>/` | `RuntimeStatusView` | `runtime-status` |

### 21.2 Root URL Routing (`agentictools/urls.py`)

| Path | Module |
|---|---|
| `/api/agentictools/` | `agentictools.api_urls` |
| `/api/accounts/` | `accounts.urls` |
| `/api/core/` | `core.urls` |
| `/api/brainbox/` | `brainbox.urls` |
| `/api/billing/` | `billing.urls` |
| `/api/monica/` | `monica.urls` |
| `/api/marketer/` | `marketer.urls` |
| `/api/businessfinder/` | `businessfinder.urls` |
| `/api/finance/` | `finance.urls` |
| `/api/governance/` | `governance.urls` |
| `/api/maintenance/` | `maintenance.urls` |
| `/api/risk_detection/` | `risk_detection.urls` |
| `/admin/` | Django admin |
| `/` | Frontend SPA catch-all |

---

## 22. V3 Data Models

### 22.1 V3-Specific Models (`agentictools/models.py`)

| Model | Purpose | Key Fields |
|---|---|---|
| `TaskPlanModel` | Persisted task plans | `id`, `tenant`, `agent`, `goal`, `plan_data`, `status`, `current_node` |
| `WorkflowModel` | Workflow definitions | `id`, `tenant`, `workflow_id`, `goal`, `steps`, `status`, `workflow_data` |
| `ToolExecution` | Tool execution history | `id`, `tenant`, `tool_name`, `agent_id`, `parameters`, `success`, `result`, `error`, `duration_ms`, `cost_estimate` |
| `Artifact` | Persistent file artifacts | `artifact_id`, `tenant`, `name`, `artifact_type`, `content`, `storage_path`, `checksum`, `version`, `workspace`, `agent` |
| `MemoryRecord` | Memory bus entries | `memory_id`, `tenant`, `memory_type`, `content`, `agent`, `workspace_id`, `source_ref`, `brainbox_ref` |
| `Plugin` | Registered plugin definitions | `id`, `tenant`, `name`, `version`, `description`, `configuration`, `is_active` |
| `Skill` | Reusable skill definitions | `id`, `tenant`, `name`, `description`, `permissions`, `triggers`, `tools`, `prompt_template`, `output_schema`, `is_active` |
| `RuntimeEvent` | Canonical persisted events | `id`, `tenant`, `event_type`, `source`, `subject`, `agent`, `session_id`, `workspace_id`, `correlation_id`, `causation_id`, `payload`, `metadata`, `status` |
| `EventSubscription` | Durable event subscriptions | `id`, `tenant`, `name`, `event_types`, `handler_path`, `is_active`, `configuration` |
| `EventDelivery` | Event delivery tracking | `id`, `event`, `subscription`, `status`, `attempts`, `last_error`, `delivered_at` |
| `PackageInstallation` | Installed package records | `id`, `tenant`, `package_id`, `name`, `version`, `package_type`, `manifest`, `source_path`, `status`, `is_enabled` |
| `WorkspaceModel` | Workspace metadata | `id`, `tenant`, `agent`, `task_id`, `session_id`, `metadata`, `snapshot` |
| `RuntimeSessionModel` | Runtime sessions | `id`, `tenant`, `session_id`, `agent`, `workspace_id`, `status`, `variables`, `execution_state`, `metrics`, `memory_scope`, `tool_scope` |
| `PolicyRuleModel` | Configurable policy rules | `id`, `tenant`, `agent_pattern`, `action_pattern`, `constraint_type`, `constraint_value`, `requires_approval_from`, `is_active`, `priority` |
| `TenantAgentModel` | Tenant-scoped agent configs | `agent_id`, `tenant`, `name`, `agent_type`, `skill_ids`, `tool_scope`, `trigger_words`, `memory_types`, `system_prompt`, `persona_name`, `is_published`, `is_active` |
| `MarketplaceRating` | Agent marketplace ratings | `id`, `tenant`, `package_id`, `rating`, `review` |

### 22.2 V2 Models (from `brainbox/models.py`)

| Model | Layer | Purpose |
|---|---|---|
| `BrainBoxEvent` | Event Store | Chronological audit trail of every agent action |
| `BrainBoxMemory` | Semantic Memory | Vectorized documents and agent outputs (384-dim pgvector) |
| `BrainBoxEntity` | Knowledge Graph (Nodes) | Real-world constructs: Vendor, Asset, Invoice, etc. |
| `BrainBoxRelationship` | Knowledge Graph (Edges) | Connections between entities |
| `BrainBoxInference` | Inference Layer | Derived facts and predictions |

### 22.3 V1 Models (from `accounts/models.py`)

| Model | Purpose |
|---|---|
| `Tenant` | Organization/company with `subdomain`, `api_key`, `owner` |
| `UserProfile` | Links Django `User` to a `Tenant` |
| `UniversalUser` | End-user/customer of the tenant |
| `UniversalTransaction` | Payment records |
| `UniversalTicket` | Support tickets with sentiment scoring |
| `StrategicContext` | Marketing intelligence |
| `TenantIntegration` | Encrypted API keys for third-party services |
| `AgentConfig` | Per-tenant agent settings (mode, personality prompt) |

### 22.4 Core Models (from `core/models.py`)

| Model | Purpose |
|---|---|
| `ApprovalQueue` | HITL pipeline for agent actions |
| `KnowledgeBase` | Tenant file storage for RAG |
| `KnowledgeBaseChunk` | Vectorized text chunks for semantic search |
| `TaskLog` | Celery task audit log |
| `Notification` | In-app notifications for tenants |

---

## 23. Module Reference

### 23.1 agentictools (Kernel)

The system kernel. Provides global configuration, URL routing, ASGI/WSGI entrypoints, and shared utilities.

**Key Files:**
- `settings.py`: Defines installed apps, middleware, database, Celery, REST framework, CORS, and external API credentials.
- `urls.py`: Root URL dispatcher routing `/api/<module>/` to respective apps.
- `celery.py`: Celery app configuration with periodic task schedule.
- `asgi.py`: ASGI entrypoint using Daphne for WebSocket support.

**Installed Apps (from `settings.py`):**

```
daphne, django.contrib.admin, django.contrib.auth,
rest_framework, rest_framework_simplejwt, corsheaders, channels,
core, billing, brainbox, accounts, backup,
monica, marketer, businessfinder, governance, finance, maintenance, risk_detection
```

**Periodic Tasks (Celery Beat):**

| Task | Schedule | Module |
|---|---|---|
| `marketer.tasks.auto_execute_marketing` | Every 6 hours | marketer |
| `marketer.tasks.periodic_strategy_optimization` | Every 12 hours | marketer |
| `monica.tasks.sync_rag_knowledge` | Daily at 2:00 AM | monica |
| `businessfinder.tasks.run_intent_scraper` | Every 8 hours | businessfinder |
| `core.tasks.periodic_knowledge_base_sync` | Daily at midnight | core |

**External Integrations (Credentials in settings):**

- LLMs: Groq
- Social: Twitter (OAuth 1.0a), LinkedIn, Meta, Google Ads, TikTok
- Translation: DeepL
- Voice: ElevenLabs
- Data Enrichment: Apollo API, API Ninjas
- Imaging: Stability AI
- Storage: Dropbox
- Error Tracking: Sentry

### 23.2 accounts (Tenant Management)

Handles multi-tenancy, user identity, authentication, and organizational isolation.

#### Data Models

| Model | Description |
|---|---|
| `Tenant` | Organization/company. Has `subdomain`, `api_key`, `owner`. |
| `UserProfile` | Links Django `User` to a `Tenant`. |
| `UniversalUser` | End-user/customer of the tenant (CRM perspective). |
| `UniversalTransaction` | Payment records tied to a `UniversalUser`. |
| `UniversalTicket` | Support tickets with sentiment scoring. |
| `StrategicContext` | Marketing intelligence: keywords, competitors, value prop, tech stack. |
| `TenantIntegration` | Encrypted API keys for third-party services (Zendesk, Stripe, etc.). |
| `AgentConfig` | Per-tenant agent settings: mode (`manual`/`hybrid`/`autonomous`), personality prompt, intelligence core. |

**Key Behaviors:**
- `Tenant.save()` auto-generates a UUID `api_key` if missing.
- `TenantIntegration.vault` property decrypts stored credentials.
- `AgentConfig` has unique constraint on `(tenant, agent_id)`.

### 23.3 core (Orchestration Layer)

The central nervous system that routes requests, manages approvals, and coordinates agents.

#### Data Models

| Model | Description |
|---|---|
| `ApprovalQueue` | HITL pipeline. Tracks proposed actions with `risk_level`, `confidence_score`, `reasoning`. Statuses: pending, approved, rejected, overridden, executed, failed. |
| `KnowledgeBase` | Tenant file storage for RAG. Supports PDF, CSV, TXT, etc. Triggers async indexing. |
| `KnowledgeBaseChunk` | Vectorized text chunks (384-dim pgvector) for semantic search. |
| `TaskLog` | Celery task audit log. |
| `Notification` | In-app notifications for tenants. |

#### Core Logic

**`core/logic/IntentManager.py`** (referenced in views):
- Resolves incoming intents to the appropriate agent vertical.
- Manages the full lifecycle: trigger → propose → (approve) → execute → log.
- Interacts with `ApprovalQueue` for HITL workflows.

**`core/logic/SystemHealth.py`**:
- Health check aggregator that validates the master script and frontend availability.

#### API Views

| View / ViewSet | Endpoints | Purpose |
|---|---|---|
| `ApprovalQueueViewSet` | CRUD + `/approve/`, `/reject/`, `/pending_count/` | HITL approval management |
| `KnowledgeBaseViewSet` | CRUD + `/search/?q=` | Document upload and RAG search |
| `NotificationViewSet` | CRUD + `/mark_all_read/` | Tenant notifications |
| `TaskLogViewSet` | Read-only | Celery task history |
| `RiskMapAggregatorView` | GET | Aggregates `BrainBoxInference` risk scores by department |
| `SystemHealthView` | GET | System health diagnostics |

### 23.4 brainbox (Memory Substrate)

The shared intelligence layer. Decoupled from agent logic to enable cross-agent learning.

#### Data Models

| Model | Layer | Description |
|---|---|---|
| `BrainBoxEvent` | 1 - Event Store | Chronological audit trail of every agent action. Tracks status, risk, confidence, outcome, duration. |
| `BrainBoxMemory` | 2 - Semantic Memory | Vectorized documents and agent outputs. 384-dim embeddings via pgvector. Source types: document, agent_run, chat, contract, policy, audit. |
| `BrainBoxEntity` | 3 - Knowledge Graph (Nodes) | Real-world constructs: Vendor, Asset, Contractor, Invoice, Customer, etc. |
| `BrainBoxRelationship` | 3 - Knowledge Graph (Edges) | Connections between entities: `supplies`, `maintained_by`, `manages`, `approved_by`, `belongs_to`. |
| `BrainBoxInference` | 4 - Inference Layer | Derived facts and predictions. Types: `vendor_risk`, `failure_probability`, `runway_forecast`. Includes confidence, reasoning, and expiry. |

#### Indexing Strategy

- `BrainBoxEvent`: Composite index on `(tenant, agent, -created_at)` and `(tenant, action_type)`.
- `BrainBoxEntity`: Index on `(tenant, entity_type)`.
- `BrainBoxRelationship`: Index on `(tenant, relation_type)`.
- `BrainBoxInference`: Index on `(tenant, inference_type)`.

### 23.5 billing (Monetization)

Proxies the **Pluggedspace Payments Platform** (`https://auth.pluggedspace.org/api/v1/billing`). Weave no longer stores local billing models; instead it delegates all billing operations to the centralized billing service.

**Files:**
- `client.py`: `BillingClient` wrapper covering usage metering, entitlements, wallet/balance/ledger, pricing, subscriptions, invoices, credit reservations, tax, checkout, and health checks.
- `views.py`: Tenant-scoped API endpoints that call `BillingClient`.
- `urls.py`: Routes under `/api/billing/`.
- `models.py`: Legacy models kept for reference but not actively used by the new client flow.

**Environment Variables:**
- `BILLING_API_URL`: Base URL of the payments platform.
- `Weave_BILLING_SERVICE_KEY`: Service API key sent as `X-Service-Key: Weave`.

**Source System:** All calls set `X-Source-System: Weave`.

### 23.6 backup (Resilience)

Automated data recovery and backup utilities.

- `tasks.py`: Celery tasks for scheduled backups.
- `drive_utils.py`: Cloud storage integration (e.g., Dropbox, Google Drive).
- `cron.py`: Cron-style scheduling logic.
- `management/commands/`: Custom Django management commands.

### 23.7 frontend (User Interface)

A Next.js 15+ application providing:
- Agent dashboard and status monitoring.
- HITL Approval Queue interface.
- Knowledge Base document management.
- Notification center.
- Multi-tenant switching.

Tech: React, TypeScript, TailwindCSS (PostCSS), ESLint.

---

## 24. Agent Verticals

### 24.1 Agent Overview

| Agent | Domain | Risk Profile | Key Capabilities |
|---|---|---|---|
| **Monica** | Customer Service | Low | FAQ RAG, dispute management, ticket routing, appointment scheduling, sentiment analysis |
| **Marketer** | Marketing & CRM | Medium | SEO analysis, lead generation, social media posting, CRM growth |
| **Business Finder** | Market Intelligence | Low | Competitor analysis, web scraping, lead discovery, technographics |
| **Governance** | Compliance & Procurement | High | Vendor verification, invoice auditing, compliance checking, regulatory mapping |
| **Finance** | Financial Analysis | High | Cashflow forecasting, budget tracking, anomaly detection, expense categorization |
| **Maintenance** | Industrial IoT | Medium | Predictive maintenance, sensor data analysis, failure prediction |
| **Risk Detection** | Security | High | Threat detection, anomaly alerts, security monitoring |

### 24.2 Monica Agent (`agents/monica/`)

**Models:** FAQ, Dispute, DisputeStatusHistory, SupportIntelligence, DynamicRAGConfig, ConversationContinuity, AppointmentScheduler, TicketManagement, RoutingRules, SystemLogAnalysis

**Key Logic:**
- `DiagnosticEngine` — LLM-powered log analysis with interactive guide generation
- FAQ RAG with pgvector embeddings (384-dim)
- Dispute lifecycle: `pending → in_progress → resolved/escalated/closed`
- Sentiment-based routing rules

### 24.3 Governance Agent (`agents/governance/`)

**Key Logic:**
- `GovernanceAgent` — `verify_vendor()`, `audit_invoice()`, `check_compliance()`
- High-risk agent with strict HITL enforcement
- Integrates with BrainBox for vendor entity tracking

### 24.4 Finance Agent (`agents/finance/`)

**Models:** Tracker, Category, Transaction, Budget, Workspace

**Services:**
- `analytics.py` — `detect_anomalies()`, `forecast_category_spending()`, `calculate_budget_utilization()`
- `reporting_utils.py` — `calculate_budget_status()`

---

## 25. System Flow

### 25.1 The Agentic Loop

```
Trigger (API / Webhook / Cron / User Message)
        │
        ▼
Intent Resolution (core.logic.IntentManager)
        │
        ▼
Contextualization (Query BrainBox for memory & entities)
        │
        ▼
Proposal (Agent generates action plan)
        │
        ▼
Risk Classification
   ┌──────┴──────┐
   ▼             ▼
 Low Risk      High Risk
   │             │
   ▼             ▼
 Auto-Execute  Approval Queue (HITL)
   │             │
   │             ▼
   │      Human Review
   │       ┌────┴────┐
   │       ▼         ▼
   │    Approve    Reject
   │       │
   │       ▼
   │   Celery Execution
   │       │
   └───────┘
           ▼
      Telemetry → BrainBox
```

### 25.2 HITL Modes (per AgentConfig)

| Mode | Behavior |
|---|---|
| `autonomous` | Low-risk actions execute immediately. High-risk actions still queue for approval. |
| `hybrid` | Auto-approves low-risk actions. Requires human approval for medium/high-risk actions. (Recommended default) |
| `manual` | Every action requires explicit human approval. |

---

## 26. Infrastructure & Deployment

### 26.1 Technology Stack

| Component | Technology | Purpose |
|---|---|---|
| Backend Framework | Django 5.0+ / DRF | API, ORM, Auth, Admin |
| ASGI Server | Daphne | WebSocket + HTTP |
| Task Queue | Celery + Redis | Background execution |
| Database | PostgreSQL 15+ + pgvector | Primary data + vector embeddings |
| Frontend | Next.js 15+ / React 19 / TypeScript | Dashboard |
| Containerization | Docker + Docker Compose | Deployment |
| Reverse Proxy | Caddy | TLS, static files |
| Error Tracking | Sentry | Production monitoring |
| Static Files | WhiteNoise | CDN-ready serving |

### 26.2 Celery Beat Schedule

| Task | Schedule |
|---|---|
| `marketer.tasks.auto_execute_marketing` | Every 6 hours |
| `marketer.tasks.periodic_strategy_optimization` | Every 12 hours |
| `monica.tasks.sync_rag_knowledge` | Daily at 2:00 AM |
| `businessfinder.tasks.run_intent_scraper` | Every 8 hours |
| `core.tasks.periodic_knowledge_base_sync` | Daily at midnight |

### 26.3 Environment Variables

| Variable | Purpose |
|---|---|
| `SECRET_KEY` | Django secret |
| `DEBUG` | Debug mode |
| `DB_NAME/USER/PASSWORD/HOST/PORT` | PostgreSQL connection |
| `CELERY_BROKER_URL` | Redis URL |
| `GROQ_API_KEY` | LLM provider |
| `RAPIDAPI_KEY` | External APIs |
| `DROPBOX_TOKEN` | Backup storage |
| `FERNET_SECRET/KEY` | Credential encryption |
| `SENTRY_DSN` | Error tracking |
| `BILLING_API_URL` | Payments platform |
| `Weave_BILLING_SERVICE_KEY` | Billing service key |

### 26.4 Docker Services

| Service | Image | Ports |
|---|---|---|
| `web` | Custom Django | 8000 |
| `db` | PostgreSQL 15+ pgvector | 5432 |
| `redis` | Redis 7+ | 6379 |
| `celery_worker` | Custom (same as web) | — |
| `celery_beat` | Custom (same as web) | — |
| `caddy` | Caddy 2 | 80, 443 |

---

## 27. Test Suite

### 27.1 Test Files

| File | Scope | Tests |
|---|---|---|
| `scratch/tests/test_v3_phase3_5.py` | Unit tests for V3 Phases 3-5 | 33 tests |
| `scratch/tests/test_v3_runtime_phase2.py` | Integration tests for V3 Runtime Phase 2 | 10 test sections |
| `scratch/tests/test_system_integration.py` | End-to-end system integration | 12 validation sections |

### 27.2 Test Coverage

**Phase 3-5 Tests (33 tests):**
- ToolSDK: 9 tests (schema validation, health monitoring, telemetry)
- ArtifactStore: 3 tests (create, version, serialize)
- PolicyAdmin: 3 tests (create rule, evaluate, serialize)
- Observability: 4 tests (alerts, status, health monitor)
- TenantAgents: 5 tests (create, config, publish, runner, not found)
- Marketplace: 4 tests (create rating, update, get ratings, agent listing)
- MemoryBusAPI: 2 tests (write/read, serialize)
- WebSocket: 1 test (broadcast without channels)
- URLWiring: 2 tests (URLs load, names resolvable)

**Runtime Phase 2 Tests (10 sections):**
- Workspace isolation & path validation
- Workspace snapshots & restores
- Memory Bus writes, search, legacy mirroring
- Artifact Store creation & versioning
- Policy Engine constraint evaluation
- Context Builder assembly & token budgeting
- Session creation & metrics logging
- Full integrated AgentRuntime execute flow
- Cleanup

**System Integration Tests (12 sections):**
- Tenant & Auth Isolation
- BrainBox Event Store & Knowledge Graph
- Inbox Queue & Approval Lifecycle
- Finance Services & Bug Fixes
- Governance Agent Analytics
- Maintenance Telemetry Connector
- Monica Diagnostic Workflow
- BusinessFinder Discovery
- Tool Registry & Discovery
- V2 Runtime Engine
- Workflow Composer & Multi-Agent Orchestration
- Runtime Memory Persistence

---

## 28. Known Issues & Roadmap

### 28.1 Known Issues

| Issue | Description | Status |
|---|---|---|
| `DateTimeField` naive datetime warnings | `WorkflowModel.completed_at` receives naive datetimes with `USE_TZ=True` | Open |
| `datetime.utcnow()` deprecation | `sdk.py` uses deprecated `datetime.utcnow()` | Open |
| Artifact auto-registration | Only occurs inside `tool_runner` on tool execution results, not from intent payloads | By Design |
| Cross-tenant memory leakage (historical) | Fixed by adding tenant-scoping middleware | Resolved |
| Approval Queue bottleneck | During burst testing (100 simultaneous proposals) | Mitigated (priority queuing) |
| Memory embedding degradation | Semantic memory quality degrades over time | Open (future research) |

### 28.2 Roadmap

| Phase | Features | Status |
|---|---|---|
| Phase 3 | Tool SDK, Artifact Store | ✅ Complete |
| Phase 4 | Memory Bus API, Policy API, Observability | ✅ Complete |
| Phase 5 | Tenant Agents, Marketplace | ✅ Complete |
| Phase 6 | Self-evolving memory, memory pruning | 🔜 Planned |
| Phase 7 | Cross-tenant anonymized learning | 🔜 Planned |
| Phase 8 | GNN integration for Knowledge Graph | 🔜 Planned |
| Phase 9 | Adaptive risk classification (ML-based) | 🔜 Planned |
| Phase 10 | Agent composition languages (no-code) | 🔜 Planned |
| V4 | 28 Tools, Enhanced Subsystems, Console, Scheduler | ✅ Complete |

### 28.3 Comparison: V1 vs V2 vs V3 vs V4

| Feature | V1 (Siloed) | V2 (Agentic OS) | V3 (Unified Platform) | V4 (Enhanced) |
|---|---|---|---|---|
| **Architecture** | Independent agents | Shared Runtime Engine | Unified SDK + APIs | Enhanced Ecosystem |
| **Tooling** | Hard-coded functions | Dynamic ToolRegistry | ToolSchema validation + HealthMonitor | 28 Tools, Enhanced SDK |
| **Memory** | Isolated per agent | BrainBox (4 layers) | MemoryBus API + Artifact Store | Enhanced Memory Bus |
| **Policy** | None | PolicyEngine (runtime) | PolicyRuleModel + REST API | Enhanced Policy Engine |
| **Observability** | Basic logging | EventStream | Dashboard + Metrics + Alerts | Enhanced Observability |
| **Agents** | Fixed per deployment | Runtime-managed | TenantAgentModel + Marketplace | Enhanced Tenant Agents |
| **Orchestration** | Manual | WorkflowComposer (DAG) | WorkflowComposer + simulation | Enhanced Workflows |
| **Safety** | None | SafetyLayer | SafetyLayer + PolicyEngine | Enhanced Safety |
| **HITL** | None | ApprovalQueue | ApprovalQueue + risk classification | Enhanced HITL |
| **Multi-Tenancy** | None | Tenant-scoped models | Tenant-scoped + AgentConfig | Enhanced Multi-Tenancy |
| **Artifacts** | None | None | ArtifactManager + versioning | Enhanced Artifacts |
| **Marketplace** | None | None | Package listings + ratings | Enhanced Marketplace |
| **WebSocket** | None | None | RuntimeEventConsumer | Enhanced Streaming |
| **Event System** | None | None | EventBus (27 event types) | Enhanced Events |
| **Telemetry** | None | None | TelemetryCollector + MetricAggregator | Enhanced Telemetry |
| **Skills** | None | None | SkillRegistry (5 skills) | Enhanced Skills (extensive) |
| **Background Tasks** | None | None | BackgroundTaskManager | Enhanced Scheduler |
| **Package System** | None | None | PackageManager | Enhanced Packages |
| **Console** | None | None | None | AgentConsole |
| **Tests** | None | None | 33 unit + 10 integration + 12 system | Enhanced Test Suite |

---

*Document generated from comprehensive codebase analysis. For the most up-to-date information, refer to the source code and test files.*
