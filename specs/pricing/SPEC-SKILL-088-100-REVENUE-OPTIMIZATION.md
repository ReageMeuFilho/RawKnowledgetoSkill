# Skill Specification: Revenue Optimization Intelligence System

> **Skills Covered**: SKILL-088, SKILL-095, SKILL-096, SKILL-097, SKILL-098, SKILL-099, SKILL-100
> **Category**: Pricing / Revenue Management
> **Phase**: Phase 2 - Group 3 (Revenue Optimization)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 3.txt (~7,800 lines)

---

## 📋 EXECUTIVE SUMMARY

The Revenue Optimization Intelligence System delivers **7 advanced revenue management skills** that serve as the "financial brain" of property operations, enabling:

- **15-25% RevPAR improvement** through dynamic pricing
- **95% forecast accuracy** over 3-month windows
- **50% reduction** in manual pricing tasks
- **Processing 4B+ data points/hour** for real-time decisions

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-095** | Competitor Rate Monitoring | Intelligence | Real-time competitor rate scraping and analysis |
| **SKILL-096** | Demand Sensing Engine | Forecasting | ML-powered demand prediction with 95% accuracy |
| **SKILL-097** | Length of Stay Optimization | Inventory | Dynamic min/max stay rules and gap filling |
| **SKILL-098** | Last-Minute Pricing | Pricing | Flash sales and progressive discount curves |
| **SKILL-099** | Seasonal Strategy | Strategy | Multi-year seasonal pattern management |
| **SKILL-100** | Group Booking Pricing | Sales | Corporate rates and room block management |
| **SKILL-088** | Overbooking Management | Risk | Strategic overbooking with walk protocols |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| Revenue Intelligence UI | Layer 6: Applications | React + TypeScript dashboards |
| Pricing Skills | Layer 5: Domain Bundles | Revenue domain bundle |
| Rate Calculator | Layer 4: Skills Layer | SKILL.md files with Hot Path |
| ML Pipeline | Layer 3: Hot Path | Python (scikit-learn, Prophet) |
| Financial Transactions | Layer 2: Cold Path | TigerBeetle ledger |
| Event Streaming | Layer 1: Infrastructure | Redpanda (not Kafka) |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-095 (Competitor Monitor) | **Hot** | Real-time scraping, AI analysis |
| SKILL-096 (Demand Sensing) | **Hot** | ML inference, pattern detection |
| SKILL-097 (LOS Optimization) | **Hybrid** | AI rules + deterministic calendar |
| SKILL-098 (Last-Minute) | **Hybrid** | AI triggers + rate workflows |
| SKILL-099 (Seasonal) | **Hot** | ML seasonal detection |
| SKILL-100 (Group Booking) | **Cold** | Deterministic pricing rules |
| SKILL-088 (Overbooking) | **Hybrid** | AI prediction + financial impact |

### MCP Server Requirements

```yaml
mcp_servers:
  # Read Operations
  - mcp://pricing/competitor-data     # Competitor intelligence
  - mcp://demand/forecast             # Demand predictions
  - mcp://analytics/revenue-metrics   # Performance data
  
  # Write Operations
  - mcp://pricing/calculate-rate      # Dynamic pricing
  - mcp://channel/push-rates          # Rate distribution
  - mcp://inventory/update-rules      # Stay rules
  
  # Financial (TigerBeetle)
  - mcp://treasury-read               # Revenue data
  - mcp://treasury-write              # Pricing transactions
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| Redpanda streaming | ✅ Aligned | Uses Redpanda (not Kafka) |
| TigerBeetle financial | ✅ Aligned | Revenue in TigerBeetle |
| PostgreSQL + ClickHouse | ✅ Aligned | Primary + analytics |
| Redis caching | ✅ Aligned | Rate caching layer |
| AWS ECS/Fargate | ✅ Aligned | Container orchestration |
| FastAPI services | ⚠️ Note | Hot path in Python, Cold in Rust/Axum |
| Temporal workflows | ✅ Aligned | Pricing workflow orchestration |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-095: Competitor Rate Monitoring

#### Purpose
Real-time competitor rate scraping and analysis that compares pricing across OTAs with automatic updates for maintaining competitive positioning.

#### Trigger Conditions
```yaml
triggers:
  - type: schedule
    cron: "*/15 * * * *"  # Every 15 minutes
  - type: event
    source: booking_received
  - type: manual
    action: refresh_comp_set
