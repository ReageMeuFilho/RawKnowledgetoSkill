# Stage 2: Engineering Specification Prompt
## GAP-PL-002: Event Detection System

**Gap ID**: GAP-PL-002  
**Related Skills**: SKILL-146 (Event Detection), SKILL-147 (Surge Pricing)  
**Priority**: P0 (MVP)  
**Date**: 2026-01-06

---

## Context for Engineering Agent

You are an expert software engineer creating a detailed engineering specification for an **Event Detection System** that automatically identifies demand spikes and triggers surge pricing for short-term rentals (STRs).

### Research Summary

The Research Agent has documented PriceLabs' four-way signal architecture:
1. **YoY Pacing Signal** - Compares current bookings vs same date last year
2. **Booking Velocity Signal** - Monitors recent booking activity spikes
3. **Competitor Price Signal** - Tracks competitor pricing changes
4. **Hotel ADR Signal** - Monitors hotel rate changes in area

The system must detect both **known events** (from calendars) and **unknown events** (via anomaly detection), apply confidence scoring, and trigger surge pricing with appropriate multipliers.

---

## YOUR TASK

Create a **comprehensive engineering specification** that an implementation team can use to build this Event Detection System. The specification must cover ALL 20 sections below with the depth and detail shown in the examples.

---

## SECTION 1: Executive Summary

**Requirements:**
- System overview in 2-3 paragraphs
- Key capabilities summary
- Integration touchpoints
- Expected business impact (ADR lift, detection rates)

---

## SECTION 2: Four-Way Signal Architecture

**Document for EACH of the 4 signals:**

### 2.1 YoY Pacing Signal
```
Required Details:
- Data collection methodology
- Calculation formula with variables
- Normalization approach (seasonality, market growth)
- Threshold definition for "anomaly" (e.g., +30% above baseline)
- Update frequency
- Edge cases (new markets without historical data)
```

### 2.2 Booking Velocity Signal
```
Required Details:
- Measurement windows (hourly, daily, weekly)
- Baseline calculation
- Spike detection algorithm
- Market-wide vs property-specific aggregation
- Cancellation handling
```

### 2.3 Competitor Price Signal
```
Required Details:
- Data sources (Airbnb, Vrbo, etc.)
- Comp set definition logic
- Price change detection algorithm
- Outlier filtering (avoid 1-2 listing noise)
- Geographic scoping
```

### 2.4 Hotel ADR Signal
```
Required Details:
- Hotel data sources (Booking.com, etc.)
- Geographic radius determination
- Hotel category filtering
- ADR baseline calculation
- Correlation with STR demand
```

---

## SECTION 3: Confidence Scoring Algorithm

**Document the signal combination logic:**

### 3.1 Signal Weighting
```yaml
required_specification:
  - Weight per signal (YoY, Velocity, Competitor, Hotel)
  - Justification for weights
  - Dynamic weight adjustment rules
  - Minimum signals required for detection
```

### 3.2 Confidence Score Calculation
```
Provide:
- Mathematical formula
- Score normalization (0-100 or 0-1)
- Confidence tier definitions:
  - Low (60-70%): Actions taken
  - Medium (70-85%): Actions taken
  - High (85-100%): Actions taken
```

### 3.3 False Positive Prevention
```
Document mechanisms:
- Multi-signal validation rules
- Outlier detection and exclusion
- Human review triggers
- Self-correction feedback loop
- Target false positive rate (<5%)
```

---

## SECTION 4: Known Event Detection

### 4.1 Event Calendar Integration
```yaml
external_apis:
  eventbrite:
    endpoint: ""
    data_fields: []
    rate_limits: ""
    refresh_frequency: ""
    
  songkick:
    endpoint: ""
    data_fields: []
    
  sports_leagues:
    mlb: {}
    nfl: {}
    nba: {}
    nhl: {}
    
  government_calendars:
    integration_method: ""
```

