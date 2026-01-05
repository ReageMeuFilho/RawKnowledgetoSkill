# Unified Treasury OS: Business Plan

> **Version**: Draft 1.0
> **Date**: January 2026
> **Author**: [Founder]
> **Status**: Working Document

---

## Executive Summary

We are building **Unified Treasury OS**—a next-generation property management operating system that combines the best capabilities from 23+ market leaders into a single, AI-native platform. Unlike competitors who bolt AI onto legacy systems, we're building from first principles: a **skill-based architecture** where every capability is systematically researched, specified, and implemented to production-ready standards.

**Our Moat**: A proprietary **Knowledge-to-Skill Methodology** that transforms competitive intelligence into shippable product capabilities at unprecedented speed and quality. This methodology combines **probabilistic AI** (agents, LLMs, retrieval) with **deterministic workflows** (state machines, policies, data contracts) to create reliable, auditable, and scalable systems.

---

# PART 1: THE VISION

## 1.1 What We're Building

**Unified Treasury OS** is a comprehensive property management platform that spans:

| Vertical | Capabilities | Target Users |
|----------|--------------|--------------|
| **Short-Term Rental (STR)** | Channel management, dynamic pricing, guest communication, operations | Airbnb hosts, vacation rental managers |
| **Long-Term Rental (LTR)** | Leasing, tenant management, maintenance, accounting | Property managers, landlords |
| **Fintech** | Banking, payments, tax automation, compliance | All property owners/managers |
| **Consumer** | Rent rewards, credit building, loyalty | Renters, residents |
| **Investment** | Portfolio analytics, investor relations, capital management | Real estate investors, funds |
| **HOA/Community** | Association management, architectural review, violations | HOA managers, board members |

**The Vision**: One platform that handles **any property type** with **AI-native operations**—from a single Airbnb host to a 50,000-unit institutional portfolio.

## 1.2 Why Now?

Three converging forces create a once-in-a-generation opportunity:

### 1. Market Fragmentation
- Property managers use 5-10+ disconnected tools
- No single platform does everything well
- Integration costs are crippling (time, money, data loss)

### 2. AI Inflection Point
- LLMs enable human-level understanding of unstructured communication
- Agentic AI can now execute multi-step workflows autonomously
- Cost per AI operation has dropped 100x in 3 years

### 3. Competitive Complacency
- Legacy players (Yardi, RealPage, AppFolio) are bolting AI onto 20-year-old architectures
- Vertical-specific tools (Guesty, Hostaway) can't expand across property types
- Point solutions (PriceLabs, EliseAI) remain siloed

**Our Timing**: Build AI-native from day one, across all property verticals, with a methodology that compounds.

## 1.3 The End State

In 5 years, Unified Treasury OS will be:

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         UNIFIED TREASURY OS                                      │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │
│   │ STR Engine  │  │ LTR Engine  │  │ HOA Engine  │  │ Invest Eng  │           │
│   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘           │
│          │                │                │                │                   │
│          └────────────────┴────────────────┴────────────────┘                   │
│                                    │                                            │
│                          ┌─────────┴─────────┐                                  │
│                          │  UNIFIED CORE     │                                  │
│                          │                   │                                  │
│                          │  • Skill Registry │                                  │
│                          │  • AI Workforce   │                                  │
│                          │  • Policy Engine  │                                  │
│                          │  • Data Platform  │                                  │
│                          │  • Fintech Rails  │                                  │
│                          └───────────────────┘                                  │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

# PART 2: THE PRODUCT

## 2.1 Core Capabilities (MVP)

Based on our analysis of **23 competitors** and **265 identified skills**, our MVP focuses on **79 P0 skills** across these domains:

| Domain | P0 Skills | Key Capabilities |
|--------|-----------|------------------|
| **Communication** | 13 | Unified inbox, AI response, sentiment routing |
| **Booking** | 8 | Multi-calendar, instant booking, quote management |
| **Pricing** | 8 | Dynamic pricing, HLP algorithm, event detection |
| **Operations** | 12 | Cleaning scheduling, maintenance AI, unit turns |
| **Financial** | 14 | Payments, trust accounting, owner statements |
| **Channel** | 6 | OTA sync, rate parity, inventory distribution |
| **AI Workforce** | 8 | Voice agent, leasing AI, maintenance AI, HITL |

