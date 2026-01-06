# Skill Specification: Maintenance Brain Architecture

**Skills**: SKILL-270, SKILL-271, SKILL-272  
**Gap ID**: GAP-VEN-001  
**Status**: ✅ SPECIFIED  
**Date**: January 2026  
**Engineering Spec**: `knowledge/operations/ES-VEN-001-maintenance-brain.md` (8,209 lines)

---

## Skills Overview

| Skill ID | Name | Category | Priority |
|----------|------|----------|----------|
| SKILL-270 | Predictive Maintenance Intelligence | operations | P0 |
| SKILL-271 | Vendor Performance Optimization | operations | P0 |
| SKILL-272 | Maintenance Cost Forecasting | financial | P0 |

---

## SKILL-270: Predictive Maintenance Intelligence

### Description
AI-powered system that learns from maintenance history, identifies patterns, predicts failures before they occur, and recommends preventive actions to reduce emergency repairs and extend asset lifespans.

### Key Features

| Feature | Description | Implementation |
|---------|-------------|----------------|
| Pattern Recognition | Identify recurring issues by property/unit/asset | ML models trained on historical data |
| Failure Prediction | Predict equipment failures before occurrence | Time-series analysis + anomaly detection |
| Root Cause Detection | Trace symptoms back to underlying causes | Knowledge graph + causal inference |
| Preventive Scheduling | Recommend maintenance before failures | Risk scoring + scheduling optimization |
| IoT Integration | Real-time sensor data for anomaly detection | MQTT broker + stream processing |

### Technical Architecture

```
IoT Sensors → MQTT Broker → Stream Processing → Anomaly Detection
                                    ↓
Historical Data → Pattern Recognition → Prediction Models → Alert Generation
                                    ↓
                            Preventive Work Order Creation
```

### Performance Targets

| Metric | Target |
|--------|--------|
| Prediction Accuracy | >80% for common failures |
| Lead Time | 7-30 days before failure |
| Emergency Reduction | 50% fewer emergency repairs |
| False Positive Rate | <10% |

### Data Requirements

- 12+ months of maintenance history
- Asset registry with age/condition data
- IoT sensor data (temperature, vibration, pressure)
- Weather data for environmental correlation

---

## SKILL-271: Vendor Performance Optimization

### Description
Intelligent vendor selection, scoring, and dispatch system that optimizes for performance, cost, availability, and property familiarity to ensure the best vendor is assigned to every job.

### Key Features

| Feature | Description | Implementation |
|---------|-------------|----------------|
| Performance Scoring | Track and score vendor performance metrics | Weighted composite scoring |
| Smart Dispatch | Auto-select best vendor based on multiple factors | Multi-criteria decision algorithm |
| Load Balancing | Distribute work fairly across vendor network | Round-robin with performance bias |
| Cost Optimization | Balance quality with cost efficiency | Cost-performance frontier analysis |
| Relationship Building | Favor vendors with property familiarity | Familiarity score tracking |

### Vendor Scoring Algorithm

```python
composite_score = (
    0.40 × performance_score +    # First-time fix, completion rate, satisfaction
    0.25 × cost_score +           # Cost vs estimate, hourly rate efficiency
    0.20 × familiarity_score +    # Previous jobs at property, tenant feedback
    0.15 × availability_score     # Response time, current workload
)
```

### Vendor Selection Pipeline

1. **Trade Filter** - Match vendor specialization to issue type
2. **Coverage Filter** - Verify service area includes property
3. **Compliance Filter** - Confirm insurance/license current
4. **Availability Filter** - Check calendar and workload
5. **Score Calculation** - Compute composite score
6. **Owner Preference** - Apply owner vendor preferences
7. **Emergency Override** - Skip scoring for emergencies
8. **Load Balance** - Adjust for fair distribution
9. **Final Selection** - Dispatch to top-scoring vendor

### Performance Targets

| Metric | Target |
|--------|--------|
| Vendor Response Time | <2 hours |
| First-Time Fix Rate | >85% |
| Cost Variance | <10% over estimate |
| Vendor Satisfaction | >4.5/5 |

### Data Model

```json
{
  "vendor_id": "VENDOR-001",
  "performance_metrics": {
    "overall_score": 8.7,
    "response_time_avg": 2.3,
    "completion_rate": 0.96,
    "first_time_fix_rate": 0.88,
    "cost_variance_avg": -0.05,
    "satisfaction_rating": 4.6
  }
}
```

---

## SKILL-272: Maintenance Cost Forecasting

### Description
AI-powered cost estimation, budget forecasting, and financial analytics system that provides accurate cost predictions, manages approval workflows, and helps property managers control maintenance expenses.

### Key Features

