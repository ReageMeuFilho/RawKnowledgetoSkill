# Stage 2 Engineering Prompt: Maintenance Brain Architecture

> **Gap ID**: GAP-VEN-001
> **Skills Covered**: SKILL-270, SKILL-271, SKILL-272 (3 skills)
> **Priority**: P0 (MVP Critical)
> **Stage 1 Document**: `knowledge/operations/KD-VEN-001-maintenance-brain.md`
> **Quality Rating**: 9.5/10 ⭐ EXCEPTIONAL (129+ citations, 1,045 lines)
> **Created**: January 2026

---

## 📋 EXECUTIVE SUMMARY

### What is the Maintenance Brain?

The **Maintenance Brain** is the intelligent learning system at the core of AI property maintenance. Unlike traditional maintenance software that only provides tools, the Maintenance Brain **autonomously handles maintenance workflows end-to-end**:

- **Predicting issues** before they become failures
- **Triaging requests** and determining urgency
- **Selecting optimal vendors** based on performance data
- **Forecasting costs** and managing budgets
- **Learning continuously** from every work order

### Business Impact (Research Findings)

| Metric | Target | Source |
|--------|--------|--------|
| Maintenance Cost Reduction | **20-30%** | Vendoroo benchmark |
| Emergency Repairs Reduction | **Up to 50%** | Predictive maintenance |
| Remote Resolution Rate | **20-35%** | Troubleshooting before dispatch |
| AI Automation Rate | **80-90%** | After 6-12 months learning |
| Work Orders Without Vendor | **Significant %** | Self-resolution guidance |

### Primary Research Reference: Vendoroo

- **Company**: vendoroo.ai
- **Positioning**: "Your expert AI in-house maintenance coordinator"
- **Key Differentiator**: "Powered by AI. Driven by Humans" - agentic AI with human oversight
- **CEO Quote**: "The future is software that does the service"

---

## 🎯 ENGINEERING AGENT TASK

You must produce a **comprehensive engineering specification** for the Maintenance Brain Architecture. The specification should enable a development team to build a production-ready system.

**Stage 1 Research Document**: `knowledge/operations/KD-VEN-001-maintenance-brain.md` (1,045 lines, 129+ citations)

---

## 📋 REQUIRED SPECIFICATION SECTIONS

### Section 1: System Architecture Overview

**Requirements:**
1. Design a **4-layer architecture**:
   - **Data Ingestion Layer**: Multi-source data capture
   - **AI Engine Layer**: ML models and decision logic
   - **Workflow Orchestration Layer**: Task automation
   - **Learning & Feedback Layer**: Continuous improvement

2. Component diagram showing:
   - Data flows between layers
   - External integrations (PMS, IoT, vendors)
   - State persistence mechanisms
   - Event-driven triggers

3. Microservices breakdown:
   - Service responsibilities
   - Inter-service communication patterns
   - Deployment considerations

---

### Section 2: Predictive Maintenance Engine

**Requirements:**
1. **Baseline Performance Modeling**:
   - How "normal" is established for building systems
   - Metrics tracked (HVAC performance, energy consumption, etc.)
   - Sensor data normalization

2. **Anomaly Detection**:
   - Algorithm selection (statistical, ML-based)
   - Threshold configuration
   - False positive handling

3. **Failure Prediction**:
   - Time-to-failure estimation
   - Confidence scoring
   - Prediction accuracy metrics

4. **Trigger Conditions**:
   ```yaml
   triggers:
     threshold_exceedance:
       description: "Metric exceeds safe threshold"
       action: "Generate maintenance alert"
     trend_anomaly:
       description: "Abnormal trend even within allowed range"
       action: "Schedule investigation"
     usage_milestone:
       description: "Asset reaches runtime/cycle milestone"
       action: "Recommend inspection"
     repeat_pattern:
       description: "Same issue 3+ times in 30 days"
       action: "Escalate for root cause analysis"
   ```

---

### Section 3: Root Cause Detection & Pattern Recognition

**Requirements:**
1. **Recurring Issue Identification**:
   - Cross-reference algorithm for new vs historical issues
   - Pattern matching across units/buildings
   - Time-window analysis

2. **Automated RCA Techniques**:
   - "5 Whys" automation
   - Fishbone diagram generation
   - Contributing factor analysis

3. **Pattern Library**:
   - Known problem patterns with solutions
   - Confidence scoring for pattern matches
   - Learning from confirmed diagnoses

4. **Risk Flagging**:
   - Liability detection (safety concerns)
   - Escalation triggers
   - Priority adjustment logic