```

#### Core Logic
```python
class CompetitorMonitor:
    """
    Competitor rate monitoring with intelligent scraping.
    Achieves <15 minute data freshness, >95% scraping success.
    """
    
    def __init__(self, property_id: str, comp_set: List[str]):
        self.property_id = property_id
        self.comp_set = comp_set  # Up to 20 competitors
        self.redis_cache = RevenueCacheManager()
    
    async def scrape_competitor_rates(self) -> CompetitorSnapshot:
        """Scrape rates from all competitor properties."""
        rates = []
        for competitor_id in self.comp_set:
            try:
                rate = await self._scrape_single(competitor_id)
                rates.append(rate)
            except ScrapingError as e:
                # Fallback to cached data
                cached = self.redis_cache.get_competitor_rate(competitor_id)
                if cached:
                    rates.append(cached)
        
        return CompetitorSnapshot(
            property_id=self.property_id,
            rates=rates,
            scraped_at=datetime.utcnow()
        )
    
    def calculate_position(self, our_rate: Decimal) -> MarketPosition:
        """Determine our rate position vs competitors."""
        snapshot = self.get_latest_snapshot()
        competitor_rates = [r.rate for r in snapshot.rates]
        
        percentile = self._calculate_percentile(our_rate, competitor_rates)
        median_rate = statistics.median(competitor_rates)
        
        return MarketPosition(
            percentile=percentile,
            vs_median=(our_rate - median_rate) / median_rate,
            recommendation=self._get_recommendation(percentile)
        )
```

#### Data Requirements
| Data | Source | Freshness |
|------|--------|-----------|
| Competitor rates | OTA scraping | <15 minutes |
| Property metadata | PMS integration | Daily |
| Market comp set | User-defined | On change |

#### Output Schema
```json
{
  "competitor_snapshot": {
    "property_id": "uuid",
    "date": "2026-02-01",
    "competitors": [
      {
        "competitor_id": "airbnb_12345",
        "platform": "airbnb",
        "rate": 150.00,
        "min_stay": 2,
        "availability": "available",
        "similarity_score": 0.85
      }
    ],
    "market_position": {
      "percentile": 65,
      "vs_median": 0.08,
      "recommendation": "maintain"
    },
    "scraped_at": "2026-01-07T09:00:00Z"
  }
}
```

#### Performance SLAs
| Metric | Target |
|--------|--------|
| Data freshness | <15 minutes |
| Scraping success | >95% |
| Response time | <2 seconds |
| Comp set size | Up to 20 |

---

### SKILL-096: Demand Sensing Engine

#### Purpose
AI-powered demand forecasting processing 4B+ data points/hour, achieving 95% accuracy over 3-month windows through analysis of booking patterns, events, weather, and search volume.

#### ML Model Architecture
```python
class DemandSensingEngine:
    """
    Multi-horizon demand forecasting with ensemble models.
    Achieves 95% accuracy (3-month), 85% accuracy (6-month).
    """
    
    def __init__(self, property_id: str):
        self.property_id = property_id
        self.models = {
            'prophet': ProphetForecaster(),
            'lstm': AttentionLSTMForecaster(),
            'xgboost': XGBoostDemandModel()
        }
        self.ensemble_weights = [0.4, 0.35, 0.25]
    
    async def forecast_demand(
        self, 
        horizon_days: int = 90,
        include_events: bool = True,
        include_weather: bool = True
    ) -> DemandForecast:
        """Generate demand forecast with confidence intervals."""
        
        # Gather input signals
        signals = await self._gather_signals(
            include_events=include_events,
            include_weather=include_weather
        )
        
        # Run ensemble prediction
        predictions = []
        for model, weight in zip(self.models.values(), self.ensemble_weights):
            pred = model.predict(signals, horizon_days)
            predictions.append(pred * weight)
        
        ensemble_forecast = sum(predictions)
        confidence = self._calculate_confidence(predictions)
        
        return DemandForecast(
            property_id=self.property_id,
            predictions=[
                DailyPrediction(
                    date=date,
                    demand_score=score,
                    confidence_interval=confidence[i],
                    contributing_factors=self._identify_factors(date)
                )
                for i, (date, score) in enumerate(ensemble_forecast)
            ],
            model_accuracy=self._get_model_accuracy()
        )
    
    def detect_demand_spike(self) -> List[DemandEvent]:
        """Detect unusual demand patterns indicating events."""
        forecast = self.forecast_demand()
        historical_avg = self._get_historical_average()
        
        spikes = []
        for pred in forecast.predictions:
            if pred.demand_score > historical_avg * 1.3:
                spikes.append(DemandEvent(
                    date=pred.date,
                    spike_magnitude=pred.demand_score / historical_avg,
                    likely_cause=self._identify_cause(pred.date)
                ))
        
        return spikes
