# Skill Specification: Advanced Analytics Intelligence Platform

> **Skills Covered**: SKILL-043, SKILL-044, SKILL-045, SKILL-090, SKILL-105, SKILL-106
> **Category**: Analytics / Business Intelligence
> **Phase**: Phase 2 - Group 1 (Advanced Analytics)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 1.txt (~6,400 lines)

---

## 📋 EXECUTIVE SUMMARY

The Advanced Analytics Intelligence Platform delivers **6 analytics skills** that transform property management from reactive reporting to predictive intelligence:

- **<10% MAPE** forecast accuracy for revenue predictions
- **<500ms** real-time dashboard latency
- **95% accuracy** on NLP sentiment analysis
- **25% reduction** in manual reporting time
- **Processing** 1000+ concurrent WebSocket connections

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-043** | Real-Time Dashboard | Visualization | WebSocket-driven live operational updates |
| **SKILL-044** | Performance Forecasting | Predictive | ML-powered revenue/occupancy forecasting |
| **SKILL-045** | Benchmarking Analytics | Intelligence | Dynamic comp set generation and market positioning |
| **SKILL-090** | Housekeeping Performance | Operations | Staff metrics, quality tracking, efficiency analysis |
| **SKILL-105** | Conversation Intelligence | NLP/AI | Sentiment analysis and topic extraction |
| **SKILL-106** | Market Intelligence | Strategy | Macro trends and investment decision support |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| Analytics Dashboards | Layer 6: Applications | React 19 + TypeScript |
| Analytics Domain | Layer 5: Domain Bundles | Analytics domain bundle |
| Analytics Skills | Layer 4: Skills Layer | SKILL.md files |
| ML Pipeline | Layer 3: Hot Path | Python (Prophet, scikit-learn) |
| Time-Series Storage | Layer 2: Cold Path | TimescaleDB + PostgreSQL |
| Event Streaming | Layer 1: Infrastructure | Redpanda + Redis Pub/Sub |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-043 (Dashboard) | **Hot** | Real-time WebSocket streaming |
| SKILL-044 (Forecasting) | **Hot** | ML inference, Prophet models |
| SKILL-045 (Benchmarking) | **Hybrid** | AI matching + cached market data |
| SKILL-090 (Housekeeping) | **Cold** | Deterministic metrics calculation |
| SKILL-105 (Conversation) | **Hot** | OpenAI API for NLP |
| SKILL-106 (Market Intel) | **Hybrid** | AI analysis + data aggregation |

### MCP Server Requirements

```yaml
mcp_servers:
  # Read Operations
  - mcp://analytics/forecast-data       # Forecast results
  - mcp://analytics/benchmarks          # Comp set data
  - mcp://analytics/market-intel        # Market trends
  - mcp://analytics/housekeeping-stats  # Operations metrics
  
  # Write Operations
  - mcp://analytics/trigger-forecast    # Initiate ML pipeline
  - mcp://analytics/update-dashboard    # Push dashboard updates
  
  # Real-Time
  - mcp://websocket/broadcast           # Dashboard streaming
  - mcp://redis/pubsub                  # Event distribution
  
  # Financial (TigerBeetle)
  - mcp://treasury-read                 # Revenue data
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| WebSocket (FastAPI) | ✅ Aligned | FastAPI for Hot Path |
| TimescaleDB | ✅ Aligned | Time-series extension |
| Redis Pub/Sub | ✅ Aligned | Event distribution |
| PostgreSQL 16+ | ✅ Aligned | Primary database |
| Prophet ML | ✅ Aligned | Python Hot Path |
| OpenAI API | ✅ Aligned | NLP services |
| ECS/Fargate | ⚠️ Note | Research mentions K8s, we use ECS |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-043: Real-Time Dashboard

#### Purpose
WebSocket-driven live operational updates providing <500ms latency for property performance monitoring with drill-down capabilities from portfolio to unit level.

#### Technical Architecture
```python
from fastapi import FastAPI, WebSocket, WebSocketDisconnect
from typing import Set
import asyncpg
import redis.asyncio as redis
import json

