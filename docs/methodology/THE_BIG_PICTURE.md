# The Big Picture: UnifiedOS AI-Powered Vertical Platform

## How Knowledge-to-Skills Fits Into the Complete System

**Version:** 1.0  
**Date:** 2026-01-04  
**Purpose:** Provide context for how skill creation enables the entire UnifiedOS platform

---

## 🎯 Executive Summary

**Knowledge-to-Skills is NOT the product. It's the manufacturing process.**

The actual product is **UnifiedOS** — a model-agnostic AI runtime that powers multiple industry verticals (Rentals, Health, Loyalty, Treasury, etc.) using a **Skills-based architecture** where the LLM acts as an operating system.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        THE COMPLETE PICTURE                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  KNOWLEDGE-TO-SKILLS          UNIFIED RUNTIME           END USER             │
│  (Manufacturing)              (Operating System)        (Experience)         │
│                                                                              │
│  ┌──────────────┐            ┌──────────────┐         ┌──────────────┐      │
│  │ Raw Domain   │            │  Skills      │         │  Tenant      │      │
│  │ Knowledge    │───────────▶│  Library     │─────────▶│  WhatsApp   │      │
│  │              │            │              │         │  Conversation│      │
│  └──────────────┘            └──────────────┘         └──────────────┘      │
│                                     │                                        │
│  This methodology                   │                 This is the            │
│  creates skills                     │                 user experience        │
│                              ┌──────┴──────┐                                │
│                              │   LLM       │                                │
│                              │   Runtime   │                                │
│                              │ (OS Layer)  │                                │
│                              └──────┬──────┘                                │
│                                     │                                        │
│                              ┌──────┴──────┐                                │
│                              │ Databases   │                                │
│                              │ APIs        │                                │
│                              │ Services    │                                │
│                              └─────────────┘                                │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🏗️ The UnifiedOS Architecture

### Mental Model: LLM as Operating System

We've adopted a paradigm shift inspired by Karpathy's "LMOS" concept:

| Traditional Computer | UnifiedOS (AI-Native) |
|---------------------|----------------------|
| CPU executes instructions | **LLM** processes context and decides actions |
| RAM stores working memory | **Context Window** holds conversation + skills |
| OS manages processes | **Runtime** loads skills, routes to tools |
| Applications run on OS | **Skills** are the applications |
| Bytes are data units | **Tokens** are data units |

### The Runtime Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         UNIFIEDOS RUNTIME                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  USER MESSAGE (WhatsApp, Web, App)                                          │
│         │                                                                    │
│         ▼                                                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │                     UNIFIED RUNTIME (Python)                         │    │
│  │                                                                      │    │
│  │  1. RECEIVE message                                                  │    │
│  │  2. IDENTIFY vertical (LTR, STR, HOA, Health, BILT)                 │    │
│  │  3. LOAD relevant skills from library                                │    │
│  │  4. BUILD system prompt = base + skills + memory + context          │    │
│  │  5. CALL LLM (Claude/GPT-4/Gemini - model agnostic via LiteLLM)    │    │
│  │  6. LLM DECIDES: respond OR call tool/script                        │    │
│  │  7. IF tool: EXECUTE script (deterministic Python)                  │    │
│  │  8. RETURN result to LLM, loop until done                           │    │
│  │  9. SEND final response to user                                     │    │
│  │                                                                      │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│         │                    │                    │                          │
│         ▼                    ▼                    ▼                          │
│  ┌───────────┐        ┌───────────┐        ┌───────────┐                    │
│  │  SKILLS   │        │  SCRIPTS  │        │  MEMORY   │                    │
│  │  LIBRARY  │        │  (Tools)  │        │  SYSTEM   │                    │
│  │           │        │           │        │           │                    │
│  │ SKILL.md  │        │ Python    │        │ Context   │                    │
│  │ files     │        │ functions │        │ History   │                    │
│  │           │        │           │        │ Tenant DB │                    │
│  └───────────┘        └───────────┘        └───────────┘                    │
│         │                    │                    │                          │
│         └────────────────────┼────────────────────┘                          │
│                              │                                               │
│                              ▼                                               │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │                     EXTERNAL SYSTEMS                                 │    │
│  │                                                                      │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐            │    │
│  │  │PostgreSQL│  │  Twilio  │  │  Plaid   │  │Mastercard│            │    │
│  │  │ + pgvec  │  │ WhatsApp │  │  Banking │  │ Payments │            │    │
│  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘            │    │
│  │                                                                      │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐            │    │
│  │  │  Redis   │  │ Temporal │  │TigerBtle │  │ Formance │            │    │
│  │  │  Cache   │  │ Workflows│  │  Ledger  │  │ Accounting│           │    │
│  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘            │    │
│  │                                                                      │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🎯 The Verticals