```

#### Input Signals
| Signal | Source | Weight |
|--------|--------|--------|
| Historical bookings | PMS (24+ months) | 40% |
| Event calendar | PredictHQ, Eventbrite | 20% |
| Weather forecasts | OpenWeatherMap | 15% |
| Search volume | Google Trends API | 15% |
| Competitor rates | SKILL-095 | 10% |

#### Output Schema
```json
{
  "demand_forecast": {
    "property_id": "uuid",
    "generated_at": "2026-01-07T09:00:00Z",
    "horizon": "90_days",
    "predictions": [
      {
        "date": "2026-02-01",
        "demand_score": 0.85,
        "confidence_interval": [0.78, 0.92],
        "contributing_factors": ["local_event", "weather", "seasonality"]
      }
    ],
    "detected_events": [
      {
        "date_range": "2026-02-14 to 2026-02-16",
        "event_type": "valentines_day",
        "demand_multiplier": 1.45
      }
    ],
    "model_accuracy": 0.95
  }
}
```

#### Performance SLAs
| Metric | Target |
|--------|--------|
| 3-month accuracy | >95% |
| 6-month accuracy | >85% |
| Prediction latency | <5 seconds |
| Retraining frequency | Weekly |

---

### SKILL-097: Length of Stay Optimization

#### Purpose
Dynamic minimum and maximum stay rule optimization that maximizes occupancy through intelligent gap-filling algorithms and orphan day prevention.

#### Core Logic
```python
class LengthOfStayOptimizer:
    """
    Dynamic stay rule optimization with gap filling.
    Achieves 5-10% occupancy improvement.
    """
    
    def __init__(self, property_id: str, turnover_cost: Decimal):
        self.property_id = property_id
        self.turnover_cost = turnover_cost
        self.demand_engine = DemandSensingEngine(property_id)
    
    def optimize_stay_rules(self, date: date) -> StayRules:
        """Calculate optimal min/max stay for a date."""
        
        demand = self.demand_engine.get_forecast(date)
        booking_window = (date - date.today()).days
        gaps = self._detect_calendar_gaps()
        
        # Far-out bookings: stricter min stay
        if booking_window > 30:
            min_stay = 3 if demand.demand_score > 0.7 else 2
        # Close-in: flexible to fill gaps
        else:
            min_stay = 1 if date in gaps else 2
        
        # Calculate turnover premium
        pricing_premium = self._calculate_turnover_premium(
            min_stay, self.turnover_cost
        )
        
        return StayRules(
            date=date,
            min_stay=min_stay,
            max_stay=14,
            gap_fill_logic="exact_match" if date in gaps else "standard",
            pricing_premium=pricing_premium,
            rule_profile="close_in" if booking_window <= 7 else "far_out"
        )
    
    def detect_orphan_days(self) -> List[OrphanDay]:
        """Find and flag orphan days (gaps of 1-2 days)."""
        calendar = self._get_booking_calendar()
        orphans = []
        
        for i, day in enumerate(calendar):
            if day.is_available:
                # Check if surrounded by bookings
                prev_booked = i > 0 and not calendar[i-1].is_available
                next_booked = i < len(calendar)-1 and not calendar[i+1].is_available
                
                if prev_booked and next_booked:
                    orphans.append(OrphanDay(
                        date=day.date,
                        gap_size=1,
                        recommended_action="drop_min_stay"
                    ))
        
        return orphans
