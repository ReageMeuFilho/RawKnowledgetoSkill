# HOAi - Skill Inventory

> **Source**: HOAi_Replication_PRD.md
> **Analysis Date**: January 2026
> **Focus**: AI Workforce Platform for HOA Management

---

## 🎯 **CRITICAL: HOAi = AI WORKFORCE PARADIGM SHIFT**

HOAi represents a fundamentally different approach from other competitors:

| Traditional AI | HOAi AI Workforce |
|----------------|-------------------|
| Single AI features | Specialized AI agents |
| Chatbots provide info | Agents PERFORM work |
| Human does the work | Human APPROVES the work |
| Feature add-on | Digital employee model |

This is the first **"AI-as-a-Service Workforce"** model in our registry.

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 25+ |
| **New Unique Skills** | 8 |
| **Overlapping with Registry** | 10+ |
| **Knowledge Gaps Identified** | 5 |
| **New Architectural Pattern** | AI Workforce Model |

---

## 🆕 Unique Skills (New to Registry)

### SKILL-261: ai-voice-agent-multichannel

**Priority**: P0
**Category**: ai-workforce

**Description**: 
24/7 AI voice agent handling inbound/outbound calls, SMS, web chat, and email with resident identification and action execution.

**Metrics**:
- Response time: <3 seconds
- Resolution rate: >70% without human
- CSAT: >4.5/5

**Channels**:
| Channel | Capability |
|---------|------------|
| Phone | Inbound + outbound calling |
| SMS | Two-way text messaging |
| Web Chat | Embeddable widget |
| Email | Ingestion + auto-response |

**Features**:
- **Natural Language Understanding** - Industry-specific terminology
- **Resident Identification** - Cross-reference PMS by phone/email
- **Contextual Conversation** - Maintain context across channels
- **Action Execution** - Submit requests, provide balances, send documents
- **Intelligent Escalation** - Transfer with transcript + summary

**Why Unique**: Combines phone, SMS, chat, email in single AI agent with action execution.

**Overlap**: Similar to Boom AI (voice) but with more channels and action execution.

---

### SKILL-262: ai-ap-agent

**Priority**: P0
**Category**: ai-workforce

**Description**: 
Full accounts payable automation from invoice receipt to payment processing.

**Metrics**:
- Processing time: >90% reduction
- Accuracy: >99% data extraction
- Cost: >75% reduction per invoice

**Features**:
- **Invoice Ingestion** - Email attachments, vendor portals
- **OCR + AI Extraction** - Vendor, invoice #, date, amount, line items
- **GL Coding** - Auto-code based on history + rules
- **Duplicate Detection** - Flag potential duplicates
- **Approval Routing** - Configurable workflows

**Why Unique**: End-to-end AP automation, not just OCR or approval.

**Overlap**: Similar to AppFolio Smart Bill Entry but more comprehensive.

---

### SKILL-263: ai-budget-agent

**Priority**: P1
**Category**: ai-workforce

**Description**: 
AI agent that automatically generates annual budgets with variance analysis and scenario modeling.

**Metrics**:
- Budget creation: >90% time reduction
- Accuracy: 100% adherence to rules

**Features**:
- **Data Aggregation** - Historical financials, contracts, reserve studies
- **Draft Generation** - Meeting-ready budget with pre-filled line items
- **Variance Analysis** - Flag significant variances with explanations
- **Scenario Modeling** - Real-time impact of different scenarios

**Why Unique**: No other competitor has full AI budget generation.

---

### SKILL-264: ai-research-agent

**Priority**: P1
**Category**: ai-workforce

**Description**: 
AI agent providing instant answers from governing documents with semantic search and source citation.

**Metrics**:
- Response time: <5 seconds
- Accuracy: >95% correct source

**Features**:
- **Document Ingestion** - PDF, Word, scanned images
- **Semantic Search** - Natural language questions, not just keywords
- **Source Citation** - Direct link + highlighted passage

**Why Unique**: RAG specifically optimized for HOA governing documents.

**Overlap**: Similar to Visito AI knowledge hub but specialized for HOA documents.

---

### SKILL-265: managerial-hub-hitl

**Priority**: P0
**Category**: ai-workflow

**Description**: 
Human-in-the-loop dashboard for reviewing, approving, and managing AI agent work.

**Features**:
- **Unified Task List** - Consolidated view of all agent work
- **One-Click Approval** - Fast approval workflow
- **Drill-Down Capability** - Full context and history
- **Feedback Mechanism** - Continuous model improvement
- **Customizable Workflows** - Configurable approval paths

**Why Critical**: This is THE control layer for AI workforce model.

**Architectural Pattern**:
```
AI Agent → Work Product → Managerial Hub → Human Review → Approval/Reject → Action
```