UnifiedOS serves multiple industry verticals, all powered by the same runtime but with different skill libraries:

### Current Verticals

| Vertical | Description | Key Skills Needed |
|----------|-------------|-------------------|
| **LTR (Landlord OS)** | Long-term rental management | Maintenance triage, rent payment, lease renewal, tenant support |
| **STR (Host OS)** | Short-term rental (Airbnb-style) | Guest check-in, housekeeping, review management, dynamic pricing |
| **HOA (Community OS)** | HOA/Condo management | Violation reports, amenity booking, governance, assessments |
| **Health (Leona-BR)** | Patient management (Brazil) | Appointment scheduling, reminders, triage, LGPD compliance |
| **BILT (Loyalty)** | Rewards and loyalty engine | Points accrual, redemption, status tiers, credit reporting |
| **Treasury/Cinema** | Financial operations | Payment processing, ticket workflows, multi-rail payments |

### Shared Infrastructure (NEXUS Core)

All verticals share common capabilities:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           NEXUS CORE (Horizontal)                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  MONEY                    IDENTITY                INTELLIGENCE               │
│  ┌──────────────┐        ┌──────────────┐        ┌──────────────┐           │
│  │ Multi-Ledger │        │ User Profiles│        │ Skills       │           │
│  │ Banking      │        │ RBAC/Context │        │ Runtime      │           │
│  │ Payments     │        │ Auth/Tokens  │        │ Memory       │           │
│  └──────────────┘        └──────────────┘        └──────────────┘           │
│                                                                              │
│  COMMUNICATION            WORKFLOW                INTEGRATION                │
│  ┌──────────────┐        ┌──────────────┐        ┌──────────────┐           │
│  │ WhatsApp     │        │ Temporal     │        │ MCP Servers  │           │
│  │ SMS/Email    │        │ Event Bus    │        │ APIs         │           │
│  │ Push         │        │ Automation   │        │ Webhooks     │           │
│  └──────────────┘        └──────────────┘        └──────────────┘           │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🔄 How Knowledge-to-Skills Enables This

### The Manufacturing Metaphor

Think of it like a car factory:

| Car Factory | UnifiedOS |
|-------------|-----------|
| Raw materials (steel, rubber) | Raw knowledge (videos, SOPs, interviews) |
| Manufacturing line | Knowledge-to-Skills pipeline |
| Quality control | Gauntlet testing |
| Finished car | Production-ready skill |
| Car on the road | Skill in runtime serving users |

