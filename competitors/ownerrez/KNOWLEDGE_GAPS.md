# OwnerRez - Knowledge Gaps

> **Source**: OWNERREZ (v2)PRD.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 6

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 2 | QuickBooks, rental agreements |
| **P1 - Important** | 3 | Deposit sync, quotes, modular pricing |
| **P2 - Nice-to-have** | 1 | Owner stays |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-ORZ-001: QuickBooks Online Integration Architecture

**Skill**: SKILL-200 (quickbooks-first-accounting)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Data Flow Design**
   - What entities sync to QB?
   - What is sync direction (one-way, two-way)?
   - What triggers sync?
   - How are conflicts resolved?

2. **Account Mapping**
   - How are revenue accounts mapped?
   - How are expense categories mapped?
   - What about multi-entity accounting?
   - Class/location tracking support?

3. **Reconciliation Support**
   - How does deposit sync work?
   - What about partial payments?
   - How are refunds handled?
   - Bank feed matching?

4. **Implementation Effort**
   - QB API authentication
   - Rate limits
   - Error handling
   - Retry logic

**Why Critical**: **#1 feature** for accounting-focused PMCs in US market.

**Ideal Source**:
- [ ] QuickBooks Online API documentation
- [ ] Accounting integration best practices
- [ ] PM accounting workflows

---

### GAP-ORZ-002: Digital Rental Agreement System

**Skill**: SKILL-205 (digital-rental-agreements)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Agreement Templates**
   - What clauses are required?
   - How to handle per-property customization?
   - What variables are supported?
   - Multi-language support?

2. **E-Signature Integration**
   - Which providers (DocuSign, HelloSign)?
   - What's the signature flow?
   - How are signatures validated?
   - Legal enforceability?

3. **Automation Integration**
   - Trigger on booking creation?
   - Block check-in until signed?
   - Reminder sequences?
   - Storage and retrieval?

**Why Critical**: **Legal protection** - essential for liability management.

**Ideal Source**:
- [ ] Vacation rental agreement templates
- [ ] E-signature provider APIs
- [ ] Legal compliance requirements

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-ORZ-003: Deposit Syncing for Reconciliation

**Skill**: SKILL-201 (deposit-syncing-reconciliation)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Sync Mechanics**
   - How are deposits grouped?
   - What about payment processor timing?
   - How are fees handled?
   - Multi-currency support?

2. **Reconciliation Flow**
   - How does bank feed matching work?
   - What about split deposits?
   - How are discrepancies flagged?
   - Audit trail requirements?

**Ideal Source**:
- [ ] Bank reconciliation patterns
- [ ] Payment processor documentation
- [ ] Accounting reconciliation workflows

---

### GAP-ORZ-004: Quote-to-Booking Workflow

**Skill**: SKILL-204 (quote-to-booking-workflow)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Quote Creation**
   - What fields are included?
   - How are taxes/fees calculated?
   - Quote validity period?
   - Revision handling?

2. **Guest Experience**
   - How is quote delivered?
   - What's the acceptance flow?
   - Payment collection process?
   - Counter-offer support?

3. **Conversion Logic**
   - How does quote become booking?
   - What about availability holds?
   - Expiration handling?
   - Audit trail?

**Ideal Source**:
- [ ] Quote management systems
- [ ] Sales workflow patterns
- [ ] PM quoting practices

---

### GAP-ORZ-005: Modular Pricing Implementation

**Skill**: SKILL-202 (modular-pricing-architecture)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Module Definition**
   - What modules exist?
   - How are dependencies managed?
   - Upgrade/downgrade flows?
   - Feature gating?

2. **Pricing Logic**
   - Per-property vs flat?
   - Volume discounts?
   - Annual vs monthly?
   - Enterprise custom?

3. **Billing System**
   - Proration handling?
   - Add-on mid-cycle?
   - Usage-based (SMS)?
   - Invoicing?