## 2.2 Differentiated Capabilities

These are capabilities we've identified as **best-in-class** from specific competitors, which we will implement at parity or better:

| Capability | Source | Our Implementation |
|------------|--------|-------------------|
| **AI Workforce Model** | HOAi | Specialized AI agents as "digital employees" with human-in-the-loop supervision |
| **Hyper-Local Pulse (HLP)** | PriceLabs | Dynamic pricing using 0.5-5km granular market data |
| **AI Leasing Assistant** | EliseAI | 24/7 lead qualification, tour scheduling, 95% autonomous handling |
| **Maintenance Brain** | Vendoroo | Persistent learning per property, predictive maintenance |
| **Fintech Platform** | Baselane | Integrated banking, Schedule E categorization, tax packages |
| **Rent Rewards** | BILT | Consumer loyalty, credit reporting, 3-sided marketplace |

## 2.3 The Skill Registry

Our central innovation is treating every product capability as a **"Skill"** with:

```yaml
skill_id: SKILL-261
name: Multi-Channel Voice Agent
category: ai-workforce
priority: P0  # MVP, P1, P2, P3
status: SPECIFIED  # NEEDED → RESEARCHED → SPECIFIED → IMPLEMENTED
competitors: [HOAi, Boom AI]
best_implementation: HOAi
effort: L  # S, M, L, XL
specification: specs/ai-workforce/SPEC-SKILL-261-268.md
```

**Current Status**:
- **265 skills** identified across 23 competitors
- **79 MVP skills** (P0) prioritized
- **8 skills fully specified** (10.1% of MVP)
- **10 knowledge gaps** in pipeline

---

# PART 3: THE METHODOLOGY (Our Moat)

## 3.1 The Knowledge-to-Skill Pipeline

This is our core innovation—a systematic methodology for transforming market intelligence into production-ready capabilities.

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                     KNOWLEDGE-TO-SKILL PIPELINE                                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────┐      ┌──────────────┐      ┌──────────────┐      ┌──────────────┐ │
│  │   STAGE 1    │      │   STAGE 2    │      │   STAGE 3    │      │   STAGE 4    │ │
│  │              │      │              │      │              │      │              │ │
│  │  RESEARCH    │ ──▶  │   REVIEW &   │ ──▶  │ ENGINEERING  │ ──▶  │    SKILL     │ │
│  │   AGENT      │      │    PROMPT    │      │    AGENT     │      │    SPEC      │ │
│  │              │      │              │      │              │      │              │ │
│  │  Conceptual  │      │  Gap Check   │      │  Technical   │      │   Final      │ │
│  │  Knowledge   │      │  + Prompt    │      │    Spec      │      │   Output     │ │
│  └──────────────┘      └──────────────┘      └──────────────┘      └──────────────┘ │
│                                                                                      │
│       AI Agent            Quality Gate          AI Agent           Quality Gate     │
│      (Research)           (Cursor AI)         (Engineering)        (Cursor AI)     │
│                                                                                      │
│   Output: KD-*.md      Output: PROMPT_*.md   Output: ES-*.md    Output: SPEC-*.md  │
│   (Conceptual)         (Custom Prompt)       (Technical)        (Implementation)   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### Stage 1: Research Agent
- **Input**: Knowledge gap ID
- **Process**: Competitive research across websites, YouTube, Reddit, forums, reviews
- **Output**: Conceptual knowledge document (what, why, who does it best)
- **Quality Bar**: Answers "What does this feature do and why does it matter?"

### Stage 2: Quality Review + Engineering Prompt
- **Input**: Stage 1 document
- **Process**: Gap analysis, custom prompt generation
- **Output**: Detailed engineering prompt (17+ sections)
- **Quality Bar**: Prompt is specific enough for implementation-ready specs

### Stage 3: Engineering Agent
- **Input**: Stage 2 prompt + Stage 1 research
- **Process**: Technical specification (schemas, state machines, APIs)
- **Output**: 3,000-5,000 line engineering specification
- **Quality Bar**: Answers "How do we build this—exactly?"