```

#### Gap Filling Strategy
| Gap Size | Strategy | Min Stay Adjustment |
|----------|----------|---------------------|
| 1 day | Orphan rescue | Set min_stay = 1 |
| 2 days | Short-stay promotion | Set min_stay = 2 |
| 3+ days | Normal rules | Use demand-based rules |

#### Output Schema
```json
{
  "stay_optimization": {
    "property_id": "uuid",
    "date": "2026-02-01",
    "rules": {
      "min_stay": 2,
      "max_stay": 14,
      "gap_fill_active": true,
      "pricing_premium": 0.15
    },
    "orphan_days": [
      {
        "date": "2026-02-05",
        "action": "drop_min_stay",
        "estimated_fill_probability": 0.65
      }
    ],
    "estimated_occupancy_lift": 0.08
  }
}
```

---

### SKILL-098: Last-Minute Pricing

#### Purpose
Automated flash sale system that adjusts rates based on booking patterns, occupancy, and time-to-arrival, preventing revenue loss from unsold inventory.

#### Core Logic
```python
class LastMinutePricing:
    """
    Progressive discount engine for last-minute bookings.
    Achieves 15-25% conversion improvement.
    """
    
    DISCOUNT_CURVES = {
        'aggressive': [0.10, 0.20, 0.30, 0.40],  # Days: 7, 5, 3, 1
        'moderate': [0.05, 0.10, 0.15, 0.25],
        'conservative': [0.05, 0.08, 0.10, 0.15]
    }
    
    def __init__(self, property_id: str, strategy: str = 'moderate'):
        self.property_id = property_id
        self.discount_curve = self.DISCOUNT_CURVES[strategy]
    
    def evaluate_flash_sale(self, date: date) -> FlashSaleDecision:
        """Determine if flash sale should trigger."""
        
        days_out = (date - date.today()).days
        occupancy = self._get_current_occupancy(date)
        
        # Flash sale triggers
        should_trigger = (
            days_out <= 7 and
            occupancy < 0.40 and
            not self._is_high_demand_period(date)
        )
        
        if not should_trigger:
            return FlashSaleDecision(trigger=False)
        
        # Calculate discount based on urgency
        discount = self._get_discount_for_days(days_out)
        
        return FlashSaleDecision(
            trigger=True,
            discount_percentage=discount,
            urgency_level=self._calculate_urgency(days_out, occupancy),
            countdown_hours=days_out * 24,
            merchandising_tags=self._get_tags(discount)
        )
    
    def _get_discount_for_days(self, days_out: int) -> float:
        """Progressive discount based on days until arrival."""
        if days_out >= 7:
            return self.discount_curve[0]
        elif days_out >= 5:
            return self.discount_curve[1]
        elif days_out >= 3:
            return self.discount_curve[2]
        else:
            return self.discount_curve[3]
```

#### Trigger Rules
| Condition | Threshold | Action |
|-----------|-----------|--------|
| Days out | ≤7 days | Enable evaluation |
| Occupancy | <40% | Trigger flash sale |
| High demand | Detected | Suppress flash sale |
| Competitor discount | >20% | Match discount |

#### Output Schema
```json
{
  "last_minute_pricing": {
    "property_id": "uuid",
    "date": "2026-02-01",
    "flash_sale": {
      "trigger_active": true,
      "discount_percentage": 0.25,
      "urgency_level": "high",
      "countdown_hours": 48,
      "original_rate": 200.00,
      "sale_rate": 150.00
    },
    "merchandising": {
      "tags": ["Great Deal", "Limited Time"],
      "badge": "25% OFF",
      "expiry_display": "Ends in 48 hours"
    },
    "notification": {
      "send_to_watchers": true,
      "channel": ["email", "push"]
    }
  }
}
```

---

### SKILL-099: Seasonal Strategy Management

#### Purpose
Comprehensive seasonal pricing strategy that handles macro-demand curves, shoulder season transitions, and multi-year trend analysis for optimized year-round revenue.

#### Core Logic
```python
class SeasonalStrategyManager:
    """
    Multi-year seasonal pattern detection and optimization.
    Achieves 8-15% revenue improvement through seasonal planning.
    """
    
    SEASONS = ['peak', 'shoulder_high', 'shoulder_low', 'off_peak']
    
    def __init__(self, property_id: str, min_years: int = 3):
        self.property_id = property_id
        self.historical_data = self._load_historical(min_years)
    
    def detect_seasons(self) -> SeasonalCalendar:
        """Automatically identify seasonal patterns."""
        
        # Analyze multi-year booking patterns
        patterns = self._analyze_patterns()
        
        seasons = []
        for month in range(1, 13):
            avg_occupancy = patterns[month]['avg_occupancy']
            avg_adr = patterns[month]['avg_adr']
            
            season_type = self._classify_season(avg_occupancy, avg_adr)
            seasons.append(SeasonPeriod(
                month=month,
                season_type=season_type,
                strength=self._calculate_strength(avg_occupancy),
                historical_performance=patterns[month]
            ))
        
        return SeasonalCalendar(seasons=seasons)
    
    def get_seasonal_adjustment(self, date: date) -> SeasonalAdjustment:
        """Calculate pricing adjustment for date based on season."""
        
        calendar = self.detect_seasons()
        current_season = calendar.get_season(date)
        pacing = self._calculate_pacing(date)
        
        # Base adjustment from season
        base_modifier = {
            'peak': 0.30,
            'shoulder_high': 0.10,
            'shoulder_low': -0.05,
            'off_peak': -0.15
        }[current_season.season_type]
        
        # Pacing adjustment
        pacing_modifier = (pacing - 1.0) * 0.5  # 50% of pacing variance
        
        return SeasonalAdjustment(
            date=date,
            season=current_season.season_type,
            base_rate_modifier=base_modifier + pacing_modifier,
            min_stay_adjustment=self._get_min_stay_for_season(current_season),
            confidence=current_season.strength
        )
