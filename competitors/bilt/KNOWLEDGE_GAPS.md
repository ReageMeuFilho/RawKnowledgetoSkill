# BILT Rewards - Knowledge Gaps

> **Source**: BILT_Rewards_Enhanced_PRD.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 7
> **NEW CATEGORY**: Consumer Loyalty Platform

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 2 | Three-sided marketplace, credit reporting |
| **P1 - Important** | 4 | Rewards, neighborhood, incentives, transfers |
| **P2 - Nice-to-have** | 1 | Card-linked offers |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-BLT-001: Three-Sided Marketplace Architecture

**Skill**: SKILL-217 (three-sided-marketplace)
**Status**: 🔴 RESEARCH NEEDED

**What We Need**:
1. **Flywheel Economics**
   - How does value flow between stakeholders?
   - What's the revenue model for each side?
   - How is revenue shared with PMs?
   - What makes the flywheel self-reinforcing?

2. **Network Effects**
   - At what scale do network effects kick in?
   - How is chicken-and-egg problem solved?
   - What's the CAC for each side?
   - How is retention achieved (100% PM retention)?

3. **Platform Design**
   - How are the three interfaces designed?
   - What shared data flows between sides?
   - How are conflicts between stakeholders resolved?

**Why Critical**: BILT's $10.75B valuation is based on this architecture.

**Ideal Source**:
- [ ] Platform economics research
- [ ] BILT partnership documentation
- [ ] Multi-sided marketplace case studies

---

### GAP-BLT-002: Credit Bureau Rent Reporting System

**Skill**: SKILL-216 (credit-boost-rent-reporting)
**Status**: 🔴 BLOCKING (for tenant value-add)

**What We Need**:
1. **Bureau Integration**
   - How to report to Experian, Equifax, TransUnion?
   - What data format is required?
   - What's the certification process?
   - What are the costs?

2. **Compliance Requirements**
   - FCRA compliance for rent reporting
   - Dispute handling process
   - Data accuracy requirements
   - Member consent requirements

3. **Technical Implementation**
   - What APIs are available?
   - What's the reporting frequency?
   - How is payment verification done?
   - What about late payments?

**Why Critical**: **Free credit reporting** is major tenant value-add.

**Ideal Source**:
- [ ] Credit bureau APIs (Experian RentBureau, etc.)
- [ ] FCRA compliance guidelines
- [ ] Rent reporting service providers

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-BLT-003: Rent Rewards Program Design

**Skill**: SKILL-215 (rent-rewards-program)
**Status**: 🟡 NEEDED (if building own)

**What We Need**:
1. **Points Economics**
   - How much is 1 point worth?
   - What's the earn rate on rent?
   - How is point liability managed?
   - What's the breakage rate?

2. **Partner Funding**
   - Who funds the points? PM? BILT? Merchant?
   - What's the interchange model?
   - How do transfer partners value points?

**Ideal Source**:
- [ ] Loyalty program economics
- [ ] Credit card rewards models
- [ ] BILT investor presentations

---

### GAP-BLT-004: Neighborhood Benefits Network Design

**Skill**: SKILL-219 (neighborhood-benefits-network)
**Status**: 🟡 NEEDED (if building own)

**What We Need**:
1. **Merchant Acquisition**
   - How are 50K+ merchants recruited?
   - What's the value prop to merchants?
   - What commission/fees do merchants pay?

2. **Hyper-Local Targeting**
   - How is 15-mile radius targeted?
   - How are offers personalized?
   - How is merchant discovery presented?

**Ideal Source**:
- [ ] Local commerce platforms
- [ ] Card-linked offer networks
- [ ] Merchant acquisition strategies

---

### GAP-BLT-005: PM Incentive Campaign System

**Skill**: SKILL-222 (pm-resident-incentives)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Campaign Types**
   - What incentive structures work?
   - How are points funded (PM budget)?
   - What behaviors can be incentivized?

2. **ROI Measurement**
   - How is 3x early payment lift measured?
   - How is 20% acquisition cost reduction calculated?
   - What analytics are provided to PMs?

**Ideal Source**:
- [ ] BILT Alliance documentation
- [ ] Property manager case studies
- [ ] Incentive program research

---

### GAP-BLT-006: Loyalty Transfer Partner Network

**Skill**: SKILL-220 (loyalty-transfer-partners)
**Status**: 🟡 NEEDED (if building own)

**What We Need**:
1. **Partner Agreements**
   - How are transfer ratios negotiated?
   - What volume is required for partnerships?
   - What's the settlement process?

