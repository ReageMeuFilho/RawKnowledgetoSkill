# Stage 2: Engineering Specification Prompt

## Quote Chaser Automation System

**Gap ID**: GAP-GW-001  
**Skill ID**: SKILL-232  
**Knowledge Document**: `knowledge/channel/KD-GW-001-quote-chaser.md`  
**Created By**: Cursor AI  
**Date**: January 2026

---

## MISSION

You are an expert software architect and engineer. Your task is to produce a **production-ready engineering specification** for the Quote Chaser Automation System.

The Knowledge Document contains comprehensive research on 11 platforms, complete data models, state machines, and industry benchmarks. Your job is to transform this into a detailed technical specification that an engineering team can implement directly.

---

## INPUT CONTEXT

### Problem Statement
- **70% of quotes are never finalized** (quote abandonment)
- Manual follow-up is slow and inconsistent
- 5-minute vs 30-minute response difference = **100× conversion difference**
- Well-designed flows recover **3.33% of lost revenue**

### Key Benchmarks (from Research)
| Metric | Target |
|--------|--------|
| Email Open Rate | ≥50% |
| Click-through Rate | 6% |
| Conversion Rate | 3.33% |
| Unsubscribe Rate | <0.6% |
| Time Savings | 60+ hrs/month |

### Best Implementation: GuestWisely Quote Chaser
- Native email/SMS in PMS
- Configurable timing and message count
- GDPR-compliant consent tracking
- Full guest record integration

---

## SPECIFICATION REQUIREMENTS

### Section 1: Executive Summary
- Business value proposition
- Technical approach overview
- Integration with CitadelOS architecture
- Success metrics and KPIs

### Section 2: System Architecture

#### 2.1 Component Diagram
Create a high-level architecture showing:
- Quote Engine (state management)
- Sequence Orchestrator (Temporal workflows)
- Message Dispatcher (multi-channel)
- Template Engine (personalization)
- Analytics Collector (metrics)
- Consent Manager (compliance)

#### 2.2 Integration Points
| System | Integration | Protocol |
|--------|-------------|----------|
| PMS Core | Quote lifecycle events | Internal API |
| Email Provider | SendGrid/SES | REST API |
| SMS Provider | Twilio | REST API |
| Analytics | Event tracking | Webhook |
| Channel Manager | Availability sync | API |

### Section 3: Quote State Machine

#### 3.1 State Definitions
Define all states with:
- State name and description
- Valid transitions
- Trigger events
- Side effects (actions taken)

Required states:
- `NEW` - Quote created, not sent
- `SENT` - Quote delivered to guest
- `VIEWED` - Guest opened/clicked
- `PENDING` - Awaiting response
- `ACCEPTED` - Converted to booking
- `CANCELLED` - Guest declined
- `EXPIRED` - Validity lapsed

#### 3.2 State Transition Matrix
| From | To | Trigger | Action |
|------|-----|---------|--------|
| NEW | SENT | Send quote | Start sequence |
| SENT | VIEWED | Link clicked | Log event |
| SENT | ACCEPTED | Booking created | Stop sequence |
| SENT | EXPIRED | 30 days passed | Stop sequence |
| ... | ... | ... | ... |

#### 3.3 Implementation (Temporal Workflow)
Provide Python workflow definition with:
- State persistence
- Transition validation
- Event logging
- Error handling

### Section 4: Sequence Orchestrator

#### 4.1 Workflow Definition
```yaml
sequence:
  name: "standard-quote-follow-up"
  trigger: "QuoteSent"
  steps:
    - step: 1
      delay: "2h"
      channel: "email"
      template: "quote-reminder-1"
      exit_on: ["Booked", "Unsubscribed"]
    - step: 2
      delay: "24h"
      channel: "email"
      template: "quote-reminder-2"
      exit_on: ["Booked", "Unsubscribed"]
    - step: 3
      delay: "48h"
      channel: "sms"
      template: "quote-final-sms"
      exit_on: ["Booked", "Unsubscribed"]
```