### Stage 4: Final Skill Specification
- **Input**: Stage 3 engineering spec
- **Process**: Extract skills, tools, user stories, dependencies
- **Output**: Updated skill registry + detailed spec files
- **Quality Bar**: Engineering team can create tickets and start building

## 3.2 Why This Methodology is a Moat

### Compounding Assets
Each cycle through the pipeline produces:
- **Skill definitions** (reusable across verticals)
- **Data schemas** (standardized contracts)
- **State machines** (tested workflows)
- **API specifications** (integration patterns)
- **User stories** (acceptance criteria)
- **Evaluation sets** (quality benchmarks)

### Quality Through Structure
- **Two AI passes** (Research + Engineering) with **two human gates** (Quality Review)
- **42+ open items tracked** per major skill (nothing falls through cracks)
- **Evaluation sets** ensure AI+deterministic integration works

### Speed Through Parallelization
- Multiple gaps can be researched simultaneously
- Pipeline is independent per skill
- Target: 2-3 gaps closed per week → **full MVP in 6-8 months**

## 3.3 The Evaluation Framework

Every skill specification includes evaluation criteria:

| Evaluation Type | Purpose | Example |
|-----------------|---------|---------|
| **Functional Tests** | Does it do what it should? | "AI responds within 2 seconds" |
| **Integration Tests** | Does it work with other skills? | "Payment flows to accounting" |
| **AI Accuracy Tests** | Does AI understand correctly? | "Intent recognition >85%" |
| **Policy Compliance** | Does it follow rules? | "Never violates fair housing" |
| **Human Fallback Tests** | Does escalation work? | "HITL dashboard receives task" |

---

# PART 4: THE ARCHITECTURE

## 4.1 Two Paths: Hot Path + Cold Path

Our architecture cleanly separates **probabilistic AI operations** from **deterministic system operations**:

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                              UNIFIED ARCHITECTURE                                    │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌────────────────────────────────────────────────────────────────────────────────┐ │
│  │                           HOT PATH (Probabilistic)                              │ │
│  │                                                                                  │ │
│  │   User Input → Intent Recognition → Agent Selection → LLM Processing →         │ │
│  │   → Retrieval (RAG) → Response Generation → Confidence Scoring                 │ │
│  │                                                                                  │ │
│  │   Technologies: LangChain/LangGraph, Vector DB, LLM APIs                       │ │
│  │   Characteristics: Fast, adaptive, uncertain, requires evaluation              │ │
│  │                                                                                  │ │
│  └────────────────────────────────────────────────────────────────────────────────┘ │
│                                        │                                            │
│                                        │ Action Requests                            │
│                                        ▼                                            │
│  ┌────────────────────────────────────────────────────────────────────────────────┐ │
│  │                          COLD PATH (Deterministic)                              │ │
│  │                                                                                  │ │
│  │   Policy Engine → State Machine → Data Validation → Transaction →              │ │
│  │   → Audit Log → Notification → External Integration                            │ │
│  │                                                                                  │ │
│  │   Technologies: State machines, Policy DSL, SQL/Document DB, Message queues   │ │
│  │   Characteristics: Reliable, auditable, predictable, compliance-ready          │ │
│  │                                                                                  │ │
│  └────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### Hot Path (Probabilistic) — "The AI Path"
- **What it does**: Understanding, reasoning, generation, retrieval
- **When used**: User communication, intent classification, knowledge lookup, response drafting
- **Technologies**: LangChain, LangGraph, OpenAI/Anthropic APIs, Vector stores
- **Key Patterns**:
  - Confidence scoring (know when AI is uncertain)
  - Human-in-the-loop escalation
  - Multi-agent orchestration
  - RAG for knowledge retrieval

### Cold Path (Deterministic) — "The Hard Path"
- **What it does**: Validation, state transitions, transactions, compliance
- **When used**: Payments, bookings, lease agreements, accounting, audit trails
- **Technologies**: State machines, Policy engine, PostgreSQL/MongoDB, Redis queues
- **Key Patterns**:
  - Explicit state machines (no hidden transitions)
  - Policy-as-code (auditable rules)
  - Data contracts (typed schemas)
  - Transaction guarantees (ACID where needed)