class RealTimeDashboardService:
    """
    WebSocket-driven dashboard with Redis Pub/Sub.
    Achieves <500ms update latency, 1000+ concurrent connections.
    """
    
    def __init__(self):
        self.active_connections: Set[WebSocket] = set()
        self.redis_client = None
        self.db_pool = None
    
    async def connect(self, websocket: WebSocket, user_id: str):
        """Accept WebSocket connection with JWT validation."""
        await websocket.accept()
        self.active_connections.add(websocket)
        
        # Subscribe to user's property channels
        properties = await self._get_user_properties(user_id)
        for prop_id in properties:
            await self._subscribe_channel(f"property:{prop_id}")
    
    async def broadcast_update(self, channel: str, data: dict):
        """Broadcast update to all subscribed clients."""
        message = json.dumps({
            "channel": channel,
            "timestamp": datetime.utcnow().isoformat(),
            "data": data
        })
        
        # Publish to Redis for cross-instance distribution
        await self.redis_client.publish(channel, message)
    
    async def handle_postgres_notify(self, connection, pid, channel, payload):
        """Handle PostgreSQL LISTEN/NOTIFY events."""
        data = json.loads(payload)
        await self.broadcast_update(channel, data)
    
    async def setup_db_listeners(self):
        """Setup PostgreSQL triggers for real-time events."""
        async with self.db_pool.acquire() as conn:
            await conn.add_listener('booking_update', self.handle_postgres_notify)
            await conn.add_listener('revenue_update', self.handle_postgres_notify)
            await conn.add_listener('occupancy_change', self.handle_postgres_notify)
```

#### Dashboard Components
| Component | Update Frequency | Data Source |
|-----------|------------------|-------------|
| Occupancy Gauge | Real-time | PostgreSQL NOTIFY |
| Revenue Chart | 5-second batch | Redis cache |
| Booking Feed | Real-time | Redpanda stream |
| Alert Panel | Real-time | Event processor |
| Performance KPIs | 1-minute refresh | TimescaleDB |

#### WebSocket Message Schema
```json
{
  "dashboard_update": {
    "type": "occupancy_change",
    "property_id": "uuid",
    "timestamp": "2026-01-07T10:00:00Z",
    "data": {
      "current_occupancy": 0.85,
      "change_delta": 0.02,
      "trend": "increasing",
      "forecast_7d": 0.82
    },
    "metadata": {
      "source": "booking_engine",
      "correlation_id": "uuid"
    }
  }
}
```

#### Performance SLAs
| Metric | Target |
|--------|--------|
| Update latency | <500ms |
| Connection capacity | 1000+ concurrent |
| Uptime | 99.9% |
| Reconnection time | <3 seconds |

---

### SKILL-044: Performance Forecasting

#### Purpose
ML-powered revenue and occupancy forecasting using Prophet and LSTM models with <10% MAPE accuracy, handling seasonality, trends, and holiday effects.

#### ML Model Architecture
```python
from prophet import Prophet
import pandas as pd
import numpy as np
from sklearn.ensemble import GradientBoostingRegressor
from typing import Tuple, List

class PerformanceForecastingEngine:
    """
    Ensemble forecasting with Prophet + XGBoost.
    Achieves <10% MAPE for 12-month revenue predictions.
    """
    
    def __init__(self, property_id: str):
        self.property_id = property_id
        self.prophet_model = None
        self.xgboost_model = None
        self.ensemble_weights = [0.6, 0.4]  # Prophet, XGBoost
    
    def train_prophet_model(self, historical_data: pd.DataFrame):
        """Train Prophet for time series decomposition."""
        self.prophet_model = Prophet(
            yearly_seasonality=True,
            weekly_seasonality=True,
            daily_seasonality=False,
            holidays=self._get_holiday_df(),
            changepoint_prior_scale=0.05,
            seasonality_mode='multiplicative'
        )
        
        # Add custom regressors
        self.prophet_model.add_regressor('local_events')
        self.prophet_model.add_regressor('competitor_rates')
        
        # Fit model
        df = historical_data.rename(columns={'date': 'ds', 'revenue': 'y'})
        self.prophet_model.fit(df)
    
    def generate_forecast(
        self, 
        horizon_days: int = 365,
        include_components: bool = True
    ) -> ForecastResult:
        """Generate revenue forecast with confidence intervals."""
        
        # Create future dataframe
        future = self.prophet_model.make_future_dataframe(
            periods=horizon_days, 
            freq='D'
        )
        
        # Add regressor values for future dates
        future['local_events'] = self._predict_future_events(future['ds'])
        future['competitor_rates'] = self._predict_competitor_rates(future['ds'])
        
        # Generate Prophet forecast
        prophet_forecast = self.prophet_model.predict(future)
        
        # Generate XGBoost forecast
        xgb_forecast = self._xgboost_predict(future)
        
        # Ensemble combination
        ensemble_forecast = (
            self.ensemble_weights[0] * prophet_forecast['yhat'] +
            self.ensemble_weights[1] * xgb_forecast
        )
        
        return ForecastResult(
            property_id=self.property_id,
            predictions=ensemble_forecast.tolist(),
            confidence_lower=prophet_forecast['yhat_lower'].tolist(),
            confidence_upper=prophet_forecast['yhat_upper'].tolist(),
            components=prophet_forecast[['trend', 'yearly', 'weekly']].to_dict() if include_components else None,
            mape=self._calculate_mape(),
            generated_at=datetime.utcnow()
        )
    
    def _calculate_mape(self) -> float:
        """Calculate Mean Absolute Percentage Error."""
        # Cross-validation for accuracy assessment
        cv_results = cross_validation(
            self.prophet_model,
            initial='365 days',
            period='90 days',
            horizon='30 days'
        )
        return performance_metrics(cv_results)['mape'].mean()