#### 4.2 Temporal Workflow Implementation
Provide complete Python code for:
- `QuoteFollowUpWorkflow` class
- Activity definitions (send_email, send_sms, check_status)
- Timer handling
- Cancellation on conversion
- Error recovery

#### 4.3 Configurable Parameters
| Parameter | Type | Default | Range |
|-----------|------|---------|-------|
| `max_steps` | int | 3 | 1-5 |
| `first_delay_hours` | int | 2 | 1-24 |
| `second_delay_hours` | int | 24 | 12-72 |
| `third_delay_hours` | int | 48 | 24-168 |
| `expiration_days` | int | 30 | 7-90 |

### Section 5: Message Dispatcher

#### 5.1 Multi-Channel Architecture
```
┌─────────────┐
│  Dispatcher │
└──────┬──────┘
       │
  ┌────┴────┬────────┬─────────┐
  │         │        │         │
  ▼         ▼        ▼         ▼
┌─────┐  ┌─────┐  ┌──────┐  ┌─────┐
│Email│  │ SMS │  │WhatsApp│  │Push │
└─────┘  └─────┘  └──────┘  └─────┘
```

#### 5.2 Channel Handlers
For each channel, specify:
- Provider integration (SendGrid, Twilio)
- Rate limits
- Retry strategy
- Delivery confirmation
- Cost per message

#### 5.3 Priority & Fallback
- Primary channel selection based on guest preference
- Fallback if primary fails
- Time-of-day restrictions (no SMS 9pm-9am)

### Section 6: Template Engine

#### 6.1 Template Schema
```json
{
  "template_id": "quote-reminder-1",
  "channel": "email",
  "subject": "Your {{property_name}} quote is ready!",
  "body": "Hi {{guest_first_name}},...",
  "variables": [
    "guest_first_name",
    "property_name",
    "check_in_date",
    "check_out_date",
    "total_price",
    "quote_link"
  ],
  "cta_button": {
    "text": "Book Now",
    "url": "{{quote_link}}"
  }
}
```

#### 6.2 Variable Resolution
| Variable | Source | Format |
|----------|--------|--------|
| `guest_first_name` | Guest profile | String |
| `property_name` | Property | String |
| `check_in_date` | Quote | "Jan 15, 2026" |
| `total_price` | Quote | "$1,250.00" |
| `quote_link` | Generated | URL with tracking |

#### 6.3 Template Library
Provide complete templates for:
- Email #1: Initial reminder (excitement)
- Email #2: Follow-up (assistance + optional discount)
- Email #3: Final urgency (expiring)
- SMS #1: Brief reminder
- SMS #2: Last chance

### Section 7: Analytics & Tracking

#### 7.1 Event Schema
```json
{
  "event_type": "quote_email_opened",
  "quote_id": "QT-123456",
  "guest_id": "G-789",
  "sequence_id": "SEQ-001",
  "step_number": 1,
  "channel": "email",
  "timestamp": "2026-01-06T10:30:00Z",
  "metadata": {
    "device": "mobile",
    "client": "Gmail"
  }
}
```

#### 7.2 Metrics Dashboard
Required visualizations:
- Quote funnel (Sent → Opened → Clicked → Booked)
- Conversion rate by step
- Channel performance comparison
- Time-to-conversion distribution
- A/B test results

#### 7.3 Attribution Model
- First-touch vs last-touch
- UTM parameter tracking
- Revenue attribution to sequence

### Section 8: Consent & Compliance

#### 8.1 Consent Management
| Regulation | Requirement | Implementation |
|------------|-------------|----------------|
| CAN-SPAM | Unsubscribe link | Footer in every email |
| GDPR | Explicit opt-in | Consent checkbox, stored |
| TCPA | Written consent for SMS | Opt-in during quote request |
| CASL | Identify organization | Company name in sender |