### 4.2 Event Classification Schema
```json
{
  "categories": [
    {
      "type": "concert",
      "typical_radius_km": 0,
      "typical_duration_days": 0,
      "booking_pattern": "",
      "price_multiplier_range": [0, 0]
    }
  ]
}
```

### 4.3 Impact Modeling
```
Document algorithms for:
- Attendance estimation
- Geographic radius calculation
- Duration impact on adjacent nights
- Price multiplier determination
- Historical impact data usage
```

---

## SECTION 5: Unknown Event Detection (Anomaly Detection)

### 5.1 Baseline Modeling
```
Specify:
- Time series decomposition method (STL, LOESS, etc.)
- Seasonality extraction
- Trend component handling
- Residual analysis
```

### 5.2 Anomaly Detection Algorithm
```
Document:
- Statistical method (z-score, percentile, IQR)
- Threshold values (e.g., z > 2.5)
- Rolling window configuration
- Multi-metric anomaly correlation
```

### 5.3 Event Discovery Pipeline
```
Workflow:
1. Anomaly detected → 
2. Automated event search (query Eventbrite, etc.) →
3. RM team notification →
4. Event classification →
5. Database update
```

---

## SECTION 6: Surge Pricing Implementation

### 6.1 Price Adjustment Algorithm
```python
# Provide pseudocode:
def calculate_surge_price(base_price, event, confidence_score):
    """
    Calculate the surge price for a listing on an event date.
    
    Args:
        base_price: Dynamic base price from SKILL-103
        event: Event object with classification and impact data
        confidence_score: 0-1 confidence from detection
        
    Returns:
        surge_price: Final adjusted price
        multiplier: Applied multiplier
    """
    pass
```

### 6.2 Distance-Based Multipliers
```
Define tier structure:
- Tier 1: 0-1 mile from venue → multiplier X
- Tier 2: 1-5 miles → multiplier Y
- Tier 3: 5-15 miles → multiplier Z
- Tier 4: 15+ miles → no adjustment
```

### 6.3 Timing Logic
```
Specify:
- Advance application rules
- Lead time effect on multiplier
- Event decay algorithm (as date approaches)
- Post-event normalization
```

### 6.4 Constraints
```
Document:
- Min/max price bound enforcement
- Owner override handling
- Regulatory compliance checks
- Maximum multiplier caps by market
```

---

## SECTION 7: Data Model

### 7.1 Event Entity
```sql
-- Provide complete schema:
CREATE TABLE events (
    event_id UUID PRIMARY KEY,
    name VARCHAR(255),
    type VARCHAR(50),
    -- ... all fields with types, constraints, indexes
);
```

### 7.2 Signal Entity
```sql
-- Provide complete schema with time-series optimization
```

### 7.3 Price Adjustment Entity
```sql
-- Provide complete schema linking events to listings
```

### 7.4 Entity Relationships
```
Provide ER diagram in text format showing:
- Event ↔ Market relationships
- Signal ↔ Event relationships
- Price Adjustment ↔ Listing relationships
```

---

## SECTION 8: API Specification

### 8.1 Event Detection API
```yaml
# OpenAPI format
paths:
  /api/v1/events/detect:
    post:
      summary: "Trigger event detection for market"
      requestBody: {}
      responses: {}
      
  /api/v1/events/{market_id}:
    get:
      summary: "Get detected events for market"
```

### 8.2 Surge Pricing API
```yaml
# OpenAPI format
paths:
  /api/v1/pricing/surge:
    post:
      summary: "Calculate surge price for listing/date"
      
  /api/v1/pricing/surge/bulk:
    post:
      summary: "Bulk surge price calculation"
```

### 8.3 Event Management API
```yaml
# For user-reported events
paths:
  /api/v1/events/report:
    post:
      summary: "User reports new event"
      
  /api/v1/events/override:
    post:
      summary: "Override event pricing"
```

---

## SECTION 9: Integration Requirements

### 9.1 External Data Sources
```yaml
integrations:
  eventbrite:
    type: "REST API"
    authentication: ""
    rate_limit: ""
    retry_strategy: ""
    
  hotel_data:
    source: "Booking.com scraping / API"
    legal_considerations: ""
    
  competitor_pricing:
    source: "Internal Market Dashboard"
    refresh_frequency: ""
```

