# Engineering Specification Prompt: HLP Dynamic Pricing Algorithm

## Gap ID: GAP-PL-001
## Skill: SKILL-101 (Dynamic Pricing Algorithm)
## Created: 2026-01-05
## Stage: 2 (Research → **Engineering Prompt** → Specification → Skills)

---

## 🎯 PURPOSE

You are an **Engineering Agent** tasked with creating a comprehensive engineering specification for implementing a **Hyper-Local Pulse (HLP) Dynamic Pricing Algorithm**. This system will provide intelligent, automated nightly rate optimization for short-term rental properties using hyper-local market data, demand forecasting, and price elasticity modeling.

The specification you create will serve as the blueprint for implementing SKILL-101 and related pricing skills in our AI-powered property management platform.

---

## 📚 REQUIRED READING

Before creating the specification, thoroughly review:

1. **Knowledge Document**: `knowledge/pricing/KD-PL-001-hlp-dynamic-pricing.md`
   - 613 lines of comprehensive research
   - 293+ authoritative citations
   - Complete data model, business rules, integration requirements

2. **Agent Guide**: `docs/AGENT_GUIDE.md`
   - Process overview and expectations

3. **Reference Specification** (optional): `specs/ai-workforce/SPEC-SKILL-261-268.md`
   - Example of expected specification depth and format

---

## 📋 SPECIFICATION REQUIREMENTS

Your engineering specification must address ALL of the following 20 sections in exhaustive detail:

---

### SECTION 1: EXECUTIVE SUMMARY (1-2 pages)

Provide:
- System purpose and value proposition
- Key capabilities summary
- Target users and use cases
- Expected business outcomes
- Technology stack overview
- Integration points summary

---

### SECTION 2: TECHNICAL ARCHITECTURE OVERVIEW (3-4 pages)

Create detailed documentation including:

**2.1 System Architecture Diagram**
- High-level component diagram (ASCII or description)
- Data flow diagram showing:
  - Market data ingestion
  - Demand forecasting pipeline
  - Price optimization engine
  - Price sync to OTAs

**2.2 Core Components**
| Component | Responsibility | Technology | Scale Requirements |
|-----------|---------------|------------|-------------------|
| Market Data Collector | ... | ... | ... |
| Hyper-Local Indexer | ... | ... | ... |
| Demand Forecaster | ... | ... | ... |
| Price Optimizer | ... | ... | ... |
| Price Syncer | ... | ... | ... |

**2.3 Processing Layers**
Document:
- Real-time layer (price updates)
- Batch layer (model training, comp set updates)
- Streaming layer (market event detection)

---

### SECTION 3: HYPER-LOCAL MARKET DEFINITION (4-5 pages)

This is THE core differentiator. Specify in detail:

**3.1 Comp Set Definition Algorithm**
```python
# Pseudocode required
def define_comp_set(listing: Listing) -> CompSet:
    """
    Define the 350 nearest comparable listings
    using H3 geo-indexing within ~15km radius
    """
    # 1. Get H3 cells at resolution 7
    # 2. Expand search in concentric rings
    # 3. Filter by bedroom count, property type
    # 4. Rank by similarity score
    # 5. Return top 350 comps
```

**3.2 H3 Geo-Indexing Implementation**
- H3 resolution levels (7, 8, 9)
- Cell adjacency algorithms
- Performance optimization for comp queries
- Sample H3 calculations

**3.3 Similarity Scoring Model**
Specify the algorithm for matching listings:
| Factor | Weight | Calculation |
|--------|--------|-------------|
| Distance | 30% | Decay function |
| Bedroom count | 25% | Exact/adjacent match |
| Property type | 20% | Category hierarchy |
| Amenities | 15% | Jaccard similarity |
| Quality tier | 10% | Review score bucket |

**3.4 Dynamic Radius Calculation**
- Urban vs rural density handling
- Minimum comp count requirements
- Maximum radius constraints (15km)
- Edge case: new markets with sparse data

---

### SECTION 4: DEMAND FORECASTING ENGINE (5-6 pages)

