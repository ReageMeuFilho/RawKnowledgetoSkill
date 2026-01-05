# 🏗️ CitadelOS Complete Technical Architecture
## The Unified Digital Workforce Platform

**Version**: 1.0
**Date**: January 2026
**Status**: Architecture Specification

---

## Executive Summary

CitadelOS combines a **production-ready financial core** (Treasury OS) with an **AI-powered skills framework** (Digital Workforce) to create an unprecedented platform for property management, fintech, and loyalty.

### What's Already Built (Treasury OS)

| Component | Technology | Status | Capability |
|-----------|------------|--------|------------|
| **Financial DB** | TigerBeetle | ✅ Production | 384+ TPS sustained, strict serializability |
| **Ledger Engine** | Formance | ✅ Production | Programmable double-entry accounting |
| **Workflow Orchestration** | Temporal | ✅ Production | Durable execution, saga patterns |
| **Event Streaming** | Redpanda | ✅ Production | Event sourcing, real-time processing |
| **API Gateway** | Rust/Axum | ✅ Production | Zero-GC, rate limiting, idempotency |
| **Buffering** | Redis (AOF) | ✅ Production | Dust-to-bricks batching |
| **Test Suite** | Go | ✅ 104 tests | Double-ledger verification, E2E |

### What We're Building (AI/Agent Layer)

| Component | Technology | Status | Capability |
|-----------|------------|--------|------------|
| **Agent Runtime** | Suna (Kortix) | 🔄 Integrate | Multi-modal agent execution |
| **Multi-Agent Orchestration** | LangGraph | 🔄 Integrate | State management, handoffs |
| **LLM Abstraction** | LangChain + LiteLLM | 🔄 Integrate | Model agnostic, failover |
| **Skills Framework** | Claude Code Model | 🔨 Build | Agent=OS, Skills=Apps, Context=RAM |
| **Skill Registry** | 265+ Skills | 🔄 In Progress | Knowledge-to-Skill pipeline |

---

