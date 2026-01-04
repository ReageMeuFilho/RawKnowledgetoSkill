# Besty AI - Skill Inventory

> **Source**: `besty_ai_revenue_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: STR Revenue Optimization & Guest Messaging
> **Type**: AI Copilot Layer (NOT a full PMS)

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 28 | 11 NEW, 17 overlap (with DEPTH) |
| Tools | 14 | 5 NEW |
| Memory Types | 8 | 3 NEW |
| Workflows | 12 | 8 NEW |

---

## 🎯 Besty AI Context

**Besty is NOT a full PMS** - it's a specialized AI layer focused on:
- **Communication** - 24/7 AI-powered guest messaging
- **Revenue** - Gap nights, early check-in, late checkout upselling
- **Journeys** - Multi-step automated communication sequences
- **Reviews** - 100% automated review response

**Key Differentiators**:
- Integration-first (works with Guesty, OwnerRez, Hostaway, etc.)
- 9% commission on upsell revenue only (pure ROI alignment)
- 5-minute deployment (not 4-6 weeks)
- Co-pilot → Autopilot progression
- 15,000+ properties globally

---

## 🆕 NEW Skills (Not in Previous PRDs)

### NEW-BESTY-001: Inquiry Winback Automation
**Category**: revenue
**Priority**: P0
**Description**: Automatically follow up on abandoned inquiries to recover lost bookings.

**Unique Capabilities**:
- Track inquiry dropoff points
- 3-message follow-up sequence (24h, 48h, 72h)
- Objection-based messaging (price, availability, trust)
- Progressive escalation
- 8-20% recovery rate documented

**Workflow**:
1. Inquiry received → Response sent → No guest reply
2. 24h: "Still interested in [DATE]?"
3. 48h: Address objection + incentive
4. 72h: Final "last chance" appeal
5. Stop after 3 messages (avoid spam)

**Knowledge Required**:
- KG-BESTY-001: Inquiry objection patterns

---

### NEW-BESTY-002: Direct Booking Conversion
**Category**: revenue
**Priority**: P1
**Description**: Convert OTA inquiries (Airbnb, VRBO) to direct bookings to save commission.

**Unique Capabilities**:
- Respond helpfully on OTA first
- Suggest direct booking with discount
- Show savings (OTA 15% vs direct 5% discount)
- WhatsApp pivot for commission-free chat
- 5-15% conversion rate

**Knowledge Required**:
- KG-BESTY-002: Direct booking conversion tactics

---

### NEW-BESTY-003: Co-Pilot vs Autopilot Mode
**Category**: ai-control
**Priority**: P0
**Description**: Graduated automation from human-review (Co-Pilot) to full automation (Autopilot).

**Unique Capabilities**:
- AI drafts, human reviews → approve/edit/reject
- Feedback trains model (rejected responses improve)
- Progressive trust-building
- Configurable confidence threshold (95%+ for auto-send)
- Audit trail of all AI decisions

**Implementation**:
- Start Co-Pilot for new properties
- Graduate to Autopilot after trust established
- Override capability always available

---

### NEW-BESTY-004: Confidence Threshold System
**Category**: ai-control
**Priority**: P0
**Description**: Route messages to human when AI confidence is below threshold.

**Unique Capabilities**:
- 0-100% confidence scoring per response
- Configurable threshold by message type
- Auto-escalation logic
- Confidence distribution tracking
- Learning curve visualization

**Escalation Rules**:
- Confidence < 80%: Escalate to human
- Health/safety: Always escalate
- Refunds/disputes: Always escalate
- Complex requests: Escalate if uncertain

---

### NEW-BESTY-005: Visual Journey Builder
**Category**: automation
**Priority**: P1
**Description**: Drag-and-drop builder for multi-step guest communication sequences.

**Unique Capabilities**:
- No coding required
- Sequential steps with time delays
- Branching logic (if/then)
- A/B testing built-in
- 30+ pre-built journey templates
- Multi-channel (SMS, email, WhatsApp)

**Journey Types**:
- Pre-arrival (booking → check-in)
- During-stay (check-in → check-out)
- Post-checkout (departure → future)
- Event-triggered (damage, no-show, bad review)

---

### NEW-BESTY-006: Real-Time Sentiment Alerts
**Category**: communication
**Priority**: P1
**Description**: Detect negative guest sentiment and alert property manager immediately.

**Unique Capabilities**:
- 0-100 sentiment scoring
- Emotion detection (frustration, anger, urgency)
- Automatic flag when sentiment < 40
- Alert distribution to manager/owner
- Response tone adaptation (empathetic to frustrated guests)
- Trend tracking over stay

---

### NEW-BESTY-007: Brand Voice Training
**Category**: ai-control
**Priority**: P1
**Description**: Train AI to match property's unique communication style.

**Unique Capabilities**:
- Tone setting (formal, friendly, casual)
- Upload example messages for style learning
- Signature greetings/sign-offs
- Phrases to avoid
- Personality attributes
- Per-property customization

---

### NEW-BESTY-008: Extended Stay Discount Automation
**Category**: revenue
**Priority**: P1
**Description**: Proactively offer discounts for 7+ night stays to fill calendar.

**Discount Tiers**:
- 7-13 nights: 10% off
- 14-29 nights: 20% off
- 30+ nights: 30% off

**Targeting**:
- Current guests mid-stay: "Extend for 10% off"
- Inquiry prospects: "Book 14+ nights, save 20%"
- Repeat guests: Extra loyalty discount

---

### NEW-BESTY-009: Review Response by Sentiment
**Category**: communication
**Priority**: P0
**Description**: Generate contextual review responses matched to sentiment.

**Response Templates**:
- **5-star**: Grateful, personal, invite return
- **4-star**: Acknowledge positive, address concern, commit to fix
- **3-star**: Professional, ownership, concrete solution
- **1-2 star**: Sincere apology, root cause, service recovery offer

**Capabilities**:
- Reference specific details from review
- Maintain brand voice
- Auto-post or queue for review
- 100% response rate (vs manual 40-50%)

---

### NEW-BESTY-010: Knowledge Base Auto-Population
**Category**: ai-control
**Priority**: P1
**Description**: Automatically populate AI knowledge from PMS property data.

**Auto-Populated**:
- Property address, check-in/out times
- Amenities list
- House rules
- Cancellation policy
- Rates and availability

**Manual Upload**:
- House manual (WiFi, appliances, etc.)
- Local guide (restaurants, attractions)
- Brand voice examples

---

### NEW-BESTY-011: Conversation Summary Intelligence
**Category**: analytics
**Priority**: P2
**Description**: Auto-generate summaries of conversation threads with issue identification.

**Capabilities**:
- Key points extraction
- Issue identification ("What problem is guest reporting?")
- Pattern detection across properties
- Resolution tracking
- Context retention for repeat guests
- Actionable insights ("WiFi mentioned 15x = operational issue")

---

## 🔄 Skills Enhanced with Besty Depth

These skills exist in Guesty/Host OS but Besty provides **production-ready workflows**:

### SKILL-069: Gap Night Revenue Optimization (ENHANCED)

**Besty Enhancement - Full Workflow**:
1. Calendar scanning (auto-identify gaps)
2. Turnover feasibility check
3. Availability verification
4. Guest identification (departing AND arriving)
5. Smart pricing calculation (base rate × 70%)
6. Personalized message generation
7. Multi-channel delivery
8. Response tracking
9. Auto-booking creation in PMS
10. Calendar sync (prevent overbooking)
11. Housekeeping notification

**Psychology/Pricing Strategy**:
- Don't discount base rate in PMS
- Create two separate upsell offers
- Departing guest: "Extend for $91 (30% off)"
- Arriving guest: "Come early for $91 (30% off)"
- Margin maintained, perceived generous discount

**Documented Impact**:
- 40-60% fill rate on gap nights
- 10-30% revenue uplift per property
- $3,264-7,344/month for 30-property operator

---

### SKILL-039: Early Check-In Management (ENHANCED)

**Besty Enhancement - Full Workflow**:
1. Identify eligible bookings (arriving tomorrow)
2. Check housekeeping schedule feasibility
3. Calculate premium ($163-195 for $130 base)
4. Send proactive offer 2-3 days before
5. Offer multiple times (11am, 1pm, 2pm)
6. Track acceptance
7. Add charge to booking
8. Notify housekeeping of new timeline

**Documented Impact**:
- 5-15% acceptance rate
- $40-50 premium per early check-in
- $1,350/month for 30 properties

---

### SKILL-040: Late Checkout Management (ENHANCED)

**Besty Enhancement - Full Workflow**:
1. Identify eligible guests (no next arrival pressure)
2. Check housekeeping flexibility
3. Offer options:
   - 11am → 1pm: +$25
   - 11am → 4pm: +$50
   - 11am → 6pm: +$75
4. Multi-touch timing (3-5 days, 1-2 days, morning of)
5. Track acceptance
6. Coordinate housekeeping schedule

**Documented Impact**:
- 3-10% acceptance rate
- $35-50 per late checkout
- $945/month for 30 properties

---

### SKILL-001: Guest Message Response (ENHANCED)

**Besty Enhancement - 12+ Channels**:
- Airbnb, VRBO, Booking.com
- Email, SMS, WhatsApp
- Telegram, WeChat, Facebook Messenger
- PMS native inbox
- Mobile app

**Message Types (100% Automated)**:
- Pre-booking inquiries
- Booking confirmations
- Countdown sequences (1 week, 3 days, 1 day)
- During-stay requests (60%+ automated)
- Review management
- Post-checkout sequences

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-BESTY-001 | calculate_confidence_score | Score AI response confidence | BUILD |
| TOOL-BESTY-002 | detect_sentiment | Real-time sentiment analysis | BUY (NLP API) |
| TOOL-BESTY-003 | build_journey_step | Create journey workflow step | BUILD |
| TOOL-BESTY-004 | track_inquiry_status | Monitor inquiry conversion | BUILD |
| TOOL-BESTY-005 | generate_review_response | Create sentiment-matched response | BUILD |

---

## 🔀 NEW Workflows from Besty

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-BESTY-001 | Pre-Arrival Journey | Booking confirmed | 5 steps over 7 days |
| WF-BESTY-002 | During-Stay Journey | Guest checked in | 3-5 mid-stay touchpoints |
| WF-BESTY-003 | Post-Checkout Journey | Guest departed | Review request, loyalty offer |
| WF-BESTY-004 | Inquiry Winback | No response 24h | 3-message sequence |
| WF-BESTY-005 | Gap Night Outreach | Gap detected | Dual offers to departing/arriving |
| WF-BESTY-006 | Early Check-In Offer | Arrival -3 days | Proactive premium offer |
| WF-BESTY-007 | Late Checkout Offer | Departure -3 days | Tiered pricing offer |
| WF-BESTY-008 | Extended Stay Pitch | Guest mid-stay | Discount for 7+ nights |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-BESTY-001 | Inquiry Funnel | Track inquiry → booking conversion | 1 year |
| MEM-BESTY-002 | Confidence History | AI confidence scores per message | 90 days |
| MEM-BESTY-003 | Journey Progress | Guest position in active journey | Duration of stay |

---

## 📋 Knowledge Gaps from Besty

| ID | Knowledge Needed | Skills Blocked |
|----|------------------|----------------|
| KG-BESTY-001 | Inquiry objection patterns | Inquiry Winback |
| KG-BESTY-002 | Direct booking conversion tactics | Direct Booking Conversion |
| KG-BESTY-003 | Gap night pricing psychology | Gap Night (ENHANCED) |
| KG-BESTY-004 | Review response templates by sentiment | Review Response |
| KG-BESTY-005 | Journey message timing best practices | Journey Builder |
| KG-BESTY-006 | Confidence threshold tuning | Co-Pilot/Autopilot |

---

## 🏆 What Besty Adds to Our Solution

**ADOPT (Critical)**:
1. **Inquiry Winback** - 8-20% recovery rate is huge
2. **Confidence Threshold System** - Production-ready AI control
3. **Gap Night Full Workflow** - Complete automation
4. **Review Response by Sentiment** - 100% response rate

**ADOPT (Valuable)**:
1. **Co-Pilot → Autopilot Progression** - Trust-building
2. **Visual Journey Builder** - No-code automation
3. **Real-Time Sentiment Alerts** - Catch problems early
4. **Extended Stay Automation** - Fill long gaps

**CONSIDER**:
1. **Direct Booking Conversion** - Depends on OTA terms
2. **Brand Voice Training** - Nice for consistency

---

## 📊 Besty vs Other Platforms

| Dimension | Besty | Guesty | Host OS | Mews |
|-----------|-------|--------|---------|------|
| **Focus** | Revenue + Comms | Full PMS | Agentic AI | Hotel PMS |
| **Gap Night** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |
| **AI Messaging** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Journeys** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Reviews** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Confidence** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |
| **Operations** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Analytics** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

**Bottom Line**: Besty is the **deep source** for revenue upselling and AI messaging workflows. Use Besty patterns for gap nights, inquiry recovery, journeys, and AI confidence control.

