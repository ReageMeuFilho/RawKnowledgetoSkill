# Stage 1 Research Prompt: Event Detection System

> **Gap ID**: GAP-PL-002
> **Skill ID**: SKILL-146 (four-way-event-detection)
> **Priority**: P0 (MVP Critical)
> **Category**: pricing
> **Created**: January 2026

---

## 📋 QUICK START

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-PL-002 (Event Detection System)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology  
3. This prompt - Detailed research questions

SAVE OUTPUT TO:
knowledge/pricing/KD-PL-002-event-detection.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-PL-002
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-PL-002 Event Detection System" && git push
```

---

## 🎯 EXECUTIVE SUMMARY

### What is Event Detection?

Event Detection is a critical component of dynamic pricing that automatically identifies demand-driving events (concerts, festivals, conferences, sports, holidays) and triggers pricing adjustments. **PriceLabs pioneered the "Four-Way" redundant signal approach** that combines multiple data sources to detect both known and unknown events with high confidence.

### Why This Matters

| Without Event Detection | With Event Detection |
|------------------------|---------------------|
| Miss demand spikes | Capture 20-40% rate increases |
| Manual event research | Automated 24/7 monitoring |
| Reactive pricing | Proactive surge pricing |
| Missed revenue | Optimized ADR |

### Related Skills Already Specified

- **SKILL-101**: HLP Dynamic Pricing (GAP-PL-001) - ✅ COMPLETE
- **SKILL-102**: Demand Forecasting Engine - ✅ COMPLETE  
- **SKILL-103**: Price Elasticity Optimization - ✅ COMPLETE

This gap (GAP-PL-002) fills the **event-driven component** that was identified in the HLP spec but not deeply researched.

---

## 🔬 RESEARCH QUESTIONS

### Section 1: Four-Way Signal Architecture

**CRITICAL**: PriceLabs uses four redundant signals to detect events. We need to understand each signal deeply.

#### 1.1 YoY Pacing Signal
- How is Year-over-Year booking pace calculated?
- What constitutes a "surge" in pacing (e.g., +30% vs baseline)?
- How far back does the comparison window look?
- How is seasonality factored out to isolate event impact?

#### 1.2 Booking Velocity Signal
- What time window measures "booking surge" (hourly? daily?)?
- What velocity threshold triggers detection?
- How are cancellations factored into velocity?
- Is this property-specific or market-wide?

#### 1.3 Competitor Price Signal
- What defines a "competitor price spike" (60%+ from baseline)?
- Which competitors are monitored (comp-set or entire market)?
- How often are competitor prices checked?
- How is the baseline price calculated?

#### 1.4 Hotel ADR Signal
- Which hotel data sources are used (Booking.com, STR data, direct APIs)?
- How are hotel rates correlated with STR demand?
- What hotel types are monitored (luxury, midscale, all)?
- What geographic radius for hotel data?

---

### Section 2: Confidence Scoring Algorithm

#### 2.1 Signal Combination
- How do the 4 signals combine into a confidence percentage?
- Are signals weighted differently (e.g., pacing 40%, velocity 30%, etc.)?
- What's the minimum number of signals needed to trigger?
- Is this a simple average or a more complex model?

#### 2.2 Threshold Definition
- What confidence level triggers "event detected" (70%? 85%)?
- Are there multiple tiers (low, medium, high confidence)?
- How is confidence communicated to users?

#### 2.3 False Positive Handling
- What triggers false positive filtering?
- How are outliers handled (one property booking 10 nights skewing data)?
- What's the false positive rate target?
- How are corrections made when events are misidentified?

---

### Section 3: Known Event Detection

#### 3.1 Event Calendar Integration
- Which event calendar APIs are integrated (Eventbrite, Songkick, etc.)?
- How are local government event calendars accessed?
- What about private/corporate events (conferences)?
- How comprehensive is the event database?

#### 3.2 Event Classification
- What are the event categories?
  - Concerts/Music Festivals
  - Sports (games, tournaments, marathons)
  - Conferences/Trade Shows
  - Cultural/Religious Holidays
  - Local Festivals/Fairs
  - University Events (graduation, move-in)
- How are events tagged with multiple categories?

#### 3.3 Impact Modeling
- How is expected attendance estimated?
- How is event impact radius determined (1 mile, 5 miles, 15 miles)?
- How does event duration affect pricing (1 day vs 3-day festival)?
- Are there event-specific pricing multipliers?

---

### Section 4: Unknown Event Detection (Anomaly Detection)

#### 4.1 Anomaly Definition
- What statistical method detects "unknown" demand spikes?
- How is normal demand baseline established?
- What deviation triggers an anomaly flag?
- How quickly can unknown events be detected?

#### 4.2 Event Discovery
- Once anomaly detected, how is the cause identified?
- Are there feedback loops for user-reported events?
- How are newly discovered events added to the known calendar?
- What's the learning process for new event types?

---

### Section 5: Surge Pricing Implementation

#### 5.1 Price Adjustment Algorithm
- What percentage increase is applied per confidence level?
- Is the surge additive or multiplicative?
- How does surge interact with base dynamic pricing?
- What's the maximum surge cap?

#### 5.2 Timing
- How far in advance is surge pricing applied?
- How does lead time affect surge magnitude?
- When is surge pricing removed (post-event)?
- Is there a cool-down period?

#### 5.3 Constraints
- How are minimum/maximum price bounds enforced during surge?
- How do owner price preferences override surge?
- Are there regulatory considerations (price gouging laws)?

---

### Section 6: Data Model

#### 6.1 Event Schema
```
Research the data structure for:
- Event ID, name, type, category
- Location (lat/long, radius)
- Date/time (start, end, duration)
- Expected attendance
- Confidence score
- Data sources
- Historical pricing impact
```

#### 6.2 Signal Schema
```
Research how signals are stored:
- Signal type (pacing, velocity, competitor, hotel)
- Timestamp
- Value/magnitude
- Confidence contribution
- Geographic scope
```

#### 6.3 Price Adjustment Schema
```
Research how adjustments are tracked:
- Base price
- Surge multiplier
- Event ID association
- Effective date range
- Override status
```

---

### Section 7: User Interface

#### 7.1 Event Calendar View
- How are detected events visualized?
- Can users see confidence scores?
- How are unknown vs known events differentiated?
- What manual override options exist?

#### 7.2 Notifications
- How are users alerted to new events?
- What notification channels (email, SMS, in-app)?
- Can users subscribe to specific event types?

#### 7.3 Manual Event Addition
- Can users add custom events?
- How do user-added events affect pricing?
- What validation exists for user input?

---

### Section 8: Performance Metrics

Research key KPIs:

| Metric | Target | Measurement |
|--------|--------|-------------|
| Event Detection Rate | ? | % of actual events detected |
| False Positive Rate | ? | % of detections that were wrong |
| Detection Lead Time | ? | Days before event detected |
| Revenue Impact | ? | % ADR increase during events |
| Coverage | ? | % of market events detected |

---

### Section 9: Integration Requirements

#### 9.1 External Data Sources
- Eventbrite API
- Songkick API
- Local government calendars
- Sports league APIs (MLB, NFL, NBA, etc.)
- Conference databases
- Hotel rate APIs
- Competitor pricing feeds

#### 9.2 Internal Integration
- How does Event Detection feed into:
  - Demand Forecasting (SKILL-102)
  - Price Optimization (SKILL-103)
  - Calendar sync
  - Rate pushing to OTAs

---

### Section 10: Competitive Analysis

#### 10.1 PriceLabs (Primary)
- What makes their four-way approach unique?
- What's their detection accuracy?
- How long have they had this feature?

#### 10.2 Wheelhouse
- How does their event detection compare?
- Any unique approaches?

#### 10.3 Beyond Pricing
- How do they handle events?
- Any differentiators?

#### 10.4 AirDNA
- What event data do they provide?
- Integration options?

---

## 📚 PRIMARY SOURCES

### Must Check
- [ ] **PriceLabs Help Center** - Event detection documentation
- [ ] **PriceLabs Blog** - Event pricing best practices
- [ ] **YouTube**: "PriceLabs event detection", "PriceLabs surge pricing"
- [ ] **Reddit**: r/airbnb_hosts "event pricing", r/STRowners "PriceLabs events"

### Secondary Sources
- [ ] Wheelhouse documentation on events
- [ ] Beyond Pricing event features
- [ ] AirDNA event data products
- [ ] STR analytics blog posts

### Technical/Academic
- [ ] Academic papers on demand forecasting
- [ ] Event impact analysis methodologies
- [ ] Anomaly detection in time-series data

---

## ✅ DEFINITION OF DONE

Your knowledge document is complete when you can answer:

1. **Architecture**
   - [ ] How do the 4 signals work together?
   - [ ] What's the confidence scoring formula?
   - [ ] How are false positives handled?

2. **Known Events**
   - [ ] Which event calendars are integrated?
   - [ ] How are events classified and tagged?
   - [ ] How is impact radius determined?

3. **Unknown Events**
   - [ ] What statistical method detects anomalies?
   - [ ] How quickly can unknown events be detected?
   - [ ] What's the learning feedback loop?

4. **Surge Pricing**
   - [ ] What multipliers are applied per confidence level?
   - [ ] How does timing affect surge?
   - [ ] What constraints exist?

5. **Data Model**
   - [ ] Event schema defined
   - [ ] Signal schema defined
   - [ ] Adjustment tracking defined

6. **Performance**
   - [ ] Detection accuracy documented
   - [ ] False positive rates known
   - [ ] Revenue impact quantified

---

## 📝 OUTPUT FORMAT

Save your research to: `knowledge/pricing/KD-PL-002-event-detection.md`

Use this structure:

```markdown
# Knowledge Document: Event Detection System