## 🎯 The Full Architecture Stack

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    CITADELOS COMPLETE STACK                                      │
├─────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                  │
│  ┌─────────────────────────────────────────────────────────────────────────────────────────────┐│
│  │  LAYER 6: APPLICATIONS (User-Facing)                                                         ││
│  │  ────────────────────────────────────                                                        ││
│  │                                                                                              ││
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐           ││
│  │  │ Landlord OS │ │  HOA/Condo  │ │  Resident   │ │    HITL     │ │  Developer  │           ││
│  │  │   Web/App   │ │     OS      │ │  Rewards    │ │  Dashboard  │ │   Portal    │           ││
│  │  │ (React/RN)  │ │ (React/RN)  │ │  (Mobile)   │ │  (React)    │ │  (Next.js)  │           ││
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘           ││
│  │                                                                                              ││
│  └─────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                              │                                                   │
│                                              ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────────────────────────────┐│
│  │  LAYER 5: DOMAIN BUNDLES (Skill Compositions)                                                ││
│  │  ─────────────────────────────────────────────                                               ││
│  │                                                                                              ││
│  │  ┌─────────────────────┐  ┌─────────────────────┐  ┌─────────────────────┐                 ││
│  │  │     STR Bundle      │  │     LTR Bundle      │  │     HOA Bundle      │                 ││
│  │  │ ─────────────────── │  │ ─────────────────── │  │ ─────────────────── │                 ││
│  │  │ • channel-sync      │  │ • lease-management  │  │ • dues-collection   │                 ││
│  │  │ • dynamic-pricing   │  │ • tenant-screening  │  │ • board-governance  │                 ││
│  │  │ • guest-comms       │  │ • rent-collection   │  │ • violation-mgmt    │                 ││
│  │  │ • cleaning-coord    │  │ • maintenance       │  │ • vendor-bidding    │                 ││
│  │  │ • revenue-mgmt      │  │ • credit-reporting  │  │ • architectural-rv  │                 ││
│  │  └─────────────────────┘  └─────────────────────┘  └─────────────────────┘                 ││
│  │                                                                                              ││
│  │  ┌─────────────────────┐  ┌─────────────────────┐  ┌─────────────────────┐                 ││
│  │  │   Fintech Bundle    │  │   Loyalty Bundle    │  │  Localization Cfg   │                 ││
│  │  │ ─────────────────── │  │ ─────────────────── │  │ ─────────────────── │                 ││
│  │  │ • banking-as-svc    │  │ • rent-rewards      │  │ • Language/tone     │                 ││
│  │  │ • stablecoin-wallet │  │ • merchant-network  │  │ • Payment rails     │                 ││
│  │  │ • high-yield-save   │  │ • credit-boost      │  │ • Tax rules         │                 ││
│  │  │ • on-chain-credit   │  │ • loyalty-transfer  │  │ • Compliance        │                 ││
│  │  │ • fiat-on-off-ramp  │  │ • down-pmt-redeem   │  │ • Cultural context  │                 ││
│  │  └─────────────────────┘  └─────────────────────┘  └─────────────────────┘                 ││
│  │                                                                                              ││
│  └─────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                              │                                                   │
│                                              ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────────────────────────────┐│
│  │  LAYER 4: SKILLS LAYER (Claude Code Model)                                                   ││
│  │  ──────────────────────────────────────────                                                  ││
│  │                                                                                              ││
│  │              Agent = Operating System                                                        ││
│  │              Skills = Applications                                                           ││
│  │              Context = RAM                                                                   ││
│  │                                                                                              ││
│  │  ┌─────────────────────────────────────────────────────────────────────────────────────┐   ││
│  │  │                           SKILL DEFINITION SCHEMA                                    │   ││
│  │  │                                                                                      │   ││
│  │  │  skill:                                                                              │   ││
│  │  │    id: SKILL-253                        # Unique identifier                         │   ││
│  │  │    name: lead-qualification             # kebab-case name                           │   ││
│  │  │    category: communication              # Skill category                            │   ││
│  │  │    version: 1.2.0                       # Semantic version                          │   ││
│  │  │                                                                                      │   ││
│  │  │    inputs:                              # What skill needs                           │   ││
│  │  │      - prospect_message: string                                                      │   ││
│  │  │      - property_criteria: PropertyCriteria                                          │   ││
│  │  │                                                                                      │   ││
│  │  │    outputs:                             # What skill produces                        │   ││
│  │  │      - qualification_score: number (0-100)                                          │   ││
│  │  │      - next_action: Action                                                          │   ││
│  │  │                                                                                      │   ││
│  │  │    tools_required:                      # Tools for execution                        │   ││
│  │  │      - mcp://database-toolbox/query                                                 │   ││
│  │  │      - mcp://whatsapp/send                                                          │   ││
│  │  │                                                                                      │   ││
│  │  │    knowledge_required:                  # RAG knowledge                              │   ││
│  │  │      - property_rules                                                               │   ││
│  │  │      - qualification_criteria                                                       │   ││
│  │  │                                                                                      │   ││
│  │  │    execution:                           # Path selection                             │   ││
│  │  │      path: hybrid                       # hot | cold | hybrid                       │   ││
│  │  │      hot_steps: [understand, generate]                                              │   ││
│  │  │      cold_steps: [log, update_crm]                                                  │   ││
│  │  │                                                                                      │   ││
│  │  │    evaluation:                          # Quality benchmarks                         │   ││
│  │  │      accuracy_target: 0.85                                                          │   ││
│  │  │      latency_target_ms: 2000                                                        │   ││
│  │  │      test_cases: [...]                                                              │   ││
│  │  │                                                                                      │   ││
│  │  └─────────────────────────────────────────────────────────────────────────────────────┘   ││
│  │                                                                                              ││
│  │  SKILL REGISTRY: 265+ skills | Versioned | Composable | Evaluated                          ││
│  │  KNOWLEDGE PIPELINE: PRD → Knowledge Doc → Engineering Spec → Skills + Tools               ││
│  │                                                                                              ││
│  └─────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                              │                                                   │
│              ┌───────────────────────────────┼───────────────────────────────┐                  │
│              ▼                               │                               ▼                  │
│  ┌─────────────────────────────────────┐    │    ┌─────────────────────────────────────┐       │
│  │  LAYER 3A: HOT PATH                 │    │    │  LAYER 3B: COLD PATH                │       │
│  │  (AI/Agent Infrastructure)          │    │    │  (Treasury OS Core)                 │       │
│  │  ───────────────────────────────    │    │    │  ───────────────────────────────    │       │
│  │                                     │    │    │                                     │       │
│  │  ┌───────────────────────────────┐ │    │    │  ┌───────────────────────────────┐ │       │
│  │  │ SUNA (Kortix Open Source)     │ │    │    │  │ TEMPORAL                      │ │       │
│  │  │ ─────────────────────────────│ │    │    │  │ ─────────────────────────────│ │       │
│  │  │ • Agent runtime environment   │ │    │    │  │ • Durable workflow execution  │ │       │
│  │  │ • Browser/tool integration    │ │    │    │  │ • Saga patterns for txns      │ │       │
│  │  │ • Multi-modal (text,voice)    │ │    │    │  │ • Retry, timeout, compensate  │ │       │
│  │  │ • Sandboxed execution         │ │    │    │  │ • Workflow visibility         │ │       │
│  │  │ • We extend, not rebuild      │ │    │    │  │ • Detached async workflows    │ │       │
│  │  └───────────────────────────────┘ │    │    │  └───────────────────────────────┘ │       │
│  │                                     │    │    │                                     │       │
│  │  ┌───────────────────────────────┐ │    │    │  ┌───────────────────────────────┐ │       │
│  │  │ LANGGRAPH                     │ │    │    │  │ FORMANCE                      │ │       │
│  │  │ ─────────────────────────────│ │    │    │  │ ─────────────────────────────│ │       │
│  │  │ • State management (convos)   │ │    │    │  │ • Programmable ledger         │ │       │
│  │  │ • Multi-agent coordination    │ │    │    │  │ • Double-entry accounting     │ │       │
│  │  │ • Branching/looping/conditns  │ │    │    │  │ • Multi-currency support      │ │       │
│  │  │ • Checkpoint/resume           │ │    │    │  │ • Compliance/audit trail      │ │       │
│  │  │ • Human-in-the-loop hooks     │ │    │    │  │ • "Shadow Ledger" pattern     │ │       │
│  │  └───────────────────────────────┘ │    │    │  └───────────────────────────────┘ │       │
│  │                                     │    │    │                                     │       │
│  │  ┌───────────────────────────────┐ │    │    │  ┌───────────────────────────────┐ │       │
│  │  │ LANGCHAIN + LITELLM           │ │    │    │  │ TIGERBEETLE                   │ │       │
│  │  │ ─────────────────────────────│ │    │    │  │ ─────────────────────────────│ │       │
│  │  │ • LLM provider abstraction    │ │    │    │  │ • 384+ TPS sustained          │ │       │
│  │  │ • Tool/function calling       │ │    │    │  │ • Strict serializability      │ │       │
│  │  │ • RAG pipelines               │ │    │    │  │ • ACID guarantees             │ │       │
│  │  │ • Memory management           │ │    │    │  │ • Immutable audit trail       │ │       │
│  │  │ • Model failover/routing      │ │    │    │  │ • "Source of Truth"           │ │       │
│  │  └───────────────────────────────┘ │    │    │  └───────────────────────────────┘ │       │
│  │                                     │    │    │                                     │       │
│  │  🔥 Understanding, Reasoning,      │    │    │  ❄️ Transactions, Compliance,      │       │
│  │     Generation, Retrieval          │    │    │     Audit, State Management        │       │
│  │     Adaptive, Probabilistic        │    │    │     Deterministic, Guaranteed      │       │
│  │                                     │    │    │                                     │       │
│  └─────────────────────────────────────┘    │    └─────────────────────────────────────┘       │
│              │                               │                               │                  │
│              └───────────────────────────────┼───────────────────────────────┘                  │
│                                              │                                                   │
│                                              ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────────────────────────────┐│
│  │  LAYER 2: SOCKET ARCHITECTURE (Composable, Zero Vendor Lock-in)                             ││
│  │  ─────────────────────────────────────────────────────────────                              ││
│  │                                                                                              ││
│  │  CORE PRINCIPLE: "Sockets over Solutions" - Vendors are just Plugins                        ││
│  │                                                                                              ││
│  │  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐           ││
│  │  │ Foundation      │ │ Binding         │ │ Orchestration   │ │ Execution       │           ││
│  │  │ Sockets         │ │ Sockets         │ │ Sockets         │ │ Sockets         │           ││
│  │  │ ─────────────── │ │ ─────────────── │ │ ─────────────── │ │ ─────────────── │           ││
│  │  │ MachineIdentity │ │ CredentialBind  │ │ IntentSocket    │ │ ExecutionSocket │           ││
│  │  │ IdentityGraph   │ │ TokenExchange   │ │ SolverSocket    │ │ TradFiRails     │           ││
│  │  │ AuditSocket     │ │ SecureEnclave   │ │ PolicySocket    │ │ CryptoRails     │           ││
│  │  │ LedgerSocket    │ │ BiscuitMint     │ │ AIModelSocket   │ │ LedgerSocket    │           ││
│  │  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘           ││
│  │                                                                                              ││
│  │  ADAPTERS: TigerBeetleAdapter | FormanceAdapter | PersonaAdapter | SwiftAdapter | etc.     ││
│  │                                                                                              ││
│  └─────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                              │                                                   │
│                                              ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────────────────────────────┐│
│  │  LAYER 1: INFRASTRUCTURE                                                                     ││
│  │  ─────────────────────────                                                                   ││
│  │                                                                                              ││
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐      ││
│  │  │PostgreSQL│ │ MongoDB │ │ Redis  │ │Redpanda │ │ Vector  │ │  K8s   │ │ Observ  │      ││
│  │  │+pgvector │ │ Atlas   │ │ (AOF)  │ │ Kafka   │ │ DB      │ │ Docker │ │ Stack   │      ││
│  │  │(Operate) │ │(Docs/RAG)│ │(Cache) │ │(Events) │ │(Embed)  │ │(Orch)  │ │(Monitor)│      ││
│  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘      ││
│  │                                                                                              ││
│  └─────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🔀 The Hot/Cold/Hybrid Execution Patterns

### Pattern 1: "Dust to Bricks" (High-Frequency Ingestion)

