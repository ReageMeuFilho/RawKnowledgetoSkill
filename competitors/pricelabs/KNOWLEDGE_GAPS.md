# PriceLabs - Knowledge Gaps

> **Source**: PriceLabs Complete PRD (1).md
> **Analysis Date**: January 2026
> **Total New Gaps**: 10

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 3 | Algorithm core |
| **P1 - Important** | 5 | Optimization logic |
| **P2 - Nice-to-have** | 2 | Analytics |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-PL-001: Hyper-Local Pulse Algorithm Mathematics

**Skill**: SKILL-145 (hyper-local-pulse-algorithm)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Radius Selection Logic**
   - How does system choose 0.5km vs 2km vs 5km radius?
   - What property density threshold triggers radius expansion?
   - How is urban vs rural detected?

2. **Demand Forecasting Model**
   - What features drive the <12% MAPE accuracy?
   - How is seasonality weighted?
   - What's the training window (30 days? 365 days? 3 years?)

3. **Price Optimization Formula**
   - Base price × demand factor × competition factor × elasticity
   - What are the weight coefficients?
   - How is "optimal" defined (max revenue vs max occupancy)?

**Ideal Source**:
- [ ] PriceLabs white paper or documentation
- [ ] Academic papers on STR dynamic pricing
- [ ] Expert interviews with revenue managers

---

### GAP-PL-002: Four-Way Event Detection System

**Skill**: SKILL-146 (four-way-event-detection)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Signal Integration**
   - How are YoY pacing signals calculated?
   - What threshold triggers "booking surge" detection?
   - How is competitor pricing spike defined (60%+ from what baseline?)
   - Which hotel data sources (Booking.com API? Scraping?)

2. **Confidence Scoring Algorithm**
   - How do 4 signals combine into confidence %?
   - Are signals weighted differently?
   - What triggers false positive filtering?

3. **Event Classification**
   - Concert, Conference, Festival, Sports, Holiday categories
   - How are dates automatically extracted?
   - How is event impact radius determined?

**Ideal Source**:
- [ ] PriceLabs event detection documentation
- [ ] Expert interviews about event pricing strategy
- [ ] Historical event data with pricing impact

---

### GAP-PL-003: Price Elasticity Estimation Model

**Skill**: SKILL-147 (price-elasticity-estimation)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Elasticity Calculation**
   - Formula: % change in bookings / % change in price
   - What time window is used?
   - How is property-level vs market-level separated?

2. **Elasticity Coefficient Interpretation**
   - What does -0.5 vs -1.5 vs -2.0 mean practically?
   - How does this translate to pricing action?
   - At what point is demand "inelastic"?

3. **Data Requirements**
   - Minimum booking history needed?
   - How often is elasticity recalculated?
   - How are seasonal elasticity variations handled?

**Ideal Source**:
- [ ] Economic literature on price elasticity
- [ ] PriceLabs methodology documentation
- [ ] Revenue manager practical examples

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-PL-004: Dynamic Minimum Stay Optimization

**Skill**: SKILL-148 (dynamic-min-stay-4-methods)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Gap-Fill Logic**
   - What gap sizes trigger action (1 night? 2?)
   - How deep is the discount for gap-filling?
   - When is it better to leave a gap vs fill it?

2. **Lead-Time Based Rules**
   - What lead-time thresholds are used?
   - How does min-stay decrease as check-in approaches?
   - Typical curve: 3-night min at 90 days → 1-night at 3 days?

3. **Demand-Based Adjustment**
   - What occupancy level triggers min-stay increase?
   - How quickly does it respond to demand spikes?

**Ideal Source**:
- [ ] Property manager interviews
- [ ] Channel manager documentation on min-stay sync
- [ ] Historical booking data with min-stay impact

---

### GAP-PL-005: Customization Option Logic

**Skill**: SKILL-149 (twelve-price-customization-options)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Option Stacking Order**
   - In what order are 12 customizations applied?
   - Can they conflict? How are conflicts resolved?
   - What's the formula: Base × Seasonal × DayOfWeek × Event × ...?

2. **Typical Ranges**
   - Seasonal adjustment: +/- what %?
   - Day-of-week swing: Weekend vs weekday spread?
   - OTA-specific markup: Airbnb vs Vrbo vs Booking.com?

