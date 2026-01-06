# Implementation Planning Agent Prompt

## 🎯 YOUR MISSION

You are an **Implementation Planning Agent** responsible for creating a detailed implementation roadmap for **Citadel OS** - a Digital Workforce platform for property management.

---

## 📂 REPOSITORY CONTEXT

You have access to **TWO repositories**:

### Repository 1: UnifiedTreasuryOS (Financial Core)
**Path**: `C:\Users\wrios\Documents\GitHub\UnifiedTreasuryOS`
**Status**: Existing infrastructure - partially built

**Contains**:
- TigerBeetle ledger integration
- Formance programmable accounting
- Temporal workflow orchestration
- Double-entry ledger architecture
- Rust/Axum API gateway foundation

**Key Files to Review**:
```
UnifiedTreasuryOS/
├── README.md                          # Project overview
├── COMPLETE_RESOURCE_INDEX.md         # Full resource map
├── docs/architecture/
│   ├── ARCHITECTURE_MANIFESTO.md      # Core principles
│   ├── COMPOSABLE_TREASURY_PLATFORM.md
│   └── MODEL_AGNOSTIC_ARCHITECTURE.md
├── internal/ledger/ledger.go          # Ledger implementation
├── adapters/tigerbeetle/adapter.go    # TigerBeetle adapter
├── core/interfaces/                   # Interface definitions
├── runtime/unified_runtime.py         # Python runtime
└── skills/skill-authoring-standards/  # Skill standards
```

### Repository 2: RawKnowledgetoSkill (Specifications)
**Path**: `C:\Users\wrios\Documents\GitHub\RawKnowledgetoSkill`
**Status**: Complete specifications - ready for implementation

**Contains**:
- 10 MVP knowledge gaps fully specified (87,000+ lines)
- 20 P0 skills with engineering specifications
- 42 infrastructure decisions (all resolved)
- Phase 1 research prompts (28 more skills)
- Business plan and architecture docs

**Key Files to Review**:
```
RawKnowledgetoSkill/
├── STATUS.md                          # Current project status
├── docs/
│   ├── BUSINESS_PLAN_DRAFT.md         # Vision and strategy
│   ├── COMPLETE_TECHNICAL_ARCHITECTURE.md
│   ├── OPEN_ITEMS_TRACKER.md          # All 42 items resolved
│   ├── PHASE1_SKILL_TRACKER.md        # Phase 1 planning
│   └── architecture/
│       └── LAYER4_SKILLS_ARCHITECTURE.md  # Skills framework
├── knowledge/infrastructure/
│   └── KD-PRODUCTION-INFRASTRUCTURE-FINAL.md  # Infrastructure decisions
├── specs/                             # Final skill specifications
│   ├── ai-workforce/SPEC-SKILL-261-268.md
│   ├── communication/SPEC-SKILL-253.md
│   ├── communication/SPEC-SKILL-269-MULTI-CHANNEL-VOICE.md
│   ├── pricing/SPEC-SKILL-101-HLP-PRICING.md
│   ├── pricing/SPEC-SKILL-146-EVENT-DETECTION.md
│   ├── operations/SPEC-SKILL-254-AI-MAINTENANCE.md
│   ├── operations/SPEC-SKILL-257-UNIT-TURN-BOARD.md
│   ├── operations/SPEC-SKILL-270-272-MAINTENANCE-BRAIN.md
│   └── channel/SPEC-SKILL-232-QUOTE-CHASER.md
└── knowledge/                         # Engineering specs (detailed)
    ├── ai-workforce/ES-HOAI-001-*.md  # 11,398 lines
    ├── communication/ES-*.md           # Voice + Leasing specs
    ├── pricing/ES-*.md                 # HLP + Event Detection
    └── operations/ES-*.md              # Maintenance specs
```

---

## 🏗️ INFRASTRUCTURE DECISIONS (Already Made)

Reference: `knowledge/infrastructure/KD-PRODUCTION-INFRASTRUCTURE-FINAL.md`

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **Cloud** | AWS (us-east-1 primary, sa-east-1 Brazil) | Best Twilio integration, Brazil presence |
| **Containers** | ECS/Fargate | $0 control plane, simpler than EKS |
| **TigerBeetle** | EC2 with local NVMe (6-replica) | Performance requirements |
| **Voice Edge** | Latitude.sh (São Paulo) | <260ms latency for Brazil |
| **Database** | MongoDB Atlas + Vector Search | Already decided in specs |
| **Workflows** | Temporal Cloud | Already in Treasury OS |
| **LLM** | Claude 3.5 Sonnet + Groq (voice) | Per spec decisions |
| **Voice** | Twilio ConversationRelay + Deepgram + Cartesia | Per spec |

---

## 📋 YOUR TASK: Create Implementation Roadmap

### Step 1: Review Both Repositories