### The Integration Pattern
```
HOT PATH                           COLD PATH
─────────                          ─────────
AI generates action request   →    Policy engine validates
                                   State machine checks transition
                                   Data validation runs
                                   ↓
                              If confidence < threshold OR policy violation:
                                   → HITL Dashboard (human review)
                              Else:
                                   → Execute transaction
                                   → Emit event
                                   → Update state
                                   → Log audit trail
```

## 4.2 Technology Stack

### AI Path (Hot)

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Orchestration** | LangGraph | Multi-agent workflows, state management |
| **Framework** | LangChain | LLM abstractions, tool calling, chains |
| **LLM** | OpenAI GPT-4, Anthropic Claude | Understanding, generation |
| **Embeddings** | OpenAI, Cohere | Semantic search |
| **Vector Store** | MongoDB Atlas Vector Search | Knowledge retrieval |
| **Monitoring** | LangSmith | LLM observability, debugging |

### System Path (Cold)

| Layer | Technology | Purpose |
|-------|------------|---------|
| **API** | Python/Flask or Node/Express | REST endpoints |
| **State Machine** | Custom DSL, XState | Workflow definitions |
| **Policy Engine** | Open Policy Agent (OPA) or custom | Rule evaluation |
| **Database** | PostgreSQL + MongoDB | Relational + document storage |
| **Queue** | Redis Streams | Event-driven messaging |
| **Cache** | Redis | Session, rate limiting |

### Frontend

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Framework** | React 19 + TypeScript | UI components |
| **Styling** | TailwindCSS 4.1 | Design system |
| **State** | Zustand / React Query | Client state management |
| **Real-time** | WebSocket | Live updates (HITL, chat) |

### Infrastructure

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Containerization** | Docker | Consistent environments |
| **Orchestration** | Kubernetes | Scaling, deployment |
| **CI/CD** | GitHub Actions | Automated pipelines |
| **Monitoring** | Prometheus + Grafana | System observability |
| **Logging** | ELK Stack | Centralized logs |
| **Tracing** | Jaeger | Distributed tracing |

## 4.3 Leveraging Open Source + Frameworks

### Claude Code / Anthropic Ecosystem
- **Meta-knowledge framework**: Use Claude's ability to understand codebases and generate consistent implementations
- **Skill translation**: Convert specifications into code following patterns
- **Review automation**: Quality gates at each stage

### Suna AI / Kortix Architecture Patterns
- **Agent-first design**: Treating AI agents as first-class workers
- **Modular orchestration**: Plug-in different agents for different tasks
- **Browser/tool integration**: Agents that can interact with external systems

### LangChain / LangGraph
- **Agent orchestration**: Multi-agent collaboration patterns
- **State management**: Conversation and workflow state
- **Tool calling**: Structured function invocation
- **Retrieval**: RAG pipelines for knowledge

### Open Source Leverage

| Component | Open Source Option | Purpose |
|-----------|-------------------|---------|
| Policy Engine | Open Policy Agent | Rule evaluation |
| Workflow | Temporal / n8n | Long-running workflows |
| Vector DB | Qdrant / Milvus | Self-hosted vectors |
| LLM | Ollama / vLLM | Self-hosted inference |
| Auth | Keycloak | Self-hosted identity |

---

# PART 5: COMPETITIVE MOAT

## 5.1 Why We Win

### Moat 1: The Skill Registry (Data Asset)
- **265 skills** mapped across 23 competitors
- Normalized taxonomy with IDs, categories, priorities
- Coverage matrix showing who does what
- **Compounds**: Every new competitor analyzed adds to the registry

### Moat 2: The Specification Library (IP Asset)
- Production-ready specs for each skill
- Data schemas, state machines, APIs, user stories
- **Compounds**: Each spec informs the next; patterns emerge

### Moat 3: The Methodology (Process Asset)
- 4-stage pipeline with quality gates
- Agent prompts tuned for property management domain
- **Compounds**: Pipeline gets faster/better with each cycle

### Moat 4: The Evaluation Sets (Quality Asset)
- Test cases for AI accuracy
- Integration test scenarios
- Compliance verification
- **Compounds**: Every bug fixed becomes a test case

### Moat 5: The Open Items Tracker (Knowledge Asset)
- 42+ open questions logged per major skill
- Prioritized backlog of decisions needed
- **Compounds**: Nothing gets lost; every edge case captured