```

#### Forecast Types
| Forecast | Horizon | Accuracy Target | Refresh |
|----------|---------|-----------------|---------|
| Revenue | 12 months | <10% MAPE | Daily |
| Occupancy | 90 days | <8% MAPE | Daily |
| ADR | 30 days | <5% MAPE | Hourly |
| Demand | 7 days | <3% MAPE | Real-time |

#### Output Schema
```json
{
  "performance_forecast": {
    "property_id": "uuid",
    "generated_at": "2026-01-07T10:00:00Z",
    "model_version": "prophet_v1.1_ensemble",
    "forecast": {
      "revenue": [
        {
          "date": "2026-02-01",
          "predicted": 45000.00,
          "lower_bound": 42000.00,
          "upper_bound": 48000.00,
          "confidence": 0.95
        }
      ],
      "occupancy": [
        {
          "date": "2026-02-01",
          "predicted": 0.82,
          "lower_bound": 0.78,
          "upper_bound": 0.86
        }
      ]
    },
    "components": {
      "trend": "increasing",
      "seasonality": {
        "yearly_peak": "July",
        "weekly_peak": "Saturday"
      },
      "holiday_impact": {
        "new_years": 1.35,
        "valentines": 1.20
      }
    },
    "accuracy": {
      "mape": 0.078,
      "rmse": 3500.00,
      "r_squared": 0.92
    }
  }
}
```

---

### SKILL-045: Benchmarking Analytics

#### Purpose
Dynamic competitive set generation using algorithmic matching with distance, amenities, and bedroom similarity, providing MPI, ARI, and RGI calculations.

#### Core Logic
```python
from dataclasses import dataclass
from typing import List
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

@dataclass
class CompSetProperty:
    property_id: str
    match_score: float
    distance_miles: float
    bedrooms: int
    avg_rate: float
    occupancy: float
    revenue: float

class BenchmarkingEngine:
    """
    Dynamic comp set generation with market positioning.
    Match scores >70 required for inclusion.
    """
    
    def __init__(self, property_id: str, market_data_client):
        self.property_id = property_id
        self.market_client = market_data_client
        self.airdna_accuracy = {'airbnb': 0.949, 'vrbo': 0.987}
    
    def generate_comp_set(
        self,
        max_properties: int = 100,
        max_distance_miles: float = 10.0,
        min_match_score: float = 70.0
    ) -> List[CompSetProperty]:
        """Generate comparable property set."""
        
        # Get subject property features
        subject = self._get_property_features(self.property_id)
        
        # Fetch nearby properties from market data
        candidates = self.market_client.get_properties_in_radius(
            lat=subject.latitude,
            lon=subject.longitude,
            radius_miles=max_distance_miles
        )
        
        comp_set = []
        for candidate in candidates:
            match_score = self._calculate_match_score(subject, candidate)
            
            if match_score >= min_match_score:
                comp_set.append(CompSetProperty(
                    property_id=candidate.id,
                    match_score=match_score,
                    distance_miles=self._haversine_distance(subject, candidate),
                    bedrooms=candidate.bedrooms,
                    avg_rate=candidate.avg_rate,
                    occupancy=candidate.occupancy,
                    revenue=candidate.revenue
                ))
        
        # Sort by match score and limit
        comp_set.sort(key=lambda x: x.match_score, reverse=True)
        return comp_set[:max_properties]
    
    def _calculate_match_score(self, subject, candidate) -> float:
        """Calculate similarity score (0-100)."""
        weights = {
            'bedrooms': 0.25,
            'bathrooms': 0.15,
            'guests': 0.15,
            'amenities': 0.20,
            'property_type': 0.15,
            'distance': 0.10
        }
        
        scores = {
            'bedrooms': 100 if subject.bedrooms == candidate.bedrooms else max(0, 100 - abs(subject.bedrooms - candidate.bedrooms) * 20),
            'bathrooms': 100 if subject.bathrooms == candidate.bathrooms else max(0, 100 - abs(subject.bathrooms - candidate.bathrooms) * 15),
            'guests': max(0, 100 - abs(subject.max_guests - candidate.max_guests) * 10),
            'amenities': self._amenity_similarity(subject.amenities, candidate.amenities) * 100,
            'property_type': 100 if subject.property_type == candidate.property_type else 50,
            'distance': max(0, 100 - self._haversine_distance(subject, candidate) * 10)
        }
        
        return sum(scores[k] * weights[k] for k in weights)
    
    def calculate_indexes(self, comp_set: List[CompSetProperty]) -> BenchmarkIndexes:
        """Calculate MPI, ARI, and RGI."""
        subject = self._get_property_features(self.property_id)
        
        comp_avg_occupancy = np.mean([p.occupancy for p in comp_set])
        comp_avg_rate = np.mean([p.avg_rate for p in comp_set])
        comp_avg_revenue = np.mean([p.revenue for p in comp_set])
        
        return BenchmarkIndexes(
            mpi=subject.occupancy / comp_avg_occupancy * 100,  # Market Penetration Index
            ari=subject.avg_rate / comp_avg_rate * 100,         # Average Rate Index
            rgi=subject.revenue / comp_avg_revenue * 100,       # Revenue Generation Index
            percentile_rank=self._calculate_percentile(subject.revenue, comp_set)
        )
