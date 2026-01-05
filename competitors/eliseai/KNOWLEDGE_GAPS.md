# EliseAI - Knowledge Gaps

> **Source**: eliseai_prd_founder_v2_extended.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 10

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 5 | Core modules, compliance |
| **P1 - Important** | 3 | Operations, training |
| **P2 - Nice-to-have** | 2 | Analytics, optimization |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-EAI-001: Purpose-Built CRM Architecture

**Skill**: SKILL-168 (purpose-built-housing-crm)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **CRM vs PMS Boundary**
   - What data lives in EliseCRM vs PMS?
   - How is bi-directional sync managed?
   - What is "system-of-engagement" vs "system-of-record"?

2. **Unified Inbox Design**
   - How are conversations threaded across channels?
   - How are duplicates detected (same person, different channels)?
   - How is conversation assignment handled?

3. **Multi-Portfolio Structure**
   - How is role-based access implemented?
   - How do central teams vs on-site differ?
   - How are cross-portfolio reports generated?

**Ideal Source**:
- [ ] CRM architecture best practices
- [ ] Multifamily software vendor documentation
- [ ] Enterprise PM software consultant

---

### GAP-EAI-002: Leasing Funnel Automation

**Skill**: SKILL-169 (leasing-ai-full-funnel)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Lead Qualification Flow**
   - What questions qualify/disqualify a lead?
   - What income/credit thresholds are checked?
   - How is affordability calculated?

2. **Tour Scheduling Logic**
   - How are available slots generated?
   - What is AI-guided self-tour flow?
   - How are no-shows handled?

3. **Lead Nurturing Campaigns**
   - What cadence? (Day 1, Day 3, Day 7...?)
   - What content at each stage?
   - When does AI give up?

**Ideal Source**:
- [ ] Leasing agent interviews
- [ ] Multifamily lead nurturing best practices
- [ ] Tour conversion analytics

---

### GAP-EAI-003: Delinquency Communication Scripts

**Skill**: SKILL-171 (delinquency-empathy-automation)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Reminder Cadence**
   - Day before due? Day of? Day after?
   - How many reminders before escalation?
   - What time of day?

2. **Empathetic Messaging**
   - What phrases protect relationships?
   - How is hardship acknowledged?
   - What payment plan options are offered?

3. **Promises-to-Pay Capture**
   - What counts as a valid promise?
   - How is promise tracked?
   - What happens when promise is broken?

**Ideal Source**:
- [ ] Property management collections procedures
- [ ] Empathetic communications training
- [ ] Fair debt collection guidelines

---

### GAP-EAI-004: Fair Housing Compliance Rules

**Skill**: SKILL-173 (fair-housing-compliance-ai)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Protected Classes**
   - Full list of protected categories
   - How is each enforced in conversations?
   - What phrases are forbidden?

2. **Equal Treatment**
   - How is "steering" prevented?
   - How are unit recommendations validated?
   - What audit trails are required?

3. **Phrasing Templates**
   - Compliant ways to discuss income requirements
   - Compliant ways to describe neighborhoods
   - Compliant ways to answer family questions

**Ideal Source**:
- [ ] Fair Housing Act documentation
- [ ] HUD guidance on AI in housing
- [ ] Fair housing attorney consultation

---

### GAP-EAI-005: AI-Human Collaboration Handoff

**Skill**: SKILL-176 (ai-human-realtime-collaboration)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Handoff Triggers**
   - What signals AI should hand off?
   - How is complexity measured?
   - What sentiment triggers handoff?

2. **Seamless Transition**
   - How does resident not notice handoff?
   - What context is passed to human?
   - How is conversation resumed?

3. **Override Mechanism**
   - How do humans override AI decisions?
   - What approvals are needed?
   - How is override logged?

**Ideal Source**:
- [ ] AI handoff design patterns
- [ ] Customer service escalation procedures
- [ ] Conversational AI best practices

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-EAI-006: Maintenance App Auto-Assignment

**Skill**: SKILL-172 (maintenance-technician-app)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Assignment Algorithm**
   - How are skills matched to job types?
   - How is location factored in?
   - What about workload balancing?

2. **Skill Levels**
   - What skill categories exist?
   - How are levels determined?
   - How is certification tracked?