```

#### Season Classification
| Season Type | Occupancy | ADR vs Avg | Rate Modifier |
|-------------|-----------|------------|---------------|
| Peak | >85% | >120% | +30% |
| Shoulder High | 70-85% | 100-120% | +10% |
| Shoulder Low | 55-70% | 80-100% | -5% |
| Off Peak | <55% | <80% | -15% |

#### Output Schema
```json
{
  "seasonal_strategy": {
    "property_id": "uuid",
    "generated_at": "2026-01-07",
    "calendar": [
      {
        "month": 6,
        "season_type": "peak",
        "strength": 0.92,
        "recommended_modifier": 0.30,
        "min_stay": 4,
        "historical_performance": {
          "avg_occupancy": 0.89,
          "avg_adr": 245.00,
          "revpar": 218.05
        }
      }
    ],
    "pacing_analysis": {
      "current_vs_last_year": 1.15,
      "adjustment_recommendation": 0.08
    }
  }
}
```

---

### SKILL-100: Group Booking Pricing

#### Purpose
Automated group and corporate rate management with dynamic quoting, room block inventory management, and negotiation flexibility controls.

#### Core Logic
```python
class GroupBookingPricing:
    """
    Automated group rate calculation and management.
    Achieves 25-35% group conversion rate.
    """
    
    def __init__(self, property_id: str):
        self.property_id = property_id
        self.corporate_accounts = self._load_corporate_accounts()
    
    def calculate_group_rate(
        self, 
        room_nights: int,
        dates: DateRange,
        corporate_account_id: str = None
    ) -> GroupQuote:
        """Generate group booking quote."""
        
        # Get base rate for dates
        base_rate = self._get_avg_rate(dates)
        demand = self._get_demand_forecast(dates)
        
        # Calculate discount based on volume
        volume_discount = self._volume_discount(room_nights)
        
        # Corporate account additional discount
        corporate_discount = 0.0
        if corporate_account_id:
            account = self.corporate_accounts.get(corporate_account_id)
            if account:
                corporate_discount = account.negotiated_discount
        
        total_discount = min(volume_discount + corporate_discount, 0.25)
        quoted_rate = base_rate * (1 - total_discount)
        
        # Room block allocation
        block_size = self._calculate_block_size(room_nights, demand)
        
        return GroupQuote(
            group_id=self._generate_group_id(),
            room_nights=room_nights,
            dates=dates,
            base_rate=base_rate,
            quoted_rate=quoted_rate,
            discount_percentage=total_discount,
            room_block_size=block_size,
            release_date=dates.start - timedelta(days=14),
            attrition_threshold=0.80,
            valid_until=datetime.utcnow() + timedelta(days=7)
        )
    
    def _volume_discount(self, room_nights: int) -> float:
        """Calculate discount based on room night volume."""
        if room_nights >= 100:
            return 0.20
        elif room_nights >= 50:
            return 0.15
        elif room_nights >= 25:
            return 0.10
        elif room_nights >= 10:
            return 0.05
        return 0.0