**Problem**: Millions of micro-transactions would choke the ledger
**Solution**: Buffer in Redis, batch-commit to TigerBeetle

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│    Ingest    │────▶│    Redis     │────▶│   Temporal   │────▶│ TigerBeetle  │
│  10K packets │     │   HINCRBY    │     │  (5s batch)  │     │  (1 Brick)   │
│              │     │  "Dust"      │     │  "Scoop"     │     │  "Settle"    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
```

### Pattern 2: "Shadow Ledger" (Never Block Hot Path)

**Problem**: Compliance logging shouldn't block transactions
**Solution**: TigerBeetle commits instantly, Formance records asynchronously

```
┌──────────────┐     ┌──────────────┐                    ┌──────────────┐
│   Request    │────▶│ TigerBeetle  │────▶ <10ms         │   Formance   │
│              │     │   (Commit)   │                    │   (Record)   │
└──────────────┘     └──────────────┘                    └──────────────┘
                            │                                   ▲
                            │       ┌──────────────┐           │
                            └──────▶│   Temporal   │───────────┘
                                    │  (Detached)  │
                                    └──────────────┘
```

### Pattern 3: Skill Execution Flow (Hot/Cold/Hybrid)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         SKILL EXECUTION FLOW                                     │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│   TASK: "Process rent payment from John for $1,500"                             │
│                                                                                  │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │  STEP 1: SKILL SELECTION (LangGraph + Skills Registry)                   │   │
│   │                                                                          │   │
│   │  Agent analyzes task → Selects skills:                                   │   │
│   │  • message-understanding (HOT - AI reasoning)                            │   │
│   │  • payment-validation (COLD - rules engine)                              │   │
│   │  • payment-processing (COLD - TigerBeetle)                               │   │
│   │  • receipt-generation (HOT - AI text gen)                                │   │
│   │  • ledger-update (COLD - Formance)                                       │   │
│   │  • notification-send (HYBRID - AI + API)                                 │   │
│   │                                                                          │   │
│   └─────────────────────────────────────────────────────────────────────────┘   │
│                                        │                                        │
│                                        ▼                                        │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │  STEP 2: ORCHESTRATION (LangGraph State Machine)                         │   │
│   │                                                                          │   │
│   │  [understand] → [validate] → [process] → [record] → [notify]            │   │
│   │       │              │            │           │          │               │   │
│   │      HOT           COLD         COLD        COLD      HYBRID             │   │
│   │    (Suna)        (Temporal)   (TigerB)   (Formance)  (Suna+API)          │   │
│   │                                                                          │   │
│   └─────────────────────────────────────────────────────────────────────────┘   │
│                                        │                                        │
│          ┌─────────────────────────────┼─────────────────────────────┐          │
│          ▼                             │                             ▼          │
│   ┌──────────────────┐                 │                ┌──────────────────┐   │
│   │    HOT PATH      │                 │                │    COLD PATH     │   │
│   │  (AI/Suna)       │                 │                │  (Treasury OS)   │   │
│   │                  │                 │                │                  │   │
│   │  • Parse intent  │                 │                │  • Validate:     │   │
│   │    "John paying  │                 │                │    - Account OK  │   │
│   │    $1,500 rent"  │                 │                │    - Funds avail │   │
│   │                  │                 │                │    - Policy pass │   │
│   │  • Extract:      │                 │                │                  │   │
│   │    - tenant_id   │                 │                │  • Execute:      │   │
│   │    - amount      │                 │                │    - TigerBeetle │   │
│   │    - property_id │                 │                │      transfer    │   │
│   │                  │                 │                │                  │   │
│   │  • Generate:     │                 │                │  • Record:       │   │
│   │    - Receipt txt │                 │                │    - Formance    │   │
│   │    - Thank you   │                 │                │      journal     │   │
│   │      message     │                 │                │                  │   │
│   │                  │                 │                │  • Audit:        │   │
│   │  • Decide:       │                 │                │    - Merkle root │   │
│   │    - WhatsApp?   │                 │                │    - Event emit  │   │
│   │    - Email?      │                 │                │                  │   │
│   │                  │                 │                │                  │   │
│   └──────────────────┘                 │                └──────────────────┘   │
│          │                             │                             │          │
│          └─────────────────────────────┼─────────────────────────────┘          │
│                                        │                                        │
│                                        ▼                                        │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │  STEP 3: RESULT AGGREGATION                                              │   │
│   │                                                                          │   │
│   │  Payment processed ✓     Transfer ID: TXN-2026-001234                    │   │
│   │  Ledger updated ✓        Merkle Root: 0x8f3a...                          │   │
│   │  Receipt sent ✓          WhatsApp: delivered                             │   │
│   │  Audit trail ✓           Event: payment.completed                        │   │
│   │                                                                          │   │
│   └─────────────────────────────────────────────────────────────────────────┘   │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🏛️ Treasury OS Core Architecture (Already Built)

### The "Hansen Pattern" (Your Current Stack)

| Component | Technology | Role | Superpower |
|-----------|------------|------|------------|
| **Ingestion** | Rust (Axum) | The Gateway | Zero-GC memory safety. Catches the "Firehose." |
| **Buffer** | Redis (AOF) | The Dam | Captures "Dust" before it chokes the DB. |
| **Orchestration** | Temporal (Go) | The Switchboard | Guarantees code *eventually* finishes. No zombie states. |
| **The Engine** | TigerBeetle | Layer 1 | Strict Serializability. The "Source of Truth." |
| **The Shadow** | Formance | Layer 2 | Programmable Accounting. The "Audit Log." |

### Validated Performance

| Metric | Achieved | Target |
|--------|----------|--------|
| **Throughput** | 384 TPS (sustained) | >10,000 TPS |
| **Latency** | <100ms (ingestion) | <100ms |
| **Data Integrity** | Zero loss (10K storm) | 100% |
| **Test Coverage** | 104 tests (10 categories) | Complete |

### Double-Entry Verification Tests

From your test suite (`category2/double_ledger_verification_test.go`):

- **Test 2.1**: TigerBeetle Atomic Consistency (1000 concurrent transfers)
- **Test 2.2**: TigerBeetle ↔ Formance Full Reconciliation
- **Test 2.3-2.5**: State transitions (Initial → Pending → Posted/Voided)
- **Test 2.6**: Posted → Reversed (compensation pattern)
- **Test 2.7**: Pending Timeout Expiry (auto-void)
- **Test 2.8**: Idempotent Transfer Re-execution
- **Test 2.9**: Linked Transfers (Two-Phase Commit)
- **Test 2.10**: Account Code Enforcement

---

## 🤖 AI/Agent Layer Architecture (To Integrate)

### How Suna + LangGraph + Claude Skills Come Together

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         AI/AGENT LAYER INTEGRATION                               │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│                          ┌─────────────────────┐                                │
│                          │   USER MESSAGE      │                                │
│                          │ "Schedule a showing │                                │
│                          │  for Apt 5B"        │                                │
│                          └──────────┬──────────┘                                │
│                                     │                                           │
│                                     ▼                                           │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │                    SUNA AGENT RUNTIME                                    │   │
│   │                    (Kortix Open Source)                                  │   │
│   │                                                                          │   │
│   │  • Receives message via API/WhatsApp/Voice                              │   │
│   │  • Multi-modal input processing                                         │   │
│   │  • Maintains conversation state                                         │   │
│   │  • Sandbox execution environment                                        │   │
│   │                                                                          │   │
│   └──────────────────────────────┬──────────────────────────────────────────┘   │
│                                  │                                              │
│                                  ▼                                              │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │                    LANGGRAPH ORCHESTRATOR                                │   │
│   │                    (Multi-Agent Coordination)                            │   │
│   │                                                                          │   │
│   │  ┌───────────────────────────────────────────────────────────────────┐  │   │
│   │  │  GRAPH STATE:                                                      │  │   │
│   │  │  {                                                                 │  │   │
│   │  │    "intent": "schedule_showing",                                   │  │   │
│   │  │    "property_id": "apt_5b",                                        │  │   │
│   │  │    "prospect_info": {...},                                         │  │   │
│   │  │    "available_slots": null,  // to be filled                       │  │   │
│   │  │    "selected_slot": null,                                          │  │   │
│   │  │    "confirmation": null                                            │  │   │
│   │  │  }                                                                 │  │   │
│   │  └───────────────────────────────────────────────────────────────────┘  │   │
│   │                                                                          │   │
│   │  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                  │   │
│   │  │ Qualify     │───▶│ Check       │───▶│ Schedule    │                  │   │
│   │  │ Lead Agent  │    │ Avail Agent │    │ Tour Agent  │                  │   │
│   │  └─────────────┘    └─────────────┘    └─────────────┘                  │   │
│   │        │                   │                  │                          │   │
│   │        │                   │                  │                          │   │
│   │        ▼                   ▼                  ▼                          │   │
│   │  ┌───────────────────────────────────────────────────────────────────┐  │   │
│   │  │                      SKILLS LAYER                                  │  │   │
│   │  │                  (Claude Code Framework)                           │  │   │
│   │  │                                                                    │  │   │
│   │  │  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐   │  │   │
│   │  │  │ lead-qualify    │  │ avail-check     │  │ tour-schedule   │   │  │   │
│   │  │  │ SKILL.md        │  │ SKILL.md        │  │ SKILL.md        │   │  │   │
│   │  │  │                 │  │                 │  │                 │   │  │   │
│   │  │  │ tools:          │  │ tools:          │  │ tools:          │   │  │   │
│   │  │  │ - crm_query     │  │ - calendar_api  │  │ - calendar_api  │   │  │   │
│   │  │  │ - score_lead    │  │ - pms_api       │  │ - notify_api    │   │  │   │
│   │  │  │                 │  │                 │  │ - crm_update    │   │  │   │
│   │  │  │ scripts:        │  │ scripts:        │  │ scripts:        │   │  │   │
│   │  │  │ - qualify.py    │  │ - check.py      │  │ - schedule.py   │   │  │   │
│   │  │  └─────────────────┘  └─────────────────┘  └─────────────────┘   │  │   │
│   │  │                                                                    │  │   │
│   │  └───────────────────────────────────────────────────────────────────┘  │   │
│   │                                                                          │   │
│   └─────────────────────────────────────────────────────────────────────────┘   │
│                                  │                                              │
│                                  ▼                                              │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │                    LANGCHAIN + LITELLM                                   │   │
│   │                    (LLM Abstraction Layer)                               │   │
│   │                                                                          │   │
│   │  Model Selection:                                                        │   │
│   │  • Simple intent → Gemini Flash (fast, cheap)                           │   │
│   │  • Complex reasoning → Claude Sonnet (best quality)                     │   │
│   │  • Structured output → GPT-4o (reliable JSON)                           │   │
│   │  • Sensitive data → Llama 3.1 (local, private)                          │   │
│   │                                                                          │   │
│   │  Failover Chain: Claude → GPT-4o → Gemini → Llama                       │   │
│   │                                                                          │   │
│   └─────────────────────────────────────────────────────────────────────────┘   │
│                                  │                                              │
│                                  ▼                                              │
│   ┌─────────────────────────────────────────────────────────────────────────┐   │
│   │                    MCP TOOL PROTOCOL                                     │   │
│   │                    (Model Context Protocol)                              │   │
│   │                                                                          │   │
│   │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐       │   │
│   │  │ database-   │ │ whatsapp-   │ │ calendar-   │ │ treasury-   │       │   │
│   │  │ toolbox     │ │ mcp         │ │ mcp         │ │ mcp         │       │   │
│   │  │             │ │             │ │             │ │             │       │   │
│   │  │ • query     │ │ • send_msg  │ │ • get_avail │ │ • transfer  │       │   │
│   │  │ • execute   │ │ • send_tmpl │ │ • book_slot │ │ • balance   │       │   │
│   │  │ • insert    │ │ • get_msgs  │ │ • cancel    │ │ • statement │       │   │
│   │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘       │   │
│   │                                                                          │   │
│   └─────────────────────────────────────────────────────────────────────────┘   │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🔌 Socket Architecture (Composable Platform)

### Interface Definitions (From Your Codebase)

```go
// Layer 1: Foundation Sockets
type LedgerSocket interface {
    CreateAccount(ctx context.Context, account Account) error
    PostTransaction(ctx context.Context, txn Transaction) error
    GetBalance(ctx context.Context, accountID string) (Balance, error)
}

