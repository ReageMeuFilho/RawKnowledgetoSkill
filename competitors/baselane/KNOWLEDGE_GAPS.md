# Baselane - Knowledge Gaps

> **Source**: Baselane_Product_Requirements_Document.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 7
> **NEW CATEGORY**: Fintech + Property Management

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 2 | Banking integration, Schedule E |
| **P1 - Important** | 4 | Account linking, tenant screening, marketplace, entities |
| **P2 - Nice-to-have** | 1 | High-yield tiers |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-BSL-001: Integrated Banking Platform Architecture

**Skill**: SKILL-207 (integrated-banking-platform)
**Status**: 🔴 BLOCKING (for fintech features)

**What We Need**:
1. **Banking Partnership Model**
   - How does Baselane offer banking? (Partner bank)
   - What banking licenses are required?
   - What regulatory compliance is needed?
   - What's the revenue model? (Float interest)

2. **Account Structure**
   - How are checking/savings accounts created?
   - How are debit cards issued?
   - What's the KYC/AML process?
   - How are transfers processed?

3. **Technical Integration**
   - What banking APIs are used?
   - How is real-time balance tracked?
   - How are transactions reported?
   - What's the reconciliation process?

**Why Critical**: If we want to compete with Baselane, we need to understand how they built banking.

**Alternative Approach**: Focus on excellent QuickBooks/Xero integration instead of native banking.

**Ideal Source**:
- [ ] Banking-as-a-Service providers (Synapse, Unit, Treasury Prime)
- [ ] Fintech platform architecture patterns
- [ ] Banking compliance requirements

---

### GAP-BSL-002: Schedule E Auto-Categorization Engine

**Skill**: SKILL-209 (schedule-e-auto-categorization)
**Status**: 🔴 BLOCKING (for US market)

**What We Need**:
1. **Category System**
   - Complete Schedule E line item mapping
   - How to handle edge cases?
   - What about non-Schedule E transactions?
   - Multi-property allocation?

2. **AI Categorization**
   - What ML model suggests categories?
   - How are rules learned from user corrections?
   - What's the accuracy rate?
   - How to handle ambiguous transactions?

3. **Tax Package Generation**
   - How is Schedule E pre-filled?
   - How are 1099s generated?
   - What accountant sharing features?
   - What audit trail is required?

**Why Critical**: **#1 pain point** for US landlords is tax preparation.

**Ideal Source**:
- [ ] IRS Schedule E documentation
- [ ] Tax software APIs (TurboTax, etc.)
- [ ] Landlord bookkeeping best practices

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-BSL-003: Property-Account Association System

**Skill**: SKILL-210 (property-account-association)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Data Model**
   - How are properties linked to accounts?
   - How are transactions auto-assigned?
   - What about shared expenses?
   - Multi-property transaction split?

2. **Legal Compliance**
   - Security deposit separation requirements by state
   - Trust accounting integration
   - Audit trail requirements

**Ideal Source**:
- [ ] State-by-state security deposit laws
- [ ] Property management accounting patterns

---

### GAP-BSL-004: Tenant Screening Integration

**Skill**: SKILL-213 (tenant-screening-integrated)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Provider Integration**
   - TransUnion SmartMove API?
   - Alternative providers (Experian, Equifax)?
   - What reports are included?
   - Pricing structure?

2. **Workflow Design**
   - Application process
   - Applicant authorization flow
   - Results presentation
   - Adverse action compliance

**Ideal Source**:
- [ ] TransUnion SmartMove API docs
- [ ] FCRA compliance requirements
- [ ] Tenant screening best practices

---

### GAP-BSL-005: Partner Marketplace Architecture

**Skill**: SKILL-212 (partner-marketplace)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Partnership Model**
   - How are partners recruited?
   - What's the revenue share model?
   - How is quality maintained?
   - What integration depth?

2. **Categories to Build**
   - Insurance partners
   - Lending partners
   - Legal partners
   - Contractor marketplace
   - Tax preparation

**Ideal Source**:
- [ ] Marketplace platform patterns
- [ ] Real estate service provider landscape

---

### GAP-BSL-006: Multi-Entity Onboarding System

**Skill**: SKILL-214 (multi-entity-onboarding)
**Status**: 🟡 NEEDED