**4.1 Forecast Model Architecture**
```
Input Features:
├── Historical booking curves
├── Seasonality signals
├── Day-of-week patterns
├── Holiday/event calendar
├── Pacing metrics
└── Pickup velocity

Model Stack:
├── Time series decomposition (trend, seasonality, residual)
├── Reference day selection (k-NN on booking curves)
├── Ensemble forecaster (XGBoost + LSTM)
└── Confidence interval estimation
```

**4.2 Reference Day Selection Algorithm**
Specify how to find analogous historical days:
- Season matching (±14 days YoY)
- Day-of-week exact match
- Holiday type matching
- Booking curve shape similarity (DTW distance)

**4.3 Pacing Analysis**
| Metric | Definition | Update Frequency | Use |
|--------|------------|------------------|-----|
| Pacing Ratio | Current occupancy / Reference occupancy at same lead time | Daily | Demand surge detection |
| Pickup Velocity | New bookings in last N days | Daily | Trend acceleration |
| Market Pacing | Comp set occupancy vs historical | Daily | Relative positioning |

**4.4 Occupancy Probability Model**
```math
P(booked | date, price) = f(demand_score, price_elasticity, competitive_position)
```
- Logistic regression coefficients
- Feature engineering for demand score
- Model calibration approach

**4.5 Forecast Output Schema**
```json
{
  "listing_id": "LST-12345",
  "forecasts": [
    {
      "date": "2026-02-14",
      "expected_occupancy": 0.85,
      "confidence_interval": [0.78, 0.92],
      "demand_score": 1.42,
      "reference_days": ["2025-02-14", "2025-02-07", "2024-02-14"],
      "pacing_ratio": 1.15,
      "pickup_7d": 12
    }
  ]
}
```

---

### SECTION 5: PRICE ELASTICITY & OPTIMIZATION (5-6 pages)

This is the mathematical heart of the system.

**5.1 Elasticity Model**
```
Premise: Demand = Probability of Booking (PB) at given price
Goal: Find price P* that maximizes Expected Revenue = P × PB(P)
```

**5.2 Demand Curve Estimation**
Specify the model for estimating booking probability at different prices:
- Logistic demand curve parameters
- Market-specific elasticity coefficients
- Date-specific elasticity adjustments
- Confidence intervals on elasticity estimates

**5.3 Revenue Optimization Algorithm**
```python
def optimize_price(listing_id: str, date: date, forecast: Forecast) -> Price:
    """
    Find price that maximizes expected revenue
    """
    # 1. Get demand curve parameters for this listing/date
    # 2. Generate price candidates in range [min_price, max_price]
    # 3. For each candidate:
    #    - Calculate P(booked) from demand curve
    #    - Calculate expected_revenue = price × P(booked)
    # 4. Return price with highest expected revenue
    # 5. Apply constraints (min/max, last-minute, far-out)
```

**5.4 Expected Revenue Curve**
Document:
- How to visualize the revenue optimization
- Example calculation showing peak revenue price
- Sensitivity analysis (how wrong can we be?)

**5.5 Price Constraints**
| Constraint | Priority | Logic |
|------------|----------|-------|
| Minimum Price | Hard floor | Never go below |
| Maximum Price | Soft ceiling | Allow override |
| Last-Minute Discount | Dynamic | Market-driven or fixed |
| Far-Out Premium | Dynamic | Market-driven or fixed |
| Adjacent Day Factor | Optional | Fill gaps |

---

### SECTION 6: SEASONALITY ANALYSIS (3-4 pages)

**6.1 Hyper-Local Seasonality Detection**
- Per-comp-set seasonality curves (not city-wide)
- Rolling calculation methodology
- Year-over-year adjustment for market changes

**6.2 Seasonality Factor Calculation**
```python
def calculate_seasonality_factor(listing_id: str, date: date) -> float:
    """
    Returns multiplier (0.7 - 1.5) based on comp set's 
    historical occupancy/rate patterns for this time of year
    """
    # 1. Get comp set occupancy for same week YoY
    # 2. Compare to annual average
    # 3. Normalize to seasonality factor
```