### 9.2 Internal System Integration
```yaml
internal_systems:
  skill_102_demand_forecasting:
    interface: ""
    data_flow: ""
    
  skill_103_price_optimization:
    interface: ""
    data_flow: ""
    
  pms_sync:
    interface: ""
    sync_frequency: ""
```

---

## SECTION 10: User Interface Requirements

### 10.1 Event Calendar View
```
Wireframe description:
- Layout structure
- Event card components
- Filtering options
- Color coding for event types
- Unknown event indication
```

### 10.2 Event Detail Modal
```
Components:
- Event information display
- Impact radius visualization (map)
- Historical comparison charts
- Override controls
```

### 10.3 Report Event Form
```
Form fields:
- Event name (required)
- Dates (required)
- Location (required)
- Expected attendance (optional)
- Impact estimate (dropdown)
- Supporting links (optional)
```

---

## SECTION 11: Processing Pipeline

### 11.1 Daily Detection Pipeline
```
Define Temporal workflow:
- Step 1: Fetch external event data
- Step 2: Calculate signals for all dates
- Step 3: Run anomaly detection
- Step 4: Match anomalies to known events
- Step 5: Create/update event records
- Step 6: Calculate surge prices
- Step 7: Queue price updates for sync
```

### 11.2 Real-Time Signal Updates
```
Define event-driven triggers:
- New booking received
- Competitor price change detected
- Hotel rate change detected
- User event report submitted
```

---

## SECTION 12: Performance Requirements

### 12.1 Detection SLAs
```yaml
slas:
  detection_latency:
    target: "<24 hours from signal emergence"
    measurement: ""
    
  detection_accuracy:
    target: ">90% of significant events"
    measurement: ""
    
  false_positive_rate:
    target: "<5%"
    measurement: ""
```

### 12.2 System Performance
```yaml
performance:
  signal_calculation:
    target_latency: "<5 seconds per market"
    throughput: "1000 markets/hour"
    
  price_calculation:
    target_latency: "<100ms per listing"
    throughput: "10,000 listings/minute"
```

---

## SECTION 13: Error Handling

### 13.1 Data Source Failures
```
For each external source, define:
- Failure detection
- Fallback strategy
- Alert thresholds
- Recovery procedures
```

### 13.2 Signal Calculation Errors
```
Define handling for:
- Missing historical data
- Incomplete competitor data
- Hotel data unavailable
- Calculation timeouts
```

### 13.3 Pricing Errors
```
Define safeguards:
- Sanity checks on multipliers
- Maximum price caps
- Minimum price floors
- Audit logging
```

---

## SECTION 14: Security Requirements

### 14.1 Data Protection
```
Specify:
- Competitor data storage (anonymization)
- Hotel data compliance
- User override audit trail
- Data retention policies
```

### 14.2 Access Control
```
Define RBAC:
- Event detection service (internal)
- RM team (event management)
- Users (view events, report, override)
- Admin (full control)
```

---

## SECTION 15: Monitoring & Observability

### 15.1 Detection Metrics
```yaml
metrics:
  - name: "events_detected_total"
    type: "counter"
    labels: ["market", "event_type", "detection_method"]
    
  - name: "confidence_score_distribution"
    type: "histogram"
    
  - name: "detection_lead_time_days"
    type: "histogram"
```

### 15.2 Pricing Metrics
```yaml
metrics:
  - name: "surge_multiplier_applied"
    type: "histogram"
    labels: ["market", "event_type"]
    
  - name: "revenue_impact_pct"
    type: "gauge"
```

### 15.3 Alerts
```yaml
alerts:
  - name: "EventDetectionDown"
    condition: "No events detected in 24h"
    
  - name: "HighFalsePositiveRate"
    condition: "FP rate > 10% in 7d window"
    
  - name: "ExternalAPIFailure"
    condition: "API error rate > 20%"
```