```

#### Benchmark Metrics
| Index | Formula | Interpretation |
|-------|---------|----------------|
| **MPI** | Property Occ / Comp Occ × 100 | >100 = outperforming on occupancy |
| **ARI** | Property ADR / Comp ADR × 100 | >100 = premium pricing position |
| **RGI** | Property RevPAR / Comp RevPAR × 100 | >100 = overall revenue leader |

#### Output Schema
```json
{
  "benchmarking_analysis": {
    "property_id": "uuid",
    "comp_set": {
      "total_properties": 85,
      "avg_match_score": 82.5,
      "coverage_radius_miles": 8.2
    },
    "indexes": {
      "mpi": 108.5,
      "ari": 95.2,
      "rgi": 103.3,
      "percentile_rank": 72
    },
    "market_position": {
      "occupancy_vs_market": "+8.5%",
      "rate_vs_market": "-4.8%",
      "revenue_vs_market": "+3.3%"
    },
    "recommendations": [
      "Rate opportunity: market supports 5% increase",
      "Occupancy leader in comp set"
    ]
  }
}
```

---

### SKILL-090: Housekeeping Performance Analytics

#### Purpose
Staff performance tracking with time-per-clean metrics, quality scores, photo verification, and efficiency optimization across multi-property operations.

#### Core Logic
```python
from datetime import datetime, timedelta
from typing import List, Dict
from dataclasses import dataclass

@dataclass
class CleaningTask:
    task_id: str
    property_id: str
    staff_id: str
    scheduled_start: datetime
    actual_start: datetime
    actual_end: datetime
    quality_score: float
    photos_submitted: int
    issues_found: List[str]

class HousekeepingAnalyticsEngine:
    """
    Staff performance and efficiency analytics.
    Tracks time-per-clean, quality scores, and cost metrics.
    """
    
    def __init__(self, portfolio_id: str):
        self.portfolio_id = portfolio_id
    
    def calculate_staff_metrics(
        self, 
        staff_id: str, 
        date_range: Tuple[date, date]
    ) -> StaffPerformanceMetrics:
        """Calculate comprehensive staff performance metrics."""
        
        tasks = self._get_staff_tasks(staff_id, date_range)
        
        # Time metrics
        cleaning_times = [(t.actual_end - t.actual_start).total_seconds() / 60 for t in tasks]
        scheduled_times = [(t.actual_start - t.scheduled_start).total_seconds() / 60 for t in tasks]
        
        return StaffPerformanceMetrics(
            staff_id=staff_id,
            total_cleans=len(tasks),
            avg_time_per_clean=np.mean(cleaning_times),
            time_variance=np.std(cleaning_times),
            on_time_rate=sum(1 for t in scheduled_times if t <= 15) / len(tasks),
            avg_quality_score=np.mean([t.quality_score for t in tasks]),
            photo_compliance=sum(1 for t in tasks if t.photos_submitted >= 5) / len(tasks),
            issues_per_clean=sum(len(t.issues_found) for t in tasks) / len(tasks),
            efficiency_score=self._calculate_efficiency(tasks)
        )
    
    def calculate_property_metrics(self, property_id: str) -> PropertyCleaningMetrics:
        """Calculate property-level cleaning metrics."""
        
        tasks = self._get_property_tasks(property_id)
        costs = self._get_cleaning_costs(property_id)
        
        return PropertyCleaningMetrics(
            property_id=property_id,
            avg_clean_time_minutes=np.mean([self._task_duration(t) for t in tasks]),
            cost_per_clean=np.mean(costs),
            quality_trend=self._calculate_trend([t.quality_score for t in tasks]),
            re_clean_rate=self._calculate_reclean_rate(tasks),
            turnover_efficiency=self._calculate_turnover_efficiency(property_id)
        )
    
    def generate_optimization_recommendations(self) -> List[Recommendation]:
        """Generate data-driven optimization recommendations."""
        
        staff_metrics = self._get_all_staff_metrics()
        property_metrics = self._get_all_property_metrics()
        
        recommendations = []
        
        # Identify underperformers
        for staff in staff_metrics:
            if staff.efficiency_score < 70:
                recommendations.append(Recommendation(
                    type='training',
                    target_id=staff.staff_id,
                    message=f"Staff efficiency below threshold ({staff.efficiency_score}%)",
                    priority='medium'
                ))
        
        # Identify scheduling opportunities
        for prop in property_metrics:
            if prop.turnover_efficiency < 80:
                recommendations.append(Recommendation(
                    type='scheduling',
                    target_id=prop.property_id,
                    message=f"Turnover efficiency can be improved",
                    priority='high'
                ))
        
        return recommendations