**6.3 Day-of-Week Patterns**
Document per-market DOW adjustments:
- Business district patterns (higher mid-week)
- Resort patterns (higher weekends)
- Automatic detection algorithm

**6.4 Sensitivity Options**
| Option | Effect | Use Case |
|--------|--------|----------|
| No Seasonality | Factor = 1.0 always | Hotels with flat demand |
| Conservative | ±10% max swing | Risk-averse hosts |
| Recommended | Full calculated factor | Default |
| Aggressive | Amplified swings | Highly seasonal markets |

---

### SECTION 7: EVENT & HOLIDAY DETECTION (4-5 pages)

**7.1 Known Event Integration**
- Event calendar data sources
- Distance-based impact scaling
- Category-based impact factors

**7.2 Unknown Event Detection**
```python
def detect_demand_anomaly(comp_set_id: str, date: date) -> Optional[Event]:
    """
    Detect unexpected demand surge from booking patterns
    """
    # 1. Compare actual pacing to forecast
    # 2. If pacing_ratio > 1.3 for 3+ consecutive days
    # 3. Flag as potential event
    # 4. Apply auto-surge pricing
```

**7.3 Event Pricing Logic**
| Event Type | Base Impact | Distance Decay | Duration |
|------------|-------------|----------------|----------|
| Major Concert | +50-100% | 50% per 5km | Event day only |
| Multi-day Festival | +30-60% | 30% per 5km | Duration + 1 day |
| Sports Championship | +100-200% | 40% per 5km | Event + travel days |
| Holiday | +20-40% | N/A (market-wide) | Holiday period |

**7.4 Event Price Factor Application**
Document the formula for combining event factors with base pricing.

---

### SECTION 8: LAST-MINUTE & FAR-OUT STRATEGIES (3-4 pages)

**8.1 Last-Minute Pricing**
| Strategy | Description | When to Use |
|----------|-------------|-------------|
| Market Driven (Balanced) | Dynamic daily discount based on comp behavior | Default (HLP) |
| Market Driven (Conservative) | Smaller dynamic discount | Premium properties |
| Market Driven (Aggressive) | Larger dynamic discount | Maximize occupancy |
| % Gradual | Fixed schedule (e.g., -5% per day from day 7) | Legacy/simple |
| % Flat | Single discount within window | Simple approach |
| No Discount | Maintain base pricing | Premium strategy |

**8.2 Market-Driven Last-Minute Algorithm**
```python
def calculate_market_driven_lm_discount(
    listing_id: str, 
    date: date, 
    days_out: int
) -> float:
    """
    Returns discount factor (0.70 - 1.0) based on market conditions
    """
    # 1. Get comp set last-minute bookings at similar lead times
    # 2. Analyze successful discount levels
    # 3. Apply listing-specific adjustment
    # 4. Cap at configured maximum discount
```

**8.3 Far-Out Premium Strategy**
| Strategy | Description | Default |
|----------|-------------|---------|
| Market Driven (Balanced) | +0-20% premium that decays as date approaches | HLP Default |
| No Far-Out Premium | Book early at standard rates | Early booking preference |

**8.4 Configuration Schema**
```json
{
  "last_minute": {
    "strategy": "market_driven_balanced",
    "window_days": 14,
    "max_discount_pct": 30,
    "min_last_minute_price": null
  },
  "far_out": {
    "strategy": "market_driven_balanced",
    "start_days": 60,
    "max_premium_pct": 20
  }
}
```

---

### SECTION 9: DATA MODEL & STORAGE (4-5 pages)

**9.1 Core Entities**
Define complete schemas for:

