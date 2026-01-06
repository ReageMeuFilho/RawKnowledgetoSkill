# Engineering Specification: Event Detection System

**Gap ID**: GAP-PL-002  
**Skill ID**: SKILL-146  
**Status**: Stage 3 COMPLETE  
**Quality Score**: 9.5/10  
**Lines**: 7,828  
**Date**: January 2026

---

## Executive Summary

The Event Detection System (SKILL-146) is a sophisticated demand spike identification and surge pricing platform designed to maximize revenue for short-term rental (STR) properties. The system employs a four-way signal architecture that automatically identifies demand spikes and adjusts prices to capitalize on high-demand events.

### Core Capabilities
- **Four-Way Signal Architecture**: YoY pacing, booking velocity, competitor pricing, hotel ADR
- **Confidence Scoring**: Weighted algorithm (40/30/20/10) for event validation
- **Surge Pricing**: Distance-based multipliers with configurable tiers
- **External Integration**: Eventbrite, Songkick, sports leagues, hotel rate feeds

### Business Impact
- **10-20% ADR lift** during event periods
- **>90% detection rate** for significant events
- **<5% false positive rate**
- **80% reduction** in manual event management

---

## Product Requirements

### Feature Catalog (12 Core Features)

| Feature ID | Name | Category | Priority |
|------------|------|----------|----------|
| F-001 | YoY Pacing Signal Calculator | Signal Processing | Critical |
| F-002 | Booking Velocity Signal Monitor | Signal Processing | Critical |
| F-003 | Competitor Price Signal Tracker | Signal Processing | Critical |
| F-004 | Hotel ADR Signal Analyzer | Signal Processing | Critical |
| F-005 | Confidence Score Calculator | Event Detection | Critical |
| F-006 | Known Event Calendar Integration | Event Detection | Critical |
| F-007 | Anomaly Detection Pipeline | Event Detection | Critical |
| F-008 | Event Classification System | Event Detection | High |
| F-009 | Price Adjustment Calculator | Surge Pricing | Critical |
| F-010 | Distance-Based Multiplier Engine | Surge Pricing | High |
| F-011 | Timing and Decay Logic | Surge Pricing | High |
| F-012 | Constraint Enforcement System | Surge Pricing | Critical |

---

## Four-Way Signal Architecture

### Signal Weighting

| Signal | Weight | Description |
|--------|--------|-------------|
| **YoY Pacing** | 40% | Current year bookings vs same date previous years |
| **Booking Velocity** | 30% | Recent booking rate vs historical baseline |
| **Competitor Pricing** | 20% | Competitor rate increases in market |
| **Hotel ADR** | 10% | Local hotel rate correlation |

### YoY Pacing Signal

```python
def calculate_yoy_pacing(current_bookings, historical_average, market_growth_rate):
    """
    Calculate Year-over-Year pacing signal
    
    Pacing Factor = ((Current - Historical) / Historical) × 100 - Market Growth
    """
    if historical_average <= 0:
        return 0
    
    pacing_factor = ((current_bookings - historical_average) / historical_average) * 100
    adjusted_pacing = pacing_factor - market_growth_rate
    
    # Determine signal strength
    if adjusted_pacing >= 50:
        signal_strength = "high"
        confidence = min(0.95, 0.7 + (adjusted_pacing - 50) * 0.005)
    elif adjusted_pacing >= 25:
        signal_strength = "medium"
        confidence = 0.4 + (adjusted_pacing - 25) * 0.012
    elif adjusted_pacing >= 10:
        signal_strength = "low"
        confidence = 0.1 + (adjusted_pacing - 10) * 0.02
    else:
        signal_strength = "none"
        confidence = max(0.05, 0.1 + adjusted_pacing * 0.005)
    
    return YoYPacingSignal(
        pacing_factor=adjusted_pacing,
        signal_strength=signal_strength,
        confidence=confidence
    )
```

### Confidence Score Calculation

