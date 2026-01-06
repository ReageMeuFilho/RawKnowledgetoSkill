# Skill Specification: Event Detection System

**Skill ID**: SKILL-146  
**Gap ID**: GAP-PL-002  
**Status**: ✅ SPECIFIED  
**Date**: January 2026  
**Engineering Spec**: `knowledge/pricing/ES-PL-002-event-detection.md` (7,828 lines)

---

## Skill Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Event Detection System |
| **Category** | pricing |
| **Priority** | P0 (MVP) |
| **Effort** | L (16-20 weeks) |
| **Best Implementation** | PriceLabs |

---

## Description

AI-powered demand spike identification and surge pricing system that uses a four-way signal architecture (YoY pacing, booking velocity, competitor pricing, hotel ADR) to automatically detect events and adjust prices to maximize revenue during high-demand periods.

---

## Key Features

### 1. Four-Way Signal Architecture

| Signal | Weight | Purpose |
|--------|--------|---------|
| **YoY Pacing** | 40% | Compare current bookings vs same date previous years |
| **Booking Velocity** | 30% | Measure recent booking rate vs baseline |
| **Competitor Pricing** | 20% | Track competitor rate increases |
| **Hotel ADR** | 10% | Correlate with local hotel rates |

### 2. Event Detection Methods

| Method | Source | Detection Time |
|--------|--------|----------------|
| **Known Events** | Eventbrite, Songkick, Sports APIs | 30+ days advance |
| **Unknown Events** | Anomaly detection (Isolation Forest) | <24 hours |
| **User Reported** | Manual input, feedback loops | Real-time |

### 3. Confidence Scoring

```
Composite = (0.40 × YoY) + (0.30 × Velocity) + (0.20 × Competitor) + (0.10 × Hotel)
+ Correlation Bonus (0.05-0.10 for multi-signal agreement)
```

### 4. Surge Pricing Multipliers

| Distance from Venue | Multiplier | Confidence Level |
|---------------------|------------|------------------|
| < 1 mile | +30% | High: +50% to +150% |
| 1-5 miles | +20% | Medium: +10% to +50% |
| 5-15 miles | +10% | Low: +5% to +10% |
| > 15 miles | +5% | - |

---

## Performance Targets

| Metric | Target |
|--------|--------|
| Detection Rate | >90% for significant events |
| False Positive Rate | <5% |
| Signal Calculation | <5 seconds per market |
| Price Calculation | <100ms per listing |
| Market Processing | 1,000 markets/hour |
| Pricing Capacity | 10,000 listings/minute |
| Detection Latency | <24 hours from signal emergence |

---

## Business Impact

| Metric | Target |
|--------|--------|
| ADR Lift | 10-20% during events |
| Manual Overhead Reduction | 80% |
| Event Coverage | ~100% major events |
| User Price Acceptance | 95% |

---

## Technology Stack

| Component | Technology |
|-----------|------------|
| Backend | Python 3.12+, Flask |
| Signal Processing | NumPy, Pandas |
| ML/Anomaly Detection | scikit-learn (Isolation Forest) |
| Time-Series DB | MongoDB 6.0+ (time-series collections) |
| Transactional DB | PostgreSQL |
| Caching | Redis 7.2+ |
| Infrastructure | AWS ECS, Docker, Terraform |

---

## Data Models

### Event Entity
```json
{
  "event_id": "EVT-2026-001234",
  "name": "Event Name",
  "type": "concert|sports|conference|festival|holiday|local",
  "dates": { "start": "datetime", "end": "datetime" },
  "location": { "venue": "string", "coordinates": [lng, lat] },
  "impact": {
    "estimated_attendance": "number",
    "impact_radius_km": "number",
    "booking_lead_days": "number"
  },
  "confidence_score": "0.0-1.0",
  "source": "eventbrite|songkick|sports_api|anomaly|user_reported"
}
```