**Ideal Source**:
- [ ] SaaS pricing strategies
- [ ] Modular software patterns
- [ ] Billing system design

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-ORZ-006: Owner Stay Tracking

**Skill**: SKILL-206 (owner-stay-tracking)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Calendar Integration**
   - How are owner stays displayed?
   - Blocking logic?
   - Overlap handling?

2. **Financial Treatment**
   - No revenue recorded?
   - Expense allocation?
   - Report exclusion?

**Ideal Source**:
- [ ] PM owner use policies
- [ ] Calendar management patterns

---

## 📋 Knowledge Collection Plan

### Phase 1: Accounting Critical (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-ORZ-001 | QB API docs + accounting research | TBD |
| GAP-ORZ-002 | E-sign providers + legal templates | TBD |

### Phase 2: Financial Flows (Week 3-4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-ORZ-003 | Bank reconciliation patterns | TBD |
| GAP-ORZ-004 | Sales workflow research | TBD |

### Phase 3: Commercial (Week 5)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-ORZ-005 | SaaS pricing research | TBD |

### Phase 4: Operations (Week 6)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-ORZ-006 | PM practices research | TBD |

---

## 🎯 Strategic Priorities

### For US Mid-Market

If we want to compete with OwnerRez:
1. **Must have**: QuickBooks integration (GAP-ORZ-001)
2. **Must have**: Rental agreements (GAP-ORZ-002)
3. **Should have**: Deposit sync (GAP-ORZ-003)
4. **Nice to have**: Quote workflow (GAP-ORZ-004)

### Implementation Order

```
1. Digital Rental Agreements → Legal protection
2. QuickBooks Integration → Accounting compliance
3. Deposit Syncing → Reconciliation accuracy
4. Quote Workflow → Professional sales flow
5. Owner Stay Tracking → Owner management
```

---

## 🏆 Competitive Intelligence

### OwnerRez's Moat

1. **QuickBooks-first** - Deep integration, not afterthought
2. **Power-user orientation** - Complexity for capability
3. **Transparent pricing** - Public, modular costs
4. **Strong retention** - Loyal accounting-focused users

### How to Compete

| Approach | Pros | Cons |
|----------|------|------|
| **Match QB depth** | Capture accounting PMCs | Development effort |
| **Multi-accounting** | QB + Xero + others | Complexity |
| **Focus enterprise** | Let OwnerRez have mid-market | Miss segment |
| **AI + accounting** | Combine OwnerRez + Hospitable | Novel positioning |

**Recommendation**: Match OwnerRez's QB integration AND Hospitable's AI features. This combination doesn't exist in market.

---

## 📊 Market Analysis Complete!

With 17 PRDs analyzed, we have:

| Segment | Champion | Focus |
|---------|----------|-------|
| SMB Website | Lodgify | Website-first |
| SMB AI | Hospitable | Automation-first |
| Mid-Market Accounting | **OwnerRez** | QuickBooks-first |
| Enterprise STR | Guesty/Hostaway | Scale + features |
| Enterprise LTR | EliseAI | Housing ops |
| Pricing Vertical | PriceLabs | Algorithm excellence |
| Maintenance Vertical | Vendoroo | Deep specialization |

### The Unified Opportunity

No platform combines:
- Lodgify's **website builder simplicity**
- Hospitable's **AI automation**
- OwnerRez's **accounting depth**
- Guesty's **enterprise scale**
- PriceLabs' **pricing intelligence**
- Vendoroo's **maintenance depth**
- EliseAI's **housing expertise**

**That's our opportunity: The Best-of-Breed Unified Platform!**

---

## 🎉 Milestone: 200+ Skills!

With OwnerRez, we've crossed **200 unique skills** in the registry!

| Metric | Value |
|--------|-------|
| **Total Skills** | 206+ |
| **Competitors** | 17 |
| **Knowledge Gaps** | 123+ |
| **Market Coverage** | Complete |

