# Final Skill Specification: HLP Dynamic Pricing Algorithm

> **Gap ID**: GAP-PL-001
> **Skills Specified**: SKILL-101, SKILL-102, SKILL-103
> **Priority**: P0 (MVP Critical)
> **Stage 4 Completed**: January 2026
> **Engineering Spec**: `knowledge/pricing/ES-PL-001-hlp-dynamic-pricing.md` (6,060 lines)

---

## 📋 EXECUTIVE SUMMARY

The **Hyper-Local Pulse (HLP) Dynamic Pricing Algorithm** is a revolutionary advancement in short-term rental revenue optimization. This system uses H3 geospatial indexing, machine learning, and real-time market data to deliver intelligent pricing recommendations that maximize revenue while maintaining competitive occupancy rates.

### Business Impact
| Metric | Target | Achievement Method |
|--------|--------|-------------------|
| Revenue Lift | 20-40% | Price elasticity optimization |
| ADR Improvement | 15-40% | Hyper-local competitive analysis |
| Occupancy Improvement | 5-15% | Demand forecasting |
| Manual Pricing Time | -95% | Full automation |
| OTA Sync Success | >98% | Multi-platform adapters |

---

## 🎯 SKILLS SPECIFIED

### SKILL-101: Hyper-Local Market Definition

| Attribute | Value |
|-----------|-------|
| **Skill Name** | hyper-local-market-definition |
| **Category** | pricing |
| **Priority** | P0 (Critical) |
| **Status** | ✅ SPECIFIED |

#### Description
H3 geospatial indexing system at resolutions 7-9 to create precise competitive sets within ~15km radius for each listing. Uses Uber's hexagonal hierarchical spatial index for hyper-local market analysis.

#### Key Features
- **F-001**: H3 Cell Assignment at resolutions 7, 8, 9
- **F-001-RQ-002**: Comp Set Generation (350 most similar listings)
- **F-001-RQ-003**: Similarity Scoring (Distance 30%, Bedrooms 25%, Property Type 20%, Amenities 15%, Quality 10%)
- **F-001-RQ-004**: Dynamic Radius Adjustment (expand to 15km max if <50 comps)

#### Technical Specifications
```yaml
input:
  - listing_id: string
  - latitude: float (-90 to 90)
  - longitude: float (-180 to 180)
  - property_attributes: PropertyAttributes

output:
  type: CompSet
  properties:
    listing_id: string
    h3_cells:
      resolution_7: string  # ~5km² cells
      resolution_8: string  # ~1.2km² cells
      resolution_9: string  # ~0.3km² cells
    comparable_listings:
      count: 350
      items: ComparableListing[]
    similarity_scores: float[]

performance:
  latency: "<500ms"
  availability: "99.9%"
```

#### Dependencies
- PostgreSQL with PostGIS extension
- H3 geospatial library
- Property Service for listing details

---

### SKILL-102: Demand Forecasting Engine

| Attribute | Value |
|-----------|-------|
| **Skill Name** | demand-forecasting-engine |
| **Category** | pricing |
| **Priority** | P0 (Critical) |
| **Status** | ✅ SPECIFIED |

#### Description
Machine learning-powered occupancy probability model that predicts booking likelihood for each date up to 540 days forward using historical booking curves, seasonality patterns, and market pacing analysis.

#### Key Features
- **F-002-RQ-001**: Occupancy Probability Calculation with confidence intervals
- **F-002-RQ-002**: Reference Day Selection (3-5 analogous historical days)
- **F-002-RQ-003**: Pacing Analysis (current vs reference occupancy)
- **F-002-RQ-004**: Forecast Accuracy Tracking (MAE/MAPE)

#### Technical Specifications
```yaml
input:
  - listing_id: string
  - date_range: DateRange (up to 540 days)
  - historical_booking_data: BookingHistory[]
  - market_conditions: MarketConditions

output:
  type: DailyForecast[]
  properties:
    date: date
    occupancy_probability: float (0-1)
    demand_score: float
    confidence_interval:
      lower: float
      upper: float
    reference_days: Date[]

performance:
  forecast_generation: "<30 seconds for 540 days"
  accuracy_target: ">75% (MAE)"
  
ml_model:
  architecture: "Ensemble (XGBoost + LSTM)"
  reference_selection: "k-NN on booking curves"
  training_data: "2+ years historical"
```