```typescript
interface Listing {
  listing_id: string;
  location: { lat: number; lng: number; h3_cell: string };
  property_type: PropertyType;
  bedrooms: number;
  amenities: string[];
  base_price: number;
  min_price: number;
  max_price: number;
  algorithm_version: "hlp" | "legacy";
  config: PricingConfig;
}

interface CompSet {
  listing_id: string;
  comp_listing_ids: string[];
  h3_cells: string[];
  radius_km: number;
  updated_at: Date;
}

interface DailyForecast {
  listing_id: string;
  date: Date;
  expected_occupancy: number;
  demand_score: number;
  seasonality_factor: number;
  event_factor: number;
  recommended_price: number;
  price_breakdown: PriceBreakdown;
}
```

**9.2 Time Series Storage**
- Daily price recommendations (hot storage: 90 days)
- Historical bookings (warm storage: 2 years)
- Market statistics (cold storage: 5+ years)

**9.3 Caching Strategy**
| Data | Cache TTL | Invalidation |
|------|-----------|--------------|
| Comp set | 24 hours | On listing change |
| Market stats | 1 hour | Time-based |
| Price recommendation | 6 hours | On config change |
| H3 index | 7 days | Rarely changes |

**9.4 Database Schema**
```sql
-- Listings table
CREATE TABLE listings (
  listing_id VARCHAR(36) PRIMARY KEY,
  h3_cell_r7 VARCHAR(15) NOT NULL,
  h3_cell_r8 VARCHAR(15) NOT NULL,
  property_type VARCHAR(50),
  bedrooms SMALLINT,
  base_price DECIMAL(10,2),
  min_price DECIMAL(10,2),
  max_price DECIMAL(10,2),
  config JSONB,
  INDEX idx_h3_r7 (h3_cell_r7),
  INDEX idx_h3_r8 (h3_cell_r8)
);

-- Daily prices table
CREATE TABLE daily_prices (
  listing_id VARCHAR(36),
  date DATE,
  recommended_price DECIMAL(10,2),
  price_breakdown JSONB,
  forecast JSONB,
  created_at TIMESTAMP DEFAULT NOW(),
  PRIMARY KEY (listing_id, date)
);
```

---

### SECTION 10: INTEGRATION REQUIREMENTS (4-5 pages)

**10.1 OTA Integrations (Price Push)**
| Platform | API Method | Rate Limit | Sync Frequency |
|----------|-----------|------------|----------------|
| Airbnb | GraphQL API | 100/min | Daily + on-demand |
| Vrbo | REST API | 60/min | Daily + on-demand |
| Booking.com | REST API | 50/min | Daily + on-demand |

**10.2 PMS/Channel Manager Integrations**
Document connection patterns for:
- Direct API integration
- Channel manager pass-through
- Webhook-based updates

**10.3 Market Data Ingestion**
| Source | Data Type | Frequency | Method |
|--------|-----------|-----------|--------|
| Airbnb | Competitor prices, availability | Daily | Scraping/API |
| AirDNA | Market statistics | Weekly | API |
| Event APIs | Local events | Daily | API |
| Holiday DB | Holiday calendar | Monthly | Static |

**10.4 Internal Service Integrations**
```
HLP Pricing Service
├── Treasury Service (payment processing, cost data)
├── Booking Service (reservation data)
├── Property Service (listing details)
├── Analytics Service (performance metrics)
└── Notification Service (nudges, alerts)
```

**10.5 API Specification**
Define key endpoints:
```
POST /api/v1/pricing/calculate
  - Input: { listing_id, date_range }
  - Output: { prices[], breakdown[] }

GET /api/v1/pricing/forecast/{listing_id}
  - Output: { forecasts[] }

PUT /api/v1/pricing/config/{listing_id}
  - Input: PricingConfig
  - Output: { updated: true }

POST /api/v1/pricing/sync/{listing_id}
  - Trigger immediate price sync to OTAs
```

---

### SECTION 11: REAL-TIME PROCESSING (3-4 pages)

**11.1 Daily Price Update Pipeline**
```
Schedule: 02:00 UTC daily

Pipeline Steps:
1. [Batch] Refresh comp sets for all listings
2. [Batch] Pull latest market data
3. [Batch] Run demand forecaster for D+0 to D+540
4. [Batch] Calculate optimal prices
5. [Stream] Push prices to OTA sync queue
6. [Stream] Send nudge notifications where applicable
```