---

### Section 4: Vendor Performance Scoring Algorithm

**Requirements:**
1. **Key Performance Metrics**:
   | Metric | Weight | Description |
   |--------|--------|-------------|
   | Response Time | 20% | Hours from assignment to acceptance |
   | Completion Speed | 20% | Days to job completion |
   | Communication | 10% | Responsiveness in coordination |
   | Resident Satisfaction | 25% | Tenant rating (1-5 stars) |
   | Cost vs Benchmark | 25% | Invoice vs market median |

2. **Scoring Algorithm**:
   - Composite score calculation
   - Rolling window (e.g., last 90 days)
   - Trade-specific scoring
   - Decay function for older data

3. **Vendor Selection Rules**:
   ```python
   def select_vendor(work_order, vendor_pool):
       # Filter by trade match
       candidates = filter_by_trade(vendor_pool, work_order.issue_type)
       
       # Filter by service area
       candidates = filter_by_location(candidates, work_order.property.location)
       
       # Apply preferred vendor priority
       preferred = get_preferred_vendors(work_order.property_id)
       candidates = prioritize_preferred(candidates, preferred)
       
       # Check availability
       candidates = filter_available(candidates)
       
       # Sort by composite score
       candidates = sort_by_score(candidates, work_order.issue_type)
       
       # Apply cost consideration
       if candidates[0].avg_cost_variance > 0.2:
           require_manager_confirmation()
       
       return candidates[0]
   ```

4. **Load Balancing**:
   - Prevent overloading top vendors
   - Backup vendor engagement
   - Dynamic assignment adjustment

---

### Section 5: Cost Forecasting & Budget Model

**Requirements:**
1. **Maintenance Cost History Analysis**:
   - Time-series modeling
   - Category segmentation (plumbing, HVAC, etc.)
   - Seasonal pattern detection

2. **Predictive Budget Modeling**:
   - Asset lifecycle cost projection
   - Capital expense forecasting
   - Probability-weighted estimates

3. **Per-Work-Order Cost Estimation**:
   - Historical comparison for similar jobs
   - Market rate validation
   - Outlier detection and flagging

4. **Budget Output**:
   ```json
   {
     "property_id": "PROP1001",
     "forecast_year": 2026,
     "total_projected": 52000.00,
     "by_category": {
       "hvac": 15000.00,
       "plumbing": 12000.00,
       "electrical": 8000.00,
       "appliances": 10000.00,
       "general": 7000.00
     },
     "major_expenses": [
       {
         "description": "Water heater replacement (2 units)",
         "estimated_cost": 3000.00,
         "probability": 0.8,
         "timing": "Q2 2026"
       }
     ],
     "confidence_interval": {
       "low": 45000.00,
       "high": 60000.00
     }
   }
   ```

---

### Section 6: Data Model Specification

**Requirements**: Define complete schemas for all entities from research:

#### 6.1 MaintenanceHistory
```json
{
  "id": "WO-12345",
  "propertyId": "PROP1001",
  "unit": "5B",
  "assetId": "ASSET-HVAC-005B",
  "issueType": "HVAC > Cooling > Not Cooling",
  "description": "AC blowing warm air",
  "dateReported": "2025-07-15T10:30:00Z",
  "dateCompleted": "2025-07-16T14:00:00Z",
  "reportedBy": "Tenant",
  "priority": "URGENT",
  "assignedVendorId": "VEND-42",
  "vendorResponseTime": 2.5,
  "resolutionSummary": "Replaced capacitor, recharged refrigerant",
  "cost": 450.00,
  "costBreakdown": {
    "labor": 200.00,
    "parts": 150.00,
    "trip_charge": 100.00
  },
  "rating": 5,
  "followUpNeeded": false,
  "rootCause": "Capacitor degradation due to age",
  "preventiveSuggestion": "Annual HVAC tune-up recommended"
}
```

#### 6.2 VendorProfile
```json
{
  "vendorId": "VEND-42",
  "companyName": "CoolAir HVAC Services",
  "tradeSpecialty": ["HVAC", "Refrigeration"],
  "serviceArea": {
    "cities": ["Austin", "Round Rock", "Cedar Park"],
    "radius_miles": 25
  },
  "performanceMetrics": {
    "avgResponseTime": 3.2,
    "completionRate": 0.95,
    "onTimeRate": 0.92,
    "avgRating": 4.7,
    "avgCostPerJob": 380.00,
    "costVarianceFromMedian": 0.05,
    "jobsCompleted": 234
  },
  "contactInfo": {
    "phone": "+1-512-555-1234",
    "email": "dispatch@coolair.com",
    "preferredContact": "SMS"
  },
  "availability": {
    "normalHours": "Mon-Fri 8am-6pm",
    "emergencyAvailable": true,
    "emergencyFee": 150.00
  },
  "insurance": {
    "liability": true,
    "workersComp": true,
    "expirationDate": "2026-03-15"
  },
  "compositeScore": 87.5
}
```