## 5.2 Defensibility Over Time

| Year | Moat Depth |
|------|------------|
| **Year 1** | Skill registry + initial specs + methodology validated |
| **Year 2** | 100+ skills implemented + evaluation sets + integration patterns |
| **Year 3** | Cross-vertical patterns + proprietary AI training data + customer data flywheel |
| **Year 4** | Platform effects (marketplace, integrations) + brand recognition |
| **Year 5** | Industry standard status + regulatory relationships + talent moat |

## 5.3 Competitor Comparison

| Dimension | Legacy Players | Vertical Specialists | Point Solutions | **Us** |
|-----------|---------------|---------------------|-----------------|--------|
| **Architecture** | 20-year monoliths | Modern but narrow | API-first but siloed | AI-native, unified |
| **AI Approach** | Bolted on | Feature-specific | Deep but narrow | Systemic (workforce model) |
| **Methodology** | Waterfall/Agile | Agile | Agile | **Skill-based + AI pipeline** |
| **Expansion** | Slow (legacy debt) | Hard (architecture) | Hard (focus) | Fast (skill composition) |
| **Moat** | Customer lock-in | Vertical expertise | Algorithm IP | **Compounding assets** |

---

# PART 6: GO-TO-MARKET

## 6.1 Market Entry: STR Professional Managers

**Why STR First**:
- Highest pain (fragmented tools, channel management complexity)
- Highest willingness to pay for automation
- Most innovation happening (pricing, AI, operations)
- Natural expansion to LTR (many managers do both)

**Target Segment**: 50-500 unit professional STR managers

**Wedge Product**: AI-powered unified inbox + smart pricing + operations automation

## 6.2 Expansion Path

```
Year 1: STR Professional (50-500 units)
        ↓
Year 2: STR Enterprise (500+ units) + LTR Entry
        ↓
Year 3: Multi-family + HOA + Investment Management
        ↓
Year 4: Full platform + Fintech + Consumer
        ↓
Year 5: Platform (marketplace, white-label, API)
```

## 6.3 Pricing Model

| Tier | Target | Price | Includes |
|------|--------|-------|----------|
| **Starter** | 1-10 units | Free / $29/mo | Core PMS, limited AI |
| **Professional** | 11-50 units | $99-199/mo | Full AI, pricing, ops |
| **Business** | 51-200 units | $299-499/mo | Advanced analytics, API |
| **Enterprise** | 200+ units | Custom | White-label, dedicated support |

---

# PART 7: EXECUTION PLAN

## 7.1 Phase 0: Foundation (Months 1-3)

**Goal**: Complete MVP skill specifications

| Milestone | Target | Status |
|-----------|--------|--------|
| Skill Registry | 265 skills mapped | ✅ Complete |
| MVP Gaps Identified | 10 gaps, 79 skills | ✅ Complete |
| Pipeline Validated | First gap through full cycle | ✅ Complete (GAP-HOAI-001) |
| MVP Specs | 79 P0 skills specified | 🔄 10.1% complete |

**Current Work**:
- GAP-AF-001 (AI Leasing Assistant) at Stage 3
- 7 gaps remaining in pipeline

## 7.2 Phase 1: MVP Build (Months 4-9)

**Goal**: Shippable MVP with core capabilities

| Track | Skills | Effort |
|-------|--------|--------|
| Communication (Unified Inbox) | 13 | 8 weeks |
| Booking Engine | 8 | 6 weeks |
| Pricing Engine | 8 | 6 weeks |
| Operations Core | 12 | 8 weeks |
| Financial Core | 14 | 10 weeks |
| Channel Integrations | 6 | 8 weeks |
| AI Workforce (Core Agents) | 8 | 16 weeks |

**Parallelization**: 3-4 tracks running simultaneously → 6 months

## 7.3 Phase 2: Launch + Iterate (Months 10-15)

- Private beta with 10-20 STR managers
- Rapid iteration based on feedback
- Performance optimization
- Security audit
- Public launch

## 7.4 Phase 3: Scale (Months 16-24)

- Enterprise features
- LTR vertical entry
- Advanced AI capabilities
- Platform/marketplace foundations

---

# PART 8: TEAM & RESOURCES

## 8.1 Current State

