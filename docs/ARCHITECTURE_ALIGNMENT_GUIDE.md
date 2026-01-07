# Architecture Alignment Guide for Skill Specifications

**Version**: 1.0
**Date**: January 7, 2026
**Purpose**: Ensure all incoming specifications align with Citadel OS reference architecture

---

## 📐 Reference Architecture (Source of Truth)

All skill specifications MUST align with this established architecture:

### 6-Layer Stack

| Layer | Components | Technology | Status |
|-------|------------|------------|--------|
| **Layer 6** | User Applications | React/RN, Next.js, Mobile | ✅ Defined |
| **Layer 5** | Domain Bundles | STR, LTR, HOA, Fintech, Loyalty | ✅ Defined |
| **Layer 4** | Skills Layer | Claude Skills Framework, SKILL.md | ✅ Defined |
| **Layer 3A** | Hot Path | Suna, LangGraph, LangChain/LiteLLM | ✅ Defined |
| **Layer 3B** | Cold Path | Treasury OS (TigerBeetle, Formance, Temporal) | ✅ Built |
| **Layer 2** | Infrastructure | AWS ECS/Fargate, Redis, Redpanda | ✅ Decided |
| **Layer 1** | Network | Multi-region US/Brazil, Latitude.sh Edge | ✅ Decided |

---

## 🏗️ Core Technology Decisions (MANDATORY)

### Financial Core (Treasury OS) - MANDATORY
These components are **already built** and MUST be used for financial operations:

| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| **Financial Database** | TigerBeetle | Latest | 1M+ TPS, immutable ledger, double-entry |
| **Programmable Ledger** | Formance | Latest | Numscript DSL, reconciliation |
| **Workflow Orchestration** | Temporal | Latest | Durable execution, saga patterns |
| **Event Streaming** | Redpanda | Latest | Event sourcing |
| **API Gateway** | Rust/Axum | Latest | Zero-GC, rate limiting |
| **Micro-tx Buffering** | Redis (AOF) | Latest | Dust-to-bricks pattern |

### Infrastructure Decisions - MANDATORY
From `KD-PRODUCTION-INFRASTRUCTURE-FINAL.md`:

| Decision | Choice | NOT This | Rationale |
|----------|--------|----------|-----------|
| **Cloud Provider** | AWS Primary | Azure, GCP (secondary) | Brazil presence, voice ecosystem |
| **Container Orchestration** | ECS/Fargate | Kubernetes/EKS | $0 control plane vs $74/mo |
| **Brazil Voice Edge** | Latitude.sh | US-only | <260ms latency requirement |
| **TigerBeetle Config** | 6-replica federated | Single region | LGPD compliance |
| **Crypto Custody** | Fireblocks MPC | Custodial | SPSAV compliance |

### AI/Agent Layer - MANDATORY
| Component | Technology | Purpose |
|-----------|------------|---------|
| **Agent Runtime** | Suna (Kortix) | Multi-modal execution |
| **Orchestration** | LangGraph | State management, handoffs |
| **LLM Abstraction** | LangChain + LiteLLM | Model agnostic |
| **Skills Framework** | Claude Code Model | Agent=OS, Skills=Apps |
| **Vector DB** | MongoDB Atlas Vector Search | RAG, embeddings |

---

## ✅ Alignment Checklist for Incoming Specifications

When processing incoming engineering specifications, verify:

### Financial Operations
- [ ] Uses TigerBeetle for financial transactions (NOT PostgreSQL)
- [ ] Uses Formance/Numscript for accounting logic
- [ ] Uses Temporal for workflow orchestration
- [ ] Integrates via MCP servers (not direct API calls)

### Data Storage
- [ ] Financial data → TigerBeetle (immutable)
- [ ] Application metadata → PostgreSQL (OK)
- [ ] Caching → Redis
- [ ] Documents/Reports → MongoDB
- [ ] Vector embeddings → MongoDB Atlas Vector Search

### Infrastructure
- [ ] AWS ECS/Fargate (NOT Kubernetes/EKS)
- [ ] Multi-region US/Brazil
- [ ] Latitude.sh for Brazil voice edge
- [ ] Auth0 for authentication

