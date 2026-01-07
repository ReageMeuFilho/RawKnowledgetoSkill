# Research Prompt: Phase 2 Group 3 - Revenue Optimization

> **For**: AI Research Agent
> **Output**: Knowledge Document → `knowledge/pricing/KD-PHASE2-G3-revenue-optimization.md`
> **Priority**: HIGHEST (Direct revenue impact)
> **Date**: January 2026

---

## 🎯 Research Objective

Research and document comprehensive knowledge for implementing **7 Revenue Optimization skills** that enhance pricing intelligence, demand forecasting, and booking optimization capabilities.

---

## 📋 Skills to Research

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| SKILL-095 | competitor-rate-monitoring | pricing | Real-time competitor rate scraping and analysis |
| SKILL-096 | demand-sensing | pricing | Demand forecasting with event and seasonality detection |
| SKILL-097 | length-of-stay-optimization | pricing | Minimum/maximum stay optimization algorithms |
| SKILL-098 | last-minute-pricing | pricing | Gap night discounting and last-minute deals |
| SKILL-099 | seasonal-strategy | pricing | Seasonal pricing strategy management |
| SKILL-100 | group-booking-pricing | pricing | Group/corporate rate management |
| SKILL-088 | overbooking-management | booking | Strategic overbooking with backup logic |

---

## 🔍 Research Questions Per Skill

### SKILL-095: Competitor Rate Monitoring

**Key Questions**:
1. How do competitors like PriceLabs, Beyond Pricing, and Wheelhouse scrape competitor rates?
2. What data sources are used (OTA APIs, web scraping, aggregators)?
3. How is competitor matching done (location, amenities, capacity)?
4. What is the update frequency and data freshness requirement?
5. How are rate trends visualized and acted upon?
6. What legal/ToS considerations exist for rate scraping?

**Research Sources**:
- PriceLabs documentation on comp sets
- Beyond Pricing market intelligence
- AirDNA competitor analysis features
- Mashvisor, AllTheRooms data providers
- STR (Smith Travel Research) methodology

### SKILL-096: Demand Sensing

**Key Questions**:
1. What signals indicate demand changes (search volume, booking velocity, events)?
2. How is local event detection implemented (Eventbrite, sports, concerts)?
3. What machine learning models work best for demand forecasting?
4. How far ahead can demand be reliably predicted?
5. How does weather integration affect demand prediction?
6. What is the accuracy target for demand forecasting?

**Research Sources**:
- PriceLabs HLP algorithm (already researched in MVP - reference SPEC-SKILL-101-HLP-PRICING.md)
- Beyond Pricing demand prediction
- Revenue management literature (Cornell hospitality)
- Event detection providers (PredictHQ, Eventbrite API)

### SKILL-097: Length of Stay Optimization

**Key Questions**:
1. How do minimum stay requirements affect revenue vs. occupancy?
2. What algorithms optimize min/max stay for gap filling?
3. How do different OTAs handle minimum stay (Airbnb vs. Booking.com)?
4. When should orphan day prevention override minimum stay?
5. How does seasonality affect optimal length of stay?

**Research Sources**:
- PriceLabs minimum stay optimization
- Wheelhouse gap night strategies
- Revenue management case studies
- Airbnb host forums on minimum stay

### SKILL-098: Last-Minute Pricing

**Key Questions**:
1. What discount curves work best for last-minute bookings?
2. How do you balance urgency vs. cannibalization?
3. What is the optimal timing window for last-minute deals?
4. How do competitors implement flash sales?
5. What notification strategies drive last-minute conversions?

**Research Sources**:
- Booking.com last-minute deals
- Hotel flash sale platforms
- PriceLabs urgent booking discounts
- Dynamic pricing literature

### SKILL-099: Seasonal Strategy

**Key Questions**:
1. How do you define seasons for different markets?
2. What is the planning cycle for seasonal pricing?
3. How do you handle shoulder season transitions?
4. What role do historical patterns play vs. forward-looking signals?
5. How do multi-year trends affect seasonal strategies?

**Research Sources**:
- AirDNA seasonal patterns
- Tourism board seasonality data
- Revenue management textbooks
- PriceLabs seasonal adjustments

