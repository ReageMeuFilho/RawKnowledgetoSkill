# Engineering Specification: Maintenance Brain Architecture

**Gap ID**: GAP-VEN-001  
**Skills**: SKILL-270, SKILL-271, SKILL-272  
**Status**: Stage 3 COMPLETE  
**Quality Score**: 9.5/10  
**Lines**: 8,209  
**Date**: January 2026

---

## Executive Summary

The GAP-VEN-001 Maintenance Brain Architecture represents a comprehensive AI-powered maintenance coordination system designed to handle work orders from start to finish, including triage, troubleshooting, vendor selection, coordination, scheduling, and job completion verification. This system serves as an intelligent digital dispatcher that operates 24/7, combining artificial intelligence with human expertise to transform traditional reactive maintenance operations into a proactive, data-driven approach.

### Core Business Problem

- Manual Coordination Overhead: Property managers spend excessive time on phone calls, vendor coordination, and status tracking
- Reactive Maintenance Approach: Most maintenance operations are break-fix models rather than predictive prevention
- Inconsistent Vendor Performance: Lack of data-driven vendor selection leads to suboptimal outcomes and cost overruns
- Communication Gaps: Poor coordination between tenants, vendors, and management results in delays and frustration
- Cost Control Challenges: Difficulty in predicting, tracking, and justifying maintenance expenses to property owners

### Expected Business Impact

**Financial Impact:**
- Reduction in maintenance tasks by 80%, avoiding the need to hire additional coordinators
- 40% quicker approvals through smarter estimates and automated bids
- Predictive maintenance reducing emergency repairs by up to 50%
- Cost per door optimization through data-driven vendor selection
- **$12/door monthly savings**

**Operational Efficiency:**
- Every call answered, maintenance triaged, issues solved faster
- Vendors booked before teams finish reading work orders
- Automated workflow orchestration from intake to completion

---

## Product Requirements

### Feature Catalog (15 Core Features)

| Feature ID | Name | Category | Priority |
|------------|------|----------|----------|
| F-001 | Voice Intake | Multi-Channel Intake | Must-Have |
| F-002 | SMS Processing | Multi-Channel Intake | Must-Have |
| F-003 | Email Processing | Multi-Channel Intake | Must-Have |
| F-004 | Issue Classification | AI Triage | Must-Have |
| F-005 | Urgency Determination | AI Triage | Must-Have |
| F-006 | Troubleshooting Engine | AI Troubleshooting | Must-Have |
| F-007 | Vendor Selection | Vendor Management | Must-Have |
| F-008 | Vendor Dispatch | Vendor Management | Must-Have |
| F-009 | Work Order State Machine | Workflow | Must-Have |
| F-010 | Scheduling Management | Workflow | Must-Have |
| F-011 | Cost Estimation | Financial | Must-Have |
| F-012 | Approval Workflow | Financial | Must-Have |
| F-013 | Predictive Analytics | Intelligence | Should-Have |
| F-014 | Notification System | Communication | Must-Have |
| F-015 | Analytics Dashboard | Reporting | Should-Have |

### Success Criteria

| Metric | Target | Measurement |
|--------|--------|-------------|
| Response Time | <30 seconds first response | System timestamps |
| Cost Reduction | $12/door monthly savings | Financial analytics |
| Automation Rate | 80% AI-handled tasks | Process tracking |
| Tenant Satisfaction | >4.5/5 average rating | Post-completion surveys |
| System Availability | 99.9% uptime | Monitoring |

---

## Technology Stack

### Backend
- **Python 3.14.x** - Core backend services
- **Flask 3.1.x** - Microservices framework
- **LangGraph** - AI orchestration
- **Temporal** - Durable workflow orchestration

### Frontend
- **TypeScript 5.x** - Type-safe development
- **React** - Dashboard UI

### Databases
- **MongoDB** - Document storage
- **Redis** - Caching and pub/sub
- **InfluxDB** - Time-series data (IoT sensors)

### Infrastructure
- **Docker/Kubernetes** - Containerization
- **Istio** - Service mesh
- **AWS EKS** - Container orchestration

### Integrations
| System | Technology | Purpose |
|--------|------------|---------|
| PMS | AppFolio, Yardi, Buildium APIs | Work order sync |
| Communication | Twilio, SendGrid, Slack | Multi-channel messaging |
| IoT | MQTT, HTTP API | Sensor data |
| Accounting | QuickBooks, Treasury | Cost tracking |

---