```

#### Metrics Dashboard
| Metric | Calculation | Target |
|--------|-------------|--------|
| Time per Clean | Actual duration / unit size | <45 min/1BR |
| Quality Score | Inspection checklist | >90% |
| On-Time Rate | Started within 15 min | >95% |
| Photo Compliance | Min 5 photos/clean | 100% |
| Re-Clean Rate | Re-cleans / total cleans | <2% |

#### Output Schema
```json
{
  "housekeeping_analytics": {
    "portfolio_id": "uuid",
    "period": "2026-01-01 to 2026-01-07",
    "staff_performance": [
      {
        "staff_id": "uuid",
        "name": "Maria Garcia",
        "total_cleans": 42,
        "avg_time_minutes": 38.5,
        "quality_score": 94.2,
        "on_time_rate": 0.97,
        "efficiency_rank": 2
      }
    ],
    "property_metrics": [
      {
        "property_id": "uuid",
        "avg_clean_time": 42.0,
        "cost_per_clean": 85.00,
        "quality_trend": "improving",
        "re_clean_rate": 0.01
      }
    ],
    "cost_analysis": {
      "total_labor_cost": 12500.00,
      "total_supplies_cost": 2100.00,
      "cost_per_turnover": 95.50,
      "vs_budget": -5.2
    }
  }
}
```

---

### SKILL-105: Conversation Summary Intelligence

#### Purpose
NLP-powered sentiment analysis using GPT-4 with aspect-based topic extraction, automated summarization, and predictive guest satisfaction modeling.

#### Core Logic
```python
from openai import AsyncOpenAI
from typing import List, Tuple
import json

class ConversationIntelligenceEngine:
    """
    NLP sentiment analysis with OpenAI GPT-4.
    Achieves 95% accuracy on sentiment classification.
    """
    
    def __init__(self):
        self.client = AsyncOpenAI()
        self.model = "gpt-4-turbo-preview"
    
    async def analyze_conversation(
        self, 
        messages: List[Message],
        include_pii_redaction: bool = True
    ) -> ConversationAnalysis:
        """Analyze conversation for sentiment and topics."""
        
        # Redact PII if required
        if include_pii_redaction:
            messages = await self._redact_pii(messages)
        
        # Prepare conversation text
        conversation_text = self._format_conversation(messages)
        
        # Call GPT-4 for analysis
        response = await self.client.chat.completions.create(
            model=self.model,
            messages=[
                {"role": "system", "content": self._get_analysis_prompt()},
                {"role": "user", "content": conversation_text}
            ],
            response_format={"type": "json_object"},
            temperature=0.3
        )
        
        analysis = json.loads(response.choices[0].message.content)
        
        return ConversationAnalysis(
            overall_sentiment=analysis['sentiment']['overall'],
            sentiment_score=analysis['sentiment']['score'],
            topics=analysis['topics'],
            action_items=analysis['action_items'],
            escalation_needed=analysis['escalation_needed'],
            guest_satisfaction_prediction=analysis['satisfaction_prediction'],
            summary=analysis['summary']
        )
    
    def _get_analysis_prompt(self) -> str:
        return """Analyze this guest conversation and provide:
        1. Overall sentiment (very_positive, positive, neutral, negative, very_negative)
        2. Sentiment score (-1.0 to 1.0)
        3. Main topics discussed with sentiment for each
        4. Action items for the host
        5. Whether escalation is needed (true/false)
        6. Predicted guest satisfaction (1-10)
        7. Brief summary (max 100 words)
        
        Return as JSON with keys: sentiment, topics, action_items, escalation_needed, satisfaction_prediction, summary"""
    
    async def batch_analyze(
        self, 
        conversations: List[List[Message]]
    ) -> List[ConversationAnalysis]:
        """Batch analyze multiple conversations."""
        
        tasks = [self.analyze_conversation(conv) for conv in conversations]
        return await asyncio.gather(*tasks)
    
    async def _redact_pii(self, messages: List[Message]) -> List[Message]:
        """Redact personally identifiable information."""
        
        pii_patterns = [
            (r'\b\d{3}-\d{2}-\d{4}\b', '[SSN]'),  # SSN
            (r'\b\d{16}\b', '[CARD]'),             # Credit card
            (r'\b[\w.-]+@[\w.-]+\.\w+\b', '[EMAIL]'),
            (r'\b\d{3}[-.]?\d{3}[-.]?\d{4}\b', '[PHONE]')
        ]
        
        redacted = []
        for msg in messages:
            text = msg.content
            for pattern, replacement in pii_patterns:
                text = re.sub(pattern, replacement, text)
            redacted.append(Message(sender=msg.sender, content=text, timestamp=msg.timestamp))
        
        return redacted
