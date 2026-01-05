# PriceLabs - Skill Inventory

> **Source**: PriceLabs Complete PRD (1).md
> **Analysis Date**: January 2026
> **Focus**: Dynamic Pricing & Revenue Management

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 42 |
| **New Unique Skills** | 12 |
| **Overlapping with Registry** | 30 |
| **Knowledge Gaps Identified** | 10 |

---

## 🆕 Unique Skills (New to Registry)

### 1. SKILL-145: hyper-local-pulse-algorithm
- **Priority**: P0
- **Description**: Proprietary algorithm generating optimized daily pricing based on hyper-local (0.5-5km radius) market conditions
- **Key Differentiator**: Most granular pricing algorithm in market - focuses on neighborhood-level data, not city-wide

### 2. SKILL-146: four-way-event-detection
- **Priority**: P0
- **Description**: Industry-first redundant event detection using 4 independent signals
- **4 Methods**:
  1. YoY Pacing comparison
  2. Early demand signals (booking surge)
  3. Competitor pricing spikes (60%+ raise)
  4. Hotel price indicators (Booking.com)

### 3. SKILL-147: price-elasticity-estimation
- **Priority**: P1
- **Description**: Determine how sensitive demand is to price changes at neighborhood level
- **Key Differentiator**: UNIQUE - No other competitor offers this!

### 4. SKILL-148: dynamic-min-stay-4-methods
- **Priority**: P1
- **Description**: Most comprehensive min-stay optimization with 4 adjustment methods
- **4 Methods**:
  1. Gap-filling (detect & fill short gaps)
  2. Lead-time based (far-out vs last-minute)
  3. Demand-based (high occ → raise, low → lower)
  4. Adjacent day consideration

### 5. SKILL-149: twelve-price-customization-options
- **Priority**: P1
- **Description**: Most comprehensive price customization framework with 12 options
- **Options**: Base Price, Seasonal, Lead-Time, Day-of-Week, LOS Discounts, OTA-Specific, Event-Based, Occupancy-Based, Weekday/Peak, Foreign Currency, Cleaning Fee Factor, Bulk Updates

### 6. SKILL-150: automation-rules-engine
- **Priority**: P1
- **Description**: Conditional logic for pricing/availability without manual intervention
- **6 Rule Types**: Occupancy-based, Pacing, Event, Booking window, Channel-specific, Time-based

### 7. SKILL-151: pacing-analysis-yoy
- **Priority**: P1
- **Description**: Forward-looking booking trajectory and YoY forecast analysis
- **Metrics**: Current vs prior year pace, Booking window analysis, Lead-time distribution, Revenue projection

### 8. SKILL-152: revenue-estimator-pro
- **Priority**: P2
- **Description**: Investment analysis tool for new properties or portfolio evaluation
- **Key Differentiator**: UNIQUE - No other competitor offers this!

### 9. SKILL-153: pms-integration-management-161
- **Priority**: P0
- **Description**: Most extensive PMS/channel manager integration ecosystem
- **Count**: 161+ integrations (second only to Cloudbeds' 200+)

### 10. SKILL-154: team-management-6-roles
- **Priority**: P1
- **Description**: Enterprise-grade role-based access control with 6 distinct roles
- **6 Roles**: Account Owner, Account Administrator, Revenue Manager, Property Manager, View-Only/Analyst, Integration Manager

### 11. SKILL-155: comp-set-management
- **Priority**: P1
- **Description**: Sophisticated comparable property selection and monitoring
- **Max Comps**: 350 (highest in market)

### 12. SKILL-156: market-dashboards-free
- **Priority**: P1
- **Description**: Free competitive benchmarking and market analysis dashboards
- **8 KPIs**: ADR, Occupancy, RevPAR, Annual Revenue, Booking Velocity, Occupancy Heatmap, ADR Trends, Competitive Positioning

---

## 🔄 Overlapping Skills (Already in Registry)

| Skill ID | Name | Registry Match | Notes |
|----------|------|----------------|-------|
| Dynamic Pricing | Multiple algorithms | SKILL-003 | Registry has general; PriceLabs is BEST |
| Seasonal Pricing | Profiles | SKILL-044 | PriceLabs more granular |
| Last-Minute Discounts | Auto-drop | SKILL-045 | Similar |
| LOS Discounts | Tiered | SKILL-048 | PriceLabs has 12 tiers |
| Market Analysis | Comp-set | SKILL-004 | PriceLabs superior |
| Multi-Property | Portfolio | SKILL-062 | Similar |
| Channel-Specific | OTA markup | SKILL-043 | PriceLabs has OTA-specific strategy |
| Event Detection | Demand surge | SKILL-033 | PriceLabs 4-way is BEST |
| Revenue Reports | Analytics | SKILL-052 | PriceLabs has pacing |
| Calendar Sync | PMS integration | SKILL-029 | PriceLabs has 161+ |
| Demand Forecasting | AI-based | SKILL-135 | Cloudbeds/PriceLabs similar |

---

## 🏆 Best-in-Class Features

PriceLabs leads the market in:

| Feature | Why Best | Notes |
|---------|----------|-------|
| **Hyper-Local Pricing** | 0.5-5km radius vs city-wide | No one else does this |
| **Event Detection** | 4-way redundant signals | Most reliable |
| **Price Elasticity** | Unique capability | No competitor |
| **Min-Stay Optimization** | 4 methods vs 1-2 | Most flexible |
| **Price Customization** | 12 options vs 6-8 | Most comprehensive |
| **Comp-Set Size** | 350 properties | Largest in market |
| **Market Dashboards** | Free with 8 KPIs | Others charge |
| **Forecast Accuracy** | <12% MAPE | Industry-leading |

---

## 📊 Feature Categories

| Category | Features | Priority |
|----------|----------|----------|
| **Pricing Algorithm** | 4 | P0-P1 |
| **Event Detection** | 2 | P0 |
| **Customization** | 3 | P1 |
| **Automation** | 2 | P1 |
| **Analytics** | 3 | P1-P2 |
| **Integrations** | 2 | P0-P1 |
| **Access Control** | 1 | P1 |

---

## 🎯 Impact on Our Platform

### Revenue Management Suite
PriceLabs provides the most sophisticated pricing engine. Recommendation:
- **Adopt**: HLP algorithm structure, 4-way event detection, elasticity modeling
- **Integrate**: 161+ PMS connections via their API layer
- **Differentiate**: Combine with AI communication for "Revenue Concierge"

### Key Architecture Insight
PriceLabs is **pricing-focused only** - no communication, operations, or accounting. This validates our **unified platform** strategy: one system that combines:
- PriceLabs-level pricing intelligence
- Cloudbeds-level channel distribution
- Guesty-level operations management
- Besty/Inntelo-level AI communication

---

## Next Steps

1. **Capture HLP Algorithm Knowledge** - How exactly does hyper-local radius selection work?
2. **4-Way Event Detection Logic** - Document the confidence scoring system
3. **Elasticity Model Training** - What data is needed? How often updated?
4. **Comp-Set Selection Criteria** - How are 350 comps ranked/filtered?