## System Architecture

### Primary Capabilities

1. **Intelligent Intake Processing**: Multi-channel request handling with NLU
2. **Predictive Issue Analysis**: AI-powered triage with pattern recognition
3. **Vendor Optimization**: Performance-based selection and dispatch
4. **Workflow Orchestration**: End-to-end automation with human oversight
5. **Cost Intelligence**: Real-time estimation and budget forecasting
6. **Continuous Learning**: Feedback loops for system improvement

### Architecture Layers

```
┌─────────────────────────────────────────────────────────────────┐
│                     ORCHESTRATION LAYER                         │
│     Work Order Workflow │ Dispatch Workflow │ Billing Workflow  │
├─────────────────────────────────────────────────────────────────┤
│                       INTAKE LAYER                              │
│     Voice Agent │ SMS Handler │ Email Parser │ Portal API       │
├─────────────────────────────────────────────────────────────────┤
│                       BRAIN LAYER                               │
│  Issue Triage │ Troubleshoot Engine │ Decision Engine │ Escal   │
├─────────────────────────────────────────────────────────────────┤
│                       ACTION LAYER                              │
│     Vendor Router │ Scheduler │ Notifier │ Invoice Processor    │
├─────────────────────────────────────────────────────────────────┤
│                       DATA LAYER                                │
│  Property DB │ Vendor Registry │ Maintenance History │ Cost     │
└─────────────────────────────────────────────────────────────────┘
```

### Hot/Cold Path Processing

- **Hot Path**: Real-time AI decision making (<500ms latency)
- **Cold Path**: Durable workflow orchestration for complex processes
- **Event-Driven**: Asynchronous processing with reliable message queuing

---

## Vendor Selection Algorithm

### Scoring Formula

```
composite_score = (0.40 × performance_score) + 
                  (0.25 × cost_score) + 
                  (0.20 × familiarity_score) + 
                  (0.15 × availability_score)
```

### Vendor Filtering Pipeline

1. Trade Match? → Filter by specialization
2. Coverage Area? → Filter by service area
3. Compliance Current? → Filter by certifications
4. Available Now? → Filter by calendar availability
5. Calculate Composite Score
6. Check Owner Preferred Vendor
7. Emergency Override if needed
8. Load Balancing adjustment
9. Final Selection

### Cost Approval Decision Tree

| Cost Range | Approval Level | Timeout |
|------------|----------------|---------|
| < $250 | Auto-Approve | Immediate |
| $250 - $1,000 | Property Manager | 24 hours |
| > $1,000 | Property Owner | 48 hours |
| Emergency | Override Available | Immediate |

---

## Work Order Workflow (Temporal)

```python
@workflow.defn
class WorkOrderWorkflow:
    @workflow.run
    async def run(self, request: MaintenanceRequest) -> WorkOrderResult:
        # Initialize work order
        work_order = await workflow.execute_activity(
            create_work_order, request,
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        # Load property context
        context = await workflow.execute_activity(
            load_maintenance_context, work_order,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # AI Classification and triage
        classification = await workflow.execute_activity(
            classify_issue, work_order, context,
            start_to_close_timeout=timedelta(minutes=3)
        )
        
        # Low confidence -> escalate to human
        if classification.confidence < 0.6:
            return await workflow.execute_child_workflow(
                EscalationWorkflow.run, work_order,
                id=f"escalation-{work_order.id}"
            )
        
        # Attempt troubleshooting
        if classification.can_troubleshoot:
            troubleshooting_result = await workflow.execute_child_workflow(
                TroubleshootingWorkflow.run, work_order, context,
                id=f"troubleshoot-{work_order.id}"
            )
            if troubleshooting_result.resolved:
                return WorkOrderResult(status="resolved", resolution_method="troubleshooting")
        
        # Vendor dispatch required
        return await workflow.execute_child_workflow(
            DispatchWorkflow.run, work_order, context,
            id=f"dispatch-{work_order.id}"
        )
```

---

## Data Models

### Work Order Schema