First, thoroughly review:

1. **Treasury OS Current State**:
   - What's already built?
   - What APIs exist?
   - What's the deployment status?
   - What gaps exist vs what we need?

2. **Specification Completeness**:
   - Review each spec in `specs/` folder
   - Identify dependencies between specs
   - Map specs to Treasury OS capabilities

### Step 2: Create Implementation Plan

Produce a document with:

#### 2.1 Dependency Analysis
```markdown
## Dependency Graph

### Layer 0: Infrastructure (Treasury OS exists)
- [ ] TigerBeetle cluster deployment status
- [ ] Formance ledger deployment status
- [ ] Temporal Cloud connection
- [ ] MongoDB Atlas setup

### Layer 1: Platform Services (Build on Treasury OS)
- [ ] Authentication (Auth0)
- [ ] API Gateway enhancement
- [ ] Message queues (Redis Streams)

### Layer 2: AI Engine (New - from specs)
- [ ] Suna Agent Runtime
- [ ] LangGraph Router
- [ ] MCP Server Gateway
- [ ] Skills Repository structure

### Layer 3: MVP Skills (From specifications)
- [ ] AI Workforce (SKILL-261-268)
- [ ] Voice Agent (SKILL-269)
- [ ] AI Leasing (SKILL-253)
- [ ] HLP Pricing (SKILL-101-103)
- [ ] etc.
```

#### 2.2 Sprint/Phase Breakdown
```markdown
## Implementation Phases

### Phase 1: Foundation (Weeks 1-4)
**Goal**: Platform infrastructure ready

| Week | Focus | Deliverables |
|------|-------|--------------|
| 1 | Infrastructure | AWS setup, ECS cluster, MongoDB |
| 2 | Treasury OS | TigerBeetle deployment, Formance config |
| 3 | Platform | Auth0, API Gateway, Redis |
| 4 | AI Foundation | Suna runtime, LangGraph router |

### Phase 2: Core AI (Weeks 5-8)
**Goal**: First AI agents operational

| Week | Focus | Deliverables |
|------|-------|--------------|
| 5 | HITL Framework | Dashboard, task queue, approvals |
| 6 | Voice Infrastructure | Twilio, Deepgram, Cartesia |
| 7 | Voice Agent MVP | SKILL-269 implementation |
| 8 | Integration Testing | End-to-end voice flows |

### Phase 3: Business Logic (Weeks 9-12)
**Goal**: Revenue-generating features

| Week | Focus | Deliverables |
|------|-------|--------------|
| 9 | AI Leasing | SKILL-253 implementation |
| 10 | Dynamic Pricing | SKILL-101-103 + SKILL-146 |
| 11 | Maintenance AI | SKILL-254 + SKILL-270-272 |
| 12 | Quote Chaser | SKILL-232 implementation |
```

#### 2.3 Team Structure
```markdown
## Suggested Team Allocation

### Team 1: Platform/Infrastructure
- Treasury OS integration
- AWS infrastructure
- Database setup
- DevOps/CI-CD

### Team 2: AI Engine
- Suna runtime
- LangGraph orchestration
- MCP servers
- Skills framework

### Team 3: Voice/Communication
- Twilio integration
- Deepgram/Cartesia
- Multi-channel messaging
- Brazil edge deployment

### Team 4: Business Features
- Pricing engine
- Maintenance workflows
- Leasing automation
- Quote management
```

#### 2.4 Risk Assessment
```markdown
## Implementation Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| TigerBeetle deployment complexity | Medium | High | Start early, allocate buffer |
| Voice latency in Brazil | Medium | High | Latitude.sh fallback tested |
| LLM cost overruns | Low | Medium | Rate limiting, caching |
| Spec gaps discovered | Medium | Medium | Agile adjustment, researcher on standby |
```

### Step 3: Create Task Breakdown

For each skill specification, create detailed tasks:

```markdown
## SKILL-269: Multi-Channel Voice Agent

### Reference: specs/communication/SPEC-SKILL-269-MULTI-CHANNEL-VOICE.md

### Pre-requisites:
- [ ] Twilio account with ConversationRelay enabled
- [ ] Deepgram API credentials
- [ ] Cartesia/ElevenLabs API credentials
- [ ] MongoDB collections created
- [ ] Redis pub/sub configured

### Implementation Tasks:

#### Infrastructure (3 days)
- [ ] TASK-269-001: Create ECS task definition for voice service
- [ ] TASK-269-002: Configure Twilio webhook endpoints
- [ ] TASK-269-003: Set up Deepgram streaming connection
- [ ] TASK-269-004: Configure Cartesia TTS pipeline

#### Core Logic (5 days)
- [ ] TASK-269-005: Implement ConversationRelay handler
- [ ] TASK-269-006: Build LangGraph conversation flow
- [ ] TASK-269-007: Implement barge-in detection
- [ ] TASK-269-008: Create emergency escalation flow

#### Integration (3 days)
- [ ] TASK-269-009: Connect to PMS for data lookup
- [ ] TASK-269-010: Integrate with HITL dashboard
- [ ] TASK-269-011: Implement cross-channel threading

#### Testing (2 days)
- [ ] TASK-269-012: Unit tests (80% coverage)
- [ ] TASK-269-013: Integration tests
- [ ] TASK-269-014: Load testing (<300ms latency)

### Estimated Effort: 13 days (1 engineer)
### Dependencies: SKILL-261-268 (AI Workforce - HITL framework)
```