// Layer 3: Orchestration Sockets
type IntentSocket interface {
    SubmitIntent(ctx context.Context, req IntentRequest) (*IntentResponse, error)
    GetProposals(ctx context.Context, intentID string) ([]Proposal, error)
    ApproveProposal(ctx context.Context, req ApprovalRequest) error
    Execute(ctx context.Context, intentID string) (*ExecutionResult, error)
}

// Layer 5: Execution Sockets
type ExecutionSocket interface {
    ExecuteTransfer(ctx context.Context, req TransferRequest) (*TransferResult, error)
    GetTransferStatus(ctx context.Context, transferID string) (*TransferStatus, error)
    BatchExecute(ctx context.Context, req BatchRequest) (*BatchResult, error)
    Reconcile(ctx context.Context, externalRef string, status ReconcileStatus) error
}
```

### Adapter Pattern (TigerBeetle Example)

From your `adapters/tigerbeetle/adapter.go`:

```go
// Adapter wraps internal/ledger.Ledger to implement ExecutionSocket.
// This is a thin wrapper - all real work is delegated to existing code.
type Adapter struct {
    ledger ledger.Ledger
}

func (a *Adapter) ExecuteTransfer(ctx context.Context, req layer5_execution.TransferRequest) (*layer5_execution.TransferResult, error) {
    // Convert socket types to internal types
    internalReq := &models.CreateTransferRequest{
        DebitAccountID:  models.AccountID(req.SourceAccountID),
        CreditAccountID: models.AccountID(req.DestinationAccountID),
        Amount:          int64(req.Amount),
    }

    // Delegate to existing implementation (unchanged)
    result, err := a.ledger.CreateTransfer(ctx, internalReq)
    if err != nil {
        return nil, err
    }

    // Convert internal types to socket types
    return &layer5_execution.TransferResult{
        TransferID:   string(result.TransferID),
        Status:       layer5_execution.TransferStatePosted,
        Timestamp:    time.Now(),
        DebitPosted:  uint64(result.Amount),
        CreditPosted: uint64(result.Amount),
    }, nil
}
```

### Why This Architecture is Vendor-Agnostic

| Socket | Current Adapter | Alternative Adapters | Swap Time |
|--------|-----------------|---------------------|-----------|
| **LedgerSocket** | TigerBeetle | PostgreSQL, DynamoDB, Ledger-X | 2-3 days |
| **ExecutionSocket** | Formance | Stripe, Adyen, Custom | 2-3 days |
| **VerificationSocket** | Persona | Onfido, Jumio, Idwall | 1-2 days |
| **WalletSocket** | None | WalletConnect, MetaMask | 2-3 days |

---

## 📊 Skills Framework (Model-Agnostic Runtime)

### From Your `runtime/unified_runtime.py`

```python
class UnifiedOSRuntime(IAgentRuntime):
    """
    Model-agnostic runtime implementation.
    Supports multiple LLM providers with automatic failover.
    """
    
    MODELS = {
        "claude-sonnet": {
            "litellm_model": "anthropic/claude-sonnet-4-20250514",
            "max_tokens": 4096,
            "supports_tools": True,
            "cost_per_1k_input": 0.003,
            "cost_per_1k_output": 0.015,
            "strengths": ["reasoning", "code", "portuguese"],
        },
        "gpt-4o": {...},
        "gemini-2-flash": {...},
        "llama-3.1-70b": {...},  # Local, private
        "deepseek-chat": {...},   # Cheapest
    }
    
    async def process(self, message, context, active_skills, session_id):
        # Build system prompt from active skills
        system_prompt = self._build_system_prompt(active_skills)
        
        # Try primary model, then fallbacks
        models_to_try = [self.primary_model] + self.fallback_models
        
        for model_name in models_to_try:
            try:
                response = await self._call_model(model_name, messages, tools)
                return RuntimeResponse(...)
            except Exception:
                continue  # Try next model