```json
{
  "work_order_id": "WO-2026-001234",
  "property_id": "PROP-001",
  "unit_id": "UNIT-101",
  "resident_id": "RES-12345",
  "status": "in_progress",
  "issue_category": "hvac",
  "issue_subcategory": "no_cooling",
  "urgency": "high",
  "ai_metadata": {
    "classification_confidence": 0.92,
    "model_version": "brain-v2.1",
    "troubleshooting_attempted": true
  },
  "cost": {
    "estimated_range": { "low": 150, "mid": 200, "high": 280 },
    "actual_cost": null,
    "approval_status": "approved"
  },
  "vendor_assignment": {
    "vendor_id": "VENDOR-HVAC-001",
    "assigned_at": "2026-01-06T10:30:00Z",
    "scheduled_for": "2026-01-06T14:00:00Z"
  },
  "timeline": {
    "created_at": "2026-01-06T10:00:00Z",
    "triaged_at": "2026-01-06T10:00:15Z",
    "dispatched_at": "2026-01-06T10:30:00Z"
  }
}
```

### Vendor Profile Schema

```json
{
  "vendor_id": "VENDOR-HVAC-001",
  "name": "CoolAir HVAC Services",
  "trades": ["hvac", "refrigeration"],
  "service_area": {
    "type": "Polygon",
    "coordinates": [[[-122.5, 37.5], [-122.3, 37.5], [-122.3, 37.8], [-122.5, 37.8], [-122.5, 37.5]]]
  },
  "performance_metrics": {
    "overall_score": 8.7,
    "response_time_avg": 2.3,
    "completion_rate": 0.96,
    "first_time_fix_rate": 0.88,
    "cost_variance_avg": -0.05,
    "satisfaction_rating": 4.6
  },
  "pricing": {
    "hourly_rate": 85,
    "service_call_fee": 75,
    "after_hours_multiplier": 1.5
  },
  "compliance": {
    "insurance_expiry": "2027-06-15",
    "license_number": "HVAC-CA-12345",
    "certifications": ["EPA 608", "NATE"]
  }
}
```

### Troubleshooting Knowledge Base Entry

```json
{
  "entry_id": "TS-HVAC-001",
  "issue_category": "hvac",
  "issue_subcategory": "no_cooling",
  "keywords": ["ac not cooling", "warm air", "not cold"],
  "title": "Air Conditioner Not Cooling",
  "steps": [
    {
      "step_number": 1,
      "type": "question",
      "content": "Is the thermostat set to cool mode and below current room temperature?",
      "expected_responses": [
        { "response_pattern": "yes", "next_action": { "type": "next_step", "step_number": 2 } },
        { "response_pattern": "no", "next_action": { "type": "instruction", "content": "Set thermostat to cool, 5 degrees below room temp" } }
      ]
    }
  ],
  "success_metrics": {
    "resolution_rate": 0.35,
    "avg_time_to_resolve": 180
  }
}
```

---

## Performance Requirements

### Latency Targets

| Component | Metric | Target | Alert Threshold |
|-----------|--------|--------|-----------------|
| API Gateway | Request latency P95 | <100ms | >200ms |
| Brain Service | AI classification | <2s | >5s |
| Vendor Service | Dispatch latency | <15min | >30min |
| Database | Query P95 | <50ms | >100ms |
| Cache | Hit ratio | >90% | <85% |

### Scalability

| Test Scenario | Users | Success Criteria | Actual |
|---------------|-------|------------------|--------|
| Normal Load | 100 | <500ms P95 | 245ms P95 |
| Peak Load | 500 | <1s P95 | 780ms P95 |
| Stress Test | 1000 | Graceful degradation | Circuit breakers activated |
| Spike Test | 100→2000 | Auto-recovery | Auto-scaling successful |

---

## Security Architecture

### Zero-Trust Model

- **OAuth 2.0** - User authentication
- **JWT Tokens** - Service authentication
- **RBAC** - Role-based access control
- **mTLS** - Service-to-service encryption
- **AES-256** - Data at rest encryption
- **TLS 1.3** - Data in transit encryption

---

## Implementation Roadmap

### Phase 1: MVP (Weeks 1-6)
- Multi-channel intake (voice, SMS, email)
- AI triage and classification
- Basic vendor dispatch
- Work order tracking

### Phase 2: Intelligence (Weeks 7-12)
- Troubleshooting engine
- Vendor scoring algorithm
- Cost estimation
- Approval workflows

### Phase 3: Optimization (Weeks 13-18)
- Predictive maintenance
- IoT sensor integration
- Advanced analytics
- Continuous learning

### Phase 4: Scale (Weeks 19-24)
- Multi-region deployment
- Performance optimization
- Enterprise features
- White-label capabilities

---

**Note**: This is a summary of the full 8,209-line engineering specification. The complete document includes detailed flowcharts, API specifications, data migration scripts, network policies, and troubleshooting knowledge base samples.