**Ideal Source**:
- [ ] Revenue manager configuration examples
- [ ] PriceLabs pricing rule documentation
- [ ] Channel-specific markup best practices

---

### GAP-PL-006: Automation Rules Engine

**Skill**: SKILL-150 (automation-rules-engine)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Rule Evaluation**
   - How often are rules evaluated? (Real-time? Daily?)
   - What's the rule execution priority?
   - Can rules trigger other rules (chains)?

2. **Common Rule Patterns**
   - IF occupancy > 80% THEN +15% - what's typical?
   - IF lead_time < 7 days AND occupancy < 50% THEN -20%?
   - What are dangerous rule combinations to avoid?

**Ideal Source**:
- [ ] Power user rule configurations
- [ ] PriceLabs automation documentation
- [ ] Revenue management case studies

---

### GAP-PL-007: Pacing Analysis Methodology

**Skill**: SKILL-151 (pacing-analysis-yoy)
**Status**: 🟡 NEEDED

**What We Need**:
1. **YoY Calculation**
   - How is same-period comparison handled?
   - How are new properties (no YoY data) handled?
   - What about properties with major changes (added pool)?

2. **Risk Zone Identification**
   - What pacing rate triggers "at risk" status?
   - How far ahead does analysis project?

**Ideal Source**:
- [ ] PriceLabs pacing dashboard documentation
- [ ] Revenue management industry benchmarks
- [ ] Historical pacing vs actual data

---

### GAP-PL-008: Comp-Set Selection Algorithm

**Skill**: SKILL-155 (comp-set-management)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Selection Criteria Weighting**
   - How are 350 comps ranked from thousands of candidates?
   - Is proximity weighted more than bedroom count?
   - How is "similarity" calculated?

2. **Dynamic Comp Adjustment**
   - How often is comp-set refreshed?
   - When are outliers excluded?
   - How are new listings incorporated?

**Ideal Source**:
- [ ] PriceLabs comp-set documentation
- [ ] Revenue manager comp-set strategy
- [ ] Market data provider methodologies

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-PL-009: Revenue Estimator Accuracy

**Skill**: SKILL-152 (revenue-estimator-pro)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Estimation Model**
   - What data inputs drive the estimate?
   - What's the accuracy rate? (±10%? ±25%?)
   - How long before estimates stabilize for new properties?

**Ideal Source**:
- [ ] PriceLabs revenue estimator validation data
- [ ] Investor case studies
- [ ] Property acquisition best practices

---

### GAP-PL-010: Market Dashboard KPI Calculations

**Skill**: SKILL-156 (market-dashboards-free)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **KPI Definitions**
   - Exactly how is market RevPAR calculated?
   - What properties are included in "market"?
   - How are outliers handled?

**Ideal Source**:
- [ ] PriceLabs dashboard methodology
- [ ] Industry standard KPI definitions
- [ ] Market data provider documentation

---

## 📋 Knowledge Collection Plan

### Phase 1: Algorithm Core (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-PL-001 | Academic papers + Revenue manager interviews | TBD |
| GAP-PL-002 | Event pricing expert + Historical data | TBD |
| GAP-PL-003 | Economics literature + PriceLabs docs | TBD |

### Phase 2: Optimization Logic (Week 3-4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-PL-004 | Property manager interviews | TBD |
| GAP-PL-005 | Configuration examples | TBD |
| GAP-PL-006 | Power user documentation | TBD |
| GAP-PL-007 | Industry benchmarks | TBD |
| GAP-PL-008 | Market data methodology | TBD |

### Phase 3: Analytics (Week 5)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-PL-009 | Validation data | TBD |
| GAP-PL-010 | Industry standards | TBD |

---

## 🎯 Impact Assessment

PriceLabs gaps are **highly technical** compared to other competitors:

| Competitor | Gap Nature | Difficulty |
|------------|------------|------------|
| Guesty | Operational workflows | Medium |
| Inntelo | AI training examples | Medium |
| **PriceLabs** | **Mathematical models** | **High** |

### Recommendation
PriceLabs knowledge requires **data science expertise** or **revenue management consultants** rather than general property managers.

Consider:
1. Hiring STR revenue management consultant
2. Licensing PriceLabs API instead of rebuilding
3. Academic partnership for pricing algorithm research
