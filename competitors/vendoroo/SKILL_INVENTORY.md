# Vendoroo - Skill Inventory

> **Source**: vendoroo_prd_founder_extended.md
> **Analysis Date**: January 2026
> **Focus**: AI-Powered Maintenance Coordination Platform

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 45 |
| **New Unique Skills** | 11 |
| **Overlapping with Registry** | 34 |
| **Knowledge Gaps Identified** | 11 |

---

## 🎯 **Critical Insight**

Vendoroo is the **ONLY** competitor that treats maintenance as a **complete, specialized vertical** with dedicated AI agents. While other PRDs (Guesty, RentalReady, Boom) include maintenance features, Vendoroo goes **10x deeper** with:

- **5 specialized AI agents** (not general chatbots)
- **"Maintenance Brain" memory** per property/unit/system
- **80%+ autonomous handling** target
- **<0.5% emergency misclassification** requirement
- **Financial defensibility** as first-class objective

This PRD is **essential knowledge** for any maintenance-related skill.

---

## 🆕 Unique Skills (New to Registry)

### 1. SKILL-157: specialized-maintenance-agents

**Priority**: P0
**Description**: Role-based AI agent architecture with 5 specialized "Roos"

**Agent Types**:
| Agent | Role | Constraints |
|-------|------|-------------|
| **Receptionist Roo** | Intake, identity verification | Cannot promise times/costs |
| **Triage & Troubleshooting Roo** | Classification, urgency, safety | Cannot downgrade emergencies |
| **Coordinator Roo** | Vendor selection, scheduling | Cannot exceed budget w/o approval |
| **Invoice & Compliance Roo** | Validation, fraud detection | Cannot auto-approve above threshold |
| **Assistant Roo** | Natural language queries | Read-only, cannot mutate |

**Key Differentiator**: Each agent has explicit inputs, outputs, constraints, and failure modes defined.

---

### 2. SKILL-158: maintenance-brain-memory

**Priority**: P0
**Description**: Persistent per-property/unit maintenance knowledge base

**Components**:
- `MaintenanceBookEntry` per property/unit/system
- Asset info: model, age, warranty_expiry
- Recurring issues and patterns
- Recommendations and last service date
- Preferred vendor per system type

**Key Differentiator**: Unlike other PRDs that just log requests, this creates a **learning system** that improves decisions over time.

---

### 3. SKILL-159: emergency-classification-engine

**Priority**: P0
**Description**: High-accuracy emergency detection with <0.5% false negative rate

**Features**:
- Conservative classification (err toward emergency)
- After-hours stricter mapping
- Safety-first triage with tenant instructions
- Auditable logic trail
- Post-incident review workflow

**Key Differentiator**: Most competitors just have "urgent/not urgent" - this has a **measurable accuracy target** with safety fallbacks.

---

### 4. SKILL-160: vendor-intelligence-ranking

**Priority**: P0
**Description**: Multi-factor vendor scoring and tiered assignment

**Performance Metrics**:
- jobs_completed
- on_time_rate
- avg_rating (tenant feedback)
- rework_rate
- reliability_score (composite)

**Assignment Logic**:
- Tier system: Bronze → Silver → Gold
- Service area matching (postal codes, cities)
- Emergency-capable flag
- After-hours multiplier pricing
- Do-not-use list enforcement

**Key Differentiator**: Other PRDs have basic vendor assignment; this has **data-driven vendor intelligence**.

---

### 5. SKILL-161: remote-troubleshooting-flows

**Priority**: P1
**Description**: Category-specific guided troubleshooting before dispatch

**Flow**:
1. Classify issue category
2. Check MaintenanceBook for historical patterns
3. Run category-specific troubleshooting script
4. If resolved: log steps, mark "monitor"
5. If unresolved: proceed to dispatch

**Categories**: HVAC, plumbing, electrical, appliance, structural, pest, etc.

**Key Differentiator**: Goal is to **resolve without dispatch** when safe and appropriate.

---

### 6. SKILL-162: invoice-validation-ai

**Priority**: P1
**Description**: Automated invoice compliance checking against policy and history

**Validation Checks**:
- Line items match WorkOrder scope
- Rates within standard for vendor
- Parts/labor reasonable for job type
- Historical pattern comparison
- Policy threshold compliance

**Outputs**:
- `auto_approved` if clean
- `flagged` with explanation if issues
- Accounting export record
- AuditLog entry

**Key Differentiator**: Other PRDs mention invoice processing; this has **AI-driven compliance checking**.

---

### 7. SKILL-163: maintenance-policy-engine

**Priority**: P0
**Description**: Granular, scope-based policy rules with simulation

**Rule Types**:
- Budget thresholds
- Escalation rules
- Safety requirements
- Communication preferences

**Scope Levels**:
- Account-wide (company default)
- Property-level override
- Unit-level exception

**Simulation Mode**: "Show me how this rule would change decisions" - test rules before enabling.

**Key Differentiator**: The **simulation mode** is unique - test policy impact before going live.

---

### 8. SKILL-164: preventive-maintenance-campaigns