```

### Skill Definition Format (SKILL.md)

```yaml
---
name: rent-payment-processing
version: 1.2.0
description: |
  Process rent payments including validation, execution, and notification.
  Use when: resident initiates payment, scheduled payment due.
  Do NOT use: for maintenance requests.

triggers:
  keywords: ["pay rent", "payment", "pagar aluguel"]
  intents: ["process_payment", "check_balance"]

tools:
  - mcp://treasury/transfer
  - mcp://treasury/balance
  - mcp://whatsapp/send

scripts:
  - scripts/validate_payment.py
  - scripts/generate_receipt.py

validators:
  - validators/payment_validator.py

model_hints:
  preferred: claude-sonnet
  fallback: gpt-4o
---

# Rent Payment Processing

## Workflow

### Step 1: Validate Payment
1. Check tenant exists and active
2. Verify amount matches due amount
3. Confirm account has funds (if applicable)

### Step 2: Execute Payment
Call Treasury OS via MCP:
```python
result = await mcp://treasury/transfer({
    "source": tenant_wallet_id,
    "destination": property_trust_account,
    "amount": payment_amount,
    "idempotency_key": f"rent-{tenant_id}-{month}"
})
```

### Step 3: Record & Notify
1. Generate receipt
2. Send confirmation via WhatsApp
3. Update tenant ledger in Formance
```

---

## 🌍 Localization Architecture (Granular Configuration)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    LOCALIZATION CONFIGURATION HIERARCHY                          │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │  GLOBAL (Platform Defaults)                                              │   │
│  │  ────────────────────────────                                            │   │
│  │  • Base skills library (265+)                                            │   │
│  │  • Core policies                                                         │   │
│  │  • Default language: English                                             │   │
│  │  • Default currency: USD                                                 │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                        │                                        │
│                                        ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │  COUNTRY (Brazil, Spain, Portugal, Italy, US)                            │   │
│  │  ───────────────────────────────────────────                             │   │
│  │                                                                          │   │
│  │  Brazil Config:                                                          │   │
│  │  • Language: pt-BR                                                       │   │
│  │  • Payment Rails: PIX (primary), Boleto, Card                           │   │
│  │  • Tax Rules: ISS, IRRF                                                  │   │
│  │  • Compliance: LGPD, BACEN                                               │   │
│  │  • Communication: WhatsApp (priority)                                    │   │
│  │  • Cultural: Informal tone, emoji-friendly                               │   │
│  │                                                                          │   │
│  │  Spain Config:                                                           │   │
│  │  • Language: es-ES                                                       │   │
│  │  • Payment Rails: SEPA, Bizum, Card                                     │   │
│  │  • Tax Rules: IVA, IRPF                                                  │   │
│  │  • Compliance: GDPR                                                      │   │
│  │  • Communication: SMS/Email (priority)                                   │   │
│  │                                                                          │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                        │                                        │
│                                        ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │  MARKET / PM COMPANY (São Paulo, Barcelona, Miami)                       │   │
│  │  ────────────────────────────────────────────────                        │   │
│  │                                                                          │   │
│  │  São Paulo PM Config:                                                    │   │
│  │  • Business hours: 9am-6pm BRT                                           │   │
│  │  • Emergency contacts                                                    │   │
│  │  • Preferred vendors list                                                │   │
│  │  • Local regulations overlay                                             │   │
│  │  • Response time SLAs                                                    │   │
│  │                                                                          │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                        │                                        │
│                                        ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │  PROPERTY (Building, Community, Asset)                                   │   │
│  │  ──────────────────────────────────────                                  │   │
│  │                                                                          │   │
│  │  Edifício Copacabana Config:                                             │   │
│  │  • HOA rules overlay                                                     │   │
│  │  • Building-specific amenities                                           │   │
│  │  • Parking rules                                                         │   │
│  │  • Pet policies                                                          │   │
│  │  • Quiet hours                                                           │   │
│  │                                                                          │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                        │                                        │
│                                        ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │  UNIT (Apartment, Room, Space)                                           │   │
│  │  ──────────────────────────────                                          │   │
│  │                                                                          │   │
│  │  Unit 5B Config:                                                         │   │
│  │  • Specific appliance manuals                                            │   │
│  │  • WiFi credentials                                                      │   │
│  │  • Unit-specific pricing rules                                           │   │
│  │  • Custom check-in instructions                                          │   │
│  │  • Smart lock codes                                                      │   │
│  │                                                                          │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                                                                  │
│  CONFIG RESOLUTION: Unit → Property → Market → Country → Global                 │
│  (Most specific wins, cascades up for defaults)                                 │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📈 Technology Stack Summary

### Already Built (Treasury OS)

| Layer | Component | Technology | Lines of Code |
|-------|-----------|------------|---------------|
| Gateway | API Ingestion | Rust/Axum | ~3,000 |
| Buffer | Dust Collection | Redis AOF | Config |
| Orchestration | Workflows | Temporal (Go) | ~5,000 |
| Engine | Source of Truth | TigerBeetle | Native |
| Shadow | Audit Ledger | Formance | Config |
| Events | Streaming | Redpanda | Config |
| Tests | Verification | Go | ~2,500 (104 tests) |
| Interfaces | Socket Layer | Go | ~1,000 |
| Adapters | TB Adapter | Go | ~200 |

### To Build/Integrate (AI Layer)

| Layer | Component | Technology | Effort |
|-------|-----------|------------|--------|
| Agent Runtime | Suna | Python | 2-3 weeks |
| Orchestration | LangGraph | Python | 2-3 weeks |
| LLM Abstraction | LiteLLM | Python | 1 week |
| Skills Framework | Custom | Python/MD | 2-4 weeks |
| MCP Servers | Custom | TypeScript | 3-4 weeks |
| HITL Dashboard | Custom | React | 4-6 weeks |

---

## 🎯 Why This Architecture Wins

### 1. **Separation of Concerns**
- **Hot Path** (AI) handles uncertainty, reasoning, generation
- **Cold Path** (Finance) handles guarantees, audit, compliance
- **Hybrid Path** combines them intelligently per task

### 2. **Production-Ready Finance**
- **384+ TPS** sustained (tested)
- **Strict serializability** (TigerBeetle)
- **Double-entry accounting** (Formance)
- **Event sourcing** (Redpanda)
- **Durable workflows** (Temporal)

### 3. **AI Without Lock-in**
- **Model agnostic** (Claude, GPT-4, Gemini, Llama)
- **Skill portability** (Markdown format)
- **Tool abstraction** (MCP protocol)
- **Automatic failover**

### 4. **Composable Platform**
- **Socket architecture** (swap any component)
- **Adapter pattern** (thin wrappers)
- **Zero vendor lock-in**

### 5. **Global Scale**
- **Granular localization** (Global → Unit)
- **Multi-currency** (fiat + crypto)
- **Multi-language** (AI-powered)
- **Multi-rail** (PIX, SEPA, SWIFT, Crypto)

---

## 🧠 Memory Architecture: Never Starting from Scratch

### The Problem: Stateless AI = Frustrated Users

```
TRADITIONAL AI (STATELESS):
┌─────────────────────────────────────────────────────────────────────────────────┐
│  Day 1: Mario calls                                                              │
│  Mario: "My toilet is overflowing!"                                             │
│  AI: "I'm sorry to hear that. What's your unit number?"                         │
│  Mario: "5B"                                                                     │
│  AI: "I'll send a plumber. They'll arrive in 2 hours."                          │
│  [Ticket created, plumber dispatched]                                            │
├─────────────────────────────────────────────────────────────────────────────────┤
│  Day 8: Mario calls again                                                        │
│  Mario: "The toilet is overflowing AGAIN!"                                      │
│  AI: "I'm sorry to hear that. What's your unit number?" 😤                      │
│                                                                                  │
│  MARIO IS FURIOUS - AI doesn't remember ANYTHING                                │
└─────────────────────────────────────────────────────────────────────────────────┘
```

### The Solution: Multi-Layer Memory Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    CITADELOS MEMORY ARCHITECTURE                                     │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   MARIO'S TOILET SCENARIO (Day 8):                                                                  │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  INCOMING: "The toilet is overflowing again!"                                                │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 1: WORKING MEMORY (Redis) - Current Conversation                                      │   │
│   │  ─────────────────────────────────────────────────────────                                   │   │
│   │                                                                                              │   │
│   │  {                                                                                           │   │
│   │    "session_id": "conv-2026-01-05-1430",                                                     │   │
│   │    "caller_phone": "+5511999888777",                                                        │   │
│   │    "current_message": "The toilet is overflowing again!",                                   │   │
│   │    "emotional_state": "frustrated",      // Detected from "again!"                          │   │
│   │    "conversation_turns": [...]                                                               │   │
│   │  }                                                                                           │   │
│   │                                                                                              │   │
│   │  TTL: 2 hours (active conversation)                                                         │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                       ┌────────────────────┼────────────────────┐                                   │
│                       ▼                    │                    ▼                                   │
│   ┌──────────────────────────────┐         │         ┌──────────────────────────────┐              │
│   │  LAYER 2: ENTITY MEMORY      │         │         │  LAYER 3: INTERACTION MEMORY │              │
│   │  (PostgreSQL + pgvector)     │         │         │  (MongoDB + Vector Search)   │              │
│   │  ──────────────────────────  │         │         │  ────────────────────────────│              │
│   │                              │         │         │                              │              │
│   │  WHO IS MARIO?               │         │         │  MARIO'S HISTORY:            │              │
│   │  {                           │         │         │                              │              │
│   │    "entity_id": "res-7291",  │         │         │  ┌──────────────────────────┐│              │
│   │    "name": "Mario Silva",    │         │         │  │ 7 days ago               ││              │
│   │    "unit": "5B",             │         │         │  │ Issue: Toilet overflow   ││              │
│   │    "phone": "+5511999...",   │         │         │  │ Resolution: Plumber sent ││              │
│   │    "email": "mario@...",     │         │         │  │ Vendor: João's Plumbing  ││              │
│   │    "lease_start": "2024-03", │         │         │  │ Cost: R$180              ││              │
│   │    "rent_amount": 2500.00,   │         │         │  │ Duration: 45 min         ││              │
│   │    "payment_history": "✓✓✓", │         │         │  │ Parts: Flapper valve     ││              │
│   │    "maintenance_count": 3,   │         │         │  │ Status: RESOLVED         ││              │
│   │    "sentiment_avg": 0.72     │         │         │  │ Mario rating: 4/5        ││              │
│   │  }                           │         │         │  └──────────────────────────┘│              │
│   │                              │         │         │                              │              │
│   │  UNIT 5B:                    │         │         │  ┌──────────────────────────┐│              │
│   │  {                           │         │         │  │ 3 months ago             ││              │
│   │    "appliances": [...],      │         │         │  │ Issue: AC not cooling    ││              │
│   │    "last_inspection": "...", │         │         │  │ Resolution: Filter clean ││              │
│   │    "known_issues": [         │         │         │  │ Cost: R$0 (DIY)          ││              │
│   │      "old_plumbing_2018"     │         │         │  └──────────────────────────┘│              │
│   │    ]                         │         │         │                              │              │
│   │  }                           │         │         │  Vector similarity: 0.94    │              │
│   │                              │         │         │  (toilet overflow queries)  │              │
│   └──────────────────────────────┘         │         └──────────────────────────────┘              │
│                       │                    │                    │                                   │
│                       └────────────────────┼────────────────────┘                                   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 4: KNOWLEDGE MEMORY (RAG - pgvector/MongoDB Atlas Vector Search)                      │   │
│   │  ───────────────────────────────────────────────────────────────────────                     │   │
│   │                                                                                              │   │
│   │  Vector Search: "toilet overflow recurring" + "unit 5B" + "plumbing"                        │   │
│   │                                                                                              │   │
│   │  Retrieved Context:                                                                          │   │
│   │  ┌────────────────────────────────────────────────────────────────────────────────────────┐ │   │
│   │  │ • Building 5B plumbing was installed in 2018, copper pipes, known for lime buildup     │ │   │
│   │  │ • Recurring toilet issues often indicate: 1) Clog in main line, 2) Faulty wax ring     │ │   │
│   │  │ • If same issue <14 days: Escalate to senior plumber, check main line                  │ │   │
│   │  │ • João's Plumbing: 4.2/5 rating, but recurring call rate is 18%                        │ │   │
│   │  │ • Alternative: Pedro's Plumbing: 4.8/5 rating, recurring call rate is 4%               │ │   │
│   │  └────────────────────────────────────────────────────────────────────────────────────────┘ │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 5: FINANCIAL MEMORY (Treasury OS - TigerBeetle + Formance)                            │   │
│   │  ────────────────────────────────────────────────────────────────                            │   │
│   │                                                                                              │   │
│   │  Mario's Financial Context:                                                                  │   │
│   │  ┌────────────────────────────────────────────────────────────────────────────────────────┐ │   │
│   │  │ • Current balance: R$0.00 (rent paid on time)                                          │ │   │
│   │  │ • Maintenance fund: R$2,450 available for unit 5B repairs                              │ │   │
│   │  │ • Last repair cost: R$180 (7 days ago) - Transaction ID: TXN-2025-123456              │ │   │
│   │  │ • Warranty status: ACTIVE (João's work has 30-day warranty)                            │ │   │
│   │  │ • Escalation authority: Repairs >R$500 require owner approval                          │ │   │
│   │  └────────────────────────────────────────────────────────────────────────────────────────┘ │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  CONTEXT ASSEMBLY → LLM PROMPT                                                               │   │
│   │  ─────────────────────────────────                                                           │   │
│   │                                                                                              │   │
│   │  System: You are a maintenance coordinator for Edifício Copacabana.                         │   │
│   │                                                                                              │   │
│   │  Context:                                                                                    │   │
│   │  - Caller: Mario Silva (Unit 5B, resident since 2024)                                       │   │
│   │  - CRITICAL: Same toilet overflow issue 7 days ago                                          │   │
│   │  - Previous vendor: João's Plumbing (installed flapper valve)                               │   │
│   │  - WARRANTY ACTIVE: João's work is under 30-day warranty                                    │   │
│   │  - Building Note: Unit 5B has 2018 copper pipes, known lime buildup                         │   │
│   │  - Recurring issue <14 days → Protocol: Escalate to senior plumber                          │   │
│   │  - Alternative vendor available: Pedro's Plumbing (4.8/5, 4% recurrence)                    │   │
│   │  - Financial: Maintenance fund has R$2,450 available                                        │   │
│   │                                                                                              │   │
│   │  User: "The toilet is overflowing again!"                                                   │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  AI RESPONSE (Memory-Informed):                                                              │   │
│   │  ─────────────────────────────                                                               │   │
│   │                                                                                              │   │
│   │  "Olá Mario! Vejo que o vaso sanitário voltou a dar problema - isso não deveria             │   │
│   │   ter acontecido, especialmente considerando que o João esteve aí há apenas 7 dias.        │   │
│   │                                                                                              │   │
│   │   O serviço dele ainda está na garantia de 30 dias, então vou acionar a garantia            │   │
│   │   para você sem custo adicional. Mas como é um problema recorrente, também vou              │   │
│   │   escalar para nosso encanador sênior examinar a linha principal - o prédio tem            │   │
│   │   tubulação de 2018 que às vezes acumula calcário.                                          │   │
│   │                                                                                              │   │
│   │   O Pedro's Plumbing pode estar aí em 1 hora. Posso confirmar?"                             │   │
│   │                                                                                              │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Memory Storage Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    MEMORY STORAGE LAYERS                                             │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   ┌───────────────────────────────────────────────────────────────────────────────────────────────┐ │
│   │  REDIS (Working Memory)                                                                        │ │
│   │  ─────────────────────                                                                         │ │
│   │                                                                                                │ │
│   │  Purpose: Active conversation state, emotional context, real-time cache                       │ │
│   │  TTL: 2 hours (conversation) / 24 hours (session)                                             │ │
│   │  Pattern: Hash per conversation with sliding expiry                                           │ │
│   │                                                                                                │ │
│   │  Keys:                                                                                         │ │
│   │  • conv:{session_id}       → Current conversation state                                       │ │
│   │  • entity:{phone}:recent   → Last 5 interactions (hot cache)                                  │ │
│   │  • context:{entity_id}     → Precomputed context for fast recall                              │ │
│   │                                                                                                │ │
│   └───────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                      │
│   ┌───────────────────────────────────────────────────────────────────────────────────────────────┐ │
│   │  POSTGRESQL + pgvector (Entity Memory)                                                         │ │
│   │  ─────────────────────────────────────                                                         │ │
│   │                                                                                                │ │
│   │  Purpose: Structured entity data, relationships, vector embeddings for semantic search        │ │
│   │  Retention: Permanent (with archival policy)                                                  │ │
│   │                                                                                                │ │
│   │  Tables:                                                                                       │ │
│   │  • residents          → Name, unit, contact, preferences, sentiment_score                     │ │
│   │  • units              → Property details, known_issues[], appliance_manual_embeddings        │ │
│   │  • vendors            → Performance metrics, specialty, recurrence_rate                       │ │
│   │  • entity_embeddings  → pgvector index for semantic entity lookup                             │ │
│   │                                                                                                │ │
│   │  Indexes:                                                                                      │ │
│   │  • HNSW index on entity_embeddings (cosine similarity, ef_construction=128)                  │ │
│   │                                                                                                │ │
│   └───────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                      │
│   ┌───────────────────────────────────────────────────────────────────────────────────────────────┐ │
│   │  MONGODB + Atlas Vector Search (Interaction Memory)                                            │ │
│   │  ──────────────────────────────────────────────────                                            │ │
│   │                                                                                                │ │
│   │  Purpose: Full interaction history, conversation logs, semantic search across interactions    │ │
│   │  Retention: 7 years (compliance), hot/warm/cold tiering                                       │ │
│   │                                                                                                │ │
│   │  Collections:                                                                                  │ │
│   │  • interactions                                                                                │ │
│   │    {                                                                                           │ │
│   │      "_id": ObjectId,                                                                          │ │
│   │      "entity_id": "res-7291",                                                                  │ │
│   │      "timestamp": ISODate,                                                                     │ │
│   │      "channel": "voice" | "whatsapp" | "email",                                               │ │
│   │      "intent": "maintenance_request",                                                          │ │
│   │      "category": "plumbing",                                                                   │ │
│   │      "summary": "Toilet overflow, flapper valve replaced",                                    │ │
│   │      "summary_embedding": [0.023, -0.891, ...],  // 1536-dim                                  │ │
│   │      "resolution": {...},                                                                      │ │
│   │      "satisfaction_score": 4,                                                                  │ │
│   │      "cost": 180.00,                                                                           │ │
│   │      "vendor_id": "vendor-joao"                                                                │ │
│   │    }                                                                                           │ │
│   │                                                                                                │ │
│   │  • conversation_logs   → Full transcript with turn embeddings                                 │ │
│   │  • knowledge_chunks    → RAG document chunks with embeddings                                  │ │
│   │                                                                                                │ │
│   │  Vector Search Index:                                                                          │ │
│   │  • interactions.summary_embedding (cosine, dimensions=1536)                                   │ │
│   │  • knowledge_chunks.embedding (cosine, dimensions=1536)                                       │ │
│   │                                                                                                │ │
│   └───────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                      │
│   ┌───────────────────────────────────────────────────────────────────────────────────────────────┐ │
│   │  TIGERBEETLE + FORMANCE (Financial Memory)                                                     │ │
│   │  ─────────────────────────────────────────                                                     │ │
│   │                                                                                                │ │
│   │  Purpose: Immutable financial history, payment patterns, warranty tracking                    │ │
│   │  Retention: Permanent (regulatory requirement)                                                │ │
│   │                                                                                                │ │
│   │  Already integrated via Treasury OS:                                                          │ │
│   │  • Account balances by entity                                                                 │ │
│   │  • Transaction history with Merkle proofs                                                     │ │
│   │  • Maintenance fund allocations                                                               │ │
│   │  • Warranty periods (derived from vendor payment timestamps)                                  │ │
│   │                                                                                                │ │
│   └───────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Memory Retrieval Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    MEMORY RETRIEVAL PIPELINE                                         │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   STEP 1: IDENTIFY CALLER                                                                           │
│   ────────────────────────                                                                          │
│   Input: Phone number / Email / Session ID                                                          │
│   Query: Redis (hot cache) → PostgreSQL (entity lookup)                                            │
│   Output: entity_id, basic profile                                                                  │
│   Latency: <10ms                                                                                    │
│                                                                                                      │
│   STEP 2: RETRIEVE RECENT CONTEXT                                                                   │
│   ──────────────────────────────                                                                    │
│   Query: Redis conv:{session_id} + entity:{id}:recent                                              │
│   Output: Last 5 interactions, current conversation state                                           │
│   Latency: <5ms                                                                                     │
│                                                                                                      │
│   STEP 3: SEMANTIC SIMILARITY SEARCH                                                                │
│   ─────────────────────────────────                                                                 │
│   Input: Current message embedding                                                                  │
│   Query: MongoDB Vector Search (interactions collection)                                            │
│                                                                                                      │
│   db.interactions.aggregate([                                                                       │
│     {                                                                                               │
│       "$vectorSearch": {                                                                            │
│         "index": "interaction_embeddings",                                                          │
│         "path": "summary_embedding",                                                                │
│         "queryVector": [0.012, -0.834, ...],                                                        │
│         "numCandidates": 100,                                                                       │
│         "limit": 5,                                                                                 │
│         "filter": { "entity_id": "res-7291" }                                                       │
│       }                                                                                             │
│     }                                                                                               │
│   ])                                                                                                │
│                                                                                                      │
│   Output: Top 5 semantically similar past interactions                                              │
│   Latency: <50ms                                                                                    │
│                                                                                                      │
│   STEP 4: RAG KNOWLEDGE RETRIEVAL                                                                   │
│   ───────────────────────────────                                                                   │
│   Input: Message + Entity context + Unit context                                                    │
│   Query: MongoDB Vector Search (knowledge_chunks collection)                                        │
│   Output: Relevant policies, building info, vendor data                                             │
│   Latency: <50ms                                                                                    │
│                                                                                                      │
│   STEP 5: FINANCIAL CONTEXT                                                                         │
│   ────────────────────────                                                                          │
│   Query: Treasury OS API (balances, recent transactions, warranties)                               │
│   Output: Budget availability, payment status, active warranties                                    │
│   Latency: <20ms                                                                                    │
│                                                                                                      │
│   STEP 6: CONTEXT ASSEMBLY                                                                          │
│   ──────────────────────────                                                                        │
│   Combine all layers into structured prompt context                                                 │
│   Token budget: ~2000 tokens for context                                                            │
│   Priority: Recent > Relevant > General                                                             │
│                                                                                                      │
│   TOTAL RETRIEVAL LATENCY: <150ms                                                                   │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Memory Write-Back (Learning from Interactions)

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    MEMORY WRITE-BACK PIPELINE                                        │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   After each interaction:                                                                           │
│                                                                                                      │
│   ┌────────────────────────────────────────────────────────────────────────────────────────────────┐│
│   │  1. CONVERSATION SUMMARY (Async - Temporal Workflow)                                            ││
│   │     ─────────────────────────────────────────────────                                           ││
│   │     • LLM generates summary of interaction                                                      ││
│   │     • Extract: intent, category, resolution, satisfaction                                       ││
│   │     • Generate embedding of summary                                                             ││
│   │     • Store in MongoDB interactions collection                                                  ││
│   └────────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                                                                                      │
│   ┌────────────────────────────────────────────────────────────────────────────────────────────────┐│
│   │  2. ENTITY UPDATE (Async - Temporal Workflow)                                                   ││
│   │     ────────────────────────────────────────────                                                ││
│   │     • Update sentiment_score (rolling average)                                                  ││
│   │     • Increment interaction_count                                                               ││
│   │     • Update last_interaction_date                                                              ││
│   │     • Add to known_issues[] if new issue type                                                   ││
│   └────────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                                                                                      │
│   ┌────────────────────────────────────────────────────────────────────────────────────────────────┐│
│   │  3. VENDOR PERFORMANCE UPDATE (Async - Temporal Workflow)                                       ││
│   │     ──────────────────────────────────────────────────                                          ││
│   │     • Track recurrence rate (same issue <14 days)                                               ││
│   │     • Update average satisfaction score                                                         ││
│   │     • Flag if recurrence_rate > threshold                                                       ││
│   └────────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                                                                                      │
│   ┌────────────────────────────────────────────────────────────────────────────────────────────────┐│
│   │  4. KNOWLEDGE ENHANCEMENT (Batch - Nightly)                                                     ││
│   │     ───────────────────────────────────────────                                                 ││
│   │     • Analyze interaction patterns                                                              ││
│   │     • Identify new common issues                                                                ││
│   │     • Update building-specific knowledge base                                                   ││
│   │     • Retrain embeddings if significant drift                                                   ││
│   └────────────────────────────────────────────────────────────────────────────────────────────────┘│
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Memory Data Model (Schemas)

```typescript
// Entity Memory (PostgreSQL)
interface Resident {
  entity_id: string;           // "res-7291"
  name: string;
  unit_id: string;
  phone: string;
  email: string;
  lease_start: Date;
  lease_end: Date | null;
  rent_amount: number;
  payment_history: PaymentStatus[];  // Last 12 months
  maintenance_count: number;
  sentiment_score: number;     // 0.0 - 1.0 rolling average
  preferences: {
    contact_channel: "whatsapp" | "sms" | "email" | "voice";
    language: string;
    quiet_hours: { start: string; end: string };
  };
  embedding: number[];         // 1536-dim for semantic search
}