```

#### Volume Discount Matrix
| Room Nights | Base Discount | Max with Corporate |
|-------------|---------------|--------------------|
| 10-24 | 5% | 10% |
| 25-49 | 10% | 15% |
| 50-99 | 15% | 20% |
| 100+ | 20% | 25% |

#### Output Schema
```json
{
  "group_quote": {
    "group_id": "GRP-2026-001",
    "property_id": "uuid",
    "quote_details": {
      "room_nights": 100,
      "dates": {
        "start": "2026-03-15",
        "end": "2026-03-18"
      },
      "base_rate": 180.00,
      "quoted_rate": 144.00,
      "discount_percentage": 0.20
    },
    "room_block": {
      "size": 35,
      "release_date": "2026-03-01",
      "attrition_threshold": 0.80,
      "attrition_penalty": 500.00
    },
    "terms": {
      "valid_until": "2026-01-14T23:59:59Z",
      "deposit_required": 0.25,
      "cancellation_policy": "14_days_full_refund"
    }
  }
}
```

---

### SKILL-088: Overbooking Management

#### Purpose
Strategic overbooking system with risk calculation, no-show prediction, and guest relocation protocols to maximize revenue while minimizing walk incidents.

#### Core Logic
```python
class OverbookingManager:
    """
    Risk-based overbooking with walk management.
    Achieves 3-7% revenue improvement with <2% walk rate.
    """
    
    def __init__(self, property_id: str, partner_hotels: List[str]):
        self.property_id = property_id
        self.partner_hotels = partner_hotels
        self.no_show_model = NoShowPredictor()
    
    def calculate_overbooking_level(self, date: date) -> OverbookingStrategy:
        """Calculate optimal overbooking for a date."""
        
        # Historical no-show and cancellation rates
        historical = self._get_historical_rates(date)
        no_show_rate = historical['no_show_rate']
        cancellation_rate = historical['cancellation_rate']
        
        # Current booking characteristics
        bookings = self._get_bookings(date)
        predicted_no_shows = sum(
            self.no_show_model.predict(b) for b in bookings
        )
        
        # Calculate risk score
        capacity = self._get_capacity()
        risk_score = self._calculate_risk(predicted_no_shows, capacity)
        
        # Determine overbooking level
        if risk_score < 0.10:
            level = int(capacity * 0.08)  # Aggressive: 8%
        elif risk_score < 0.20:
            level = int(capacity * 0.05)  # Moderate: 5%
        else:
            level = int(capacity * 0.02)  # Conservative: 2%
        
        return OverbookingStrategy(
            date=date,
            capacity=capacity,
            recommended_overbooking=level,
            risk_score=risk_score,
            no_show_prediction=predicted_no_shows,
            walk_cost_estimate=self._estimate_walk_cost(level)
        )
    
    async def execute_walk_protocol(
        self, 
        guest: Guest, 
        original_booking: Booking
    ) -> WalkResolution:
        """Execute guest relocation when walk is necessary."""
        
        # Find partner hotel availability
        for partner_id in self.partner_hotels:
            availability = await self._check_partner(partner_id, original_booking)
            if availability.rooms > 0:
                # Book at partner and calculate compensation
                partner_booking = await self._book_partner(
                    partner_id, guest, original_booking
                )
                compensation = self._calculate_compensation(
                    original_booking, partner_booking
                )
                
                return WalkResolution(
                    guest_id=guest.id,
                    partner_hotel=partner_id,
                    partner_booking=partner_booking,
                    compensation=compensation,
                    communication_sent=True
                )
        
        # No partner available - escalate
        return WalkResolution(
            guest_id=guest.id,
            escalate=True,
            escalation_reason="no_partner_availability"
        )