**Ideal Source**:
- [ ] Field service management software
- [ ] Maintenance supervisor interviews
- [ ] Technician skill matrix examples

---

### GAP-EAI-007: 30M Conversation Training Data

**Skill**: SKILL-174 (30m-conversation-training)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Training Categories**
   - How are conversations categorized?
   - What intent taxonomy is used?
   - How are edge cases handled?

2. **Data Collection**
   - How is conversation data collected?
   - What consent is obtained?
   - How is PII handled?

**Ideal Source**:
- [ ] NLP training data best practices
- [ ] Housing conversation datasets
- [ ] Intent classification taxonomies

---

### GAP-EAI-008: Centralized Operations Structure

**Skill**: SKILL-175 (centralized-operations-model)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Role Definitions**
   - What roles exist (central leasing, on-site, etc.)?
   - What permissions per role?
   - How is hierarchy managed?

2. **Workflow Standardization**
   - How are workflows templated?
   - What is configurable per property?
   - How are exceptions handled?

**Ideal Source**:
- [ ] Enterprise property management org charts
- [ ] Centralized leasing model documentation
- [ ] Multi-property management guides

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-EAI-009: KPI Dashboard Design

**Skill**: SKILL-168 (purpose-built-housing-crm)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Leasing KPIs**
   - Lead-to-lease conversion formula
   - Tour-to-lease conversion
   - Occupancy calculation

2. **Maintenance KPIs**
   - Time-to-first-response
   - Time-to-completion
   - Rework rate

**Ideal Source**:
- [ ] Property management KPI benchmarks
- [ ] Industry analytics reports

---

### GAP-EAI-010: Renewal Pricing Logic

**Skill**: SKILL-170 (resident-lifecycle-ai)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Renewal Offer Generation**
   - How is renewal price calculated?
   - What market factors are considered?
   - What terms are offered (6mo, 12mo, MTM)?

**Ideal Source**:
- [ ] Renewal pricing strategies
- [ ] Market rent analysis tools

---

## 📋 Knowledge Collection Plan

### Phase 1: Compliance & Core (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-EAI-004 | Fair housing attorney + HUD docs | TBD |
| GAP-EAI-001 | CRM architecture research | TBD |
| GAP-EAI-005 | Conversational AI patterns | TBD |

### Phase 2: Leasing & Collections (Week 3-4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-EAI-002 | Leasing agent interviews | TBD |
| GAP-EAI-003 | Collections best practices | TBD |

### Phase 3: Operations (Week 5-6)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-EAI-006 | Field service software research | TBD |
| GAP-EAI-007 | NLP training best practices | TBD |
| GAP-EAI-008 | Enterprise PM org research | TBD |

### Phase 4: Analytics (Week 7)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-EAI-009 | Industry benchmarks | TBD |
| GAP-EAI-010 | Pricing strategy research | TBD |

---

## 🎯 Impact Assessment

EliseAI gaps are **business-critical** - these represent the features that made them market leader:

| Gap Type | Expertise Needed | Difficulty |
|----------|------------------|------------|
| CRM Architecture | Software Architecture | High |
| Leasing Funnel | Leasing Operations | Medium |
| Delinquency | Collections + Empathy | Medium |
| Fair Housing | Legal + Compliance | High |
| AI-Human Handoff | AI/UX Engineering | High |

### Critical Insight

EliseAI's **fair housing compliance** (GAP-EAI-004) is a regulatory requirement that could expose us to legal risk if not implemented correctly. This should be prioritized and potentially require legal review.

---

## 🏆 Competitive Strategy

### What We CAN Match
- CRM Hub → Kortix/Suna base
- Leasing Funnel → Skill composition
- Maintenance App → Custom MCP server
- Voice AI → Integration with telephony

### What We CAN'T Match (Yet)
- 30M conversation training data → Start collecting now
- 60% top 50 market share → Different GTM (STR, international)
- 10+ years domain expertise → Hire/partner

### Where We CAN WIN
- STR market (EliseAI = LTR only)
- International (WhatsApp, multi-language)
- Open source transparency
- Unified platform (not just housing)
- Better pricing intelligence (PriceLabs-level)