### Signal Measurement Entity
```json
{
  "timestamp": "datetime",
  "market_id": "string",
  "target_date": "date",
  "signals": {
    "yoy_pacing": { "value": "number", "confidence": "0.0-1.0" },
    "booking_velocity": { "value": "number", "confidence": "0.0-1.0" },
    "competitor_pricing": { "value": "number", "confidence": "0.0-1.0" },
    "hotel_adr": { "value": "number", "confidence": "0.0-1.0" }
  },
  "composite_confidence": "0.0-1.0"
}
```

---

## Integration Points

| System | Integration | Protocol |
|--------|-------------|----------|
| SKILL-102 (Demand Forecasting) | Occupancy predictions | Internal API |
| SKILL-103 (Price Optimization) | Base price calculations | Internal API |
| Eventbrite | Event calendar | REST API (1000/hr) |
| Songkick | Music events | REST API |
| Sports Leagues | MLB, NFL, NBA, NHL | REST API |
| Hotel Feeds | Booking.com, Expedia | REST API |
| PMS | Rate distribution | Webhook |

---

## Algorithm Summary

### Event Detection Pipeline

```
Daily Pipeline Start
    ↓
Fetch External Events (Eventbrite, Songkick, Sports)
    ↓
Calculate Four-Way Signals for All Markets
    ↓
┌─────────────────────────────────────────┐
│ YoY Pacing (40%) → Booking Velocity (30%) │
│ Competitor Pricing (20%) → Hotel ADR (10%) │
└─────────────────────────────────────────┘
    ↓
Calculate Composite Confidence Score
    ↓
Confidence > Threshold (0.6)?
    ↓ YES                    ↓ NO
Event Detected           Continue Monitoring
    ↓
Calculate Surge Price
    ↓
Apply Distance-Based Multipliers
    ↓
Enforce User Constraints (Min/Max)
    ↓
Distribute to PMS
```

---

## Competitive Advantage

| Feature | PriceLabs | Wheelhouse | Beyond | AirDNA |
|---------|:---------:|:----------:|:------:|:------:|
| YoY Pacing | ✅ | ✅ | ✅ | ⚠️ |
| Booking Velocity | ✅ | ⚠️ | ❌ | ❌ |
| Competitor Pricing | ✅ | ❌ | ⚠️ | ❌ |
| Hotel ADR | ✅ | ❌ | ❌ | ❌ |
| **Redundancy** | **4-way** | 2-way | 1.5-way | 1-way |

**Result**: Higher confidence, fewer false positives, proactive surge pricing before competitors

---

## Implementation Timeline

| Phase | Weeks | Deliverables |
|-------|-------|--------------|
| Phase 1 | 1-4 | Signal architecture, YoY pacing, booking velocity |
| Phase 2 | 5-8 | Competitor pricing, hotel ADR, confidence scoring |
| Phase 3 | 9-12 | Event detection pipeline, API integrations |
| Phase 4 | 13-16 | Surge pricing, distance multipliers |
| Phase 5 | 17-20 | UI dashboard, analytics, optimization |

---

## Use Cases

### 1. Major Concert Detection
**Trigger**: Taylor Swift Eras Tour announcement  
**Signals**: All 4 signals spike 90 days out  
**Action**: +100% price increase within 5 miles, +50% within 15 miles

### 2. Unknown Local Event
**Trigger**: Anomaly in booking velocity without known event  
**Signals**: Booking velocity +200%, competitor prices +30%  
**Action**: Alert RM team, auto-apply +25% surge

### 3. Holiday Weekend
**Trigger**: Memorial Day Weekend  
**Signals**: Historical YoY pacing shows +50% bookings  
**Action**: Pre-programmed +20% surge, refined by real-time signals

---

## References

- Full Engineering Spec: `knowledge/pricing/ES-PL-002-event-detection.md`
- Knowledge Document: `knowledge/pricing/KD-PL-002-event-detection.md`
- Stage 2 Prompt: `docs/prompts/ENGINEERING_SPEC_PROMPT_EVENT_DETECTION.md`

