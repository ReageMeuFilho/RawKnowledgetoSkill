# Engineering Specification: Quote Chaser Automation System

**Gap ID**: GAP-GW-001  
**Skill ID**: SKILL-232  
**Status**: Stage 3 COMPLETE  
**Quality Score**: 9.5/10  
**Lines**: 9,261  
**Date**: January 2026

---

## Executive Summary

The Quote Chaser Automation System addresses a critical revenue leakage problem where **70% of quotes are never finalized**. Manual follow-up is slow and inconsistent - a 5-minute vs 30-minute response can boost conversion by 100×. Well-designed automated flows recover approximately **3.33% of lost revenue** on average.

### Business Impact
- **Revenue Recovery**: 3.33% of abandoned quote value
- **Time Savings**: 60+ hours monthly operational efficiency
- **Response Speed**: <1 second automated sequence initiation
- **Scale Capability**: 100,000+ daily messages

### Key Benchmarks (from E-commerce)
| Metric | Target |
|--------|--------|
| Email Open Rate | ≥50.5% |
| Click-through Rate | 6.25% |
| Conversion Rate | 3.33% |
| Unsubscribe Rate | <0.6% |

---

## Product Requirements

### Feature Catalog (12 Core Features)

| Feature ID | Name | Category | Priority |
|------------|------|----------|----------|
| F-001 | Quote State Machine | Core Engine | Critical |
| F-002 | Quote Lifecycle Event Processing | Core Engine | Critical |
| F-003 | Multi-Step Sequence Engine | Automation | Critical |
| F-004 | Sequence Configuration Management | Configuration | High |
| F-005 | Multi-Channel Message Dispatcher | Messaging | Critical |
| F-006 | Template Engine | Messaging | High |
| F-007 | Analytics & Tracking | Analytics | High |
| F-008 | Consent Management | Compliance | Critical |
| F-009 | A/B Testing Framework | Optimization | Medium |
| F-010 | Unsubscribe Processing | Compliance | Critical |
| F-011 | PMS Integration | Integration | High |
| F-012 | Rate Limiting | Security | High |

---

## Quote State Machine

### State Definitions

```
┌─────────┐
│   NEW   │ ← Quote created
└────┬────┘
     │ Send quote
     ▼
┌─────────┐
│  SENT   │ ← Quote emailed/SMS'd, sequence started
└────┬────┘
     │ Guest opens/clicks
     ▼
┌─────────┐
│ VIEWED  │ ← Link tracked (optional)
└────┬────┘
     │
     ├────────────────┬────────────────┐
     │                │                │
     ▼                ▼                ▼
┌─────────┐    ┌──────────┐    ┌─────────┐
│ACCEPTED │    │CANCELLED │    │ EXPIRED │
│(Booked) │    │(Declined)│    │(Timeout)│
└─────────┘    └──────────┘    └─────────┘
```

### State Transitions
| From | To | Trigger | Action |
|------|-----|---------|--------|
| NEW | SENT | Quote sent | Start sequence |
| SENT | VIEWED | Link clicked | Log event |
| SENT/VIEWED | ACCEPTED | Booking created | Stop sequence |
| SENT/VIEWED | CANCELLED | Guest declines | Stop sequence |
| SENT/VIEWED | EXPIRED | 30 days passed | Stop sequence |

---

## Sequence Orchestration (Temporal)

### Standard Follow-Up Sequence

```yaml
sequence:
  name: "Standard Quote Follow-up"
  trigger: "quote_sent"
  steps:
    - step: 1
      delay: "2h"
      channel: "email"
      template: "quote-reminder-excitement"
      exit_on: ["ACCEPTED", "CANCELLED", "EXPIRED", "UNSUBSCRIBED"]
    - step: 2
      delay: "24h"
      channel: "email"
      template: "quote-reminder-assistance"
      exit_on: ["ACCEPTED", "CANCELLED", "EXPIRED", "UNSUBSCRIBED"]
    - step: 3
      delay: "48h"
      channel: "sms"
      template: "quote-final-sms"
      exit_on: ["ACCEPTED", "CANCELLED", "EXPIRED", "UNSUBSCRIBED"]
```