```

#### Risk Calculation
| Risk Score | Overbooking Level | Walk Probability |
|------------|-------------------|------------------|
| <10% | 8% of capacity | <1% |
| 10-20% | 5% of capacity | 1-2% |
| >20% | 2% of capacity | <1% |

#### Compensation Matrix
| Scenario | Compensation |
|----------|--------------|
| Walk to equal/better | Room + $100 credit |
| Walk to lower tier | Full refund + $200 |
| No availability | Full refund + $500 |

#### Output Schema
```json
{
  "overbooking_strategy": {
    "property_id": "uuid",
    "date": "2026-02-01",
    "capacity": 100,
    "current_bookings": 105,
    "overbooking_level": 5,
    "risk_analysis": {
      "risk_score": 0.15,
      "no_show_prediction": 8,
      "cancellation_prediction": 4,
      "expected_arrivals": 93
    },
    "walk_protocol": {
      "priority_partner": "partner_hotel_123",
      "walk_cost_estimate": 450.00,
      "compensation_budget": 600.00
    }
  }
}
```

---

## 🗄️ DATABASE SCHEMA

### Core Tables

```sql
-- Competitor Rate Snapshots
CREATE TABLE competitor_rates (
    rate_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(id),
    competitor_id VARCHAR(100) NOT NULL,
    platform VARCHAR(50) NOT NULL,
    rate_date DATE NOT NULL,
    rate DECIMAL(10,2) NOT NULL,
    min_stay INTEGER,
    availability_status VARCHAR(20),
    similarity_score DECIMAL(3,2),
    scraped_at TIMESTAMPTZ NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    
    -- Partition by month for efficient querying
    CONSTRAINT pk_competitor_rates PRIMARY KEY (rate_id, scraped_at)
) PARTITION BY RANGE (scraped_at);

-- Demand Forecasts
CREATE TABLE demand_forecasts (
    forecast_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(id),
    forecast_date DATE NOT NULL,
    demand_score DECIMAL(4,3) NOT NULL,
    confidence_lower DECIMAL(4,3),
    confidence_upper DECIMAL(4,3),
    contributing_factors JSONB,
    model_version VARCHAR(50),
    generated_at TIMESTAMPTZ DEFAULT NOW(),
    
    UNIQUE (property_id, forecast_date, model_version)
);

