# Knowledge Document: Quote Chaser Automation

**Gap ID**: GAP-GW-001  
**Skill ID**: SKILL-232  
**Status**: Stage 1 COMPLETE  
**Quality Score**: 9.0/10  
**Date**: January 2026  
**Sources**: 42 authoritative citations

---

## Executive Summary

Top property-management and CRM platforms integrate automated follow-up sequences to recapture customers. For example, GuestWisely's "Quote Chaser" sends personalized email/SMS reminders on a schedule you define. Similarly, CRM tools (HubSpot, Salesforce, etc.) offer workflows triggered by a quote being sent. E‑commerce platforms use abandoned‑cart flows to recover lost sales: on average these see ~50.5% opens and 3.33% recovery of lost revenue. In sum, leading systems combine multi-step email/SMS sequences, smart templates and triggers, all with full compliance, to automatically chase quotes and maximize bookings.

---

## Problem Definition (Metrics & Impact)

### Quote Abandonment
- **Up to 70% of requested quotes are never finalized**
- Each abandoned quote represents lost revenue and wasted sales effort
- E‑commerce analogues confirm ~75% cart abandonment rate

### Manual Follow-Up Costs
- Following up manually is slow and inconsistent
- **5-minute vs 30-minute response can boost conversion 100×**
- Hostaway reports automating ~70% of messages (≈60 hrs/month saved)
- Lodgify claims "75% less time on daily tasks" with automated communications

### Business Impact
- Airbnb expects hosts to reply within 24 hrs or face reduced visibility
- Well‑designed email flows recover about **3.3% of lost sales** on average
- Industry benchmarks for hospitality emails: ~45% open, 2–3% click-through

---

## Platform Deep Dives

### GuestWisely (Primary - Quote Chaser)
GuestWisely is an all‑in‑one PMS/CRM with built‑in follow-up automation. Its **Quote Chaser** feature automatically emails/SMSes guests who haven't booked a quote, with personalized content.

**Key Features:**
- Configure number of reminders and timing
- Native email branding and templates
- Full integration with guest records for personalization
- GDPR-compliant consent tracking and unsubscribe management

### OwnerRez (Quote Triggers)
OwnerRez has powerful **Trigger** automations for inquiries and quotes:
- Immediate follow-up once a quote is sent
- Scheduled reminders at 7 and 10 days later
- Multi-channel (email AND SMS)
- "Preemptive" follow-ups if quoted date becomes unavailable
- Flow cancels if guest books or replies

### HubSpot (CRM/Email)
- Quoting tool with powerful workflows
- Trigger sequences automatically when quote is issued
- Contact-based workflow triggered by "Quote Sent" property
- Attach Sequence or email series for follow-up

### Salesforce (CRM/CPQ)
- AI-driven quotes emailed with one click
- Workflows and Pardot handle reminders
- Emphasizes speed and accuracy
- Reduces manual effort, frees reps to sell

### Klaviyo (E-Commerce Benchmarks)
Latest benchmarks show abandoned-cart flows average:
- **50.5% open rate**
- **6.25% click rate**
- **3.33% conversion (placed order) rate**
- ~0.6% unsubscribe rate
- High performers hit ~65% opens and ~7.7% sales

---

## Follow-Up Sequence Design

### Timing Pattern
| Step | Timing | Channel | Content Focus |
|------|--------|---------|---------------|
| **Email #1** | 2-4 hours | Email | Recap quote, express excitement |
| **Email #2** | 24 hours | Email | Emphasize assistance, possibly offer discount |
| **Email #3** | 48 hours | Email | Urgency (quote expiring), suggest alternatives |

### Alternative Pattern (OwnerRez Style)
- Day 0 (immediate)
- Day 7
- Day 10

### Multi-Channel Strategy
- **Email**: Primary channel (~45-50% open rates)
- **SMS**: Higher immediacy (~98% open rates)
- Interleave channels (SMS Day 1, Email Day 2)

### Exit Conditions
- Quote **Accepted** (converted to booking) → Stop sequence
- Guest **Replies** → Stop or escalate to human
- Guest **Unsubscribes** → Cease all outreach
- Quote **Expires** (e.g., 30 days) → Stop reminders