**What We Need**:
1. **KYC Requirements**
   - What verification is needed per entity type?
   - How are control persons identified?
   - What documents are collected?
   - How is EIN verified?

2. **Entity Management**
   - How are multiple entities managed?
   - How is workspace separation handled?
   - What about shared properties across entities?

**Ideal Source**:
- [ ] KYC/AML compliance requirements
- [ ] Business entity verification services

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-BSL-007: High-Yield Savings Tier System

**Skill**: SKILL-208 (high-yield-savings-tiers)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Tier Design**
   - How are tier thresholds set?
   - How is interest calculated?
   - What's the competitive landscape?

**Note**: Only relevant if we pursue banking features.

**Ideal Source**:
- [ ] High-yield savings market analysis
- [ ] Banking product design patterns

---

## 📋 Knowledge Collection Plan

### Phase 1: Tax Automation (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BSL-002 | IRS Schedule E research | TBD |

### Phase 2: Tenant Screening (Week 3)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BSL-004 | TransUnion API research | TBD |

### Phase 3: Property Accounting (Week 4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BSL-003 | State law research | TBD |

### Phase 4: Banking (If Prioritized) (Week 5-8)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BSL-001 | BaaS provider research | TBD |
| GAP-BSL-005 | Marketplace research | TBD |

---

## 🎯 Strategic Priorities

### Approach A: Match Baselane (Fintech Route)

If we want to compete head-on:
1. **Must have**: Banking partnership (GAP-BSL-001)
2. **Must have**: Schedule E engine (GAP-BSL-002)
3. **Should have**: Property-account linking (GAP-BSL-003)
4. **Nice to have**: Tenant screening (GAP-BSL-004)

**Pros**: Full feature parity, captures fintech-minded landlords
**Cons**: Requires banking license/partnership, regulatory complexity

### Approach B: Differentiate (AI + Accounting Route)

If we focus on our strengths:
1. **Match**: Schedule E alignment (GAP-BSL-002)
2. **Match**: Strong QB/Xero integration
3. **Differentiate**: Superior AI automation (from Hospitable)
4. **Differentiate**: Better operational features (from Guesty)

**Pros**: Leverages our AI strength, simpler to build
**Cons**: Won't capture fintech-focused users

### Recommended Approach

**Hybrid Strategy**:
1. Build Schedule E categorization (required for US market)
2. Offer excellent QB/Xero integration (alternative to native banking)
3. Add AI automation (Hospitable features) as differentiator
4. Consider banking partnership in v2 if market demands

---

## 🏆 Competitive Intelligence

### Baselane's Moat

1. **Banking integration** - No other PM has actual banking
2. **Tax alignment** - Schedule E from day one
3. **High-yield interest** - Earns money while managing properties
4. **Partner ecosystem** - One-stop shop for landlords

### Baselane's Weaknesses

1. **No AI automation** - Manual processes still required
2. **Limited channel management** - Not built for STR operations
3. **US-only** - No international expansion
4. **1-50 properties** - Doesn't scale to enterprise

### How to Compete

| Our Strength | Counter to Baselane |
|--------------|---------------------|
| AI automation | "Manage with AI, not spreadsheets" |
| Multi-channel | "STR + LTR in one platform" |
| International | "Global platform, local compliance" |
| Enterprise scale | "Grow without switching platforms" |

---

## 📊 Fintech Category Now Mapped!

With Baselane analyzed, we now have a new market category:

| Platform Type | Example | Focus |
|---------------|---------|-------|
| Traditional PMS | Guesty | Property operations |
| AI-First PMS | Hospitable | Automation |
| Accounting PMS | OwnerRez | QuickBooks |
| **Fintech PMS** | **Baselane** | **Banking + Tax** |

**Our position**: We can be the **AI-First PMS** that also matches Baselane's tax features!

---

## 🎉 Milestone: 214+ Skills!

With Baselane, we've added a completely new dimension to the registry:

| Metric | Before | After |
|--------|--------|-------|
| **Total Skills** | 206 | 214 |
| **Competitors** | 17 | 18 |
| **Categories** | PMS-focused | + Fintech |
| **Knowledge Gaps** | 123+ | 130+ |

