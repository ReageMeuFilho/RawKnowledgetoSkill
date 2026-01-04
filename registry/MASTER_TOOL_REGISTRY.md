# Master Tool Registry: Deterministic Functions

> **Specification for all tools** the agent needs to execute actions
> **Purpose**: Define WHAT tools do, then decide HOW to implement (Build/Buy/Open Source)
> **Last Updated**: January 2026

---

## 🎯 Tool Specification Purpose

Each tool specification answers:
1. **WHAT** does this tool do? (Function)
2. **WHAT** are the inputs/outputs? (Interface)
3. **HOW** should we implement it? (Build / Buy / Open Source)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    TOOL SPECIFICATION → IMPLEMENTATION DECISION                  │
└─────────────────────────────────────────────────────────────────────────────────┘

  TOOL SPEC                              IMPLEMENTATION OPTIONS
  
  ┌─────────────────────────┐           ┌─────────────────────────┐
  │ Tool: send_whatsapp     │           │ 🔨 BUILD                │
  │                         │           │    Custom code          │
  │ Input: phone, message   │           │                         │
  │ Output: MessageResult   │──────────►│ 💰 BUY                  │
  │                         │           │    Twilio API ($)       │
  │ Used by: 15 skills      │           │                         │
  │                         │           │ 🆓 OPEN SOURCE          │
  └─────────────────────────┘           │    whatsapp-web.js      │
                                        └─────────────────────────┘
```

---

## 📋 Tool Specification Template

```markdown
### TOOL-XXX: [tool-name]

**Category**: [communication/calendar/database/payment/iot/calculation]

## SPECIFICATION (The WHAT)

**Purpose**: [One sentence: what does this tool do?]

**Function Signature**:
```python
def tool_name(
    param1: type,      # Description
    param2: type,      # Description
) -> ReturnType:
    """What it does"""
```

**Inputs**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| param1 | str | Yes | Description |
| param2 | int | No | Description |

**Outputs**:
| Field | Type | Description |
|-------|------|-------------|
| success | bool | Whether operation succeeded |
| data | dict | Result data |
| error | str | Error message if failed |

**Used By Skills**:
- SKILL-XXX [skill-name]
- SKILL-XXX [skill-name]

**Usage Frequency**: [High/Medium/Low]

---

## IMPLEMENTATION DECISION (The HOW)

**Options Evaluated**:

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| [Option 1] | Build | [Pros] | [Cons] | Dev time |
| [Option 2] | Buy | [Pros] | [Cons] | $/month |
| [Option 3] | Open Source | [Pros] | [Cons] | Free |

**Decision**: [BUILD / BUY / OPEN SOURCE]
**Reason**: [Why this choice]
**Implementation**: [Specific library/API/code approach]

---

## IMPLEMENTATION DETAILS

**If BUILD**:
- Script location: `mcp-servers/[category]/tools/[tool-name].py`
- Dependencies: [libraries needed]

**If BUY**:
- Provider: [Company name]
- API Docs: [URL]
- Pricing: [Cost structure]
- API Key Location: [Environment variable]

**If OPEN SOURCE**:
- Library: [Name]
- GitHub: [URL]
- License: [License type]
- Version: [Version to use]
```

---

## 📊 Tool Categories

| Category | Tools | Description |
|----------|-------|-------------|
| `communication` | 0 | Send messages, make calls |
| `calendar` | 0 | Check availability, create events |
| `database` | 0 | Query, create, update records |
| `payment` | 0 | Process payments, refunds |
| `iot` | 0 | Smart locks, thermostats |
| `calculation` | 0 | Pricing, taxes, payouts |
| `validation` | 0 | Verify data, check constraints |
| `file` | 0 | Generate documents, reports |
| `integration` | 0 | Third-party API calls |

---

## 🔧 Communication Tools

### TOOL-001: send_whatsapp_message

**Category**: communication

## SPECIFICATION

**Purpose**: Send a WhatsApp message to a phone number

**Function Signature**:
```python
def send_whatsapp_message(
    phone: str,           # Phone number with country code (+1234567890)
    message: str,         # Message text (max 4096 chars)
    media_url: str = None # Optional media attachment URL
) -> MessageResult:
    """Send WhatsApp message via configured provider"""