// Interaction Memory (MongoDB)
interface Interaction {
  _id: ObjectId;
  entity_id: string;
  timestamp: Date;
  channel: "voice" | "whatsapp" | "email" | "chat" | "app";
  session_id: string;
  
  // Classification
  intent: string;              // "maintenance_request", "payment_inquiry", etc.
  category: string;            // "plumbing", "hvac", "electrical", etc.
  urgency: "low" | "medium" | "high" | "emergency";
  
  // Content
  summary: string;             // AI-generated summary
  summary_embedding: number[]; // 1536-dim
  transcript_ref: string;      // Reference to full transcript
  
  // Resolution
  resolution: {
    status: "resolved" | "pending" | "escalated";
    action_taken: string;
    vendor_id?: string;
    cost?: number;
    warranty_until?: Date;
  };
  
  // Feedback
  satisfaction_score?: number; // 1-5
  feedback_text?: string;
  
  // Derived
  is_recurring: boolean;       // Same issue type within 14 days
  related_interaction_id?: ObjectId;
}

// Working Memory (Redis)
interface ConversationState {
  session_id: string;
  entity_id: string;
  started_at: number;          // Unix timestamp
  last_activity: number;
  channel: string;
  
  // Current state
  current_intent: string;
  emotional_state: "positive" | "neutral" | "frustrated" | "angry";
  