#### 8.2 Consent Schema
```json
{
  "guest_id": "G-789",
  "consents": {
    "marketing_email": {
      "granted": true,
      "timestamp": "2026-01-01T12:00:00Z",
      "source": "quote_request_form"
    },
    "marketing_sms": {
      "granted": false
    }
  },
  "unsubscribes": []
}
```

#### 8.3 Unsubscribe Flow
- One-click unsubscribe
- Preference center option
- Channel-specific opt-out
- Immediate effect (suppress within 10 seconds)

### Section 9: A/B Testing Framework

#### 9.1 Test Configuration
```json
{
  "test_id": "AB-001",
  "name": "Subject Line Test",
  "variable": "email_subject",
  "variants": [
    { "id": "A", "value": "Your quote is ready!", "weight": 50 },
    { "id": "B", "value": "Hi {{name}}, complete your booking", "weight": 50 }
  ],
  "success_metric": "conversion_rate",
  "min_sample_size": 1000,
  "confidence_level": 0.95
}
```

#### 9.2 Variant Assignment
- Consistent assignment per guest
- Random but balanced distribution
- Exclude existing customers

#### 9.3 Statistical Analysis
- Calculate conversion rates
- Compute confidence intervals
- Determine statistical significance
- Auto-declare winner at threshold

### Section 10: API Specification

#### 10.1 Quote Lifecycle APIs
```
POST /api/v1/quotes
  Create new quote, optionally start sequence

GET /api/v1/quotes/{quote_id}
  Get quote details and sequence status

POST /api/v1/quotes/{quote_id}/send
  Send quote and start follow-up sequence

POST /api/v1/quotes/{quote_id}/cancel
  Cancel quote and stop sequence

POST /api/v1/quotes/{quote_id}/convert
  Mark quote as converted (booking created)
```

#### 10.2 Sequence Management APIs
```
GET /api/v1/sequences
  List all configured sequences

POST /api/v1/sequences
  Create new sequence configuration

GET /api/v1/quotes/{quote_id}/sequence-status
  Get current position in sequence

POST /api/v1/quotes/{quote_id}/sequence/pause
  Pause sequence (e.g., guest replied)

POST /api/v1/quotes/{quote_id}/sequence/resume
  Resume paused sequence
```

#### 10.3 Analytics APIs
```
GET /api/v1/analytics/quotes/funnel
  Quote funnel metrics

GET /api/v1/analytics/sequences/performance
  Sequence conversion metrics

GET /api/v1/analytics/ab-tests/{test_id}
  A/B test results
```

### Section 11: Data Model

#### 11.1 Database Schema (MongoDB)

**quotes collection:**
```json
{
  "_id": "ObjectId",
  "quote_id": "QT-123456",
  "guest_id": "G-789",
  "property_id": "P-001",
  "dates": {
    "check_in": "ISODate",
    "check_out": "ISODate"
  },
  "line_items": [...],
  "total_price": "Decimal128",
  "status": "SENT",
  "sequence": {
    "id": "SEQ-001",
    "current_step": 2,
    "started_at": "ISODate",
    "paused": false
  },
  "events": [
    { "type": "sent", "timestamp": "ISODate" },
    { "type": "opened", "timestamp": "ISODate" }
  ],
  "sent_at": "ISODate",
  "expires_at": "ISODate",
  "created_at": "ISODate",
  "updated_at": "ISODate"
}
```

**sequences collection:**
```json
{
  "_id": "ObjectId",
  "sequence_id": "SEQ-001",
  "name": "Standard Quote Follow-up",
  "trigger_event": "QuoteSent",
  "steps": [...],
  "active": true,
  "created_at": "ISODate"
}
```

**templates collection:**
```json
{
  "_id": "ObjectId",
  "template_id": "quote-reminder-1",
  "channel": "email",
  "name": "Initial Quote Reminder",
  "subject": "...",
  "body": "...",
  "variables": [...],
  "version": 1
}
```