```

**Inputs**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| phone | str | Yes | Phone with country code |
| message | str | Yes | Message text |
| media_url | str | No | URL to image/document |

**Outputs**:
| Field | Type | Description |
|-------|------|-------------|
| success | bool | Message sent successfully |
| message_id | str | Provider's message ID |
| timestamp | datetime | When sent |
| error | str | Error if failed |

**Used By Skills**:
- CORE-001 guest-message-responder
- STR-010 turnover-scheduler
- STR-003 check-in-coordinator
- LTR-005 rent-reminder
- (15+ skills across all verticals)

**Usage Frequency**: HIGH (core communication channel)

---

## IMPLEMENTATION DECISION

**Options Evaluated**:

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| Twilio WhatsApp API | Buy | Reliable, official, good docs | Cost per message | ~$0.005/msg |
| Meta Cloud API | Buy | Direct from Meta, cheaper | Complex setup | ~$0.003/msg |
| whatsapp-web.js | Open Source | Free, full features | Against ToS, unstable | Free |
| Custom Build | Build | Full control | Huge effort, ToS issues | Dev time |

**Decision**: **BUY - Twilio WhatsApp API**
**Reason**: 
- Official WhatsApp Business API partner
- Reliable delivery, good deliverability
- Easy setup, great documentation
- Reasonable cost at scale
- Compliant with WhatsApp ToS

**Implementation**:
- Provider: Twilio
- API Docs: https://www.twilio.com/docs/whatsapp
- Pricing: ~$0.005/outbound, $0.005/inbound
- API Key: `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`

---

### TOOL-002: send_sms

**Category**: communication

## SPECIFICATION

**Purpose**: Send an SMS text message

**Function Signature**:
```python
def send_sms(
    phone: str,      # Phone number with country code
    message: str     # Message text (max 160 chars for single SMS)
) -> MessageResult:
    """Send SMS via configured provider"""
```

**Used By Skills**: CORE-001, STR-014 emergency-handler, LTR-008

**Usage Frequency**: MEDIUM

---

## IMPLEMENTATION DECISION

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| Twilio SMS | Buy | Same provider as WhatsApp | Cost | ~$0.0075/msg |
| AWS SNS | Buy | Cheap, scalable | Less features | ~$0.00645/msg |
| Vonage | Buy | Good international | Setup complexity | Varies |

**Decision**: **BUY - Twilio SMS**
**Reason**: Same provider as WhatsApp = single integration, unified billing

---

### TOOL-003: send_email

**Category**: communication

## SPECIFICATION

**Purpose**: Send an email with optional attachments

**Function Signature**:
```python
def send_email(
    to: str,                    # Recipient email
    subject: str,               # Email subject
    body_html: str,             # HTML body
    body_text: str = None,      # Plain text fallback
    attachments: list = None,   # List of attachment URLs
    from_email: str = None      # Override sender (if allowed)
) -> EmailResult:
    """Send email via configured provider"""
```

**Used By Skills**: CORE-002, LTR-001 lease-manager, HOA-003 assessment-notice

**Usage Frequency**: HIGH

---

## IMPLEMENTATION DECISION

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| SendGrid | Buy | Reliable, good templates | Cost at scale | $20/mo + usage |
| AWS SES | Buy | Cheapest, scalable | Basic features | ~$0.10/1000 |
| Resend | Buy | Modern API, great DX | Newer company | $20/mo |
| Postmark | Buy | Best deliverability | Higher cost | $15/mo |

**Decision**: **BUY - SendGrid**
**Reason**: Good balance of features, templates, and cost

---

## 📅 Calendar Tools

### TOOL-010: check_availability

**Category**: calendar

## SPECIFICATION

**Purpose**: Check if a property/resource is available for given dates

**Function Signature**:
```python
def check_availability(
    property_id: str,       # Property to check
    start_date: date,       # Check-in date
    end_date: date,         # Check-out date
    check_type: str = "booking"  # "booking" | "cleaning" | "maintenance"
) -> AvailabilityResult:
    """Check calendar availability"""
```

**Outputs**:
| Field | Type | Description |
|-------|------|-------------|
| available | bool | Is the slot available |
| conflicts | list | List of conflicting events |
| next_available | date | Next available date if blocked |

**Used By Skills**: STR-005 availability-checker, STR-006 booking-creator

**Usage Frequency**: HIGH

---

## IMPLEMENTATION DECISION

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| Custom (PostgreSQL) | Build | Full control, fast | Dev time | Free |
| Google Calendar API | Buy | Familiar, integrations | Limited for custom | Free tier |
| Cal.com | Open Source | Full-featured | Overkill for internal | Free |

**Decision**: **BUILD - Custom PostgreSQL**
**Reason**: Core business logic, need full control over availability rules

---

## 💳 Payment Tools

### TOOL-020: process_payment

**Category**: payment

## SPECIFICATION

**Purpose**: Process a payment (charge a card, collect rent, etc.)

**Function Signature**:
```python
def process_payment(
    amount: Decimal,           # Amount to charge
    currency: str,             # ISO currency code (USD, BRL)
    customer_id: str,          # Customer/tenant ID
    payment_method_id: str,    # Saved payment method
    description: str,          # What this payment is for
    metadata: dict = None      # Additional data
) -> PaymentResult:
    """Process payment via configured provider"""