2. **Technical Integration**
   - How do transfers work technically?
   - What's the transfer timeline?
   - How are disputes handled?

**Ideal Source**:
- [ ] Loyalty coalition research
- [ ] Points.com or similar platforms
- [ ] Airline/hotel loyalty program docs

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-BLT-007: Card-Linked Offer Infrastructure

**Skill**: SKILL-223 (card-linked-offers)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Technical Architecture**
   - How are card transactions matched?
   - What CLO networks exist (Cardlytics, etc.)?
   - What's the integration effort?

**Ideal Source**:
- [ ] Card-linked offer providers
- [ ] Payment network documentation

---

## 📋 Knowledge Collection Plan

### Phase 1: Understanding BILT (Week 1)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BLT-001 | BILT Alliance research | TBD |
| GAP-BLT-005 | PM case studies | TBD |

### Phase 2: Credit Reporting (Week 2-3)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BLT-002 | Bureau API research | TBD |

### Phase 3: Rewards Program (Week 4-5, if needed)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BLT-003 | Loyalty economics research | TBD |
| GAP-BLT-004 | Merchant network research | TBD |

### Phase 4: Advanced (Week 6+, if needed)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-BLT-006 | Transfer partner research | TBD |
| GAP-BLT-007 | CLO provider research | TBD |

---

## 🎯 Strategic Priorities

### Approach A: Partner with BILT

**Strategy**: Integrate with BILT Alliance as a PMS partner.

**Benefits**:
- Access to 4M+ engaged members
- Instant tenant value-add (rewards, credit)
- Revenue share from neighborhood spend
- Competitive differentiation

**Requirements**:
- PMS integration (we'd need standard APIs)
- Alliance partnership application
- Payment flow integration

**Research Needed**:
- [ ] BILT Alliance API documentation
- [ ] Partnership terms and requirements
- [ ] Revenue share model

---

### Approach B: Build Own Loyalty

**Strategy**: Create our own rent rewards program.

**Benefits**:
- Own the consumer relationship
- Full control over economics
- Potential for $10B+ valuation (like BILT)

**Challenges**:
- Massive investment required
- Chicken-and-egg problem
- BILT has 5+ year head start
- Need merchant network, transfer partners

**NOT RECOMMENDED** unless significant funding available.

---

### Approach C: Credit Reporting Only

**Strategy**: Offer free rent reporting as PM value-add.

**Benefits**:
- Lower complexity than full loyalty
- Clear tenant value-add
- Differentiation from basic PMS
- Lower cost than full rewards program

**Requirements**:
- Credit bureau partnerships
- FCRA compliance
- Payment verification system

**RECOMMENDED** as minimum viable tenant value-add.

---

## 🏆 Competitive Intelligence

### BILT's Moat

1. **Scale**: 4M members, 4.5M properties, 50K merchants
2. **Flywheel**: Self-reinforcing three-sided marketplace
3. **Brand**: $10.75B valuation, strong consumer awareness
4. **Partnerships**: 22 transfer partners, major PMS integrations
5. **Data**: $100B+ annual transaction data

### BILT's Weaknesses

1. **Consumer-focused**: Less PM operational features
2. **US-only**: No international presence
3. **Rent-specific**: Less applicable to STR
4. **LTR focus**: Not designed for vacation rentals

### How to Position

| Scenario | Our Strategy |
|----------|--------------|
| **LTR market** | Partner with BILT for tenant value |
| **STR market** | Focus on PM operations, ignore BILT |
| **Hybrid portfolio** | Offer both BILT integration and STR features |

---

## 📊 Consumer Loyalty Category Now Mapped!

With BILT analyzed, we now understand the consumer side:

| Platform Type | Example | Focus |
|---------------|---------|-------|
| Traditional PMS | Guesty | PM operations |
| AI-First PMS | Hospitable | Automation |
| Accounting PMS | OwnerRez | QuickBooks |
| Fintech PMS | Baselane | Banking + Tax |
| **Consumer Loyalty** | **BILT** | **Renter rewards** |

**Our unique opportunity**: We can be the PMS that **integrates** with BILT to offer both PM operations AND tenant value!

---

## 🎉 Milestone: 223+ Skills!

With BILT, we've added the consumer loyalty dimension:

| Metric | Before | After |
|--------|--------|-------|
| **Total Skills** | 214 | 223 |
| **Competitors** | 18 | 19 |
| **Categories** | 5 | 6 (+ Consumer Loyalty) |
| **Knowledge Gaps** | 130+ | 137+ |