### Temporal Workflow Implementation

```python
from temporalio import workflow, activity
from datetime import timedelta

@workflow.defn
class QuoteFollowUpWorkflow:
    @workflow.run
    async def run(self, quote_id: str, sequence_config: dict):
        for step in sequence_config['steps']:
            # Wait for delay
            await workflow.sleep(timedelta(hours=step['delay_hours']))
            
            # Check exit conditions
            quote_status = await workflow.execute_activity(
                check_quote_status, quote_id,
                start_to_close_timeout=timedelta(seconds=30)
            )
            
            if quote_status in step['exit_conditions']:
                return {"status": "terminated", "reason": quote_status}
            
            # Send message
            await workflow.execute_activity(
                send_message,
                args=[quote_id, step['channel'], step['template_id']],
                start_to_close_timeout=timedelta(seconds=60)
            )
        
        return {"status": "completed", "steps_executed": len(sequence_config['steps'])}
```

---

## Multi-Channel Message Dispatcher

### Channel Configuration

| Channel | Provider | Rate Limit | Fallback |
|---------|----------|------------|----------|
| Email | SendGrid | 100/second | SES |
| SMS | Twilio | 10/second | Vonage |
| WhatsApp | Twilio | 5/second | - |

### Dispatcher Architecture

```
┌─────────────┐
│  Dispatcher │
└──────┬──────┘
       │
  ┌────┴────┬────────┬─────────┐
  │         │        │         │
  ▼         ▼        ▼         ▼
┌─────┐  ┌─────┐  ┌──────┐  ┌─────┐
│Email│  │ SMS │  │WhatsApp│ │Push │
└─────┘  └─────┘  └──────┘  └─────┘
```

---

## Technology Stack

### Backend
| Component | Technology | Version |
|-----------|------------|---------|
| Language | Python | 3.12+ |
| Framework | Flask | 3.0+ |
| Workflow | Temporal | Python SDK |
| ORM | SQLAlchemy | 2.0+ |

### Frontend
| Component | Technology | Version |
|-----------|------------|---------|
| Framework | React | 18+ |
| UI Library | Material-UI | 5+ |
| State | TanStack Query | 5+ |
| Charts | Recharts | 2+ |

### Infrastructure
| Component | Technology |
|-----------|------------|
| Database | MongoDB |
| Cache | Redis |
| Message Queue | Redis Streams |
| Email | SendGrid |
| SMS | Twilio |
| Container | Docker |
| Orchestration | AWS ECS |

---

## Data Models

### Quote Document (MongoDB)

```json
{
  "_id": "ObjectId",
  "quote_id": "QT-123456",
  "guest_id": "G-789",
  "property_id": "P-001",
  "dates": {
    "check_in": "ISODate",
    "check_out": "ISODate",
    "nights": 3
  },
  "line_items": [
    {"description": "Nightly Rate", "nights": 3, "rate": 250.00, "subtotal": 750.00},
    {"description": "Cleaning Fee", "nights": 1, "rate": 75.00, "subtotal": 75.00}
  ],
  "total_price": 825.00,
  "status": "SENT",
  "sequence": {
    "id": "SEQ-001",
    "current_step": 2,
    "started_at": "ISODate",
    "paused": false,
    "workflow_id": "quote-follow-up-workflow-123"
  },
  "events": [
    {"type": "created", "timestamp": "ISODate"},
    {"type": "sent", "timestamp": "ISODate"},
    {"type": "viewed", "timestamp": "ISODate"}
  ],
  "tracking": {
    "utm_source": "direct",
    "utm_medium": "email",
    "utm_campaign": "quote_follow_up"
  },
  "sent_at": "ISODate",
  "expires_at": "ISODate",
  "created_at": "ISODate",
  "updated_at": "ISODate"
}
```

### Guest Document (MongoDB)