**11.2 Event-Driven Updates**
| Event | Trigger | Action |
|-------|---------|--------|
| New booking | Webhook from OTA | Recalc prices for ±7 days |
| Config change | User action | Full recalc for listing |
| Event detected | Anomaly detector | Surge pricing for affected dates |
| Market shift | Hourly monitor | Selective recalc if significant |

**11.3 Sync Architecture**
```
Price Recommendation DB
        ↓
   Sync Queue (Redis)
        ↓
   Rate Limiter
        ↓
   [OTA Adapter Pool]
   ├── Airbnb Adapter
   ├── Vrbo Adapter
   └── Booking Adapter
        ↓
   Sync Status DB
```

---

### SECTION 12: UI/UX COMPONENTS (3-4 pages)

**12.1 Pricing Dashboard**
| Column | Description | Sortable | Filterable |
|--------|-------------|----------|------------|
| Listing | Name + thumbnail | Yes | Yes (search) |
| Algorithm | HLP or Legacy badge | Yes | Yes |
| Base Price | Editable inline | Yes | Yes (range) |
| Min Price | Editable inline | Yes | Yes |
| Occupancy 30d | % with market comparison | Yes | Yes |
| ADR | With trend arrow | Yes | Yes |
| RevPAR | Calculated metric | Yes | Yes |
| Sync Status | ✓ or ! icon | Yes | Yes |
| Last Sync | Timestamp | Yes | Yes |

**12.2 Pricing Calendar View**
- Daily grid with recommended prices
- Color coding (low/medium/high relative to base)
- Hover tooltip with price breakdown
- Event/holiday markers
- Booking overlay (show booked dates)
- Manual override capability

**12.3 Market Comparison Charts**
- Future Pricing Chart (listing vs market percentiles)
- Occupancy Pacing Chart
- Competitor Calendar comparison

**12.4 Nudges UI**
| Nudge Type | Trigger Condition | Message | Action |
|------------|-------------------|---------|--------|
| Base Price Too High | Consistently hitting min price | "Your base price may be too high..." | Suggest new base |
| Base Price Too Low | Booking out quickly at low rates | "You may be underpricing..." | Suggest new base |
| Min Price Warning | Min prevents competitive pricing | "Your minimum is above market..." | Review min |

---

### SECTION 13: CONFIGURATION & CUSTOMIZATION (3-4 pages)

**13.1 Complete Configuration Schema**
```typescript
interface PricingConfig {
  // Core Inputs
  base_price: number;
  min_price: number;
  max_price?: number;
  
  // Algorithm Settings
  seasonality_sensitivity: 'none' | 'conservative' | 'moderate_conservative' | 
                          'recommended' | 'moderate_aggressive' | 'aggressive';
  demand_factor_sensitivity: 'none' | 'conservative' | 'moderate_conservative' | 
                            'recommended' | 'moderate_aggressive' | 'aggressive';
  
  // Last-Minute Strategy
  last_minute: {
    strategy: 'market_driven_balanced' | 'market_driven_conservative' | 
              'market_driven_aggressive' | 'gradual_pct' | 'flat_pct' | 'none';
    window_days?: number;      // 1-90
    discount_pct?: number;     // For fixed strategies
    min_last_minute_price?: number;
  };
  
  // Far-Out Strategy
  far_out: {
    strategy: 'market_driven_balanced' | 'market_driven_conservative' | 
              'market_driven_aggressive' | 'flat_pct' | 'none';
    start_days?: number;       // 30-180
    premium_pct?: number;      // For fixed strategy
    min_far_out_price?: number;
  };
  
  // Advanced (optional)
  adjacent_day_factor?: number;      // 0.8-1.2
  booking_recency_factor?: boolean;  // Enable/disable
  hotel_comps?: boolean;             // Blend hotel data
  custom_date_overrides?: DateOverride[];
}
```