#### 6.3 AssetRegistry
```json
{
  "assetId": "ASSET-HVAC-005B",
  "propertyId": "PROP1001",
  "unit": "5B",
  "assetType": "HVAC",
  "assetSubtype": "Split System",
  "manufacturer": "Carrier",
  "model": "24ACC636A003",
  "serialNumber": "1234567890",
  "installDate": "2015-06-20",
  "expectedLifeYears": 15,
  "warrantyExpiration": "2020-06-20",
  "lastServiceDate": "2025-03-15",
  "maintenanceHistory": ["WO-11000", "WO-11500", "WO-12345"],
  "sensorIds": ["SENSOR-TEMP-5B", "SENSOR-ENERGY-5B"],
  "healthScore": 65,
  "predictedFailureWindow": "2026-Q3"
}
```

#### 6.4 CostHistory
```json
{
  "recordId": "COST-2025-07",
  "propertyId": "PROP1001",
  "period": "2025-07",
  "totalSpend": 4250.00,
  "byCategory": {
    "hvac": 1800.00,
    "plumbing": 950.00,
    "electrical": 500.00,
    "appliances": 600.00,
    "general": 400.00
  },
  "emergencyVsScheduled": {
    "emergency": 800.00,
    "scheduled": 3450.00
  },
  "workOrderCount": 12,
  "avgCostPerWorkOrder": 354.17,
  "budgetVariance": -250.00,
  "ytdTotal": 28500.00,
  "ytdBudget": 29167.00
}
```

#### 6.5 PredictionModel
```json
{
  "modelId": "PRED-MODEL-HVAC-V3",
  "modelType": "HVAC Failure Prediction",
  "version": "3.2",
  "trainingData": {
    "workOrderCount": 45000,
    "dateRange": "2020-01 to 2025-12",
    "properties": 850
  },
  "accuracy": {
    "precision": 0.82,
    "recall": 0.75,
    "f1Score": 0.78
  },
  "features": [
    "asset_age",
    "runtime_hours",
    "energy_consumption_trend",
    "repair_frequency",
    "seasonal_load"
  ],
  "lastRetrained": "2025-11-15",
  "predictions": [
    {
      "assetId": "ASSET-HVAC-005B",
      "predictedFailureWindow": "2026-Q3",
      "failureProbability": 0.70,
      "predictedIssue": "Compressor failure"
    }
  ]
}
```

#### 6.6 PropertyProfile
```json
{
  "propertyId": "PROP1001",
  "name": "Sunset Villas Apartments",
  "type": "Multifamily",
  "units": 50,
  "yearBuilt": 1990,
  "location": {
    "city": "Austin",
    "state": "TX",
    "climateZone": "Hot-Humid"
  },
  "assetInventory": {
    "HVAC": 50,
    "WaterHeaters": 50,
    "Roofs": 5,
    "Elevators": 0
  },
  "maintenancePolicies": {
    "preferredVendors": ["VEND-42", "VEND-43"],
    "approvalThreshold": 500.00,
    "notifyOnEntry": true,
    "emergencyContacts": ["+1-512-555-0001"]
  },
  "budget": {
    "annualMaintenanceBudget": 50000.00,
    "currentYTDSpend": 42000.00
  },
  "openWorkOrders": 2,
  "avgMaintenanceCostPerYear": 48000.00
}
```

---

### Section 7: Business Rules Engine

**Requirements**: Define rules for three critical areas:

#### 7.1 Vendor Selection Rules
```yaml
rules:
  trade_match:
    description: "Only vendors qualified for issue trade"
    enforcement: STRICT
    
  geo_filter:
    description: "Vendor service area must include property location"
    enforcement: STRICT
    
  preferred_priority:
    description: "Preferred vendors get first opportunity"
    enforcement: SOFT
    weight: 1.2  # Score multiplier
    
  load_balance:
    description: "Prevent vendor overload"
    max_concurrent_jobs: 5
    action: "Skip to next vendor if exceeded"
    
  emergency_override:
    description: "Speed over preference for emergencies"
    trigger: "priority == EMERGENCY"
    action: "First available vendor within 1 hour"
```