```python
def calculate_composite_confidence(signals):
    """
    Calculate composite confidence using weighted signals
    
    Composite = (0.40 × YoY) + (0.30 × Velocity) + (0.20 × Competitor) + (0.10 × Hotel)
    """
    composite = (
        0.40 * signals.yoy_pacing.confidence +
        0.30 * signals.booking_velocity.confidence +
        0.20 * signals.competitor_pricing.confidence +
        0.10 * signals.hotel_adr.confidence
    )
    
    # Bonus for multi-signal correlation
    active_signals = sum(1 for s in [
        signals.yoy_pacing.signal_strength != "none",
        signals.booking_velocity.signal_strength != "none",
        signals.competitor_pricing.signal_strength != "none",
        signals.hotel_adr.signal_strength != "none"
    ] if s)
    
    if active_signals >= 3:
        correlation_bonus = 0.1
    elif active_signals >= 2:
        correlation_bonus = 0.05
    else:
        correlation_bonus = 0
    
    return min(0.99, composite + correlation_bonus)
```

---

## Surge Pricing Implementation

### Distance-Based Multiplier Tiers

| Distance from Venue | Multiplier | Example |
|---------------------|------------|---------|
| < 1 mile | +30% | 1.30x |
| 1-5 miles | +20% | 1.20x |
| 5-15 miles | +10% | 1.10x |
| > 15 miles | +5% | 1.05x |

### Price Calculation Formula

```
Final Price = Base Dynamic Price × Event Factor × Other Adjustments
```

### Confidence-Based Multipliers

| Confidence Level | Multiplier Range |
|------------------|------------------|
| High (>0.8) | +50% to +150% |
| Medium (0.5-0.8) | +10% to +50% |
| Low (0.3-0.5) | +5% to +10% |

---

## Event Detection Methods

### Known Events (External APIs)
- **Eventbrite API v3**: 1000 calls/hour, 48,000/day
- **Songkick API**: Music events
- **Sports League APIs**: MLB, NFL, NBA, NHL
- **Hotel Rate Feeds**: Booking.com, Expedia

### Unknown Events (Anomaly Detection)

```python
class MLAnomalyDetector:
    def __init__(self):
        self.isolation_forest = IsolationForest(
            contamination=0.05,  # 5% expected anomalies
            random_state=42,
            n_estimators=100
        )
    
    def detect_anomaly(self, signal_data):
        feature_vector = [[
            signal_data['yoy_pacing'],
            signal_data['booking_velocity'],
            signal_data['competitor_pricing'],
            signal_data['hotel_adr'],
            signal_data['day_of_week'],
            signal_data['month'],
            signal_data['market_density']
        ]]
        
        anomaly_score = self.isolation_forest.decision_function(feature_vector)[0]
        is_anomaly = self.isolation_forest.predict(feature_vector)[0] == -1
        
        return {
            'is_anomaly': is_anomaly,
            'anomaly_score': anomaly_score
        }
```

---

## Technology Stack

### Backend
- **Python 3.12+** - Core services
- **Flask** - API framework
- **NumPy/Pandas** - Signal processing
- **scikit-learn** - ML anomaly detection

### Databases
- **MongoDB 6.0+** - Time-series signal data
- **PostgreSQL** - Transactional data (price adjustments, overrides)
- **Redis 7.2+** - Caching layer

### Infrastructure
- **AWS ECS** - Container orchestration
- **Docker** - Containerization
- **Terraform** - Infrastructure as code
- **GitHub Actions** - CI/CD

---

## Data Models

### Event Schema (MongoDB)

```json
{
  "event_id": "EVT-2026-001234",
  "name": "Taylor Swift Eras Tour",
  "type": "concert",
  "category": "music_festival",
  "dates": {
    "start": "2026-07-04T19:00:00Z",
    "end": "2026-07-04T23:00:00Z"
  },
  "location": {
    "venue": "Soldier Field",
    "city": "Chicago",
    "coordinates": [-87.6167, 41.8623]
  },
  "impact": {
    "estimated_attendance": 65000,
    "impact_radius_km": 15,
    "booking_lead_days": 90
  },
  "confidence_score": 0.95,
  "source": "eventbrite"
}
```