**13.2 Default Values by Algorithm**
| Setting | HLP Default | Legacy Default |
|---------|-------------|----------------|
| Seasonality | Recommended | Recommended |
| Demand Factor | Recommended | Recommended |
| Last-Minute | Market Driven (Balanced) | 30% over 15 days |
| Far-Out | Market Driven (Balanced) | 20% after 60 days |

**13.3 Group/Portfolio Customization**
- Apply settings to multiple listings
- Smart Presets (bundled configurations)
- Inheritance hierarchy (group → listing → date)

---

### SECTION 14: BUSINESS RULES ENGINE (3-4 pages)

**14.1 Core Business Rules**
Document all rules with:
- Rule ID
- Description
- Priority
- Logic (pseudocode)
- Override conditions

Example:
```
RULE-001: Minimum Price Floor
- Priority: 1 (highest)
- Logic: final_price = max(calculated_price, min_price)
- Override: Only via explicit min_last_minute_price config
```

**14.2 Price Calculation Order**
```
1. Start with base_price
2. Apply seasonality_factor
3. Apply day_of_week_factor
4. Apply demand_factor (events, pacing)
5. Apply far_out_premium (if applicable)
6. Apply last_minute_discount (if applicable)
7. Apply adjacent_day_factor (if enabled)
8. Enforce min_price floor
9. Enforce max_price ceiling
10. Return final_price with breakdown
```

**14.3 Edge Cases**
Document handling for:
- New listing (no history)
- Sparse market (< 50 comps)
- Price conflicts (manual override vs algorithm)
- Sync failures
- Missing market data

---

### SECTION 15: PERFORMANCE REQUIREMENTS (2-3 pages)

**15.1 SLAs**
| Operation | Target | Maximum |
|-----------|--------|---------|
| Single listing price calc | 200ms | 500ms |
| Full portfolio recalc (100 listings) | 30s | 120s |
| OTA sync per listing | 5s | 30s |
| Dashboard load | 1s | 3s |
| Market data refresh | 10 min | 30 min |

**15.2 Scale Requirements**
- Support 100,000+ listings
- Process 50M+ price calculations per day
- Handle 10,000 concurrent dashboard users
- Store 540 days of forward pricing per listing

**15.3 Throughput Benchmarks**
```
Daily batch job:
- 100K listings × 540 days = 54M price points
- Target completion: 4 hours
- Required throughput: ~3,750 prices/second
```

---

### SECTION 16: MONITORING & OBSERVABILITY (2-3 pages)

**16.1 Key Metrics**
| Metric | Description | Alert Threshold |
|--------|-------------|-----------------|
| Price coverage | % listings with fresh prices | < 99% |
| Sync success rate | % successful OTA syncs | < 98% |
| Calc latency p99 | Price calculation time | > 1s |
| Forecast accuracy | Occupancy prediction vs actual | < 70% |
| Revenue lift | vs baseline | < 5% |

**16.2 Logging Requirements**
- All price calculations logged with breakdown
- Config changes with before/after
- Sync attempts with success/failure
- Anomaly detections with evidence

**16.3 Dashboard Components**
- Real-time sync status
- Algorithm performance trends
- Market data freshness
- User activity metrics

---

### SECTION 17: ERROR HANDLING (2-3 pages)

**17.1 Error Categories**
| Category | Examples | Handling |
|----------|----------|----------|
| Data | Missing comp data, stale prices | Fallback to last known good |
| Integration | OTA API failure, timeout | Retry with backoff |
| Calculation | Division by zero, NaN | Log and use safe default |
| Config | Invalid settings | Validation + reject |

**17.2 Fallback Strategies**
- If comp set too small: expand radius
- If market data missing: use regional averages
- If forecast fails: use YoY comparison
- If sync fails: queue for retry

**17.3 Recovery Procedures**
Document step-by-step recovery for:
- Full market data outage
- OTA integration failure
- Database corruption
- Algorithm rollback

---

### SECTION 18: SECURITY CONSIDERATIONS (2-3 pages)