**Priority**: P1
**Description**: Rule-based scheduled maintenance with batch vendor assignment

**Features**:
- Rule definition: "HVAC inspection every 6 months for region X"
- Auto-generate WorkOrders with `job_type=preventive`
- Batch vendor assignment for efficiency
- Campaign-level completion tracking
- Aggregated reporting

**Key Differentiator**: Other PRDs handle reactive maintenance; this includes **proactive campaigns**.

---

### 9. SKILL-165: work-order-state-machine

**Priority**: P0
**Description**: Idempotent, pausable orchestration with defined transitions

**States**:
```
received → triaged → awaiting_approval → awaiting_vendor → 
scheduled → in_progress → completed → [rework] → cancelled
```

**Features**:
- Invariant enforcement (can't skip states)
- Idempotency guarantees (safe to retry)
- Pause/resume per account/property/work_order
- AuditLog for every state transition
- Human override at any point

**Key Differentiator**: Most PRDs describe workflows; this defines a **formal state machine** with guarantees.

---

### 10. SKILL-166: owner-cost-defensibility

**Priority**: P1
**Description**: Every maintenance dollar traceable and justifiable

**Components**:
- Invoice-to-policy mapping
- Historical pattern comparison
- Fraud/waste detection signals
- Owner-facing report generation
- Per-property spend analysis

**Report Templates**:
- Monthly executive summary
- Detailed breakdown by property/category
- Major repair commentary
- Budget variance analysis

**Key Differentiator**: This is a **trust-building feature** unique to Vendoroo's focus.

---

### 11. SKILL-167: after-hours-emergency-flow

**Priority**: P0
**Description**: Specialized workflow for after-hours emergency handling

**Flow**:
1. After-hours flag detection
2. Stricter emergency classification
3. Safety script for tenant (shut-off valves, etc.)
4. Emergency-capable vendor dispatch
5. PM on-call notification (Slack/SMS)
6. Human override capability
7. Post-incident review tagging

**Key Differentiator**: After-hours handling is often an afterthought; this is a **first-class workflow**.

---

## 🔄 Overlapping Skills (Enhanced by Vendoroo)

| Existing Skill | Vendoroo Enhancement |
|----------------|---------------------|
| SKILL-035: maintenance-request-handling | + Specialized agents, brain memory |
| SKILL-036: vendor-management | + Performance metrics, tiering, intelligence |
| SKILL-068: accounting-integration | + Invoice AI validation, compliance checking |
| SKILL-028: owner-reports | + Cost defensibility, fraud detection |
| SKILL-001: unified-inbox | + Maintenance-specific multi-channel |
| SKILL-113: voice-ai | + Receptionist Roo with strict constraints |
| SKILL-132: human-in-loop | + Pause/resume at any point |
| SKILL-037: smart-task-routing | + Policy-driven, performance-informed |

---

## 🏆 Best-in-Class Features

Vendoroo leads the market in:

| Feature | Why Best | Notes |
|---------|----------|-------|
| **Maintenance Specialization** | Only competitor with full vertical | Others treat maintenance as "a feature" |
| **Agent Architecture** | 5 role-specific agents with constraints | Not a general chatbot |
| **Emergency Accuracy** | <0.5% false negative target | Measurable, auditable |
| **Vendor Intelligence** | Multi-factor scoring + tiering | Data-driven assignment |
| **Policy Simulation** | Test rules before enabling | Unique capability |
| **Financial Defensibility** | First-class objective | Trust-building feature |
| **Autonomous Handling** | 80%+ target | Explicit goal metric |

---

## 📊 Feature Categories

| Category | Features | Priority |
|----------|----------|----------|
| **Agent Architecture** | 5 | P0 |
| **Maintenance Intelligence** | 3 | P0-P1 |
| **Emergency Handling** | 2 | P0 |
| **Vendor Management** | 2 | P0-P1 |
| **Financial/Compliance** | 3 | P1 |
| **Orchestration** | 2 | P0 |

---

## 🎯 Impact on Our Platform

### Maintenance Module Foundation
Vendoroo provides the **blueprint for maintenance excellence**. Recommendation:

- **Adopt**: 5-agent architecture, maintenance brain, state machine
- **Integrate**: Vendor intelligence into existing vendor management
- **Differentiate**: Combine with our multi-vertical platform

### Key Architecture Insight
Vendoroo is **maintenance-only** (explicitly NOT replacing PMS). This validates our strategy:
- Vendoroo = Maintenance vertical depth
- Our Platform = Horizontal + Vertical integration

### Competitive Position
No other PRD we've analyzed has this level of maintenance depth:
- Guesty: Basic maintenance requests
- RentalReady: Task management
- Cloudbeds: Hotel-style work orders
- **Vendoroo**: Full maintenance operations platform

---

## Next Steps

1. **Capture Agent Design Knowledge** - How exactly are Roo boundaries defined?
2. **Emergency Classification Logic** - What makes <0.5% achievable?
3. **Vendor Scoring Algorithm** - How are metrics weighted?
4. **Policy Engine Rules** - What condition expressions are supported?