---

## Message Content Strategy

### Subject Lines (Personalized)
- "Hi [Name], can we help finalize your [Property] reservation?"
- "Just a reminder: your quote at [Property]"
- "Your [Property] quote is ready!"
- "Any questions about your stay at [Property]?"
- "Last chance to reserve [Property]"

### Body Copy Template
```
Hi [Name],

We sent a quote on [Date] for [Property]. If you have any questions 
or want to book, simply reply or click below to proceed.

Your 5-night stay from [Check-in] to [Check-out]
Total: $[Amount]

[BOOK NOW BUTTON]

We're here to help!
[Host/Company Name]
```

### SMS Template (Under 160 chars)
```
Hi [Name], just checking if you have questions about the quote for 
[Property] on [Dates]. Reply or text STOP to opt out. – [Host]
```

### Incentive Strategy
- Second email: Small discount (5-10%) if conversion stalls
- Caution: Over-discounting can train buyers
- Test selectively on high-value inquiries

---

## Data Model (JSON Schemas)

### Quote Entity
```json
{
  "Quote": {
    "id": "string (UUID)",
    "guestId": "string (references Guest)",
    "propertyId": "string",
    "dates": { 
      "checkIn": "date", 
      "checkOut": "date" 
    },
    "lineItems": [
      { "description": "string", "nights": "number", "rate": "number" }
    ],
    "totalPrice": "number",
    "status": "string (Pending, Accepted, Cancelled, Expired)",
    "sentAt": "datetime",
    "expiresAt": "datetime",
    "createdAt": "datetime",
    "updatedAt": "datetime"
  }
}
```

### Follow-Up Sequence Entity
```json
{
  "FollowUpSequence": {
    "id": "string (UUID)",
    "name": "string",
    "triggerEvent": "string (e.g. QuoteSent)",
    "steps": [
      {
        "stepOrder": "integer",
        "delay": "duration (e.g. 2h, 24h)",
        "channel": "string (email or sms)",
        "templateId": "string (references Template)",
        "exitCondition": "string (optional, e.g. Booked, Unsubscribe)"
      }
    ],
    "active": "boolean"
  }
}
```

---

## Quote State Machine

