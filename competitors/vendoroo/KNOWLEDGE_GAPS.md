# Vendoroo - Knowledge Gaps

> **Source**: vendoroo_prd_founder_extended.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 11

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 5 | Agent design, emergency, orchestration |
| **P1 - Important** | 4 | Vendor, invoice, policy |
| **P2 - Nice-to-have** | 2 | Reporting, analytics |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-VDR-001: Multi-Agent Boundary Design

**Skill**: SKILL-157 (specialized-maintenance-agents)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Agent Input/Output Contracts**
   - What exact data does each Roo receive?
   - What exact outputs does each produce?
   - How is data passed between agents?

2. **Hard Constraint Definition**
   - How are "cannot" rules enforced?
   - What happens when an agent attempts forbidden action?
   - How are constraints configured per account?

3. **Failure Mode Handling**
   - What are fallbacks when agent fails?
   - How is human handoff triggered?
   - What logging occurs on failure?

**Ideal Source**:
- [ ] AI agent architecture design documents
- [ ] Multi-agent orchestration patterns
- [ ] Expert interviews with Vendoroo engineers

---

### GAP-VDR-002: Emergency Classification Algorithm

**Skill**: SKILL-159 (emergency-classification-engine)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Classification Logic**
   - What signals indicate "emergency" vs "urgent" vs "routine"?
   - How is "no heat in winter" weighted vs "no AC in summer"?
   - What tenant statements trigger immediate classification?

2. **False Negative Prevention**
   - How is <0.5% false negative achieved?
   - What conservative biases are built in?
   - How are edge cases handled?

3. **After-Hours Rules**
   - What changes at 5pm vs 2am?
   - How are weekends/holidays handled?
   - What issues become "emergency" after-hours that aren't during business hours?

**Ideal Source**:
- [ ] Property management emergency protocols
- [ ] Insurance/liability requirements for property managers
- [ ] Maintenance coordinator interviews

---

### GAP-VDR-003: Maintenance Brain Data Model

**Skill**: SKILL-158 (maintenance-brain-memory)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **MaintenanceBookEntry Structure**
   - What data is stored per property/unit/system?
   - How are recurring issues identified?
   - What triggers a "recommendation"?

2. **Learning Mechanism**
   - How does the "brain" improve over time?
   - What feedback loops exist?
   - How is bad data corrected?

3. **Query Patterns**
   - When does Triage Roo consult MaintenanceBook?
   - What patterns trigger alerts?
   - How is historical data weighted?

**Ideal Source**:
- [ ] Property maintenance history databases
- [ ] HVAC/plumbing system lifecycle data
- [ ] Experienced maintenance coordinator knowledge

---

### GAP-VDR-004: Work Order State Machine Design

**Skill**: SKILL-165 (work-order-state-machine)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **State Transition Rules**
   - What conditions allow `triaged → awaiting_approval`?
   - When can states be skipped?
   - What triggers automatic vs manual transitions?

2. **Idempotency Implementation**
   - How are duplicate requests handled?
   - What makes operations safe to retry?
   - How is state consistency maintained?

3. **Pause/Resume Logic**
   - What does "pause automation" actually stop?
   - How is state preserved during pause?
   - What triggers resume?

**Ideal Source**:
- [ ] State machine design patterns
- [ ] Workflow orchestration documentation (Temporal, etc.)
- [ ] Property management software architecture

---

### GAP-VDR-005: Remote Troubleshooting Scripts

**Skill**: SKILL-161 (remote-troubleshooting-flows)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Category-Specific Scripts**
   - What questions for "toilet won't flush"?
   - What questions for "no hot water"?
   - What questions for "electrical outlet not working"?

2. **Resolution Criteria**
   - How does agent know issue is resolved?
   - When is "monitor" status appropriate?
   - What callback triggers exist?

3. **Safety Boundaries**
   - What issues should NEVER be troubleshooted remotely?
   - What tenant instructions are appropriate?
   - When must dispatch be immediate?

**Ideal Source**:
- [ ] Maintenance technician troubleshooting guides
- [ ] Property management SOPs
- [ ] HVAC/plumbing trade documentation

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-VDR-006: Vendor Scoring Algorithm

**Skill**: SKILL-160 (vendor-intelligence-ranking)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Metric Calculation**
   - How is `on_time_rate` defined (within 15min? 1hr?)?
   - How is `rework_rate` calculated?
   - What is `reliability_score` formula?

2. **Tier Thresholds**
   - What metrics qualify for Gold vs Silver vs Bronze?
   - How often are tiers recalculated?
   - Can vendors be promoted/demoted automatically?

3. **Assignment Algorithm**
   - How are matching vendors ranked?
   - Is it cost vs quality optimization?
   - How is emergency capability weighted?

**Ideal Source**:
- [ ] Property management vendor evaluation criteria
- [ ] Service provider SLA documentation
- [ ] Vendor marketplace best practices