```

#### Sentiment Categories
| Category | Score Range | Action |
|----------|-------------|--------|
| Very Positive | 0.7 to 1.0 | Request review |
| Positive | 0.3 to 0.7 | Standard follow-up |
| Neutral | -0.3 to 0.3 | Monitor |
| Negative | -0.7 to -0.3 | Priority response |
| Very Negative | -1.0 to -0.7 | Immediate escalation |

#### Output Schema
```json
{
  "conversation_analysis": {
    "conversation_id": "uuid",
    "analyzed_at": "2026-01-07T10:00:00Z",
    "sentiment": {
      "overall": "positive",
      "score": 0.65,
      "confidence": 0.92
    },
    "topics": [
      {
        "topic": "check_in_process",
        "sentiment": "positive",
        "mentions": 3
      },
      {
        "topic": "cleanliness",
        "sentiment": "very_positive",
        "mentions": 2
      }
    ],
    "action_items": [
      {
        "action": "Send local restaurant recommendations",
        "priority": "low",
        "assignee": "host"
      }
    ],
    "escalation_needed": false,
    "satisfaction_prediction": 8.5,
    "summary": "Guest expressed satisfaction with check-in and cleanliness. Requested dining recommendations. Overall positive experience."
  }
}
```

---

### SKILL-106: Market Intelligence

#### Purpose
Macro-trend analysis for investment decision support with supply growth tracking, regulatory change monitoring, and competitive move detection across 120,000+ markets.

#### Core Logic
```python
from typing import Dict, List
from dataclasses import dataclass
import pandas as pd

@dataclass
class MarketTrend:
    metric: str
    current_value: float
    yoy_change: float
    trend_direction: str
    confidence: float

class MarketIntelligenceEngine:
    """
    Market trend analysis with AirDNA data integration.
    94.9% Airbnb accuracy, 98.7% Vrbo accuracy.
    """
    
    def __init__(self, market_id: str, data_provider):
        self.market_id = market_id
        self.provider = data_provider
        self.data_accuracy = {'airbnb': 0.949, 'vrbo': 0.987}
    
    async def analyze_market(self) -> MarketAnalysis:
        """Comprehensive market analysis."""
        
        # Fetch market data
        current_data = await self.provider.get_market_data(self.market_id)
        historical_data = await self.provider.get_historical_data(
            self.market_id, 
            years=3
        )
        
        trends = self._calculate_trends(current_data, historical_data)
        supply_analysis = self._analyze_supply_growth(historical_data)
        demand_signals = self._analyze_demand_signals(current_data)
        regulatory_alerts = await self._check_regulatory_changes()
        
        return MarketAnalysis(
            market_id=self.market_id,
            trends=trends,
            supply_analysis=supply_analysis,
            demand_signals=demand_signals,
            regulatory_alerts=regulatory_alerts,
            investment_score=self._calculate_investment_score(trends, supply_analysis),
            recommendations=self._generate_recommendations(trends)
        )
    
    def _calculate_trends(
        self, 
        current: Dict, 
        historical: pd.DataFrame
    ) -> List[MarketTrend]:
        """Calculate key market trends."""
        
        metrics = ['avg_daily_rate', 'occupancy_rate', 'revpar', 'supply_count']
        trends = []
        
        for metric in metrics:
            current_value = current[metric]
            yoy_value = historical[historical['date'] == historical['date'].max() - timedelta(days=365)][metric].iloc[0]
            
            yoy_change = (current_value - yoy_value) / yoy_value * 100
            trend_direction = 'increasing' if yoy_change > 0 else 'decreasing'
            
            trends.append(MarketTrend(
                metric=metric,
                current_value=current_value,
                yoy_change=yoy_change,
                trend_direction=trend_direction,
                confidence=self._calculate_trend_confidence(historical[metric])
            ))
        
        return trends
    
    def _analyze_supply_growth(self, historical: pd.DataFrame) -> SupplyAnalysis:
        """Analyze supply growth patterns."""
        
        supply_series = historical.groupby('date')['supply_count'].sum()
        growth_rate = supply_series.pct_change(periods=12).iloc[-1] * 100
        
        return SupplyAnalysis(
            current_supply=supply_series.iloc[-1],
            yoy_growth_rate=growth_rate,
            new_listings_30d=self._count_new_listings(30),
            deactivations_30d=self._count_deactivations(30),
            saturation_index=self._calculate_saturation()
        )
    
    def _calculate_investment_score(
        self, 
        trends: List[MarketTrend], 
        supply: SupplyAnalysis
    ) -> float:
        """Calculate overall market investment score (0-100)."""
        
        weights = {
            'revpar_trend': 0.30,
            'occupancy_trend': 0.25,
            'supply_growth': 0.20,
            'demand_stability': 0.15,
            'regulatory_risk': 0.10
        }
        
        scores = {
            'revpar_trend': self._score_trend(trends['revpar']),
            'occupancy_trend': self._score_trend(trends['occupancy']),
            'supply_growth': 100 - min(supply.yoy_growth_rate * 5, 50),
            'demand_stability': self._score_demand_stability(),
            'regulatory_risk': 100 - self._score_regulatory_risk()
        }
        
        return sum(scores[k] * weights[k] for k in weights)