### The Skill Lifecycle

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         SKILL LIFECYCLE                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. KNOWLEDGE ACQUISITION                                                    │
│     ├── Domain expert has knowledge                                          │
│     ├── Knowledge captured (video, document, interview)                      │
│     └── Raw knowledge becomes input to pipeline                              │
│                                                                              │
│  2. SKILL MANUFACTURING (Knowledge-to-Skills)                                │
│     ├── Phase 1-3: Normalize, extract, create procedure card                 │
│     ├── Phase 4-5: Classify taxonomy, generate skill folder                  │
│     ├── Phase 6-7: Generate evals, run gauntlet                             │
│     └── Phase 8: Package .skill file                                         │
│                                                                              │
│  3. SKILL DEPLOYMENT                                                         │
│     ├── Deploy to staging environment                                        │
│     ├── Test with real conversations                                         │
│     └── Promote to production                                                │
│                                                                              │
│  4. SKILL IN PRODUCTION                                                      │
│     ├── Runtime loads skill when triggered                                   │
│     ├── LLM uses skill instructions to handle conversation                   │
│     ├── Scripts execute deterministic operations                             │
│     └── User gets response                                                   │
│                                                                              │
│  5. GOVERNANCE & ITERATION                                                   │
│     ├── Monitor skill performance                                            │
│     ├── Capture failures                                                     │
│     ├── Add to eval suite                                                    │
│     ├── Fix procedure card (source of truth)                                 │
│     └── Re-deploy improved skill                                             │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 The Complete System Map

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    UNIFIEDOS: COMPLETE SYSTEM MAP                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │                     KNOWLEDGE LAYER                                  │    │
│  │                                                                      │    │
│  │  Domain Experts → Raw Knowledge → Knowledge-to-Skills Pipeline      │    │
│  │                                        │                             │    │
│  │                                        ▼                             │    │
│  │                              ┌─────────────────┐                     │    │
│  │                              │  SKILL LIBRARY  │                     │    │
│  │                              │                 │                     │    │
│  │                              │ ┌─────────────┐ │                     │    │
│  │                              │ │ LTR Skills  │ │                     │    │
│  │                              │ ├─────────────┤ │                     │    │
│  │                              │ │ STR Skills  │ │                     │    │
│  │                              │ ├─────────────┤ │                     │    │
│  │                              │ │ HOA Skills  │ │                     │    │
│  │                              │ ├─────────────┤ │                     │    │
│  │                              │ │Health Skills│ │                     │    │
│  │                              │ ├─────────────┤ │                     │    │
│  │                              │ │ BILT Skills │ │                     │    │
│  │                              │ └─────────────┘ │                     │    │
│  │                              └────────┬────────┘                     │    │
│  │                                       │                              │    │
│  └───────────────────────────────────────┼──────────────────────────────┘    │
│                                          │                                   │
│  ┌───────────────────────────────────────┼──────────────────────────────┐    │
│  │                     RUNTIME LAYER     │                               │    │
│  │                                       ▼                               │    │
│  │  ┌──────────────────────────────────────────────────────────────┐    │    │
│  │  │                  UNIFIED RUNTIME                              │    │    │
│  │  │                                                               │    │    │
│  │  │  ┌────────────┐  ┌────────────┐  ┌────────────────────────┐  │    │    │
│  │  │  │   Skill    │  │   LLM      │  │      Memory            │  │    │    │
│  │  │  │   Loader   │  │  (Claude/  │  │    Management          │  │    │    │
│  │  │  │            │  │   GPT/etc) │  │                        │  │    │    │
│  │  │  └────────────┘  └────────────┘  └────────────────────────┘  │    │    │
│  │  │                                                               │    │    │
│  │  │  ┌────────────┐  ┌────────────┐  ┌────────────────────────┐  │    │    │
│  │  │  │   Tool     │  │  Output    │  │     Validation         │  │    │    │
│  │  │  │  Executor  │  │ Guarantees │  │      Layer             │  │    │    │
│  │  │  │            │  │            │  │                        │  │    │    │
│  │  │  └────────────┘  └────────────┘  └────────────────────────┘  │    │    │
│  │  │                                                               │    │    │
│  │  └──────────────────────────────────────────────────────────────┘    │    │
│  │                              │                                        │    │
│  └──────────────────────────────┼────────────────────────────────────────┘    │
│                                 │                                             │
│  ┌──────────────────────────────┼────────────────────────────────────────┐    │
│  │             INFRASTRUCTURE LAYER                                       │    │
│  │                              │                                         │    │
│  │  ┌───────────┐  ┌───────────┼───────────┐  ┌───────────────────────┐  │    │
│  │  │  Gateway  │  │   DATA    │           │  │    EXTERNAL APIS     │  │    │
│  │  │  (Rust)   │  │           ▼           │  │                       │  │    │
│  │  │           │  │  PostgreSQL + pgvec   │  │  Twilio, Plaid,       │  │    │
│  │  │  Auth     │  │  Redis                │  │  Mastercard, etc.     │  │    │
│  │  │  Rate Lim │  │  TigerBeetle          │  │                       │  │    │
│  │  │           │  │  Formance             │  │                       │  │    │
│  │  └───────────┘  └───────────────────────┘  └───────────────────────┘  │    │
│  │                                                                        │    │
│  └────────────────────────────────────────────────────────────────────────┘    │
│                                 │                                              │
│  ┌──────────────────────────────┼────────────────────────────────────────┐     │
│  │                 USER INTERFACE LAYER                                   │     │
│  │                              │                                         │     │
│  │  ┌───────────────┐  ┌───────┴───────┐  ┌─────────────────────────┐   │     │
│  │  │   WhatsApp    │  │   Web App     │  │    Property Manager    │   │     │
│  │  │  (Tenant)     │  │   (User)      │  │      Portal            │   │     │
│  │  └───────────────┘  └───────────────┘  └─────────────────────────┘   │     │
│  │                                                                        │     │
│  └────────────────────────────────────────────────────────────────────────┘     │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🎯 Your Role as AI Knowledge Engineer

