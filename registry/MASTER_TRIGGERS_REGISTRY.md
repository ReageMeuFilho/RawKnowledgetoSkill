# Master Triggers Registry: Events & Activation Points

> **What starts the agent** - Inbound messages, events, schedules, webhooks
> **Purpose**: Define all entry points that activate the agent
> **Last Updated**: January 2026

---

## 🎯 Why Triggers Matter

The agent doesn't just respond to messages - it can be activated by:
- 📱 Inbound message (WhatsApp, SMS, Email)
- 📅 Scheduled event (24h before check-in)
- 🔔 Webhook (Booking created in Airbnb)
- ⏰ Timer (No response in 24h)
- 📊 Threshold (Review score drops below 4.0)

---

## 📊 Trigger Types

| Type | Source | Example |
|------|--------|---------|
| **Message** | User sends message | "Help with check-in" |
| **Schedule** | Time-based | "24h before checkout" |
| **Webhook** | External system | "New booking created" |
| **Event** | Internal event | "Ticket status changed" |
| **Threshold** | Metric crossed | "3 complaints in 7 days" |
| **Timer** | Elapsed time | "No vendor response in 2h" |

---

## 📱 Message Triggers

### TRIG-001: Inbound WhatsApp Message

**Type**: Message
**Source**: Twilio Webhook
**Frequency**: Real-time

**Trigger Payload**:
```json
{
  "from": "+15551234567",
  "body": "My toilet is broken",
  "timestamp": "2026-01-08T10:30:00Z",
  "media_url": null
}
```

**Actions**:
1. Identify tenant by phone number
2. Load tenant context
3. Load property context
4. Route to appropriate skill
5. Generate response

---

### TRIG-002: Inbound SMS

**Type**: Message
**Source**: Twilio Webhook
**Frequency**: Real-time

**Same as TRIG-001, different channel.**

---

### TRIG-003: Inbound Email

**Type**: Message
**Source**: SendGrid Inbound Parse / Gmail API
**Frequency**: Real-time

**Trigger Payload**:
```json
{
  "from": "tenant@email.com",
  "subject": "Maintenance Request",
  "body": "...",
  "attachments": []
}
```

---

## 📅 Scheduled Triggers

### TRIG-010: Pre-Arrival Message (STR)

**Type**: Schedule
**Timing**: 24 hours before check-in
**Source**: Scheduler (cron)

**Trigger Condition**:
```sql
SELECT * FROM bookings 
WHERE check_in_date = CURRENT_DATE + INTERVAL '1 day'
AND pre_arrival_sent = FALSE
```

**Actions**:
1. Load booking details
2. Load property info
3. Generate pre-arrival message
4. Send via WhatsApp/SMS/Email
5. Mark pre_arrival_sent = TRUE

---

### TRIG-011: Check-In Day Access Code (STR)

**Type**: Schedule
**Timing**: Check-in day, 2 hours before check-in time
**Source**: Scheduler

**Actions**:
1. Generate/retrieve access code
2. Send to guest with instructions
3. Log in conversation history

---

### TRIG-012: Post-Checkout Review Request (STR)

**Type**: Schedule
**Timing**: 24 hours after checkout
**Source**: Scheduler

**Actions**:
1. Check if guest had issues during stay
2. If no issues: Send review request
3. If issues: Send follow-up instead
4. Log outreach

---

### TRIG-013: Rent Reminder (LTR)

**Type**: Schedule
**Timing**: 3 days before rent due
**Source**: Scheduler

**Trigger Condition**:
```sql
SELECT * FROM leases 
WHERE rent_due_day = EXTRACT(DAY FROM CURRENT_DATE + INTERVAL '3 days')
AND status = 'active'
```

**Actions**:
1. Check if rent already paid
2. If not paid: Send friendly reminder
3. Include payment link

---

### TRIG-014: Lease Renewal Outreach (LTR)

**Type**: Schedule
**Timing**: 90 days before lease expiry
**Source**: Scheduler

**Actions**:
1. Check tenant eligibility
2. Generate renewal offer
3. Send renewal communication
4. Start WORKFLOW-003 (Lease Renewal)

---

## 🔔 Webhook Triggers

### TRIG-020: New Booking Created (Airbnb)