> **Gap ID**: GAP-PL-002
> **Skill ID**: SKILL-146
> **Priority**: P0 (MVP)
> **Stage**: 1 - Research
> **Researcher**: [Your Name/ID]
> **Date**: [Date]
> **Quality Target**: 9.0/10

---

## Executive Summary
[2-3 paragraphs summarizing key findings]

## 1. Four-Way Signal Architecture
### 1.1 YoY Pacing Signal
[Research findings with citations]

### 1.2 Booking Velocity Signal
[Research findings with citations]

### 1.3 Competitor Price Signal
[Research findings with citations]

### 1.4 Hotel ADR Signal
[Research findings with citations]

## 2. Confidence Scoring Algorithm
[Detailed findings]

## 3. Known Event Detection
[Detailed findings]

## 4. Unknown Event Detection (Anomaly)
[Detailed findings]

## 5. Surge Pricing Implementation
[Detailed findings]

## 6. Data Model
[Schema definitions]

## 7. User Interface
[UI/UX findings]

## 8. Performance Metrics
[KPIs and benchmarks]

## 9. Integration Requirements
[External and internal integrations]

## 10. Competitive Analysis
[PriceLabs vs others]

## References
[All sources with URLs]
```

---

## 🎯 SUCCESS CRITERIA

| Criteria | Target |
|----------|--------|
| **Citations** | 30+ authoritative sources |
| **Completeness** | All 10 sections addressed |
| **Technical Depth** | Algorithms, schemas, formulas |
| **Practical** | Actionable for engineering |
| **Quality** | 9.0/10 minimum rating |

---

## 📊 CONTEXT: How This Fits the Pipeline

```
GAP-PL-001 (HLP Algorithm) ✅ COMPLETE
    └── SKILL-101: Hyper-Local Market Definition
    └── SKILL-102: Demand Forecasting
    └── SKILL-103: Price Elasticity

GAP-PL-002 (Event Detection) ⏳ YOU ARE HERE
    └── SKILL-146: Four-Way Event Detection
    └── Feeds into: SKILL-101, SKILL-102, SKILL-103

Together: Complete Dynamic Pricing Engine
```

---

**Good luck! This is a P0 skill critical for MVP. 🚀**