```

#### Market Metrics
| Metric | Source | Update Frequency |
|--------|--------|------------------|
| ADR | AirDNA | Daily |
| Occupancy | AirDNA | Daily |
| RevPAR | Calculated | Daily |
| Supply Count | AirDNA | Daily |
| Demand Index | Multi-source | Weekly |

#### Output Schema
```json
{
  "market_intelligence": {
    "market_id": "austin_tx",
    "analyzed_at": "2026-01-07T10:00:00Z",
    "trends": [
      {
        "metric": "revpar",
        "current_value": 185.50,
        "yoy_change": 12.3,
        "trend_direction": "increasing",
        "confidence": 0.89
      }
    ],
    "supply_analysis": {
      "current_supply": 15420,
      "yoy_growth_rate": 8.5,
      "new_listings_30d": 245,
      "deactivations_30d": 112,
      "saturation_index": 0.72
    },
    "regulatory_alerts": [
      {
        "type": "permit_requirement",
        "effective_date": "2026-03-01",
        "impact": "moderate"
      }
    ],
    "investment_score": 78.5,
    "recommendations": [
      "Strong RevPAR growth supports investment",
      "Monitor supply growth - approaching saturation",
      "New permit requirements effective March 2026"
    ]
  }
}
```

---

## 🗄️ DATABASE SCHEMA

### TimescaleDB Hypertables

```sql
-- Performance Metrics (Time-Series)
CREATE TABLE property_metrics (
    time TIMESTAMPTZ NOT NULL,
    property_id UUID NOT NULL,
    metric_type VARCHAR(50) NOT NULL,
    value DECIMAL(12,4) NOT NULL,
    metadata JSONB
);

SELECT create_hypertable('property_metrics', 'time');

-- Create continuous aggregates for dashboards
CREATE MATERIALIZED VIEW property_metrics_hourly
WITH (timescaledb.continuous) AS
SELECT 
    time_bucket('1 hour', time) AS bucket,
    property_id,
    metric_type,
    AVG(value) as avg_value,
    MIN(value) as min_value,
    MAX(value) as max_value
FROM property_metrics
GROUP BY bucket, property_id, metric_type;