---

## 📄 OUTPUT REQUIREMENTS

### Deliverable 1: Implementation Roadmap
**File**: `docs/IMPLEMENTATION_ROADMAP.md`

Contents:
- Executive summary
- Dependency analysis
- Phase breakdown (16 weeks)
- Team structure
- Risk assessment
- Success metrics

### Deliverable 2: Task Registry
**File**: `docs/IMPLEMENTATION_TASK_REGISTRY.md`

Contents:
- Every task for every MVP skill
- Pre-requisites
- Effort estimates
- Dependencies
- Assignee placeholders

### Deliverable 3: Treasury OS Integration Guide
**File**: `docs/TREASURY_OS_INTEGRATION.md`

Contents:
- Current Treasury OS capabilities
- Required enhancements
- API mapping (spec → Treasury OS)
- Migration path for existing code

### Deliverable 4: Sprint Backlog (First 4 Weeks)
**File**: `docs/SPRINT_BACKLOG_WEEKS_1-4.md`

Contents:
- Detailed sprint planning
- Daily breakdown
- Acceptance criteria
- Testing requirements

---

## 🔄 WORKFLOW

1. **First**: Read both repositories thoroughly
2. **Second**: Map specifications to implementation tasks
3. **Third**: Identify dependencies and order
4. **Fourth**: Estimate effort per task
5. **Fifth**: Create phase breakdown
6. **Sixth**: Produce all deliverables
7. **Seventh**: Commit and push

---

## ✅ COMPLETION CHECKLIST

- [ ] Reviewed UnifiedTreasuryOS current state
- [ ] Reviewed all 10 MVP specifications
- [ ] Reviewed infrastructure decisions document
- [ ] Created dependency graph
- [ ] Created 16-week implementation roadmap
- [ ] Created task registry for all MVP skills
- [ ] Created Treasury OS integration guide
- [ ] Created first 4-week sprint backlog
- [ ] All documents committed to repo

---

## 💡 KEY PRINCIPLES

1. **Build on What Exists**: Treasury OS has valuable infrastructure - extend, don't replace
2. **Spec-Driven Development**: Each task traces back to a specification
3. **AI-First Architecture**: The "Agent as OS" model guides all decisions
4. **Brazil Market Ready**: Every decision considers São Paulo deployment
5. **Incremental Value**: Each phase delivers usable functionality

---

## 🚀 AFTER COMPLETING

```bash
cd C:\Users\wrios\Documents\GitHub\RawKnowledgetoSkill
git add -A
git commit -m "Implementation Planning: Complete roadmap, task registry, and sprint backlog"
git push
```

Then notify the team that implementation planning is complete.

---

## 📊 SUCCESS CRITERIA

Your implementation plan is complete when:

1. **Clarity**: Any engineer can pick up a task and know what to build
2. **Traceability**: Every task links to a specification
3. **Feasibility**: Estimates are realistic (buffer included)
4. **Dependencies**: Clear build order with no circular dependencies
5. **Testability**: Each task has acceptance criteria

---

## 🔗 QUICK LINKS FOR REVIEW

**Treasury OS**:
- `UnifiedTreasuryOS/README.md`
- `UnifiedTreasuryOS/docs/architecture/ARCHITECTURE_MANIFESTO.md`
- `UnifiedTreasuryOS/COMPLETE_RESOURCE_INDEX.md`

**Specifications**:
- `RawKnowledgetoSkill/STATUS.md`
- `RawKnowledgetoSkill/knowledge/infrastructure/KD-PRODUCTION-INFRASTRUCTURE-FINAL.md`
- `RawKnowledgetoSkill/specs/*` (all spec files)

**Architecture**:
- `RawKnowledgetoSkill/docs/COMPLETE_TECHNICAL_ARCHITECTURE.md`
- `RawKnowledgetoSkill/docs/architecture/LAYER4_SKILLS_ARCHITECTURE.md`
- `RawKnowledgetoSkill/docs/BUSINESS_PLAN_DRAFT.md`

---

**You are authorized to create new files, update existing documentation, and propose architectural decisions. Be thorough, be practical, and create something an engineering team can execute.**