  // Conversation context
  turns: {
    role: "user" | "assistant";
    content: string;
    timestamp: number;
    tools_used?: string[];
  }[];
  
  // Preloaded context (for fast LLM calls)
  preloaded_context: {
    entity_summary: string;
    recent_interactions: string[];
    relevant_knowledge: string[];
    financial_summary: string;
  };
}
```

### Why This Memory Architecture Wins

| Aspect | Traditional Chatbot | CitadelOS Memory |
|--------|---------------------|------------------|
| **Caller Recognition** | Starts fresh every time | Instant: "Hi Mario!" |
| **History Recall** | None | Full semantic search across all interactions |
| **Context Depth** | Current conversation only | Entity + Unit + Building + Historical + Financial |
| **Learning** | None | Sentiment tracking, vendor performance, pattern detection |
| **Latency** | N/A | <150ms total retrieval |
| **Personalization** | Generic responses | Tone, channel, language preferences |
| **Financial Awareness** | None | Budget, warranties, payment status integrated |

---

## Next Steps

1. **Document Integration Points** between Treasury OS and AI Layer
2. **Create MCP Server Specifications** for Treasury OS tools
3. **Define Skill-to-Workflow Mapping** (which skills trigger which Temporal workflows)
4. **Build HITL Dashboard Prototype**
5. **Implement First Domain Bundle** (STR or LTR)
6. **Implement Memory Services** (Redis + pgvector + MongoDB Atlas Vector Search)

---

**Architecture Status**: Complete Specification
**Ready For**: Implementation Phase