```json
{
  "_id": "ObjectId",
  "guest_id": "G-789",
  "email": "guest@example.com",
  "phone": "+1-555-123-4567",
  "first_name": "John",
  "last_name": "Doe",
  "preferences": {
    "communication_channel": "email",
    "timezone": "America/New_York",
    "language": "en"
  },
  "consent_records": [
    {
      "type": "marketing_email",
      "granted": true,
      "timestamp": "ISODate",
      "source": "quote_request_form"
    }
  ],
  "unsubscribes": []
}
```

---

## Compliance Workflows

### Consent Management (GDPR)
- Explicit opt-in required for EU guests
- Consent timestamp and source recorded
- Data erasure process implemented

### Unsubscribe Processing
- One-click unsubscribe
- Immediate effect (<10 seconds)
- Channel-specific opt-out
- Preference center option

### CAN-SPAM (US)
- Clear unsubscribe link in every email
- Valid physical address
- Honest subject lines

### TCPA (US SMS)
- Express written consent required
- Messaging frequency disclosure
- Permissible hours enforcement

---

## A/B Testing Framework

### Test Configuration

```json
{
  "test_id": "AB-001",
  "name": "Subject Line Test",
  "variable": "email_subject",
  "variants": [
    {"id": "A", "value": "Your quote is ready!", "weight": 50},
    {"id": "B", "value": "Hi {{name}}, complete your booking", "weight": 50}
  ],
  "success_metric": "conversion_rate",
  "min_sample_size": 1000,
  "confidence_level": 0.95
}
```

### Statistical Analysis
- Conversion rate per variant
- Confidence interval calculation
- Auto-declare winner at 95% confidence

---

## API Specifications

### Quote APIs
```
POST   /api/v1/quotes                    - Create quote
GET    /api/v1/quotes/{quote_id}         - Get quote details
POST   /api/v1/quotes/{quote_id}/send    - Send and start sequence
POST   /api/v1/quotes/{quote_id}/cancel  - Cancel quote
POST   /api/v1/quotes/{quote_id}/convert - Mark as converted
```

### Sequence APIs
```
GET    /api/v1/sequences                 - List sequences
POST   /api/v1/sequences                 - Create sequence
GET    /api/v1/quotes/{quote_id}/sequence-status - Get sequence position
POST   /api/v1/quotes/{quote_id}/sequence/pause  - Pause sequence
```

### Analytics APIs
```
GET    /api/v1/analytics/quotes/funnel   - Quote funnel metrics
GET    /api/v1/analytics/sequences/performance - Conversion metrics
GET    /api/v1/analytics/ab-tests/{test_id}    - A/B test results
```

---

## Performance Requirements

| Metric | Target |
|--------|--------|
| Sequence Start Latency | <1 second |
| Message Dispatch | <5 seconds |
| API Response Time | <200ms P95 |
| Concurrent Sequences | 10,000+ |
| Daily Message Volume | 100,000+ |

---

## UI Components

### Quote Dashboard
- Quote list with status filters
- Funnel visualization
- Conversion metrics
- Recent activity feed

### Sequence Builder
- Visual workflow editor
- Drag-and-drop steps
- Template selection
- Preview mode

### Analytics Dashboard
- Open/click/conversion rates
- A/B test results
- Channel performance
- Time-to-conversion

---

## Implementation Timeline

| Phase | Weeks | Deliverables |
|-------|-------|--------------|
| **Phase 1** | 1-3 | Quote state machine, Temporal workflows |
| **Phase 2** | 4-6 | Email dispatcher (SendGrid), basic templates |
| **Phase 3** | 7-9 | SMS integration (Twilio), multi-channel |
| **Phase 4** | 10-12 | Analytics, A/B testing framework |
| **Phase 5** | 13-14 | UI dashboard, sequence builder |

---

## References

- Full Engineering Spec: `knowledge/channel/ES-GW-001-quote-chaser.md`
- Knowledge Document: `knowledge/channel/KD-GW-001-quote-chaser.md`
- Stage 2 Prompt: `docs/prompts/ENGINEERING_SPEC_PROMPT_QUOTE_CHASER.md`

