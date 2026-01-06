# AppFolio - Knowledge Gaps

> **Source**: appfolio_prd.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 8

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 2 | AI Leasing, AI Maintenance |
| **P1 - Important** | 4 | Investment, HOA, Unit Turn, Offline |
| **P2 - Nice-to-have** | 2 | CAM, Student Housing |

**Note**: AppFolio introduces entirely new categories (Investment, HOA) that require strategic decisions before filling gaps.

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-AF-001: AI Leasing Assistant Architecture

**Skill**: SKILL-253 (ai-leasing-assistant)
**Status**: 🔴 CRITICAL

**What We Need**:
1. **Autonomous Response Logic**
   - How are leads qualified?
   - What questions can it answer?
   - When does it escalate to human?
   - How is 24/7 coverage implemented?

2. **Tour Scheduling**
   - Calendar integration
   - Availability management
   - Confirmation workflow
   - Rescheduling handling

3. **Lead Nurturing**
   - Sequence design
   - Timing logic
   - Personalization rules
   - Conversion tracking

**Overlap**: EliseAI has similar - compare implementations.

**Ideal Source**:
- [ ] EliseAI detailed architecture
- [ ] AppFolio Realm-X documentation
- [ ] Leasing AI best practices

---

### GAP-AF-002: AI Maintenance Coordinator Architecture

**Skill**: SKILL-254 (ai-maintenance-coordinator)
**Status**: 🔴 CRITICAL

**What We Need**:
1. **Troubleshooting Logic**
   - What issues can AI resolve?
   - Decision tree structure
   - Photo/video analysis?
   - Resolution confirmation

2. **Vendor Dispatch**
   - Vendor selection logic
   - Availability checking
   - Emergency handling
   - Geographic routing

3. **Follow-up Automation**
   - Status update triggers
   - Satisfaction surveys
   - Escalation rules

**Overlap**: Vendoroo has similar - compare implementations.

**Ideal Source**:
- [ ] Vendoroo architecture comparison
- [ ] AppFolio maintenance documentation
- [ ] Property maintenance AI patterns

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-AF-003: Distribution Waterfall Calculations

**Skill**: SKILL-241 (distribution-management)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Waterfall Structures**
   - Common waterfall types
   - Priority return (pref) calculations
   - Catch-up provisions
   - Promote/carry structures

2. **Calculation Engine**
   - Multi-tier logic
   - Look-back provisions
   - IRR hurdles
   - Clawback calculations

3. **Reporting**
   - Distribution statements
   - Investor-level breakdown
   - Tax reporting (K-1 integration)

**Ideal Source**:
- [ ] Real estate fund structures
- [ ] Private equity waterfall patterns
- [ ] Tax reporting requirements

---

### GAP-AF-004: Architectural Review Workflow

**Skill**: SKILL-247 (architectural-review-workflow)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Submission Process**
   - What information collected?
   - Photo/document requirements?
   - Fee handling?

2. **Review Workflow**
   - Who reviews (board, committee)?
   - Approval thresholds?
   - Timeline requirements?
   - Appeal process?

3. **Communication**
   - Status updates
   - Approval/denial letters
   - Condition notifications

**Ideal Source**:
- [ ] HOA management best practices
- [ ] CC&R requirements research
- [ ] AppFolio HOA documentation

---

### GAP-AF-005: Unit Turn Board Design

**Skill**: SKILL-257 (unit-turn-board)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Board Structure**
   - What statuses/stages?
   - Task categories (paint, clean, repair)?
   - Dependency management?

2. **Assignment Logic**
   - Vendor vs in-house routing
   - Scheduling optimization
   - Parallel task execution

3. **Metrics**
   - Turn time tracking
   - Cost per turn
   - Vacancy days impact

**Ideal Source**:
- [ ] Multifamily operations research
- [ ] Turn optimization studies
- [ ] Visual board design patterns (Kanban)

---

### GAP-AF-006: Mobile Offline Architecture

**Skill**: SKILL-260 (mobile-offline-mode)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Data Sync Strategy**
   - What data available offline?
   - Sync frequency?
   - Conflict resolution rules?

2. **Task Queue**
   - What actions work offline?
   - Queue management?
   - Retry logic?

3. **User Experience**
   - Offline indicator
   - Sync status
   - Error handling

**Ideal Source**:
- [ ] Mobile offline patterns (PWA, SQLite)
- [ ] Field service app research
- [ ] React Native / Flutter offline patterns

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-AF-007: CAM Tracking & Reconciliation

**Skill**: SKILL-258 (cam-tracking-reconciliation)
**Status**: 🟢 OPTIONAL (Commercial only)