---

### SKILL-266: ai-scenario-modeling

**Priority**: P2
**Category**: analytics

**Description**: 
Real-time budget scenario modeling to see impact of different assumptions.

**Features**:
- Adjust variables (inflation, reserves, assessments)
- See real-time impact on budget
- Compare multiple scenarios
- Export scenarios for board presentation

**Why Valuable**: Board decisions often involve "what if" questions.

---

### SKILL-267: ai-outbound-calling

**Priority**: P1
**Category**: ai-voice

**Description**: 
AI agent capability to make proactive outbound calls (reminders, follow-ups).

**Use Cases**:
- Payment reminders
- Meeting notifications
- Request follow-ups
- Survey calls

**Why Unique**: Most AI voice is inbound-only; outbound is rare.

---

### SKILL-268: configurable-ai-coverage

**Priority**: P1
**Category**: ai-workflow

**Description**: 
Configure when AI agents are active (after-hours, overflow, full front line).

**Options**:
| Mode | Description |
|------|-------------|
| After Hours | AI handles nights/weekends only |
| Overflow | AI handles when humans busy |
| Full Front Line | AI handles all inquiries |

**Why Valuable**: Companies have different comfort levels with AI autonomy.

---

## 🔄 Overlapping Skills

HOAi validates and extends existing skills:

| Existing Skill | HOAi Enhancement |
|----------------|------------------|
| SKILL-248: violation-management | AI-assisted violation tracking |
| SKILL-247: architectural-review | AI Research Agent for rules lookup |
| SKILL-255: smart-bill-entry | Full AI AP Agent (more comprehensive) |
| SKILL-252: realm-x-ai-platform | Specialized AI Workforce model |
| Voice AI (Boom) | Multi-channel + action execution |
| RAG (Visito) | HOA document specialization |

---

## 🏗️ Architectural Pattern: AI Workforce Model

### Traditional AI Feature Model
```
User → AI Feature → Response
         ↓
      (limited actions)
```

### HOAi AI Workforce Model
```
User → AI Agent → Work Product → Human Review → Approval → Action Execution
              ↓                        ↓
         Autonomous            Human-in-the-Loop
         task completion       quality control
```

### Key Differences

| Aspect | Traditional | HOAi Workforce |
|--------|-------------|----------------|
| **Scope** | Single feature | Full workflow |
| **Output** | Information | Completed work |
| **Human role** | Operator | Supervisor |
| **Scaling** | Per feature | Per "employee" |
| **Pricing** | Feature cost | "Headcount" cost |

---

## 📊 Positioning Analysis

### HOAi vs AppFolio HOA

| Dimension | HOAi | AppFolio |
|-----------|------|----------|
| **Focus** | AI automation layer | Full PMS platform |
| **Position** | Overlay on existing PMS | Replacement PMS |
| **AI Depth** | 4 specialized agents | Realm-X (general) |
| **Target** | HOA management companies | All PM companies |
| **Integration** | Works with any PMS | Native only |

### HOAi's Unique Value

1. **Integration-first** - Doesn't replace existing systems
2. **Workforce model** - AI as "digital employees"
3. **Deep specialization** - HOA-only focus
4. **Human-in-the-loop** - Built-in approval workflows
5. **Multi-PMS** - Works with Vantaca, CINC, AppFolio, Yardi

---

## 🎯 Strategic Implications

### What HOAi Teaches Us

1. **AI as workforce** - Different pricing/positioning than features
2. **Integration > replacement** - Don't force system changes
3. **Human oversight essential** - Trust requires approval workflows
4. **Vertical depth** - HOA-specific agents outperform general AI
5. **Multi-channel voice** - Phone + SMS + chat + email unified

### Our Competitive Response

| HOAi Strength | Our Response |
|---------------|--------------|
| AI Workforce Model | Consider for our STR/LTR verticals |
| Integration-first | Already strong integration approach |
| Human-in-the-loop | Add approval dashboard for AI work |
| HOA specialization | Focus on STR/LTR specialization |

---

## 📈 Impact on Registry

### New Architectural Concept
- **AI Workforce Model** - First example in registry
- **Human-in-the-Loop Dashboard** - Explicit approval layer
- **Configurable AI Coverage** - Autonomy control

### Category Enhancement
- **ai-workforce** - New category for specialized agents
- **ai-workflow** - Control and approval patterns
- **ai-voice** - Enhanced with outbound calling

---

## Next Steps

1. **Evaluate workforce model** for our platform
2. **Design HITL dashboard** for AI agent work
3. **Consider multi-channel voice** integration
4. **Research AP automation** architecture
5. **Budget generation AI** feasibility study

