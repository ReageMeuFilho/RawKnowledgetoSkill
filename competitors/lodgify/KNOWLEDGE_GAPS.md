# Lodgify - Knowledge Gaps

> **Source**: LODGIFY (v2.0)PRD.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 5

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 1 | Website builder design |
| **P1 - Important** | 2 | Widgets, statements |
| **P2 - Nice-to-have** | 2 | Google VR, pricing model |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-LDG-001: Drag-Drop Website Builder Design

**Skill**: SKILL-188 (drag-drop-website-builder)
**Status**: 🔴 BLOCKING FOR SMB

**What We Need**:
1. **Builder Components**
   - What sections/blocks are available?
   - How is drag-drop implemented?
   - What's the component library?

2. **Template System**
   - How are templates structured?
   - What makes a template "VR-optimized"?
   - How is mobile responsiveness achieved?

3. **Booking Engine Integration**
   - How is availability pulled into pages?
   - How does checkout flow work?
   - How are payments integrated?

4. **Branding Customization**
   - What can be customized?
   - Custom CSS support?
   - Domain + SSL automation?

**Why Critical**: If we want to serve SMB market, we need a website builder.

**Ideal Source**:
- [ ] Website builder best practices (Wix, Squarespace patterns)
- [ ] VR-specific website templates
- [ ] Drag-drop editor UX research

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-LDG-002: Embeddable Booking Widget Architecture

**Skill**: SKILL-189 (embeddable-booking-widgets)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Widget Types**
   - Search widget (date + property)
   - Availability calendar
   - Property card/listing
   - Quote calculator
   - Full booking flow

2. **Embedding Methods**
   - JavaScript snippet?
   - iFrame?
   - Web component?
   - What data is passed?

3. **Customization**
   - Styling options
   - Branding match
   - Responsive behavior

**Ideal Source**:
- [ ] Booking widget implementations
- [ ] Embed strategy patterns
- [ ] Cross-origin communication

---

### GAP-LDG-003: Owner Statement Strategy System

**Skill**: SKILL-192 (owner-statement-strategies)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Strategy Definition**
   - What parameters are configurable?
   - How are revenue splits defined?
   - What fee types are supported?

2. **Statement Generation**
   - What time periods?
   - What line items included?
   - What formatting options?

3. **Distribution**
   - Email automation?
   - PDF generation?
   - Owner portal access?

**Ideal Source**:
- [ ] Property management statement examples
- [ ] Owner reporting best practices
- [ ] Statement template designs

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-LDG-004: Google Vacation Rentals Integration

**Skill**: SKILL-190 (google-vacation-rentals-integration)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Integration Requirements**
   - Google VR API documentation
   - Property feed format
   - Availability sync requirements

2. **Booking Flow**
   - How are Google bookings handled?
   - Commission structure?
   - Attribution tracking?

**Ideal Source**:
- [ ] Google Vacation Rentals documentation
- [ ] GVR partner requirements

---

### GAP-LDG-005: Hybrid Pricing Model Design

**Skill**: SKILL-191 (booking-fee-pricing-model)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Fee vs Subscription Balance**
   - At what volume does fee > subscription?
   - How to incentivize upgrade?
   - How to communicate value?

2. **Implementation**
   - How are booking fees tracked?
   - When are fees charged?
   - How is reconciliation handled?

**Ideal Source**:
- [ ] SaaS pricing strategies
- [ ] Marketplace fee models
- [ ] PLG pricing research

---

## 📋 Knowledge Collection Plan

### Phase 1: SMB Foundation (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-LDG-001 | Website builder UX research | TBD |
| GAP-LDG-002 | Embed widget patterns | TBD |

### Phase 2: Owner Features (Week 3)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-LDG-003 | Statement best practices | TBD |

### Phase 3: Distribution (Week 4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-LDG-004 | Google VR documentation | TBD |
| GAP-LDG-005 | SaaS pricing research | TBD |

---

## 🎯 Strategic Priorities

### For SMB Market Entry

If we want to compete with Lodgify at SMB:
1. **Must have**: Simple website builder (GAP-LDG-001)
2. **Should have**: Embeddable widgets (GAP-LDG-002)
3. **Nice to have**: Google VR integration (GAP-LDG-004)

### For Enterprise Focus

If we stay enterprise-only:
- These gaps are **low priority**
- SMB users should use Lodgify → migrate to us at 50+ properties

### Recommended Approach

**Hybrid strategy**:
1. **SMB tier**: Simplified version with website builder
2. **Enterprise tier**: Full platform with all skills
3. **Migration path**: Easy upgrade when portfolio grows

---

## 🏆 Competitive Intelligence

### Lodgify's Moat

1. **Simplicity** - Hardest to replicate
2. **Price** - Race to bottom not sustainable
3. **Website focus** - Clear positioning

### How to Compete

| Approach | Pros | Cons |
|----------|------|------|
| **Match Lodgify** | Capture SMB | Dilute enterprise focus |
| **Partner with Lodgify** | Let them serve SMB, we serve graduates | Revenue share complexity |
| **Ignore SMB** | Focus resources on enterprise | Miss 80% of operators |
| **Freemium model** | Capture SMB free, upsell | Support costs |

**Recommendation**: Build SMB tier with website builder, but keep it separate from enterprise features. Let users "graduate" to full platform.

---

## 📈 Market Size Context

| Segment | % of Operators | Properties | Platform Fit |
|---------|---------------|------------|--------------|
| Hobbyist (1-2) | 60% | 1-2 | Lodgify/Hospitable |
| Small (3-10) | 25% | 3-10 | Lodgify/OwnerRez |
| Mid (11-50) | 10% | 11-50 | Lodgify → Hostaway |
| Enterprise (50+) | 5% | 50+ | Hostaway/Guesty |

**Insight**: Lodgify targets 95% of operators by count (but lower % of revenue).