-- Pricing Rules
CREATE TABLE pricing_rules (
    rule_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(id),
    rule_type VARCHAR(50) NOT NULL, -- 'seasonal', 'last_minute', 'group', 'los'
    effective_date DATE NOT NULL,
    end_date DATE,
    rule_config JSONB NOT NULL,
    priority INTEGER DEFAULT 100,
    is_active BOOLEAN DEFAULT TRUE,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Overbooking Events
CREATE TABLE overbooking_events (
    event_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(id),
    event_date DATE NOT NULL,
    capacity INTEGER NOT NULL,
    overbooking_level INTEGER NOT NULL,
    risk_score DECIMAL(4,3),
    actual_no_shows INTEGER,
    actual_cancellations INTEGER,
    walks_required INTEGER DEFAULT 0,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Walk Incidents
CREATE TABLE walk_incidents (
    incident_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(id),
    booking_id UUID NOT NULL REFERENCES bookings(id),
    guest_id UUID NOT NULL REFERENCES guests(id),
    incident_date DATE NOT NULL,
    partner_hotel_id VARCHAR(100),
    compensation_amount DECIMAL(10,2),
    resolution_status VARCHAR(50),
    resolution_notes TEXT,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Group Quotes
CREATE TABLE group_quotes (
    quote_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL REFERENCES properties(id),
    group_name VARCHAR(200),
    corporate_account_id UUID REFERENCES corporate_accounts(id),
    room_nights INTEGER NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    base_rate DECIMAL(10,2) NOT NULL,
    quoted_rate DECIMAL(10,2) NOT NULL,
    discount_percentage DECIMAL(4,3),
    room_block_size INTEGER,
    release_date DATE,
    attrition_threshold DECIMAL(3,2),
    status VARCHAR(50) DEFAULT 'pending',
    valid_until TIMESTAMPTZ,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes for Performance
CREATE INDEX idx_competitor_rates_property_date 
    ON competitor_rates(property_id, rate_date);
CREATE INDEX idx_demand_forecasts_property_date 
    ON demand_forecasts(property_id, forecast_date);
CREATE INDEX idx_pricing_rules_property_active 
    ON pricing_rules(property_id, is_active) WHERE is_active = TRUE;
CREATE INDEX idx_overbooking_property_date 
    ON overbooking_events(property_id, event_date);
```

---

## 🔗 INTEGRATION ARCHITECTURE

### External APIs

| API | Purpose | Auth Method | Rate Limit |
|-----|---------|-------------|------------|
| Airbnb API | Competitor rates | OAuth 2.0 | 100/min |
| Booking.com API | Rate intelligence | API Key | 200/min |
| Vrbo API | Vacation rental data | OAuth 2.0 | 100/min |
| PredictHQ | Event detection | API Key | 500/day |
| OpenWeatherMap | Weather forecasts | API Key | 1000/day |

### Channel Distribution Flow

```
┌────────────────────────────────────────────────────────────────────┐
│                    Rate Distribution Pipeline                       │
├────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   Pricing Engine                                                    │
│        │                                                            │
│        ▼                                                            │
│   ┌─────────────────┐                                              │
│   │ Temporal        │──── Rate Update Workflow                     │
│   │ Workflow        │                                              │
│   └────────┬────────┘                                              │
│            │                                                        │
│            ▼                                                        │
│   ┌─────────────────┐                                              │
│   │ Redpanda        │──── rate.updated event                       │
│   │ Event Stream    │                                              │
│   └────────┬────────┘                                              │
│            │                                                        │
│    ┌───────┼───────┬───────┬───────┐                               │
│    ▼       ▼       ▼       ▼       ▼                               │
│ Airbnb  Vrbo  Booking  Direct  Other                               │
│ Adapter Adapter Adapter  Site   OTAs                               │
│                                                                     │
└────────────────────────────────────────────────────────────────────┘
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Availability |
|-------|--------------|------------|--------------|
| SKILL-095 (Competitor) | <2s | 1000 req/s | 99.9% |
| SKILL-096 (Demand) | <5s | 500 forecasts/s | 99.5% |
| SKILL-097 (LOS) | <1s | 2000 req/s | 99.9% |
| SKILL-098 (Last-Minute) | <500ms | 100 updates/s | 99.9% |
| SKILL-099 (Seasonal) | <3s | 200 req/s | 99.5% |
| SKILL-100 (Group) | <2s | 50 quotes/min | 99.5% |
| SKILL-088 (Overbooking) | <1s | 200 calc/s | 99.9% |

---

## 🧪 TESTING STRATEGY

### Unit Tests
- Pricing calculation accuracy
- Demand model predictions
- Gap detection algorithms
- Discount curve logic

### Integration Tests
- OTA API connectivity
- Rate distribution validation
- Event streaming reliability
- Database transaction integrity

### Performance Tests
- 4B data points/hour processing
- Sub-5-second forecast generation
- Concurrent rate updates

### Acceptance Criteria
| Metric | Target |
|--------|--------|
| Forecast accuracy (3-month) | >95% |
| Walk rate | <2% |
| Rate sync latency | <5 minutes |
| Revenue improvement | 15-25% |

---

## 🔐 SECURITY CONSIDERATIONS

### Data Protection
- AES-256 encryption for competitor intelligence
- TLS 1.3 for all API communications
- Row-level security for multi-tenant data

### Compliance
- GDPR: Anonymize guest data in forecasts
- PCI DSS: No cardholder data in pricing systems
- SOC 2: Audit logging for all pricing decisions

### Access Control
| Role | Permissions |
|------|------------|
| Revenue Director | Full access, strategy approval |
| Revenue Manager | Pricing adjustments, forecasts |
| Revenue Analyst | Read-only, reports |
| System Admin | Configuration, maintenance |

---

## 📁 FILE LOCATIONS

```
specs/pricing/
└── SPEC-SKILL-088-100-REVENUE-OPTIMIZATION.md (this file)

knowledge/pricing/
└── KD-PHASE2-G3-revenue-optimization.md (research source)

skills/pricing/
├── SKILL-095-competitor-monitoring.md
├── SKILL-096-demand-sensing.md
├── SKILL-097-los-optimization.md
├── SKILL-098-last-minute-pricing.md
├── SKILL-099-seasonal-strategy.md
├── SKILL-100-group-booking.md
└── SKILL-088-overbooking.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-095 + SKILL-096 (Intelligence core) |
| 3-4 | SKILL-097 + SKILL-098 (Pricing automation) |
| 5-6 | SKILL-099 + SKILL-100 (Strategy + Groups) |
| 7-8 | SKILL-088 (Risk management) + Integration |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