#### 7.2 Cost Estimation & Approval Rules
```yaml
rules:
  auto_approval:
    threshold: 300.00
    description: "Auto-approve below threshold"
    
  owner_approval:
    threshold: 500.00
    description: "Require owner approval above threshold"
    timeout: "24 hours"
    escalation: "Manager if no response"
    
  multiple_quotes:
    threshold: 2500.00
    description: "Require 2+ quotes above threshold"
    exception: "Emergency repairs"
    
  cost_variance_alert:
    variance: 0.20
    description: "Flag if estimate > 20% above median"
    action: "Require manager confirmation"
    
  warranty_check:
    description: "Check asset warranty before dispatch"
    action: "Route to warranty provider if active"
```

#### 7.3 Predictive Maintenance Rules
```yaml
rules:
  prediction_threshold:
    probability: 0.70
    timeframe: "3 months"
    action: "Create preventive task"
    
  scheduling:
    preference: "Business hours, minimal disruption"
    notice: "48 hours to tenant"
    
  batching:
    description: "Group similar tasks for efficiency"
    scope: "Same property, same trade"
    
  budget_aware:
    description: "Queue if would exceed budget"
    action: "List as recommendation, don't auto-schedule"
```

---

### Section 8: Integration Architecture

**Requirements**: Define all external integrations:

#### 8.1 PMS Integration
```yaml
integrations:
  appfolio:
    type: "REST API"
    auth: "OAuth 2.0"
    endpoints:
      - GET /properties
      - GET /work_orders
      - POST /work_orders
      - PUT /work_orders/{id}
      - GET /residents
    sync: "Real-time webhooks + daily batch"
    
  yardi:
    type: "REST API"
    auth: "API Key"
    endpoints:
      - Similar to above
    sync: "Polling every 5 minutes"
    
  buildium:
    type: "REST API"
    auth: "OAuth 2.0"
    sync: "Webhooks"
```

#### 8.2 IoT/Sensor Integration
```yaml
integrations:
  smart_devices:
    nest_thermostat:
      data: "Temperature, humidity, runtime"
      protocol: "REST API"
      polling: "Every 15 minutes"
      
    leak_detectors:
      data: "Water presence alert"
      protocol: "Webhooks"
      action: "Immediate work order creation"
      
    energy_monitors:
      data: "kWh consumption per device"
      protocol: "MQTT"
      aggregation: "Hourly"
```

#### 8.3 Vendor Communication
```yaml
integrations:
  twilio:
    purpose: "SMS and voice for vendor dispatch"
    features:
      - Automated dispatch notifications
      - Two-way status updates
      - Appointment confirmations
      
  email:
    provider: "SendGrid"
    templates:
      - vendor_dispatch
      - resident_notification
      - owner_approval_request
      - completion_report
```

#### 8.4 Accounting Integration
```yaml
integrations:
  quickbooks:
    type: "REST API"
    auth: "OAuth 2.0"
    sync:
      - Vendor bills from completed work orders
      - Expense categorization
      - Owner statement entries
```

---

### Section 9: Learning & Feedback System

**Requirements:**
1. **Feedback Loop Architecture**:
   - Every completed work order feeds back as training data
   - Vendor performance updated after each job
   - Cost benchmarks continuously refined

2. **Model Retraining Schedule**:
   - Predictive models: Monthly
   - Scoring weights: Quarterly
   - Pattern library: Continuous

3. **Cold Start Strategy**:
   - Initial 0-3 months: Human oversight on all decisions
   - Fallback to manufacturer schedules without data
   - Progressive autonomy as data accumulates

4. **Human-in-the-Loop**:
   ```yaml
   hitl:
     required_for:
       - Emergency decisions
       - First-time scenarios
       - High-cost approvals (>$1000)
       - Vendor termination decisions
     optional_for:
       - Routine dispatches (after 90 days)
       - Standard repairs
       - Repeat patterns with high confidence
   ```

---

### Section 10: Performance Metrics & SLAs

**Requirements**: Define KPIs:

| Metric | Target | Measurement |
|--------|--------|-------------|
| AI Automation Rate | >80% | Work orders handled without human |
| Emergency Response Time | <30 min | Assignment to vendor confirmation |
| Remote Resolution Rate | >25% | Issues resolved without dispatch |
| Cost vs Budget Variance | <10% | Actual vs projected |
| Vendor Selection Accuracy | >90% | First choice completes job |
| Prediction Accuracy | >75% | Predicted failures that occur |
| False Positive Rate | <15% | Predictions that were wrong |
| Tenant Satisfaction | >4.5/5 | Post-service rating |
| First-Time Fix Rate | >85% | Jobs completed on first visit |
| Mean Time to Resolution | <48 hours | Report to completion |