---

### GAP-VDR-007: Invoice Validation Rules

**Skill**: SKILL-162 (invoice-validation-ai)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Compliance Checks**
   - What line items are expected per job type?
   - What are "standard rates" per vendor type/region?
   - What triggers "flagged" vs "rejected"?

2. **Fraud Detection Signals**
   - What patterns indicate potential fraud?
   - How is "duplicate invoice" detected?
   - What historical comparisons are made?

3. **Approval Thresholds**
   - What amounts auto-approve?
   - What requires human review?
   - How are thresholds configured per account?

**Ideal Source**:
- [ ] Property management accounting procedures
- [ ] Invoice fraud detection literature
- [ ] AP automation best practices

---

### GAP-VDR-008: Policy Engine Condition Syntax

**Skill**: SKILL-163 (maintenance-policy-engine)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Condition Expression Format**
   - What JSON/YAML syntax is used?
   - What operators are supported (=, >, <, AND, OR)?
   - What variables can be referenced?

2. **Action Types**
   - What does `auto_approve` actually do?
   - What does `auto_escalate` trigger?
   - How is `vendor_preference` applied?

3. **Simulation Engine**
   - How does "show me how this rule would change decisions" work?
   - What historical data is used?
   - How is impact quantified?

**Ideal Source**:
- [ ] Rules engine design patterns
- [ ] Business rules management systems (Drools, etc.)
- [ ] Property management policy documentation

---

### GAP-VDR-009: Preventive Maintenance Scheduling

**Skill**: SKILL-164 (preventive-maintenance-campaigns)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Schedule Definition**
   - What scheduling syntax is supported?
   - How are seasonal adjustments handled?
   - What about property-specific exceptions?

2. **Batch Assignment Logic**
   - How are multiple properties grouped?
   - How is vendor capacity considered?
   - What optimization is applied?

**Ideal Source**:
- [ ] Property maintenance schedules
- [ ] HVAC service intervals
- [ ] Building maintenance standards

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-VDR-010: Owner Reporting Templates

**Skill**: SKILL-166 (owner-cost-defensibility)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Report Sections**
   - What does "executive summary" include?
   - What breakdowns are expected?
   - What commentary is generated?

**Ideal Source**:
- [ ] Property management owner report examples
- [ ] Asset management reporting standards

---

### GAP-VDR-011: Maintenance Analytics Patterns

**Skill**: SKILL-158 (maintenance-brain-memory)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Pattern Detection**
   - What makes an issue "recurring"?
   - How is forecasting done?
   - What budget predictions are generated?

**Ideal Source**:
- [ ] Property management analytics dashboards
- [ ] Predictive maintenance literature

---

## 📋 Knowledge Collection Plan

### Phase 1: Agent & Orchestration (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-VDR-001 | Multi-agent architecture docs + AI design patterns | TBD |
| GAP-VDR-004 | State machine patterns + workflow orchestration | TBD |
| GAP-VDR-005 | Maintenance technician SOPs + trade guides | TBD |

### Phase 2: Classification & Intelligence (Week 3-4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-VDR-002 | PM emergency protocols + coordinator interviews | TBD |
| GAP-VDR-003 | Property history data + lifecycle documentation | TBD |
| GAP-VDR-006 | Vendor SLA documentation + marketplace research | TBD |

### Phase 3: Financial & Policy (Week 5-6)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-VDR-007 | AP automation best practices + fraud detection | TBD |
| GAP-VDR-008 | Rules engine patterns + policy documentation | TBD |
| GAP-VDR-009 | Building maintenance standards | TBD |

### Phase 4: Reporting (Week 7)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-VDR-010 | Owner report examples | TBD |
| GAP-VDR-011 | Predictive maintenance literature | TBD |

---

## 🎯 Impact Assessment

Vendoroo gaps are **operationally deep** - requiring domain expertise:

| Gap Type | Expertise Needed | Difficulty |
|----------|------------------|------------|
| Agent Design | AI/ML Engineering | High |
| Emergency Logic | Property Management | Medium |
| Troubleshooting | Trade Knowledge | Medium |
| Vendor Scoring | Operations | Medium |
| Policy Engine | Software Architecture | Medium |

### Recommendation
Vendoroo knowledge requires **property management operations expertise** combined with **AI architecture skills**. Consider:

1. Partnering with experienced property managers for domain knowledge
2. Reviewing open-source workflow orchestration (Temporal, Airflow) for state machine patterns
3. Consulting HVAC/plumbing trade documentation for troubleshooting scripts
4. Analyzing existing vendor marketplace platforms for scoring algorithms

---

## 🔑 Key Insight

Vendoroo is the **only competitor that could be a strategic acquisition target** for maintenance depth. If we don't capture this knowledge ourselves, acquiring Vendoroo's approach (or partnering) could accelerate maintenance module development significantly.