- **Founder**: Product vision, methodology design, orchestration
- **AI Agents**: Research, engineering specification
- **Cursor AI**: Quality gates, prompt engineering, final specs

## 8.2 Hiring Plan

| Role | When | Purpose |
|------|------|---------|
| **Founding Engineer (Full-stack)** | Month 1 | Core platform build |
| **AI/ML Engineer** | Month 2 | Agent development, fine-tuning |
| **Frontend Engineer** | Month 3 | HITL dashboard, customer UI |
| **DevOps/Platform** | Month 4 | Infrastructure, CI/CD |
| **Product Designer** | Month 4 | UX for complex workflows |

## 8.3 Funding Needs

| Use | Amount | Timeline |
|-----|--------|----------|
| Team (5 engineers, 12 months) | $750K | Year 1 |
| Infrastructure (cloud, APIs) | $100K | Year 1 |
| Tools & Services | $50K | Year 1 |
| Legal & Compliance | $50K | Year 1 |
| Buffer | $50K | Year 1 |
| **Total Seed** | **$1M** | 18-month runway |

---

# PART 9: RISKS & MITIGATIONS

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **AI costs exceed projections** | Medium | High | Self-hosted options, caching, smart routing |
| **Competitor copies methodology** | Low | Medium | Speed + compounding assets + execution |
| **Technical complexity** | High | High | Modular architecture, MVP focus |
| **Market timing** | Low | Medium | Multiple verticals as fallback |
| **Team execution** | Medium | High | Proven methodology reduces risk |
| **Regulatory changes** | Low | Medium | Compliance-first architecture |

---

# PART 10: THE ASK

## For Investors

- **Raise**: $1M Seed
- **Use**: 18 months to MVP launch + initial traction
- **Milestones**:
  - Month 6: Full MVP specs complete
  - Month 12: Private beta live
  - Month 15: 20 paying customers
  - Month 18: $50K MRR

## For Advisors

- Property management industry expertise
- AI/ML technical guidance
- GTM in proptech

## For Early Customers

- Design partner program
- Influence product direction
- Early access pricing

---

# APPENDIX A: Skill Registry Summary

| Category | Total Skills | P0 (MVP) | P1 | P2 | P3 |
|----------|--------------|----------|----|----|-----|
| Communication | 13 | 8 | 3 | 2 | 0 |
| Booking | 8 | 6 | 2 | 0 | 0 |
| Pricing | 8 | 5 | 2 | 1 | 0 |
| Operations | 12 | 8 | 3 | 1 | 0 |
| Financial | 14 | 9 | 4 | 1 | 0 |
| Channel | 6 | 5 | 1 | 0 | 0 |
| AI Workforce | 8 | 8 | 0 | 0 | 0 |
| Owner | 4 | 3 | 1 | 0 | 0 |
| Analytics | 4 | 2 | 2 | 0 | 0 |
| Other | 188 | 25 | 109 | 46 | 8 |
| **Total** | **265** | **79** | **127** | **51** | **8** |

---

# APPENDIX B: Completed Specifications

| Gap ID | Name | Skills | Status | Document |
|--------|------|--------|--------|----------|
| GAP-HOAI-001 | AI Workforce Architecture | 8 | ✅ Complete | `specs/ai-workforce/SPEC-SKILL-261-268.md` |
| GAP-AF-001 | AI Leasing Assistant | 1 | 🔄 Stage 3 | In progress |

---

# APPENDIX C: Key Documents

| Document | Location | Purpose |
|----------|----------|---------|
| STATUS.md | Root | Current state of pipeline |
| MASTER_SKILL_REGISTRY.md | registry/ | All 265 skills |
| MVP_PRIORITY_GAPS.md | docs/ | P0 gaps to close |
| PIPELINE_TRACKER.md | docs/ | Stage-by-stage progress |
| KNOWLEDGE_TO_SKILL_WORKFLOW.md | docs/ | Methodology documentation |
| AGENT_GUIDE.md | docs/ | Instructions for AI agents |
| OPEN_ITEMS_TRACKER.md | docs/ | Questions needing resolution |

---

**Document Version**: Draft 1.0
**Next Steps**: Incorporate founder's existing business plan → refine moat articulation → prepare pitch deck