**What We Need**:
1. **CAM Categories**
   - What expenses included?
   - Exclusion rules?
   - Cap provisions?

2. **Tenant Allocation**
   - Pro-rata methods (SF, %)
   - Gross-up provisions
   - Base year handling

3. **Reconciliation**
   - Annual true-up process
   - Over/under billing
   - Audit trail

**Note**: Only needed if we target commercial properties.

---

### GAP-AF-008: Rent-By-Bed Leasing

**Skill**: SKILL-259 (rent-by-bed-leasing)
**Status**: 🟢 OPTIONAL (Student housing only)

**What We Need**:
1. **Lease Structure**
   - Individual vs joint liability
   - Guarantor requirements
   - Academic year terms

2. **Bed Management**
   - Bed inventory tracking
   - Roommate matching
   - Gender considerations

3. **Billing**
   - Per-bed ledgers
   - Common area charges
   - Utility splitting

**Note**: Only needed if we target student housing.

---

## 📋 Strategic Decisions Required

### Before Filling Gaps, Decide:

| Decision | Options | Impact on Gaps |
|----------|---------|----------------|
| **Investment Management** | Build / Partner / Skip | GAP-AF-003 only if Build |
| **HOA Management** | Build / Partner / Skip | GAP-AF-004 only if Build |
| **Commercial Properties** | Include / Exclude | GAP-AF-007 only if Include |
| **Student Housing** | Include / Exclude | GAP-AF-008 only if Include |

### Recommended Approach

**Phase 1 (Core)**: Focus on STR + LTR residential
- Fill GAP-AF-001 (AI Leasing)
- Fill GAP-AF-002 (AI Maintenance)
- Fill GAP-AF-005 (Unit Turn)
- Fill GAP-AF-006 (Mobile Offline)

**Phase 2 (Expansion)**: Add verticals based on market demand
- Investment Management if targeting fund managers
- HOA if targeting community associations
- Commercial if targeting CRE

---

## 🎯 Knowledge Collection Plan

### Phase 1: AI Agents (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-AF-001 | Compare EliseAI + AppFolio | TBD |
| GAP-AF-002 | Compare Vendoroo + AppFolio | TBD |

### Phase 2: Operations (Week 3)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-AF-005 | Multifamily ops research | TBD |
| GAP-AF-006 | Mobile architecture research | TBD |

### Phase 3: Strategic (Pending Decisions)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-AF-003 | Fund structure research | TBD |
| GAP-AF-004 | HOA management research | TBD |

---

## 🏆 Competitive Intelligence

### AppFolio's Moat

1. **Realm-X AI Platform** - Native, not bolted on
2. **Multi-vertical** - Residential, Commercial, Student, HOA, Investment
3. **Cloud-native** - Modern architecture
4. **SOC 2 Type 2** - Enterprise security
5. **Partner ecosystem** - AppFolio Stack marketplace

### AppFolio's Weaknesses

1. **No STR focus** - Primarily LTR/multifamily
2. **Pricing** - Per-unit pricing can be expensive at scale
3. **Complexity** - Many features = learning curve
4. **Limited channel management** - No OTA integrations

### How to Position Against AppFolio

| Our Advantage | Message |
|---------------|---------|
| STR expertise | "Built for short-term rentals" |
| OTA integrations | "60+ channel connections" |
| Simpler pricing | "Flat fee, not per-unit" |
| Modern AI | "AI-first, not AI-added" |

---

## 📊 Registry Status: 257 Skills!

With AppFolio, we've added two new categories:

| Metric | Before | After |
|--------|--------|-------|
| **Total Skills** | 237 | **257** |
| **Competitors** | 21 | **22** |
| **Categories** | 7 | **9** |
| **New Categories** | - | Investment Mgmt, HOA Mgmt |

### Category Breakdown

| Category | Skills | Status |
|----------|--------|--------|
| PMS Core | 100+ | ✅ Strong |
| AI/Automation | 40+ | ✅ Strong |
| Accounting | 20+ | ✅ Strong |
| Enterprise | 15+ | ✅ Strong |
| Fintech | 8 | ⚠️ Limited |
| Consumer | 9 | ⚠️ Limited |
| Hybrid PM | 8 | ⚠️ Limited |
| **Investment Mgmt** | **7** | **🆕 NEW** |
| **HOA Mgmt** | **7** | **🆕 NEW** |

---

## 🎉 Major Milestone!

AppFolio significantly expands our registry into **full property management** beyond STR:

- **Investment Management** - Syndication, waterfall, investor portals
- **HOA Management** - Associations, violations, architectural review
- **LTR Features** - Unit turns, by-bed leasing, CAM tracking

**Strategic Question**: Do we expand into these verticals or stay focused on STR?