#### Dependencies
- F-001 (Hyper-Local Market Definition)
- Booking Service for reservation data
- Event calendar APIs
- Weather data providers

---

### SKILL-103: Price Elasticity Optimization

| Attribute | Value |
|-----------|-------|
| **Skill Name** | price-elasticity-optimization |
| **Category** | pricing |
| **Priority** | P0 (Critical) |
| **Status** | ✅ SPECIFIED |

#### Description
Revenue optimization engine that finds optimal price P* maximizing Expected Revenue = Price × P(booked|price). Uses logistic demand curve estimation with market-specific elasticity coefficients.

#### Key Features
- **F-003-RQ-001**: Demand Curve Estimation (logistic regression)
- **F-003-RQ-002**: Revenue Optimization (find P* maximizing Expected Revenue)
- **F-003-RQ-003**: Price Constraints Application (min/max, last-minute, far-out)
- **F-003-RQ-004**: Elasticity Confidence Intervals

#### Technical Specifications
```yaml
input:
  - listing_id: string
  - date: date
  - demand_forecast: DailyForecast
  - price_constraints: PriceConstraints
  - market_conditions: MarketConditions

output:
  type: OptimalPrice
  properties:
    recommended_price: float
    currency: string
    elasticity_coefficient: float
    confidence_interval:
      lower: float
      upper: float
    revenue_breakdown:
      expected_revenue: float
      base_price: float
      seasonality_adjustment: float
      event_adjustment: float
      last_minute_discount: float

performance:
  calculation_latency: "<200ms"
  daily_calculations: "50M+"
  price_range: "$10-$10,000"

formula: |
  Expected_Revenue = P × P(booked|P)
  P* = argmax(Expected_Revenue)
```

#### Dependencies
- F-002 (Demand Forecasting Engine)
- Analytics Service for performance tracking
- Competitor pricing data
- Real-time OTA sync

---

## 🔧 ADDITIONAL FEATURES SPECIFIED

### F-004: Seasonality Analysis
- Hyper-local seasonality detection
- Multipliers from 0.7-1.5
- Day-of-week pattern detection
- Year-over-year adjustment

### F-005: OTA Price Synchronization
- Multi-platform sync (Airbnb, Vrbo, Booking.com)
- Rate limit management per platform
- Retry logic with exponential backoff
- >98% sync success rate

### F-006: Market Data Ingestion
- AirDNA API integration
- Competitor price monitoring
- Data quality scoring

### F-007: Event Detection System
- Known event calendar integration
- Unknown event anomaly detection
- Surge pricing automation

### F-008: Real-Time Processing Pipeline
- Daily batch processing at 02:00 UTC
- Event-driven recalculation
- Sub-500ms response time

---

## 🏗️ TECHNOLOGY STACK

### Core Technologies
| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| Backend | Python | 3.14 | Pricing engine, ML models |
| Frontend | React + TypeScript | 19 / 5.0 | Dashboard |
| Database | MongoDB | 8.2 | Primary data store |
| Cache | Redis | 7.4 | Comp sets, market stats |
| ML Framework | XGBoost + PyTorch | Latest | Forecasting models |
| Geospatial | H3 | 4.x | Hexagonal indexing |
| API Framework | Flask | 3.1 | REST APIs |
| Task Queue | Celery | 5.4 | Distributed processing |

### Infrastructure
| Component | Technology | Purpose |
|-----------|------------|---------|
| Container | Docker | 29.1 | Containerization |
| Orchestration | Kubernetes | 1.31 | Container management |
| IaC | Terraform | 1.10 | Infrastructure provisioning |
| CI/CD | GitHub Actions | Latest | Automation pipeline |
| Monitoring | DataDog | Latest | APM and metrics |
| Error Tracking | Sentry | Latest | Error monitoring |

### External Integrations
| Platform | Type | Rate Limit |
|----------|------|------------|
| Airbnb | GraphQL API | 100/min |
| Vrbo | REST API | 60/min |
| Booking.com | REST API | 50/min |
| AirDNA | REST API | 1,000/hour |
| 150+ PMS | Various | Varies |