```

**Used By Skills**: STR-024 payment-collector, LTR-006 rent-collector

**Usage Frequency**: HIGH (revenue-critical)

---

## IMPLEMENTATION DECISION

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| Stripe | Buy | Best API, global | 2.9% + $0.30 | % of transaction |
| PayPal | Buy | Consumer trust | Worse API | 2.9% + $0.30 |
| Adyen | Buy | Enterprise, global | Complex | Varies |
| Square | Buy | Good for SMB | US-focused | 2.6% + $0.10 |

**Decision**: **BUY - Stripe**
**Reason**: Best developer experience, handles complexity, global coverage

---

## 🔌 IoT Tools

### TOOL-030: get_lock_code

**Category**: iot

## SPECIFICATION

**Purpose**: Get current access code for a smart lock

**Function Signature**:
```python
def get_lock_code(
    lock_id: str,              # Lock device ID
    code_type: str = "current" # "current" | "master" | "guest"
) -> LockCodeResult:
    """Get access code from smart lock"""
```

**Used By Skills**: STR-003 check-in-coordinator

**Usage Frequency**: MEDIUM

---

## IMPLEMENTATION DECISION

| Option | Type | Pros | Cons | Cost |
|--------|------|------|------|------|
| Seam API | Buy | Unified API for 20+ locks | Cost | $3/device/mo |
| August API | Buy | Direct integration | Only August | Free |
| RemoteLock API | Buy | Property-focused | Only their locks | Varies |
| Build custom | Build | Full control | Each lock brand = work | Dev time |

**Decision**: **BUY - Seam API**
**Reason**: One integration supports August, Yale, Schlage, etc.

---

## 📊 Implementation Summary

### Build vs Buy vs Open Source Matrix

| Tool | Decision | Provider/Library | Cost |
|------|----------|-----------------|------|
| send_whatsapp_message | BUY | Twilio | ~$0.005/msg |
| send_sms | BUY | Twilio | ~$0.0075/msg |
| send_email | BUY | SendGrid | $20/mo |
| check_availability | BUILD | Custom PostgreSQL | Dev time |
| create_calendar_event | BUILD | Custom PostgreSQL | Dev time |
| process_payment | BUY | Stripe | 2.9% + $0.30 |
| create_invoice | BUY | Stripe | Included |
| get_lock_code | BUY | Seam | $3/device/mo |
| query_database | BUILD | Custom MCP | Dev time |
| calculate_price | BUILD | Custom Python | Dev time |
| generate_pdf | OPEN SOURCE | WeasyPrint | Free |
| send_push_notification | BUY | Firebase/OneSignal | Free tier |

---

## 🎯 Decision Framework

### When to BUILD
- ✅ Core business logic (availability, pricing)
- ✅ Competitive differentiation
- ✅ No good external option
- ✅ Need full control

### When to BUY
- ✅ Commodity service (email, SMS)
- ✅ Complex infrastructure (payments)
- ✅ Reliability critical
- ✅ Time to market priority

### When to use OPEN SOURCE
- ✅ Well-maintained library exists
- ✅ License is compatible (MIT, Apache)
- ✅ Not mission-critical
- ✅ Want to avoid vendor lock-in

---

## 📈 Tool Priority by Vertical

### Core Tools (All Verticals Need)
| Priority | Tool | Implementation |
|----------|------|----------------|
| P0 | send_whatsapp_message | BUY - Twilio |
| P0 | query_database | BUILD |
| P0 | send_email | BUY - SendGrid |
| P1 | process_payment | BUY - Stripe |
| P1 | send_sms | BUY - Twilio |

### STR-Specific Tools
| Priority | Tool | Implementation |
|----------|------|----------------|
| P0 | check_availability | BUILD |
| P0 | create_booking | BUILD |
| P1 | get_lock_code | BUY - Seam |
| P1 | calculate_dynamic_price | BUILD |
| P2 | sync_channel_calendar | BUILD |

### LTR-Specific Tools
| Priority | Tool | Implementation |
|----------|------|----------------|
| P0 | generate_lease_document | BUILD + OPEN SOURCE |
| P0 | run_tenant_screening | BUY - TransUnion/Plaid |
| P1 | calculate_rent_increase | BUILD |
| P2 | file_eviction | BUILD |