### SKILL-100: Group Booking Pricing

**Key Questions**:
1. How are group rates calculated (per night, total stay)?
2. What negotiation flexibility is standard for groups?
3. How do corporate accounts differ from leisure groups?
4. What deposit and cancellation terms apply?
5. How is room block inventory managed?

**Research Sources**:
- Guesty group booking features
- Hotel group sales practices
- Corporate travel booking platforms
- RFP response templates

### SKILL-088: Overbooking Management

**Key Questions**:
1. What cancellation rate data drives overbooking decisions?
2. How is overbooking risk calculated by property type?
3. What is the guest relocation protocol when overbooking fails?
4. What compensation is standard for relocated guests?
5. How do airlines/hotels manage overbooking legally?

**Research Sources**:
- Hotel revenue management practices
- Airline overbooking algorithms
- Guest relocation costs and policies
- Legal requirements (EU261, US regulations)

---

## 🏗️ Architecture Context

**Important**: All skills must align with Citadel OS architecture:

### Dependencies (From Phase 1)
- **SKILL-007-010**: Booking & Calendar (availability data)
- **SKILL-101-103**: HLP Dynamic Pricing (base pricing engine)
- **SKILL-146**: Event Detection System (demand signals)
- **SKILL-024-027**: Channel Distribution (rate pushing)

### Technology Stack
| Component | Technology | Purpose |
|-----------|------------|---------|
| Pricing Engine | Python (NumPy/Pandas) | Rate calculations |
| ML Models | scikit-learn, Prophet | Demand forecasting |
| Data Pipeline | Redpanda | Event streaming |
| Caching | Redis | Rate caching |
| Workflow | Temporal | Pricing workflows |
| Storage | PostgreSQL + TigerBeetle | Pricing history + financials |

### MCP Servers Required
```yaml
mcp_servers:
  - mcp://pricing/calculate-rate
  - mcp://pricing/competitor-data
  - mcp://demand/forecast
  - mcp://channel/push-rates
  - mcp://analytics/revenue-metrics
```

---

## 📄 Output Format

Create a comprehensive knowledge document with:

### Required Sections:
1. **Executive Summary** - Key findings overview
2. **Skill-by-Skill Analysis** - Deep dive for each of 7 skills
3. **Best-in-Class Implementations** - Who does each feature best
4. **Technical Architecture** - Data flows, algorithms, integrations
5. **Data Requirements** - What data each skill needs
6. **ML/AI Components** - Models and training requirements
7. **Integration Points** - External APIs and data sources
8. **Competitive Landscape** - Feature comparison matrix
9. **Implementation Priorities** - Recommended build order
10. **Open Questions** - Areas needing clarification

### Quality Requirements:
- Minimum 2,000 lines
- At least 30 citations/sources
- Include code snippets where helpful
- Include data schemas
- Include flowcharts/diagrams (mermaid format)

---

## 🔗 Reference Documents

Before starting, review these existing documents:

1. **HLP Pricing Spec**: `specs/pricing/SPEC-SKILL-101-HLP-PRICING.md`
   - Contains demand forecasting algorithms already specified
   
2. **Event Detection Spec**: `specs/pricing/SPEC-SKILL-146-EVENT-DETECTION.md`
   - Contains event-based demand sensing

3. **Booking Calendar Spec**: `specs/booking/SPEC-SKILL-007-010-BOOKING-CALENDAR.md`
   - Contains availability and reservation logic

4. **Architecture Guide**: `docs/ARCHITECTURE_ALIGNMENT_GUIDE.md`
   - Technology decisions that must be followed

---

## ⏱️ Expected Timeline

- **Research Phase**: 3-4 hours
- **Document Creation**: 2-3 hours
- **Quality Review**: 1 hour
- **Total**: ~8 hours

---

## 📤 Delivery Instructions

1. Save output to: `knowledge/pricing/KD-PHASE2-G3-revenue-optimization.md`
2. Update: `docs/PHASE2_SKILL_TRACKER.md` - Mark Group 3 Stage 1 complete
3. Notify: Ready for Stage 2 (Engineering Prompt creation)

---

**Good luck! This is the highest priority Phase 2 group - direct revenue impact! 💰**

