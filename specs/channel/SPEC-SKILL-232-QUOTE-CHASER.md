# Skill Specification: Quote Chaser Automation

**Skill ID**: SKILL-232  
**Gap ID**: GAP-GW-001  
**Category**: Channel / Sales Automation  
**Priority**: P1  
**Status**: SPECIFIED ✅  
**Date**: January 2026

---

## Overview

**Quote Chaser Automation** is a multi-channel follow-up system that automates quote-to-booking conversion through intelligent sequencing, targeting **3.33% recovery** of the 70% of quotes that are never finalized.

---

## Key Performance Indicators

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Quote Abandonment Rate** | Reduce from 70% | % quotes without bookings |
| **Recovery Rate** | ≥3.33% | Converted quotes / abandoned quotes |
| **Email Open Rate** | ≥50.5% | Opened / delivered |
| **Click-through Rate** | ≥6.25% | Clicks / opened |
| **Response Speed** | <1 second | Time to start sequence |
| **Monthly Time Savings** | 60+ hours | Manual effort displaced |
| **Daily Message Volume** | 100,000+ | Messages per day |

---

## Core Capabilities

### 1. Quote State Machine
- **States**: NEW → SENT → VIEWED → ACCEPTED/CANCELLED/EXPIRED
- **Event-driven transitions** with audit trail
- **Real-time** status tracking

### 2. Multi-Step Sequence Engine (Temporal)
- **Fault-tolerant** workflow execution
- **Configurable timing** (2h → 24h → 48h pattern)
- **Goal-based termination** on booking or unsubscribe
- **Resume after failures** with idempotent execution

### 3. Multi-Channel Dispatcher
| Channel | Provider | Rate Limit |
|---------|----------|------------|
| Email | SendGrid | 100/second |
| SMS | Twilio | 10/second |
| WhatsApp | Twilio | 5/second |

### 4. Template Engine
- **Liquid templating** with personalization variables
- **A/B variant support** for optimization
- **Rendering preview** before send

### 5. Analytics & Attribution
- **Funnel tracking** (sent → opened → clicked → converted)
- **UTM attribution** for campaign analysis
- **A/B test statistics** with confidence intervals

### 6. Compliance Framework
- **GDPR consent management** for EU guests
- **CAN-SPAM** one-click unsubscribe
- **TCPA** SMS consent and quiet hours

---

## Standard Follow-Up Sequence

```
Quote Sent
    │
    ├─[2 hours]──→ Email 1: "Your quote is ready!"
    │                 Subject: Excitement/urgency
    │                 CTA: View Quote
    │
    ├─[24 hours]─→ Email 2: "Questions? We're here to help"
    │                 Subject: Assistance offer
    │                 CTA: Chat with us
    │
    └─[48 hours]─→ SMS: "Final reminder - quote expires soon"
                     Message: Limited availability
                     CTA: Book now link
```

---

## Technology Stack

| Layer | Component | Technology |
|-------|-----------|------------|
| **Backend** | Language | Python 3.12+ |
| | Framework | Flask 3.0 |
| | Workflow | Temporal Python SDK |
| **Frontend** | Framework | React 18 |
| | UI | Material-UI 5 |
| | Charts | Recharts |
| **Data** | Database | MongoDB |
| | Cache | Redis |
| | Queue | Redis Streams |
| **Messaging** | Email | SendGrid |
| | SMS/WhatsApp | Twilio |
| **Infra** | Container | Docker |
| | Orchestration | AWS ECS |

---

## Data Architecture

### Collections (MongoDB)
```
quotes           - Quote documents with state, sequence position
guests           - Guest profiles with consent records
sequences        - Sequence configuration templates
messages         - Delivery logs with tracking
templates        - Email/SMS templates
ab_tests         - A/B test configurations and assignments
events           - Analytics event stream
```

### Key Indexes
```javascript
quotes.createIndex({ "quote_id": 1 }, { unique: true })
quotes.createIndex({ "status": 1, "created_at": -1 })
quotes.createIndex({ "sequence.workflow_id": 1 })
guests.createIndex({ "email": 1 }, { unique: true })
messages.createIndex({ "quote_id": 1, "created_at": -1 })
```

---

## API Surface