---

### Section 11: Security & Compliance

**Requirements:**
1. **Data Protection**:
   - Encryption at rest (AES-256)
   - Encryption in transit (TLS 1.3)
   - PII handling for tenant data

2. **Access Control**:
   - RBAC for different user types
   - Vendor access limited to assigned jobs
   - Owner access to their properties only

3. **Audit Trail**:
   - All AI decisions logged
   - Human overrides tracked
   - Cost justification records

4. **Compliance**:
   - SOC 2 Type II readiness
   - GDPR for international (data deletion requests)
   - Fair Housing compliance (no discrimination in prioritization)

---

### Section 12: Error Handling & Recovery

**Requirements:**
1. **Vendor Dispatch Failures**:
   - Retry logic: 3 attempts, 5-minute intervals
   - Fallback: Try next vendor in ranking
   - Escalation: Alert manager if all fail

2. **Integration Failures**:
   - PMS offline: Queue updates, retry on recovery
   - IoT data gaps: Use last known state, flag uncertainty
   - Circuit breaker pattern for external APIs

3. **Prediction Errors**:
   - Monitor false positive/negative rates
   - Adjust thresholds automatically
   - Human review for edge cases

---

### Section 13: UI/Dashboard Requirements

**Requirements:**
1. **Maintenance Dashboard**:
   - Active work orders kanban
   - Urgent items highlighted
   - Vendor availability view
   - Budget tracker

2. **Predictive Insights Panel**:
   - Upcoming predicted failures
   - Asset health scores
   - Recommended preventive actions

3. **Analytics & Reports**:
   - Cost trends by category
   - Vendor performance leaderboard
   - Maintenance vs budget comparison
   - Owner-facing maintenance reports

---

### Section 14: Implementation Phases

**Requirements**: Define phased rollout:

#### Phase 1: Core Engine (Weeks 1-8)
- Work order intake and triage
- Basic vendor selection
- PMS integration (1 provider)
- Manual approval workflow

#### Phase 2: Intelligence (Weeks 9-14)
- Vendor scoring algorithm
- Cost estimation engine
- Pattern recognition (basic)
- Remote troubleshooting

#### Phase 3: Predictive (Weeks 15-20)
- IoT integration
- Failure prediction models
- Budget forecasting
- Root cause analysis

#### Phase 4: Optimization (Weeks 21-26)
- Full automation (<$500 jobs)
- Multi-PMS support
- Advanced analytics
- Mobile app for vendors

**Total Estimated Effort**: 26 weeks

---

## 📚 REFERENCE MATERIALS

### Stage 1 Research Document
- **Location**: `knowledge/operations/KD-VEN-001-maintenance-brain.md`
- **Lines**: 1,045
- **Citations**: 129+
- **Quality**: 9.5/10 ⭐ EXCEPTIONAL

### Key Sources from Research
1. **Vendoroo** - Primary reference (agentic AI approach)
2. **Property Meld** - MAX™ Intelligence (ML architecture)
3. **AppFolio Realm-X** - Maintenance Performer (platform integration)
4. **Latchel** - Dispatch automation
5. **Buildium** - Digital twins for predictive maintenance

### Related Completed Specifications
- `specs/operations/SPEC-SKILL-254-AI-MAINTENANCE.md` (GAP-AF-002) - Complementary
- `specs/ai-workforce/SPEC-SKILL-261-268.md` (GAP-HOAI-001) - Architecture reference

---

## ✅ DELIVERABLE REQUIREMENTS

Your engineering specification must include:

1. **All 14 sections** fully detailed
2. **Code examples** (Python/TypeScript) for key algorithms
3. **Complete data schemas** (JSON/YAML)
4. **Sequence diagrams** for major workflows
5. **API specifications** (OpenAPI format)
6. **Database design** (MongoDB collections)
7. **Integration contracts** for external systems
8. **Test scenarios** for validation

**Target Length**: 8,000-15,000 lines
**Quality Target**: 9.0/10

---

## 🚀 OUTPUT

Save your engineering specification to:
```
knowledge/operations/ES-VEN-001-maintenance-brain.md
```

**After Completing:**
1. Notify that Stage 3 is complete
2. The document will be processed through Stage 4 for final skill specifications

---

**Good luck! This is a P0 skill critical for MVP. The Maintenance Brain is the "intelligence" that makes AI property management possible. 🧠**

