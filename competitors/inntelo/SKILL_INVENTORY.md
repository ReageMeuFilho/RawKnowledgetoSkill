# Inntelo AI Platform - Skill Inventory

> **Source**: `inntelo_ai_platform_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: AI-Native Hospitality Platform (Hotels 50-500 rooms)
> **Type**: Full-Stack Operations + CDP

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 42 | 9 NEW, 33 overlap (with DEPTH) |
| Tools | 8 | 2 NEW |
| Memory Types | 8 | 3 NEW |
| Workflows | 10 | 4 NEW |

---

## 🎯 Inntelo AI Context

**Inntelo is an "AI-Native Operating Platform"** for hotels with:
- **97% guest interaction capture** (highest rate)
- **40+ languages** natively supported (most comprehensive)
- **30-40% upsell conversion** (highest I've seen)
- **60%+ front desk burden reduction**
- **Multi-Agent Architecture** (5 specialized agents)
- **Radisson, Wyndham, The First Group** partnerships

**Target**: Independent hotels (50-500 rooms), boutique properties, branded residences

**Key Differentiator**: 
- **Inntelo** = Hotels (50+ rooms, traditional hospitality)
- **Boom** = STR/Aparthotels (vacation rentals)
- **Guesty** = STR operators (Airbnb/VRBO focus)

---

## 🆕 NEW Skills (Not in Previous PRDs)

### NEW-INN-001: AI Customer Data Platform (CDP)
**Category**: data
**Priority**: P1
**Status**: NEEDED

**Description**: 
Unified first-party guest data foundation with predictive analytics.

**Unique Capabilities**:
- Customer identity resolution (single guest across properties/systems)
- Deduplication and data normalization
- Real-time event streaming (every interaction updates profile)
- Lifetime value tracking
- Churn prediction
- Price sensitivity analysis
- Retention segmentation (high-value, at-risk, growth)
- GDPR/CCPA compliance built-in

**Data Sources Unified**:
- PMS (reservations, payments)
- AI Concierge (interactions, preferences)
- Housekeeping (services requested)
- Payment Platform (transactions)
- Email/SMS (communications)
- Website (browsing behavior)
- Third-party (loyalty programs)

**Knowledge Required**:
- KG-INN-001: CDP architecture patterns

---

### NEW-INN-002: Multi-Agent Architecture
**Category**: agentic
**Priority**: P0
**Status**: NEEDED

**Description**: 
Explicit 5-agent system where specialized agents coordinate on complex tasks.

**Agent Types**:
1. **Guest Communication Agent** - All guest interactions
2. **Task Execution Agent** - Converts requests to coordinated actions
3. **Operations Planning Agent** - Housekeeping/maintenance scheduling
4. **Revenue Optimization Agent** - Upsells and personalization
5. **Escalation Agent** - Routes complex issues to humans

**Agent-to-Agent Communication**:
- Shared understanding of hotel state
- Coordinated decision-making without human intervention
- Clean handoff protocols
- No dropped context between agents

**Knowledge Required**:
- KG-INN-002: Multi-agent coordination patterns

---

### NEW-INN-003: Cross-Department Workflow Orchestration
**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Guest requests flow seamlessly across departments with coordinated timing.

**Example Flow** ("Shower isn't draining"):
1. Concierge captures issue, acknowledges "15 mins"
2. Maintenance receives work order
3. Plumber arrives, fixes issue
4. Housekeeping receives "bathroom deep clean needed"
5. Housekeeping completes
6. Concierge notifies guest "Fixed!"

**Unique Capabilities**:
- Single status update (guest notified once ALL parts complete)
- Coordinated timing (housekeeping waits for maintenance)
- Shared context across departments
- Real-time priority adjustment

---

### NEW-INN-004: Predictive Housekeeping
**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
AI anticipates room needs before requests are made.

**Unique Capabilities**:
- Anticipate needs based on guest profile + length of stay
- Schedule deep cleans at optimal times (guest at breakfast)
- Predict linen needs from occupancy patterns
- Optimize cleaning sequences to minimize walking
- Pre-allocate resources for predicted occupancy
- Dynamic re-prioritization if guest checks in early

---

### NEW-INN-005: 40+ Language Native Support
**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive multilingual support with context-aware translation.

**Unique Capabilities**:
- 40+ languages (vs. Boom's 5+)
- Dialect awareness (different English accents/spellings)
- Context translation (intent, not just words)
- Slang and colloquialism understanding
- Domain-specific hospitality terminology

---

### NEW-INN-006: Churn Prediction & Retention
**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI identifies at-risk guests and triggers retention interventions.

**Unique Capabilities**:
- Churn score per guest
- Retention intervention triggers
- Win-back campaigns for lapsed guests
- Loyalty tier conversion recommendations
- LTV optimization (where to invest in retention)

---

### NEW-INN-007: Predictive Maintenance Advanced
**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI predicts equipment failures before they impact guests.

**Unique Capabilities**:
- MTBF (Mean Time Between Failures) tracking
- MTTR (Mean Time To Repair) analytics
- Predictive failure detection
- Equipment lifecycle analysis (repair vs replace)
- Warranty tracking
- Seasonal planning (AC servicing, heating checks)

---

### NEW-INN-008: Intent Recognition System
**Category**: ai-control
**Priority**: P0
**Status**: NEEDED

**Description**: 
50+ hospitality intents with 95% accuracy target.

**Intent Categories**:
- Service requests ("My WiFi is slow")
- Amenity requests ("Extra pillows")
- Concierge services ("Book restaurant")
- Facility questions ("Where's the gym")
- Room issues ("Toilet running")
- F&B orders ("Room service")

**Unique Capabilities**:
- Emotion detection (frustration, urgency, satisfaction)
- Ambiguity handling (clarifying questions)
- Sarcasm detection
- Confidence threshold with escalation

---

### NEW-INN-009: Proactive Issue Detection
**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI detects issues from patterns and proactively offers help.

**Example**: "We noticed you struggled with WiFi yesterday. Can we help?"

**Unique Capabilities**:
- Pattern detection across interactions
- Proactive outreach for recurring issues
- Pre-emptive problem resolution
- Guest satisfaction protection

---

## 🔄 Skills Overlapping with Other PRDs

### Feature Comparison Matrix

| Feature | Inntelo | Boom | Besty | Guesty | Winner |
|---------|---------|------|-------|--------|--------|
| **Languages** | 40+ | 5+ | 5+ | 10+ | **Inntelo** |
| **AI Capture Rate** | 97% | 75% | 75% | N/A | **Inntelo** |
| **Upsell Conversion** | 30-40% | N/A | 15-20% | N/A | **Inntelo** |
| **Multi-Agent** | 5 agents | BAM | No | No | **Inntelo** |
| **Voice AI** | Phone LLM | Full | No | No | Boom |
| **CDP** | Full | Basic | No | Basic | **Inntelo** |
| **Operations** | Full | Basic | No | Full | Tie |
| **Revenue Upsells** | 30-40% | Basic | Full | Basic | Tie |
| **Target** | Hotels | STR | STR | STR | - |

### Where Inntelo Excels

1. **CDP** - Most comprehensive guest data unification
2. **Multi-Agent** - Explicit agent specialization
3. **Languages** - 40+ vs others' 5-10
4. **Cross-Department** - Seamless workflow orchestration
5. **Upsell Conversion** - 30-40% (highest)

### Where Others Excel

1. **Boom** - Voice AI (24/7 phone)
2. **Besty** - Revenue psychology (gap nights, winback)
3. **Guesty** - STR operations depth (67 skills)
4. **Mews** - Digital key, Apple Wallet

---

## 📊 Multi-Agent Architecture Deep Dive

**Traditional AI**: Single model handles everything

**Inntelo Multi-Agent**:
```
┌─────────────────────────────────────────────────────────────┐
│                    ORCHESTRATOR                              │
├─────────┬─────────┬─────────┬─────────┬─────────────────────┤
│ Guest   │ Task    │ Ops     │ Revenue │ Escalation          │
│ Comms   │ Exec    │ Planning│ Optim   │ Agent               │
│ Agent   │ Agent   │ Agent   │ Agent   │                     │
├─────────┴─────────┴─────────┴─────────┴─────────────────────┤
│                    SHARED STATE                              │
│  (hotel context, guest profiles, task queues)               │
└─────────────────────────────────────────────────────────────┘
```

**Benefits**:
- Specialized expertise per agent
- Parallel processing
- Clean handoffs
- Easier testing/debugging
- Scalable complexity

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-INN-001 | resolve_guest_identity | Match guest across systems | BUILD |
| TOOL-INN-002 | calculate_churn_score | Predict guest churn risk | BUILD |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-INN-001 | CDP Profile | Unified guest data across all sources | Permanent |
| MEM-INN-002 | Lifetime Value | Running LTV calculation | Permanent |
| MEM-INN-003 | Churn Risk | Real-time churn score | Updated daily |

---

## 🔀 NEW Workflows from Inntelo

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-INN-001 | Cross-Dept Orchestration | Guest request | Parse → Route → Coordinate → Complete → Notify |
| WF-INN-002 | Predictive Housekeeping | Guest profile | Analyze → Predict → Schedule → Execute |
| WF-INN-003 | Churn Intervention | High churn score | Detect → Segment → Offer → Track |
| WF-INN-004 | Identity Resolution | New interaction | Match → Merge → Enrich → Store |

---

## 📋 Knowledge Gaps from Inntelo

| ID | Knowledge Needed | Skills Blocked | Priority |
|----|------------------|----------------|----------|
| KG-INN-001 | CDP architecture patterns | CDP Skill | HIGH |
| KG-INN-002 | Multi-agent coordination | Multi-Agent | HIGH |
| KG-INN-003 | Identity resolution algorithms | Guest Matching | MEDIUM |
| KG-INN-004 | Churn prediction models | Retention | MEDIUM |
| KG-INN-005 | Equipment failure prediction | Predictive Maint | LOW |

---

## 🏆 What Inntelo Adds to Our Solution

**ADOPT (Critical)**:
1. **CDP** - Unified guest data is foundation for personalization
2. **Multi-Agent Architecture** - Better than single-agent for complex operations
3. **Cross-Department Orchestration** - Seamless guest experience
4. **40+ Languages** - Global reach

**ADOPT (Valuable)**:
1. **Predictive Housekeeping** - Proactive vs reactive
2. **Churn Prediction** - Retention ROI
3. **Intent Recognition** - 95% accuracy target
4. **Proactive Issue Detection** - Prevent problems

**CONSIDER**:
1. **Hotel-specific features** - May not apply to STR

---

## 📊 Strategic Positioning Update

| Dimension | Inntelo | Boom | Besty | Guesty | Mews |
|-----------|---------|------|-------|--------|------|
| **Type** | Hotel AI | AiPMS | AI Layer | STR PMS | Hotel PMS |
| **CDP** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ❌ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Multi-Agent** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ❌ | ❌ | ❌ |
| **Languages** | ⭐⭐⭐⭐⭐ (40+) | ⭐⭐⭐ (5+) | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Upsells** | ⭐⭐⭐⭐⭐ (40%) | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Voice AI** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ❌ | ❌ | ❌ |
| **Operations** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Target** | Hotels | STR | STR | STR | Hotels |

**Bottom Line**: Inntelo provides **CDP**, **Multi-Agent**, and **Cross-Department Orchestration** patterns that no other competitor matches. Essential for enterprise-grade deployments.

---

## 🎯 Complete Best-of-Breed Synthesis (6 Competitors)

| Feature | Best Source | Why |
|---------|-------------|-----|
| **STR Operations** | Guesty | 67 skills, comprehensive |
| **Voice AI** | Boom | 24/7 phone, 5+ languages |
| **Agentic Architecture** | Boom + Inntelo | BAM + Multi-Agent |
| **Revenue Upsells** | Besty | Psychology, 40-60% gap fill |
| **CDP** | **Inntelo** | Full stack, identity resolution |
| **Multi-Agent** | **Inntelo** | 5 specialized agents |
| **Cross-Dept** | **Inntelo** | Seamless orchestration |
| **Languages** | **Inntelo** | 40+ native |
| **Churn Prediction** | **Inntelo** | Full retention AI |
| **Digital Key** | Mews | Apple Wallet, BLE |
| **Booking Engine** | Mews | A/B testing |
| **Analytics** | Mews | GOPPAR |