---

## 📊 PERFORMANCE REQUIREMENTS

| Metric | Target | SLA |
|--------|--------|-----|
| System Uptime | 99.9% | Monthly |
| Price Calculation Latency | <500ms | Per request |
| Forecast Generation | <30s | 540 days |
| Daily Calculations | 50M+ | Per day |
| OTA Sync Success | >98% | Per sync |
| Forecast Accuracy | >75% | MAE |
| Cache Hit Ratio | >95% | Comp sets |
| Listings Supported | 100,000+ | Concurrent |

---

## 🗂️ DATA MODEL

### Core Collections (MongoDB)

```javascript
// listings collection
{
  _id: ObjectId,
  listing_id: "LST-12345",
  h3_cells: {
    resolution_7: "872830828ffffff",
    resolution_8: "882830828bfffff",
    resolution_9: "892830828b7ffff"
  },
  comp_set_id: ObjectId,
  property_attributes: {...},
  pricing_config: {...}
}

// daily_prices collection (time-series)
{
  _id: ObjectId,
  listing_id: "LST-12345",
  date: ISODate("2026-02-15"),
  recommended_price: 285.00,
  currency: "USD",
  breakdown: {
    base_price: 250.00,
    seasonality: 1.10,
    event_factor: 1.05,
    elasticity_adjustment: -0.02
  },
  confidence: 0.87,
  created_at: ISODate()
}

// comp_sets collection
{
  _id: ObjectId,
  primary_listing_id: "LST-12345",
  h3_cell: "872830828ffffff",
  comparable_listings: [
    {
      listing_id: "LST-67890",
      similarity_score: 0.92,
      factors: {...}
    }
  ],
  count: 350,
  last_refreshed: ISODate()
}
```

---

## 🚀 IMPLEMENTATION ROADMAP

### Phase 1: Core Engine (Weeks 1-8)
- [ ] H3 geo-indexing implementation
- [ ] Comp set generation algorithm
- [ ] Basic demand forecasting
- [ ] Price optimization engine
- [ ] MongoDB/Redis setup

### Phase 2: Integrations (Weeks 9-14)
- [ ] Airbnb API adapter
- [ ] Vrbo API adapter
- [ ] Booking.com API adapter
- [ ] Market data ingestion
- [ ] Event calendar integration

### Phase 3: Advanced Features (Weeks 15-18)
- [ ] ML model training pipeline
- [ ] Real-time event detection
- [ ] Seasonality analysis
- [ ] Performance optimization

### Phase 4: Polish & Scale (Weeks 19-22)
- [ ] Dashboard UI
- [ ] Alerting and monitoring
- [ ] Load testing
- [ ] Documentation

**Total Estimated Effort**: 22 weeks

---

## ✅ STAGE 4 COMPLETION CHECKLIST

- [x] Engineering Specification reviewed (6,060 lines)
- [x] SKILL-101 (Hyper-Local Market Definition) fully specified
- [x] SKILL-102 (Demand Forecasting Engine) fully specified
- [x] SKILL-103 (Price Elasticity Optimization) fully specified
- [x] Technology stack documented
- [x] Performance requirements defined
- [x] Data model specified
- [x] Implementation roadmap created
- [x] Dependencies mapped
- [ ] MASTER_SKILL_REGISTRY.md updated (next step)

---

## 📚 REFERENCES

- **Stage 1 Research**: `knowledge/pricing/KD-PL-001-hlp-dynamic-pricing.md` (9.5/10)
- **Stage 2 Prompt**: `docs/prompts/ENGINEERING_SPEC_PROMPT_HLP_PRICING.md`
- **Stage 3 Spec**: `knowledge/pricing/ES-PL-001-hlp-dynamic-pricing.md` (6,060 lines)
- **Primary Source**: PriceLabs HLP Algorithm
- **Secondary Sources**: Beyond Pricing, Wheelhouse, AirDNA

---

**Status**: ✅ **GAP-PL-001 COMPLETE** - 3 P0 Skills Fully Specified