-- Forecast Results
CREATE TABLE forecast_results (
    forecast_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    property_id UUID NOT NULL,
    forecast_type VARCHAR(50) NOT NULL,
    forecast_date DATE NOT NULL,
    predicted_value DECIMAL(12,2) NOT NULL,
    lower_bound DECIMAL(12,2),
    upper_bound DECIMAL(12,2),
    model_version VARCHAR(50),
    mape DECIMAL(5,4),
    generated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Comp Set Cache
CREATE TABLE comp_sets (
    comp_set_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    subject_property_id UUID NOT NULL,
    comp_property_id UUID NOT NULL,
    match_score DECIMAL(5,2) NOT NULL,
    distance_miles DECIMAL(6,2),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    expires_at TIMESTAMPTZ DEFAULT NOW() + INTERVAL '24 hours'
);

-- Conversation Analysis
CREATE TABLE conversation_analysis (
    analysis_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    conversation_id UUID NOT NULL,
    property_id UUID NOT NULL,
    overall_sentiment VARCHAR(20) NOT NULL,
    sentiment_score DECIMAL(4,3),
    topics JSONB,
    action_items JSONB,
    escalation_needed BOOLEAN DEFAULT FALSE,
    satisfaction_prediction DECIMAL(3,1),
    summary TEXT,
    analyzed_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_metrics_property_time ON property_metrics(property_id, time DESC);
CREATE INDEX idx_forecast_property_date ON forecast_results(property_id, forecast_date);
CREATE INDEX idx_conversation_property ON conversation_analysis(property_id, analyzed_at DESC);
```

---

## 🔗 INTEGRATION ARCHITECTURE

### External Services

| Service | Purpose | Auth | Rate Limit |
|---------|---------|------|------------|
| AirDNA | Market data | API Key + OAuth | 1000/hour |
| OpenAI | NLP analysis | API Key | 3000/min |
| PredictHQ | Event data | API Key | 500/day |
| Weather APIs | Demand signals | API Key | 1000/day |

### Real-Time Data Flow

```
┌────────────────────────────────────────────────────────────────────┐
│                    Real-Time Analytics Pipeline                     │
├────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   Data Sources                                                      │
│   ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐            │
│   │   PMS    │ │  Market  │ │   IoT    │ │  Guest   │            │
│   │  Events  │ │   Data   │ │ Sensors  │ │  Comms   │            │
│   └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘            │
│        │            │            │            │                    │
│        └────────────┼────────────┼────────────┘                    │
│                     │                                              │
│                     ▼                                              │
│   ┌─────────────────────────────────────────────────────────────┐ │
│   │              Redpanda Event Streaming                        │ │
│   └────────────────────────────┬────────────────────────────────┘ │
│                                │                                   │
│         ┌──────────────────────┼──────────────────────┐           │
│         │                      │                      │            │
│         ▼                      ▼                      ▼            │
│   ┌──────────┐          ┌──────────┐          ┌──────────┐        │
│   │ Forecast │          │  Bench-  │          │Conversa- │        │
│   │  Engine  │          │ marking  │          │tion NLP  │        │
│   └────┬─────┘          └────┬─────┘          └────┬─────┘        │
│        │                     │                     │               │
│        └─────────────────────┼─────────────────────┘               │
│                              │                                     │
│                              ▼                                     │
│   ┌─────────────────────────────────────────────────────────────┐ │
│   │                   Redis Pub/Sub                              │ │
│   └────────────────────────────┬────────────────────────────────┘ │
│                                │                                   │
│                                ▼                                   │
│   ┌─────────────────────────────────────────────────────────────┐ │
│   │              WebSocket Dashboard Service                     │ │
│   └─────────────────────────────────────────────────────────────┘ │
│                                                                     │
└────────────────────────────────────────────────────────────────────┘
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Availability |
|-------|--------------|------------|--------------|
| SKILL-043 (Dashboard) | <500ms | 1000+ connections | 99.9% |
| SKILL-044 (Forecast) | <2s | 100 forecasts/min | 99.5% |
| SKILL-045 (Benchmark) | <2s | 500 req/min | 99.5% |
| SKILL-090 (Housekeeping) | <1s | 1000 req/min | 99.5% |
| SKILL-105 (Conversation) | <3s | 50 analysis/min | 99.0% |
| SKILL-106 (Market Intel) | <5s | 100 req/min | 99.5% |

---

## 🧪 TESTING STRATEGY

### Unit Tests
- Prophet model accuracy validation
- Sentiment classification accuracy
- Match score calculations
- WebSocket message handling

### Integration Tests
- AirDNA API connectivity
- OpenAI API fallback handling
- Redis Pub/Sub reliability
- TimescaleDB query performance

### Performance Tests
- 1000 concurrent WebSocket connections
- Forecast generation under load
- Batch conversation analysis

### Acceptance Criteria
| Metric | Target |
|--------|--------|
| Forecast MAPE | <10% |
| Sentiment accuracy | >95% |
| Dashboard latency | <500ms |
| System uptime | 99.5% |

---

## 🔐 SECURITY CONSIDERATIONS

### Data Protection
- PII redaction for conversation analysis
- Encrypted storage for guest communications
- API key rotation for external services

### Compliance
- GDPR: Data minimization in NLP
- SOC 2: Audit logging for analytics access
- CCPA: Consumer data access controls

### Access Control
| Role | Permissions |
|------|------------|
| Executive | All dashboards, market intel |
| Revenue Manager | Forecasts, benchmarks |
| Operations Manager | Housekeeping analytics |
| Property Manager | Property-level dashboards |

---

## 📁 FILE LOCATIONS

```
specs/analytics/
└── SPEC-SKILL-043-106-ADVANCED-ANALYTICS.md (this file)

knowledge/analytics/
└── KD-PHASE2-G1-advanced-analytics.md (research source)

skills/analytics/
├── SKILL-043-realtime-dashboard.md
├── SKILL-044-performance-forecasting.md
├── SKILL-045-benchmarking-analytics.md
├── SKILL-090-housekeeping-performance.md
├── SKILL-105-conversation-intelligence.md
└── SKILL-106-market-intelligence.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-043 (Dashboard) + Infrastructure |
| 3-4 | SKILL-044 (Forecasting) ML pipeline |
| 5-6 | SKILL-045 (Benchmarking) + SKILL-106 (Market) |
| 7-8 | SKILL-090 (Housekeeping) + SKILL-105 (NLP) |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