### API Design
- [ ] External APIs → Rust/Axum API Gateway
- [ ] Internal services → FastAPI (Python) OK
- [ ] Skill scripts → Python
- [ ] Financial workflows → Temporal activities

### Skills Architecture
- [ ] Skills defined as SKILL.md files
- [ ] Progressive Disclosure (3-phase loading)
- [ ] Hot/Cold/Hybrid execution path specified
- [ ] Tools use MCP protocol (`mcp://treasury/*`, `mcp://temporal/*`)

---

## ⚠️ Common Misalignments to Catch

### 1. Database Choices
**WRONG**: "Store payments in PostgreSQL"
**RIGHT**: "Store payments in TigerBeetle via Formance Numscript"

### 2. Container Orchestration
**WRONG**: "Deploy to Kubernetes cluster"
**RIGHT**: "Deploy to AWS ECS/Fargate" (except TigerBeetle which runs on EC2)

### 3. Direct Database Access
**WRONG**: "API calls TigerBeetle directly"
**RIGHT**: "Skill calls `mcp://treasury/create_transfer` which invokes Temporal workflow"

### 4. Monolithic Services
**WRONG**: "Single Node.js service handles all financial logic"
**RIGHT**: "Financial operations routed through Temporal workflows with TigerBeetle persistence"

---

## 🔄 Mapping Incoming Tech to Our Stack

| If Spec Says | Map To | Layer |
|--------------|--------|-------|
| PostgreSQL (financial) | TigerBeetle | 3B |
| PostgreSQL (app data) | PostgreSQL (OK) | 2 |
| Kubernetes/EKS | ECS/Fargate | 2 |
| Direct API to ledger | MCP Server → Temporal → TigerBeetle | 3B |
| Redis caching | Redis (AOF for financial, regular for cache) | 2 |
| Kafka | Redpanda | 2 |
| Custom workflow | Temporal | 3B |
| AI reasoning | Hot Path (Suna/LangGraph) | 3A |
| Financial txn | Cold Path (Treasury OS) | 3B |

---

## 📝 Specification Annotation Template

Add this section to each specification:

```markdown
## Architecture Alignment Notes

### Layer Mapping
| Spec Component | Citadel Layer | Technology |
|----------------|---------------|------------|
| Payment Processing | Layer 3B | TigerBeetle via Formance |
| API Gateway | Layer 2 | Rust/Axum |
| Business Logic | Layer 4 | Skill Scripts (Python) |

### Execution Path
- **Hot Path Components**: [list AI/reasoning operations]
- **Cold Path Components**: [list financial/guaranteed operations]
- **Hybrid Components**: [list mixed operations]

### MCP Server Requirements
- `mcp://treasury/create_transfer` - For payment creation
- `mcp://temporal/trigger_workflow` - For workflow orchestration
- `mcp://vector/query` - For RAG retrieval

### Compliance with Architecture
- ✅ Uses TigerBeetle for financial data
- ✅ Uses Formance for accounting
- ✅ Uses Temporal for workflows
- ✅ Targets ECS/Fargate deployment
```

---

## 📊 Summary Table: Our Tech Stack

| Category | Decision | Version |
|----------|----------|---------|
| **Cloud** | AWS | Primary |
| **Compute** | ECS Fargate | (TigerBeetle on EC2) |
| **Financial DB** | TigerBeetle | 0.16.67 |
| **Ledger** | Formance | Latest |
| **Workflows** | Temporal | Cloud |
| **Events** | Redpanda | Latest |
| **Cache** | Redis | 7.0+ |
| **App DB** | PostgreSQL | 15+ |
| **Vector** | MongoDB Atlas | Vector Search |
| **Auth** | Auth0 | Enterprise |
| **AI Runtime** | Suna + LangGraph | Latest |
| **LLM** | Claude + GPT-4 | Via LiteLLM |
| **Voice Edge** | Latitude.sh | Brazil |
| **Crypto** | Fireblocks MPC | - |

---

*This guide should be referenced when processing all incoming engineering specifications.*