| Feature | Description | Implementation |
|---------|-------------|----------------|
| Cost Estimation | Predict repair costs before vendor dispatch | Historical cost analysis + ML models |
| Budget Forecasting | Project monthly/annual maintenance spend | Time-series forecasting |
| Approval Automation | Route approvals based on cost thresholds | Rules engine + workflow orchestration |
| Cost Justification | Generate detailed expense breakdowns for owners | Automated reporting |
| Variance Analysis | Track actual vs estimated costs | Real-time monitoring |

### Cost Approval Thresholds

| Cost Range | Approval Level | Timeout | Escalation |
|------------|----------------|---------|------------|
| < $250 | Auto-Approve | Immediate | None |
| $250 - $1,000 | Property Manager | 24 hours | Regional Manager |
| > $1,000 | Property Owner | 48 hours | Auto-notify |
| Emergency | Override Available | Immediate | Post-approval |

### Cost Estimation Model

```json
{
  "estimated_range": {
    "low": 150,    // 80% of mid estimate
    "mid": 200,    // ML model prediction
    "high": 280    // 140% of mid estimate
  },
  "confidence": 0.85,
  "factors": [
    { "factor": "issue_complexity", "impact": 0.3 },
    { "factor": "vendor_rate", "impact": 0.25 },
    { "factor": "parts_required", "impact": 0.25 },
    { "factor": "travel_distance", "impact": 0.1 },
    { "factor": "urgency_premium", "impact": 0.1 }
  ]
}
```

### Performance Targets

| Metric | Target |
|--------|--------|
| Estimation Accuracy | ±15% of actual cost |
| Budget Forecast Accuracy | ±10% monthly |
| Approval Time | <24 hours for routine |
| Cost Savings | $12/door/month |

### Budget Dashboard Metrics

- Monthly maintenance spend (actual vs budget)
- Cost per door trending
- Category breakdown (HVAC, plumbing, electrical, etc.)
- Vendor cost efficiency rankings
- Emergency vs preventive ratio
- Owner chargeback tracking

---

## Integrated System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    MAINTENANCE BRAIN                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐            │
│  │  SKILL-270  │  │  SKILL-271  │  │  SKILL-272  │            │
│  │ Predictive  │  │   Vendor    │  │    Cost     │            │
│  │ Intelligence│  │ Optimization│  │ Forecasting │            │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘            │
│         │                │                │                    │
│         └────────────────┴────────────────┘                    │
│                          │                                      │
│              ┌───────────┴───────────┐                         │
│              │    BRAIN SERVICE      │                         │
│              │  AI Decision Engine   │                         │
│              └───────────┬───────────┘                         │
│                          │                                      │
│    ┌─────────────────────┼─────────────────────┐               │
│    │                     │                     │               │
│    ▼                     ▼                     ▼               │
│ ┌──────┐            ┌──────┐            ┌──────┐              │
│ │Intake│            │Vendor│            │Finance│              │
│ │Layer │            │Layer │            │Layer  │              │
│ └──────┘            └──────┘            └──────┘              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Technology Stack

| Component | Technology |
|-----------|------------|
| Backend | Python 3.14, Flask 3.1 |
| AI/ML | LangGraph, LangChain |
| Workflows | Temporal |
| Database | MongoDB, Redis, InfluxDB |
| Messaging | Kafka, MQTT |
| Infrastructure | Kubernetes, Istio |

---

## Implementation Timeline

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Phase 1** | Weeks 1-6 | Vendor dispatch, cost estimation, basic workflows |
| **Phase 2** | Weeks 7-12 | Scoring algorithm, approval automation, analytics |
| **Phase 3** | Weeks 13-18 | Predictive models, IoT integration, learning system |
| **Phase 4** | Weeks 19-24 | Optimization, scale, enterprise features |

---

## Success Metrics

| KPI | Target | Current |
|-----|--------|---------|
| Automation Rate | 80% | TBD |
| Cost Savings | $12/door/month | TBD |
| Emergency Reduction | 50% | TBD |
| First Response | <30 seconds | TBD |
| Tenant Satisfaction | >4.5/5 | TBD |

---

## Competitive Advantage

The Maintenance Brain represents a **paradigm shift** from reactive to proactive maintenance:

1. **Vendoroo** focuses on vendor coordination - we add **predictive intelligence**
2. **AppFolio** has basic AI dispatch - we add **continuous learning**
3. **Property Meld** has scheduling - we add **cost forecasting**
4. **No competitor** has the integrated **Predictive + Vendor + Cost** brain

---

## References

- Engineering Specification: `knowledge/operations/ES-VEN-001-maintenance-brain.md`
- Knowledge Document: `knowledge/operations/KD-VEN-001-maintenance-brain.md`
- Stage 2 Prompt: `docs/prompts/ENGINEERING_SPEC_PROMPT_MAINTENANCE_BRAIN.md`