**Type**: Webhook
**Source**: Airbnb API / Channel Manager
**Frequency**: On event

**Trigger Payload**:
```json
{
  "event": "booking_created",
  "booking_id": "airbnb-12345",
  "property_id": "prop-456",
  "guest": {
    "name": "John Smith",
    "phone": "+15551234567",
    "email": "john@email.com"
  },
  "dates": {
    "check_in": "2026-01-15",
    "check_out": "2026-01-18"
  }
}
```

**Actions**:
1. Create/update booking in database
2. Create guest profile if new
3. Schedule TRIG-010 (Pre-arrival)
4. Schedule TRIG-011 (Access code)
5. Send booking confirmation

---

### TRIG-021: Booking Cancelled

**Type**: Webhook
**Source**: Airbnb API / Channel Manager

**Actions**:
1. Update booking status
2. Cancel scheduled triggers
3. Notify cleaning team if applicable
4. Update calendar

---

### TRIG-022: Payment Received (Stripe)

**Type**: Webhook
**Source**: Stripe

**Actions**:
1. Update payment status
2. Generate receipt
3. Send confirmation to tenant
4. Update ledger

---

### TRIG-023: Payment Failed (Stripe)

**Type**: Webhook
**Source**: Stripe

**Actions**:
1. Log failure reason
2. Send payment failure notification
3. Offer alternative payment method
4. Schedule retry

---

## 📊 Threshold Triggers

### TRIG-030: Multiple Complaints

**Type**: Threshold
**Condition**: 3+ complaints in 7 days for same property
**Source**: Internal monitoring

**Actions**:
1. Alert property manager
2. Generate complaint summary
3. Flag for review
4. Consider proactive outreach

---

### TRIG-031: Review Score Drop

**Type**: Threshold
**Condition**: Property average drops below 4.0
**Source**: Review aggregation

**Actions**:
1. Alert property manager
2. Analyze recent reviews
3. Generate improvement suggestions

---

### TRIG-032: Vendor Non-Response

**Type**: Timer
**Condition**: No vendor response 2 hours after dispatch
**Source**: Ticket monitoring

**Actions**:
1. Send vendor reminder
2. If still no response after 1h: Try backup vendor
3. Log non-responsiveness

---

## 📋 Trigger Specification Template

```markdown
### TRIG-XXX: [trigger-name]

**Type**: [Message / Schedule / Webhook / Event / Threshold / Timer]
**Source**: [Where it comes from]
**Frequency**: [Real-time / Daily / On event / etc.]

**Condition**:
[When this trigger fires]

**Payload**:
```json
{
  "field": "value"
}
```

**Actions**:
1. [Action 1]
2. [Action 2]

**Workflows Started**: [WORKFLOW-XXX]
**Skills Activated**: [SKILL-XXX]

**Error Handling**:
- [What if trigger fails?]
```

---

## 🔄 Trigger → Workflow → Skill Flow

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    TRIGGER → WORKFLOW → SKILL FLOW                               │
└─────────────────────────────────────────────────────────────────────────────────┘

  TRIGGER                    WORKFLOW                    SKILL
  (Entry Point)              (Multi-step Process)        (Capability)
  
  ┌─────────────────┐        ┌─────────────────┐        ┌─────────────────┐
  │ TRIG-001        │        │ WORKFLOW-001    │        │ SKILL-010       │
  │ Inbound Message │───────►│ Maintenance     │───────►│ maintenance-    │
  │ "Toilet broken" │        │ Request Flow    │        │ triage          │
  └─────────────────┘        └─────────────────┘        └─────────────────┘
  
  ┌─────────────────┐        ┌─────────────────┐        ┌─────────────────┐
  │ TRIG-010        │        │ WORKFLOW-002    │        │ SKILL-003       │
  │ Schedule: 24h   │───────►│ Check-In Flow   │───────►│ check-in-       │
  │ before check-in │        │                 │        │ coordinator     │
  └─────────────────┘        └─────────────────┘        └─────────────────┘
  
  ┌─────────────────┐                                   ┌─────────────────┐
  │ TRIG-022        │                                   │ SKILL-024       │
  │ Webhook: Payment│──────────────────────────────────►│ payment-        │
  │ Received        │        (No workflow needed)       │ confirmation    │
  └─────────────────┘                                   └─────────────────┘
```