---

## SECTION 16: Testing Requirements

### 16.1 Signal Calculation Tests
```
Test cases:
- Normal market conditions → no event detected
- YoY pacing +40% → medium confidence
- All 4 signals positive → high confidence
- Single signal spike → low confidence
```

### 16.2 Event Detection Tests
```
Test cases:
- Known event in database → correctly applied
- Unknown event (anomaly) → discovered and classified
- False positive scenario → filtered out
- Event cancellation → pricing reverted
```

### 16.3 Integration Tests
```
End-to-end scenarios:
- External API data → detection → pricing → PMS sync
- User reports event → RM review → approved → pricing applied
```

---

## SECTION 17: Deployment Configuration

### 17.1 Service Architecture
```yaml
services:
  event_detection_service:
    replicas: 3
    resources:
      cpu: "2"
      memory: "4Gi"
    scaling:
      metric: "queue_depth"
      
  surge_pricing_service:
    replicas: 2
    resources:
      cpu: "1"
      memory: "2Gi"
```

### 17.2 Environment Variables
```yaml
config:
  EVENTBRITE_API_KEY: ""
  SONGKICK_API_KEY: ""
  DETECTION_CONFIDENCE_THRESHOLD: "0.7"
  MAX_SURGE_MULTIPLIER: "3.0"
  # ... all configurable parameters
```

---

## SECTION 18: Implementation Phases

### Phase 1: Foundation (Weeks 1-4)
```
- Data model implementation
- Signal calculation framework
- Basic YoY pacing and velocity signals
- Known event database seeding
```

### Phase 2: Detection (Weeks 5-8)
```
- Confidence scoring algorithm
- Anomaly detection implementation
- Event classification system
- RM dashboard for event management
```

### Phase 3: Pricing (Weeks 9-12)
```
- Surge pricing algorithm
- Distance-based multipliers
- Integration with SKILL-103
- User override system
```

### Phase 4: Polish (Weeks 13-16)
```
- UI event calendar
- Reporting and analytics
- Performance optimization
- Production hardening
```

---

## SECTION 19: Competitive Differentiation

**Document how this implementation exceeds competitors:**

| Feature | PriceLabs | Wheelhouse | Beyond | Our Implementation |
|---------|-----------|------------|--------|-------------------|
| Signal sources | 4 | 2-3 | 3 | 4+ |
| Hotel data | Yes | Yes | No | Yes |
| Search data | No | No | Yes | Future |
| UI transparency | High | Medium | Low | High |
| User event reporting | Yes | No | No | Yes |

---

## SECTION 20: Appendices

### A. Event Type Reference
```
Complete list of event categories with default parameters
```

### B. Market Configuration
```
Per-market tuning parameters and defaults
```

### C. API Error Codes
```
Comprehensive error code reference
```

### D. Glossary
```
Technical terms and definitions
```

---

## OUTPUT REQUIREMENTS

Your engineering specification must:

1. **Be Implementation-Ready** - An engineer should be able to build from this
2. **Include All Code Examples** - Schemas, pseudocode, API specs
3. **Cover Edge Cases** - Document how to handle unusual situations
4. **Provide Performance Targets** - Specific numbers for SLAs
5. **Enable Testing** - Clear test cases for validation

**Target Length**: 5,000-10,000 lines comprehensive specification

---

## REFERENCE DOCUMENTS

The following research has been completed:

1. **Knowledge Document**: `knowledge/pricing/KD-PL-002-event-detection.md`
   - Four-way signal architecture
   - Confidence scoring methodology
   - Data model schemas (Event, Signal, Price Adjustment)
   - Performance metrics targets
   - Competitive analysis

2. **Related Skills**:
   - SKILL-102: Demand Forecasting (integration point)
   - SKILL-103: Price Optimization (integration point)

3. **Architecture Documents**:
   - `docs/architecture/LAYER4_SKILLS_ARCHITECTURE.md`
   - `docs/COMPLETE_TECHNICAL_ARCHITECTURE.md`