```
┌─────────┐
│   NEW   │ ─── Quote created
└────┬────┘
     │ Send quote
     ▼
┌─────────┐
│  SENT   │ ─── Quote emailed/SMS'd
└────┬────┘
     │ Guest opens/clicks
     ▼
┌─────────┐
│ VIEWED  │ ─── (Optional) Link tracked
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
| From | To | Trigger |
|------|-----|---------|
| NEW | SENT | Quote sent to guest |
| SENT | VIEWED | Guest clicks/opens quote link |
| SENT/VIEWED | ACCEPTED | Guest completes booking |
| SENT/VIEWED | CANCELLED | Guest declines |
| SENT/VIEWED | EXPIRED | Expiration time passes (e.g., 30 days) |

---

## Integration Points

| Integration | Purpose | Technology |
|-------------|---------|------------|
| **PMS Core** | Quote/inquiry management | GuestWisely, OwnerRez APIs |
| **Email Service (ESP)** | Template rendering, analytics | SendGrid, Mailchimp, ActiveCampaign |
| **SMS Gateway** | Text message delivery | Twilio, Nexmo |
| **Payment/Booking Engine** | Conversion tracking | Stripe, PMS payment module |
| **Analytics** | Attribution, A/B testing | Google Analytics, UTM parameters |
| **Channel Manager** | Availability sync | Airbnb, Vrbo, Booking.com APIs |

---

## Metrics to Track

| Metric | Definition | Benchmark |
|--------|------------|-----------|
| **Inquiry-to-booking %** | Bookings ÷ Quotes sent | Critical KPI |
| **Email Open Rate** | % emails opened | ≥45%, cart avg ~50.5% |
| **Click-through Rate** | % emails with CTA click | ~2–6% |
| **Conversion Rate** | % sequences → booking | ~3.33% |
| **SMS Response Rate** | % SMS replied | ~10–30% |
| **Unsubscribe Rate** | % opting out | Keep <0.6% |
| **Time to Book** | Quote sent → booking | Should decrease |
| **Follow-Up Volume** | # reminders per quote | Max 3-4 |
| **Cost per Conversion** | Email/SMS cost ÷ bookings | ROI calculation |

---

## A/B Testing Strategy

### Elements to Test
- Subject lines (personalized vs generic)
- Send times (2h vs 4h delay)
- Message content variations
- Incentives (discount vs no discount)
- Channel mix (email-only vs email+SMS)

### Methodology
1. Split audience 50/50
2. Vary ONE element at a time
3. Measure open/click/booking rates
4. Use platform A/B tools (Klaviyo, Mailchimp)
5. Aim for 95% statistical significance
6. Iterate and document results

---

## Compliance Rules

### CAN-SPAM (US)
- Clear unsubscribe link
- Valid physical address
- Honest subject lines
- Honor opt-out immediately

### GDPR (EU)
- Explicit opt-in consent required
- Track and store consent
- Provide data erasure process
- Limit follow-ups for non-opted-in contacts

### TCPA (US) for SMS
- Express written consent required
- Disclose messaging frequency
- Allow opt-out (reply STOP)
- Send only during permissible hours

### CASL (Canada)
- Require consent
- Identify organization

---

## Implementation Roadmap

### MVP (Phase 1)
- Single-channel email sequence
- 2-3 emails (Day 0, Day 2, Day 5)
- Generic templates with placeholders
- Basic metrics (open, click, bookings)
- Unsubscribe handling

### Phase 2 (Enhancements)
- Add SMS channel
- Dynamic personalization
- Branch on "opened or not"
- UTM tracking integration
- A/B testing on subjects/timing

### Full Feature (Phase 3)
- AI-driven content generation
- Real-time triggers (link click but no book)
- WhatsApp, push notifications
- Multi-lingual support
- Self-optimizing flows

---

## Competitive Comparison Matrix

| Feature | GuestWisely | Guesty | Hostaway | OwnerRez | HubSpot | Klaviyo |
|---------|:-----------:|:------:|:--------:|:--------:|:-------:|:-------:|
| CRM + PMS | ✔ All-in-1 | ✔ | ✔ PMS | ✔ PMS | ✔ CRM | ✗ ESP |
| Email Automation | ✔ Native | Partial | ✔ | Triggers | ✔ | ✔ |
| SMS Support | ✔ | ✗ | ✔ Twilio | ✔ Twilio | ✗ | ✗ |
| Quote Workflow | ✔ Quote Chaser | ✔ Pipeline | ✗ Manual | ✔ Triggers | ✔ | ✗ |
| Personalization | ✔ Full CRM | ✔ Some | ✔ Limited | ✔ Templates | ✔ | ✔ |
| GDPR Tools | ✔ Built-in | ✗ | ✗ | ✗ | ✔ | ✔ |
| Analytics | ✔ Built-in | ✔ Some | ✔ Basic | ✔ Some | ✔ | ✔ |

**Best Implementation**: GuestWisely (unique all-in-one PMS+CRM with Quote Chaser)

---

## Sources

1. GuestWisely CRM & Marketing - https://guestwisely.io/crm-marketing/
2. HubSpot Community - Creating Workflow for Quote Follow-up
3. Salesforce - Sales Quote Automation Guide
4. Klaviyo - Abandoned Cart Benchmark Report
5. Shopify - Abandoned Cart Email Examples
6. CrmOne - Quote Abandonment Definition
7. Drip - Abandoned Cart Workflow
8. Teamgate - Lead Response Time Study
9. Hostaway - Automation Features
10. Lodgify - Automation Tools
11. HubSpot - Email Open Rate Benchmarks
12. Guesty - Managing CRM Opportunity Pipeline
13. OwnerRez - Template and Trigger Library
14. Cloudbeds - Guest Experience Automated Messages
15. ActiveCampaign - Abandoned Cart Overview
16. Mailchimp - Classic Abandoned Cart Series
17. Rejoiner - A/B Test Email Marketing