### Signal Schema (MongoDB Time-Series)

```json
{
  "timestamp": "2026-07-04T10:00:00Z",
  "metadata": {
    "signal_type": "booking_velocity",
    "market_id": "chicago_il",
    "target_date": "2026-07-04"
  },
  "measurements": {
    "yoy_pacing": { "value": 3.2, "confidence": 0.85 },
    "booking_velocity": { "value": 2.8, "confidence": 0.78 },
    "competitor_pricing": { "value": 1.5, "confidence": 0.65 },
    "hotel_adr": { "value": 1.3, "confidence": 0.55 }
  },
  "composite_confidence": 0.82
}
```

### Price Adjustment Schema (PostgreSQL)

```sql
CREATE TABLE price_adjustments (
    adjustment_id UUID PRIMARY KEY,
    listing_id BIGINT NOT NULL,
    target_date DATE NOT NULL,
    event_id UUID REFERENCES events(event_id),
    base_price DECIMAL(10,2) NOT NULL,
    surge_multiplier DECIMAL(5,3) NOT NULL DEFAULT 1.000,
    adjusted_price DECIMAL(10,2) NOT NULL,
    distance_tier INTEGER CHECK (distance_tier BETWEEN 1 AND 4),
    is_override BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    
    CONSTRAINT valid_multiplier CHECK (surge_multiplier >= 1.0 AND surge_multiplier <= 5.0)
);
```

---

## Performance Requirements

| Metric | Target | Measurement |
|--------|--------|-------------|
| Signal Calculation | <5 seconds per market | Latency monitoring |
| Market Processing | 1,000 markets/hour | Throughput counter |
| Price Calculation | <100ms per listing | API latency |
| Pricing Capacity | 10,000 listings/minute | Load testing |
| Detection Latency | <24 hours from signal emergence | Time tracking |
| Detection Rate | >90% significant events | Historical comparison |
| False Positive Rate | <5% | Manual review |

---

## Success Criteria

| KPI | Target |
|-----|--------|
| Revenue Impact | 10-20% ADR lift during events |
| Detection Coverage | ~100% major events in supported markets |
| Manual Overhead | 80% reduction through automation |
| User Adoption | 95% of users accept recommended prices |

---

## Implementation Timeline

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Phase 1** | Weeks 1-4 | Four-way signal architecture, YoY pacing, booking velocity |
| **Phase 2** | Weeks 5-8 | Competitor pricing, hotel ADR, confidence scoring |
| **Phase 3** | Weeks 9-12 | Event detection pipeline, external API integration |
| **Phase 4** | Weeks 13-16 | Surge pricing calculator, distance-based multipliers |
| **Phase 5** | Weeks 17-20 | UI dashboard, analytics, A/B testing |

---

## Competitive Advantage

The Event Detection System provides **unique four-way signal redundancy** not found in competitors:

| Competitor | YoY Pacing | Booking Velocity | Competitor Pricing | Hotel ADR |
|------------|:----------:|:----------------:|:-----------------:|:---------:|
| PriceLabs | ✅ | ✅ | ✅ | ✅ |
| Wheelhouse | ✅ | ⚠️ | ❌ | ❌ |
| Beyond Pricing | ✅ | ❌ | ⚠️ | ❌ |
| AirDNA | ⚠️ | ❌ | ❌ | ❌ |

**Result**: Higher confidence, fewer false positives, proactive surge pricing

---

## References

- Engineering Specification: `knowledge/pricing/ES-PL-002-event-detection.md`
- Knowledge Document: `knowledge/pricing/KD-PL-002-event-detection.md`
- Stage 2 Prompt: `docs/prompts/ENGINEERING_SPEC_PROMPT_EVENT_DETECTION.md`