#### 11.2 Indexes
```javascript
db.quotes.createIndex({ "quote_id": 1 }, { unique: true })
db.quotes.createIndex({ "guest_id": 1, "status": 1 })
db.quotes.createIndex({ "expires_at": 1 }, { expireAfterSeconds: 0 })
db.quotes.createIndex({ "sequence.id": 1, "sequence.current_step": 1 })
```

### Section 12: Error Handling

#### 12.1 Failure Scenarios
| Scenario | Detection | Recovery |
|----------|-----------|----------|
| Email delivery failed | SendGrid webhook | Retry 3x, then SMS fallback |
| SMS delivery failed | Twilio callback | Log, alert, skip step |
| Template render error | Exception | Use default template |
| Quote expired during sequence | Timer check | Stop sequence gracefully |
| Database unavailable | Connection timeout | Retry with backoff |

#### 12.2 Dead Letter Queue
- Failed messages go to DLQ
- Manual review dashboard
- Retry capability
- Metrics on failure rates

### Section 13: Performance Requirements

| Requirement | Target | Measurement |
|-------------|--------|-------------|
| Sequence start latency | <1 second | Temporal start time |
| Message dispatch latency | <5 seconds | Provider to delivery |
| API response time | <200ms P95 | APM |
| Concurrent sequences | 10,000+ | Load test |
| Daily message volume | 100,000+ | Provider capacity |

### Section 14: Security

#### 14.1 Data Protection
- PII encryption at rest (AES-256)
- TLS 1.3 in transit
- Quote links use short-lived tokens
- Guest data access logging

#### 14.2 Rate Limiting
- 10 emails/minute per guest
- 5 SMS/hour per guest
- Prevent abuse/spam

### Section 15: Observability

#### 15.1 Logging
```json
{
  "level": "INFO",
  "service": "quote-chaser",
  "event": "sequence_step_executed",
  "quote_id": "QT-123456",
  "step": 2,
  "channel": "email",
  "result": "delivered",
  "duration_ms": 234
}
```

#### 15.2 Metrics (Prometheus)
- `quote_sequences_active` (gauge)
- `quote_messages_sent_total` (counter by channel)
- `quote_conversions_total` (counter)
- `quote_sequence_duration_seconds` (histogram)

#### 15.3 Alerts
| Alert | Condition | Severity |
|-------|-----------|----------|
| Low conversion rate | <1% for 24h | Warning |
| High unsubscribe rate | >2% for 1h | Critical |
| Delivery failures | >10% for 1h | Critical |
| Sequence backlog | >1000 pending | Warning |

### Section 16: Implementation Timeline

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Phase 1: MVP** | 3 weeks | Quote state machine, single email sequence, basic templates |
| **Phase 2: Multi-channel** | 2 weeks | SMS integration, template engine, consent management |
| **Phase 3: Analytics** | 2 weeks | Event tracking, dashboard, A/B framework |
| **Phase 4: Optimization** | 2 weeks | Performance tuning, advanced features |

---

## OUTPUT FORMAT

Your specification must include:
1. All sections above with complete technical detail
2. Mermaid diagrams for architecture and workflows
3. Complete code examples (Python for Temporal, JSON for schemas)
4. API specifications with request/response examples
5. Database schemas with indexes
6. Error handling matrices
7. Test scenarios and acceptance criteria

---

## QUALITY CRITERIA

| Criterion | Requirement |
|-----------|-------------|
| Completeness | All 16 sections fully specified |
| Implementability | Code examples are production-ready |
| Integration | Clear interfaces with CitadelOS |
| Performance | Scalable to 100K+ messages/day |
| Compliance | GDPR, CAN-SPAM, TCPA coverage |
| Testing | Comprehensive test scenarios |

---

## REFERENCE MATERIALS

- Knowledge Document: `knowledge/channel/KD-GW-001-quote-chaser.md`
- GuestWisely Quote Chaser documentation
- Klaviyo abandoned cart benchmarks
- OwnerRez trigger examples
- Temporal workflow patterns

