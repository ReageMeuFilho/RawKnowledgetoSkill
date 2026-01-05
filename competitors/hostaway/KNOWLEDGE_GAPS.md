# Hostaway - Knowledge Gaps

> **Source**: Hostaway PRD v2.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 8

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 3 | Automation, white-label, trust |
| **P1 - Important** | 3 | Cleaner ops, workflows, RBAC |
| **P2 - Nice-to-have** | 2 | Multi-engine, scaling |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-HAW-001: 93% Automation Definition

**Skill**: SKILL-178 (93-percent-message-automation)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Automation Scope Definition**
   - What counts as "automated"?
   - What's in the 7% that can't be automated?
   - Is this AI response or template-triggered?

2. **Measurement Methodology**
   - How is 93% calculated?
   - Per message? Per conversation? Per inquiry type?
   - What's the baseline comparison?

3. **AI vs Rules**
   - What % is AI-generated vs rule-triggered?
   - What intent classification is used?
   - How accurate is sentiment analysis?

**Why Critical**: This is their headline claim - we need to match or exceed.

**Ideal Source**:
- [ ] Hostaway customer interviews
- [ ] Messaging automation case studies
- [ ] AI chatbot benchmarks

---

### GAP-HAW-002: White-Label Architecture

**Skill**: SKILL-179 (white-label-platform)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Technical Architecture**
   - How is multi-tenancy implemented?
   - How is branding isolated?
   - How are custom domains managed?

2. **Customization Scope**
   - What can be customized?
   - What can't be changed?
   - How are custom features added?

3. **Reseller Model**
   - How is pricing structured for resellers?
   - What's the markup model?
   - How is billing handled?

**Why Critical**: **UNIQUE capability** - if we want enterprise, may need this.

**Ideal Source**:
- [ ] Multi-tenant SaaS architecture guides
- [ ] White-label platform case studies
- [ ] Reseller program documentation

---

### GAP-HAW-003: Trust Accounting Requirements

**Skill**: SKILL-180 (trust-accounting)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Legal Requirements**
   - Which jurisdictions require trust accounting?
   - What are the compliance requirements?
   - What happens if mixed?

2. **Account Structure**
   - How are trust accounts separated?
   - What reconciliation is required?
   - How are owner payouts processed?

3. **Audit Trail**
   - What documentation is required?
   - How long must records be kept?
   - What reports are needed for auditors?

**Why Critical**: **LEGAL COMPLIANCE** - could be liability if not implemented.

**Ideal Source**:
- [ ] Property management attorney
- [ ] Real estate commission regulations
- [ ] Accounting compliance guides

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-HAW-004: Cleaner Portal Features

**Skill**: SKILL-181 (cleaner-portal-mobile)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Task Workflow**
   - How are tasks assigned?
   - What's the checklist structure?
   - How are photos verified?

2. **Quality System**
   - How is quality rated?
   - What happens on low ratings?
   - How is performance tracked?

3. **Notifications**
   - What notification types?
   - What cadence?
   - SMS vs push vs email?

**Ideal Source**:
- [ ] Cleaning company operations
- [ ] Task management app patterns
- [ ] Field service mobile apps

---

### GAP-HAW-005: Workflow Builder Design

**Skill**: SKILL-182 (custom-workflow-builder)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Trigger Types**
   - Full list of available triggers
   - Event payload structure
   - Custom trigger support

2. **Action Types**
   - What actions can be performed?
   - Integration with external systems?
   - Custom action support?

3. **Conditional Logic**
   - How complex can conditions be?
   - Nested conditions?
   - Time-based conditions?

4. **Approval Workflows**
   - How are approval chains defined?
   - Multi-level approvals?
   - Timeout handling?

**Ideal Source**:
- [ ] Workflow automation platforms (Zapier, n8n)
- [ ] Business process automation patterns
- [ ] Visual workflow builder UX research

---

### GAP-HAW-006: Granular RBAC Implementation

**Skill**: SKILL-184 (granular-rbac)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Permission Model**
   - What's the permission hierarchy?
   - How are permissions inherited?
   - How are conflicts resolved?

2. **Property-Level Access**
   - How is property access assigned?
   - Can permissions cascade?
   - How are groups handled?

3. **Custom Roles**
   - How are custom roles created?
   - What permissions can be combined?
   - Role templates?

**Ideal Source**:
- [ ] Enterprise RBAC patterns
- [ ] Multi-tenant permission systems
- [ ] Property management access models

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-HAW-007: Multi-Booking Engine Setup

**Skill**: SKILL-183 (multi-booking-engine)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Engine Configuration**
   - How many engines per account?
   - How are properties assigned?
   - Shared vs separate inventory?

2. **Domain Management**
   - DNS configuration?
   - SSL certificates?
   - Subdomain vs custom domain?

**Ideal Source**:
- [ ] Multi-brand website management
- [ ] Domain configuration patterns

---

### GAP-HAW-008: 1000+ Property Scaling

**Skill**: SKILL-186 (1000-property-scale)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Performance Optimization**
   - Database partitioning strategy?
   - Caching approach?
   - Query optimization?

2. **Operational Scaling**
   - Team structure at 1000+ props?
   - Workflow complexity management?
   - Reporting at scale?

**Ideal Source**:
- [ ] Enterprise SaaS scaling patterns
- [ ] Large property management operations

---

## 📋 Knowledge Collection Plan

### Phase 1: Compliance Critical (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HAW-003 | Property mgmt attorney + RE commission | TBD |
| GAP-HAW-002 | Multi-tenant architecture research | TBD |

### Phase 2: Automation Validation (Week 3-4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HAW-001 | Customer interviews + benchmarks | TBD |
| GAP-HAW-005 | Workflow platform analysis | TBD |

### Phase 3: Operations (Week 5-6)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HAW-004 | Cleaning ops interviews | TBD |
| GAP-HAW-006 | Enterprise RBAC patterns | TBD |

### Phase 4: Scale (Week 7)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HAW-007 | Multi-brand website patterns | TBD |
| GAP-HAW-008 | Enterprise SaaS scaling | TBD |

---

## 🎯 Strategic Priorities

### Must Match
- ✅ High automation rate (validate 93% claim)
- ✅ Trust accounting (legal requirement)
- ✅ Visual workflow builder

### Should Match
- ⚠️ Granular RBAC
- ⚠️ Cleaner portal
- ⚠️ Multi-booking engine

### Consider for Future
- 🔮 White-label (enterprise tier only?)
- 🔮 Reseller program

---

## 🏆 Competitive Intelligence

### How Hostaway Competes with Guesty

Both target enterprise (50-1000+ props). Hostaway differentiates on:
1. **White-label** (Guesty doesn't offer)
2. **93% automation claim** (bold marketing)
3. **Trust accounting** (compliance focus)

### Our Positioning

We can beat both by combining:
- Hostaway's white-label flexibility (via open-source)
- Guesty's feature depth
- EliseAI's AI intelligence
- Vendoroo's maintenance depth
- PriceLabs' pricing intelligence

The **unified platform** that none of them can match.