**18.1 Data Classification**
| Data Type | Classification | Protection |
|-----------|---------------|------------|
| Pricing config | Internal | Encrypted at rest |
| Market data | Confidential | Access controlled |
| Algorithm params | Confidential | Code-level only |
| User credentials | PII | Encrypted + hashed |

**18.2 Access Control**
- API authentication (OAuth2/API keys)
- Rate limiting per user/account
- Audit logging for config changes

**18.3 Third-Party Security**
- OTA credential management
- Secure API communication (TLS 1.3)
- Data scraping ethics

---

### SECTION 19: TESTING STRATEGY (2-3 pages)

**19.1 Test Categories**
| Type | Coverage | Tools |
|------|----------|-------|
| Unit | Core algorithms, rules | pytest |
| Integration | OTA sync, DB ops | pytest + mocks |
| Performance | Throughput, latency | locust |
| A/B Testing | Revenue impact | Experiment platform |

**19.2 Test Cases**
Must include tests for:
- Price calculation accuracy
- Comp set generation
- Demand forecast validation
- Edge cases (new listing, sparse market)
- Regression tests for rule changes

**19.3 Validation Metrics**
- Forecast accuracy (MAE, MAPE)
- Revenue lift vs control
- Occupancy rate comparison
- User satisfaction (NPS)

---

### SECTION 20: IMPLEMENTATION ROADMAP (2-3 pages)

**20.1 Phase 1: Core Algorithm (Weeks 1-6)**
- [ ] H3 geo-indexing service
- [ ] Comp set generation
- [ ] Basic demand forecasting
- [ ] Price optimization engine
- [ ] Database schema

**20.2 Phase 2: Integration (Weeks 7-10)**
- [ ] OTA sync adapters
- [ ] PMS integration layer
- [ ] Market data ingestion
- [ ] Event calendar integration

**20.3 Phase 3: UI/UX (Weeks 11-14)**
- [ ] Pricing dashboard
- [ ] Calendar view
- [ ] Configuration UI
- [ ] Nudges system

**20.4 Phase 4: Advanced Features (Weeks 15-18)**
- [ ] Unknown event detection
- [ ] A/B testing framework
- [ ] Advanced customizations
- [ ] Portfolio analytics

---

## 📤 OUTPUT REQUIREMENTS

### Format
- Markdown document
- Well-structured with table of contents
- Code samples in appropriate language blocks
- Diagrams as ASCII or detailed descriptions
- Tables for structured data

### Length
- Expect 4,000-8,000 lines for comprehensive coverage
- Each section should be self-contained and thorough

### Save Location
```
knowledge/pricing/ES-PL-001-hlp-dynamic-pricing.md
```

### After Completion
1. Update `STATUS.md` - Mark Stage 3 complete for GAP-PL-001
2. Update `docs/PIPELINE_TRACKER.md` - Add completion date
3. Commit and push:
   ```
   git add -A
   git commit -m "Stage 3 COMPLETE: GAP-PL-001 HLP Dynamic Pricing Engineering Spec"
   git push
   ```

---

## ✅ QUALITY CHECKLIST

Before submitting, verify:

- [ ] All 20 sections completed with appropriate depth
- [ ] H3 geo-indexing algorithm fully specified
- [ ] Demand forecasting model architecture detailed
- [ ] Price elasticity/optimization math documented
- [ ] Integration requirements for 3+ OTAs specified
- [ ] Complete data model with schemas
- [ ] All business rules enumerated
- [ ] Error handling comprehensive
- [ ] Performance SLAs defined
- [ ] Implementation roadmap realistic

---

## 🔗 RELATED DOCUMENTS

| Document | Purpose |
|----------|---------|
| `knowledge/pricing/KD-PL-001-hlp-dynamic-pricing.md` | Research foundation (REQUIRED) |
| `specs/ai-workforce/SPEC-SKILL-261-268.md` | Reference spec format |
| `docs/AGENT_GUIDE.md` | Process overview |
| `registry/MASTER_SKILL_REGISTRY.md` | SKILL-101 definition |

---

**BEGIN SPECIFICATION NOW**