When you create skills using the Knowledge-to-Skills methodology, you are:

1. **Manufacturing components** for a larger system
2. **Enabling verticals** to serve their specific domains
3. **Building the brain** that powers conversational AI
4. **Creating reusable knowledge** that can be deployed across clients

### What Happens to Your Skills

```
You create skill                Runtime loads skill
      │                               │
      ▼                               ▼
┌─────────────┐              ┌─────────────────────────────────────┐
│ SKILL.md    │              │ Tenant: "I have a water leak"       │
│ + scripts   │─────────────▶│                                     │
│ + evals     │              │ LLM loads: leak-triage-protocol     │
└─────────────┘              │ LLM decides: classify_severity      │
                             │ Script runs: returns "urgent"       │
                             │ LLM generates: response with ETA    │
                             │                                     │
                             │ Tenant receives WhatsApp message    │
                             └─────────────────────────────────────┘
```

---

## 📋 Key Points to Remember

### 1. Skills are Components, Not the Product

The product is the **user experience** — a tenant getting help with a leak, a guest checking in, a patient booking an appointment. Skills are the **reusable components** that enable those experiences.

### 2. The Runtime is Model-Agnostic

We use **LiteLLM** to abstract the LLM provider. Skills work with Claude, GPT-4, Gemini, Llama, etc. Don't write skills for a specific model.

### 3. Deterministic Operations Use Scripts

The LLM handles **language and decision-making**. Scripts handle **calculations, database operations, API calls**. This ensures reliability.

### 4. Memory is Multi-Layered

```
Context Window → Current conversation (short-term)
Session Cache → Recent interactions (medium-term)
Tenant Memory → User history in DB (long-term)
Property/Asset Memory → Entity-specific history (permanent)
```

### 5. Output Guarantees Are Critical

We have multiple layers to ensure reliable output:
- Structured outputs (Instructor/Pydantic)
- Allowed-tools restrictions
- Script-based validation
- Template-based responses

### 6. Governance Prevents Drift

Skills are **living documents** that evolve. The governance process ensures changes are:
- Traceable (from failure to fix)
- Tested (gauntlet must pass)
- Approved (human review required)

---

## 🚀 Building New Verticals

When a new vertical is needed (e.g., "Pet Care Management"):

### Step 1: Gather Raw Knowledge
- Interview pet care experts
- Collect SOPs, training materials
- Document workflows

### Step 2: Run Knowledge-to-Skills Pipeline
- Create skill library for the vertical
- `skills/pet-care/appointment-booking/`
- `skills/pet-care/medication-reminders/`
- `skills/pet-care/emergency-triage/`

### Step 3: Configure Runtime
- Register new vertical in runtime config
- Map triggers to skills
- Set up integrations (pet care APIs, etc.)

### Step 4: Deploy
- Deploy skills to runtime
- Configure user interfaces
- Go live

**The same infrastructure serves all verticals. Only the skills differ.**

---

## 📊 Success Metrics

### Skill Level
- Gauntlet score ≥85%
- Forbidden action compliance 100%
- Response time <5s
- User satisfaction >4.5/5

### Vertical Level
- Task completion rate >90%
- First-contact resolution >80%
- Cost per interaction (vs. human)
- User adoption rate

### Platform Level
- Number of active verticals
- Skills deployed
- Monthly active users
- Revenue per vertical

---

## 🎯 Summary

**Knowledge-to-Skills is the manufacturing process. UnifiedOS is the product.**

Your work as an AI Knowledge Engineer:
1. **Inputs:** Raw domain knowledge
2. **Process:** 9-phase pipeline
3. **Outputs:** Production-ready skills
4. **Destination:** Skill library in UnifiedOS runtime
5. **End result:** Users get intelligent, reliable AI assistance

Every skill you create becomes a **permanent capability** of the platform, serving users across all deployments of that vertical.

---

## 📚 Related Documentation

- **Runtime Architecture:** `docs/architecture/MODEL_AGNOSTIC_ARCHITECTURE.md`
- **Skill Framework:** `docs/guides/BA_ROLE_TRANSFORMATION.md`
- **Vertical PRDs:** `docs/PMSVertical/*.md`
- **Financial Core:** `docs/architecture/MULTI_RAIL_ARCHITECTURE.md`
- **This Methodology:** `docs/methodology/README.md`