### Quote Operations
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/quotes` | Create quote |
| GET | `/quotes/{id}` | Get quote details |
| POST | `/quotes/{id}/send` | Send and start sequence |
| POST | `/quotes/{id}/cancel` | Cancel quote |
| POST | `/quotes/{id}/convert` | Mark as booked |

### Sequence Control
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/sequences` | List configurations |
| POST | `/sequences` | Create sequence |
| GET | `/quotes/{id}/sequence-status` | Get current step |
| POST | `/quotes/{id}/sequence/pause` | Pause sequence |

### Analytics
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/analytics/quotes/funnel` | Conversion funnel |
| GET | `/analytics/sequences/performance` | Sequence metrics |
| GET | `/analytics/ab-tests/{id}` | A/B test results |

---

## UI Components

### 1. Quote Dashboard
- Quote list with status filters
- Real-time funnel visualization
- Conversion metrics cards
- Activity feed

### 2. Sequence Builder
- Visual workflow editor
- Drag-and-drop step configuration
- Template selection dropdown
- Preview mode

### 3. Analytics Console
- Open/click/conversion charts
- A/B test comparison
- Channel performance breakdown
- Time-to-conversion histogram

---

## Integration Points

### Inbound (Quote Sources)
- **PMS Webhook**: New quote created event
- **Website Form**: Direct booking inquiry
- **Channel Manager**: OTA inquiry forwarding

### Outbound (Notifications)
- **SendGrid**: Transactional email delivery
- **Twilio**: SMS/WhatsApp messaging
- **PMS**: Booking confirmation sync

---

## Implementation Phases

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Phase 1** | Weeks 1-3 | Quote state machine, Temporal workflows |
| **Phase 2** | Weeks 4-6 | Email dispatcher, basic templates |
| **Phase 3** | Weeks 7-9 | SMS integration, multi-channel |
| **Phase 4** | Weeks 10-12 | Analytics, A/B testing |
| **Phase 5** | Weeks 13-14 | UI dashboard, sequence builder |

**Total Duration**: 14 weeks

---

## Success Metrics

### Month 1 (MVP)
- Quote state machine operational
- Basic 2-step email sequence
- Manual sequence configuration

### Month 2 (Growth)
- Multi-channel (email + SMS)
- A/B testing framework
- Sequence builder UI

### Month 3 (Optimization)
- Analytics dashboard
- Auto-optimization suggestions
- WhatsApp integration

---

## Competitive Advantage

| Feature | Our Implementation | Typical Competitor |
|---------|-------------------|-------------------|
| Sequence Start | <1 second | Minutes |
| A/B Testing | Native | Third-party |
| Multi-channel | Email + SMS + WhatsApp | Email only |
| Compliance | GDPR + CAN-SPAM + TCPA | Basic |
| Scale | 100,000+ msgs/day | 10,000 |

---

## Related Documentation

| Document | Path |
|----------|------|
| Knowledge Document | `knowledge/channel/KD-GW-001-quote-chaser.md` |
| Engineering Spec | `knowledge/channel/ES-GW-001-quote-chaser.md` |
| Stage 2 Prompt | `docs/prompts/ENGINEERING_SPEC_PROMPT_QUOTE_CHASER.md` |

---

## Skill Definition (Claude Format)

```yaml
name: quote-chaser
description: |
  Automate quote-to-booking conversion with multi-step email/SMS sequences.
  Use when: Quote created and not converted within timeframe.
  Do NOT use: For confirmed bookings or active guests.

version: 1.0.0
priority: P1
domain: channel
localization: global

triggers:
  events: ["quote_created", "quote_expired_warning"]
  keywords: ["quote", "booking inquiry", "price request"]

tools:
  - name: get_quote_status
    type: mcp
    uri: mcp://pms/get_quote_status
    
  - name: send_sequence_message
    type: mcp
    uri: mcp://temporal/trigger_sequence_step
    
  - name: check_consent
    type: mcp
    uri: mcp://compliance/check_marketing_consent

hitl:
  required: false
  escalate_on: ["vip_guest", "high_value_quote", "consent_unclear"]

evaluation:
  accuracy_target: 0.95
  test_cases_path: tests/quote-chaser/
```

---

**Status**: ✅ SPECIFIED - Ready for Implementation

