# GuestWisely - Skill Inventory

> **Source**: GuestWisely_PRD_Enhanced.md
> **Analysis Date**: January 2026
> **Focus**: Professional All-in-One PMS (20-500+ units)

---

## 🎯 **CRITICAL: GuestWisely = Professional All-in-One**

GuestWisely (evolved from 365Villas - 10+ years) positions as:
- **All-in-one philosophy** - No third-party plugins needed
- **Professional-grade** - 20-500+ units
- **60+ OTAs** - Wide distribution
- **Trust accounting** - Agency-ready
- **Quote Chaser** - Unique automation for lead conversion

This is a **comprehensive PMS** in the Guesty/Hostaway tier, with some unique automation features.

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 70+ |
| **New Unique Skills** | 6 |
| **Overlapping with Registry** | 50+ |
| **Knowledge Gaps Identified** | 4 |

**Note**: Most features overlap with existing registry skills from Guesty, Hostaway, OwnerRez. Focus on truly unique capabilities.

---

## 🆕 Unique Skills (New to Registry)

### 1. SKILL-232: quote-chaser-automation

**Priority**: P1
**Category**: sales-automation

**Description**: 
Automated follow-up system for quotes that haven't converted to bookings.

**How It Works**:
1. Quote sent to prospective guest
2. System tracks if quote converts
3. If not converted within timeframe, auto-send follow-up
4. Multiple follow-up sequences configurable
5. Track conversion rates

**Why Valuable**:
- Inquiries often lost without follow-up
- Manual follow-up is time-consuming
- Automation increases conversion rate
- "Set and forget" revenue recovery

**Key Differentiator**: Proactive lead nurturing, not just reactive communication.

---

### 2. SKILL-233: branded-guest-app

**Priority**: P1
**Category**: guest-experience

**Description**: 
White-label mobile app for guests with property manager branding.

**Features**:
- **Branded**: Manager's logo, colors
- **Pre-Check-in**: Forms, document upload
- **Messaging**: Direct in-app communication
- **Payments**: View balance, pay in-app
- **Guides**: Property info, local recommendations
- **Upselling**: Late checkout, cleaning, tours

**Why Valuable**:
- Professional guest experience
- Reduces inbound support requests
- Upselling revenue opportunity
- Brand reinforcement

**Competitors**: Few offer white-label guest apps.

---

### 3. SKILL-234: guest-document-collection

**Priority**: P1
**Category**: compliance

**Description**: 
Secure portal for guests to upload required documents (ID, vaccination, etc.).

**Features**:
- Secure upload portal
- Multiple document types supported
- Linked to booking and guest profile
- Automated reminders if not submitted
- Compliance tracking

**Use Cases**:
- ID verification (KYC)
- Rental agreement acknowledgment
- Vaccination proof (where required)
- Insurance certificates

**Why Valuable**: Compliance + security + automation.

---

### 4. SKILL-235: custom-report-builder

**Priority**: P1
**Category**: analytics

**Description**: 
User interface to build custom reports by selecting data points, filters, and dimensions.

**Features**:
- Select data fields (drag-and-drop)
- Apply filters (date, property, channel)
- Choose dimensions (grouping)
- Save report templates
- Share with team

**Why Valuable**:
- Every business has unique reporting needs
- Reduces "can you add this report" requests
- Self-service analytics
- Empowers power users

**Note**: Different from pre-built reports - this is user-created.

---

### 5. SKILL-236: scheduled-report-delivery

**Priority**: P2
**Category**: analytics

**Description**: 
Auto-generate and email reports to stakeholders on recurring schedule.

**Features**:
- Schedule frequency (daily, weekly, monthly)
- Select recipients (owners, managers, accountants)
- Choose report types
- Auto-generate at scheduled time
- Email with attachment (PDF, CSV)

**Use Cases**:
- Monthly owner statements (auto-send)
- Weekly performance reports to management
- Daily booking summaries to operations

**Why Valuable**: Eliminates manual report distribution.

---

### 6. SKILL-237: webhook-event-notifications

**Priority**: P1
**Category**: api-platform

**Description**: 
Real-time push notifications to external systems when events occur in PMS.

**Supported Events**:
- New booking created
- Booking cancelled
- Booking modified
- New message received
- Payment received
- Check-in/check-out

**Why Valuable**:
- Real-time integrations (vs polling)
- Lower API overhead
- Faster automations
- Modern API best practice

**Technical Note**: Enables real-time third-party integrations without constant API polling.

---

## 🔄 Overlapping Skills (Covered by Existing Registry)

GuestWisely covers many skills already documented:

| Domain | Existing Skills Covered |
|--------|------------------------|
| Channel Management | SKILL-XXX (60+ OTAs, two-way sync) |
| Website Builder | SKILL-187 (Lodgify), WordPress plugin |
| Reservation Management | Multiple existing skills |
| Communication | SKILL-XXX (unified inbox, templates) |
| Accounting | SKILL-180 (trust accounting), owner statements |
| Reports | SKILL-XXX (financial, occupancy) |
| Owner Portal | SKILL-028 (owner management) |
| Task Management | SKILL-XXX (automated tasks) |
| Multi-Currency | SKILL-XXX (international) |

---

## 🏆 Best-in-Class Features

| Feature | Why Notable | Compared To |
|---------|-------------|-------------|
| **Quote Chaser** | Auto follow-up on quotes | Manual in most PMS |
| **Branded Guest App** | White-label mobile | Few competitors |
| **Custom Report Builder** | Self-service analytics | Pre-built only |
| **Webhook Support** | Real-time API | Polling in many |

---

## 📊 Positioning Analysis

### GuestWisely vs Similar Competitors

| Dimension | GuestWisely | Guesty | Hostaway |
|-----------|-------------|--------|----------|
| **Target** | 20-500 units | 10-1000+ | 20-1000+ |
| **All-in-One** | ✅ Native | ⚠️ Marketplace | ✅ Native |
| **Quote Chaser** | ✅ | ❌ | ❌ |
| **Guest App** | ✅ White-label | ⚠️ Basic | ⚠️ Basic |
| **Custom Reports** | ✅ Builder | ⚠️ Pre-built | ⚠️ Pre-built |
| **Webhooks** | ✅ | ✅ | ✅ |
| **Trust Accounting** | ✅ | ✅ | ✅ |

**Position**: Solid professional PMS with unique automation (Quote Chaser) and guest app features.

---

## 📈 Architectural Insights

### GuestWisely Architecture Pattern
```
┌─────────────────────────────────────────────────────────────────┐
│                    GUESTWISELY PLATFORM                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ┌──────────────────────────────────────────────────────────┐  │
│   │              CHANNEL MANAGER (60+ OTAs)                   │  │
│   │  Native │ Two-Way Sync │ Rate Markups │ Content Sync     │  │
│   └──────────────────────────────────────────────────────────┘  │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              RESERVATION + COMMUNICATION                   │ │
│   │  Unified Calendar │ Quote Chaser │ Multi-Channel Inbox    │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              ACCOUNTING + REPORTING                        │ │
│   │  Trust Accounting │ Owner Payouts │ Custom Report Builder │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              GUEST EXPERIENCE                              │ │
│   │  Branded App │ Document Collection │ Upselling │ Guides   │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              API + INTEGRATIONS                            │ │
│   │  RESTful API │ Webhooks │ PriceLabs │ Smart Locks │ QB    │ │
│   └───────────────────────────────────────────────────────────┘ │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Key Insight for Our Platform

GuestWisely validates the **all-in-one native approach**:
- Native channel manager (not integration)
- Built-in accounting (not export-only)
- Quote Chaser shows value of **proactive automation**
- Guest app shows importance of **branded experience**

For our platform:
- **Quote follow-up automation** - Easy win
- **Guest document portal** - Compliance feature
- **Custom report builder** - Power user feature
- **Webhook API** - Modern integration standard

---

## 🎯 Strategic Implications

### What GuestWisely Teaches Us

1. **All-in-one works** - Reduces integration headaches
2. **Quote automation** - Proactive beats reactive
3. **Guest apps** - Mobile self-service expected
4. **Custom reports** - Users want flexibility
5. **10+ years experience** - Domain expertise matters

### Our Competitive Response

| GuestWisely Strength | Our Response |
|---------------------|--------------|
| Quote Chaser | Implement similar + AI enhancement |
| Guest App | Build or partner |
| Custom Reports | Design flexible reporting |
| Webhooks | Standard API feature |

---

## Next Steps

1. **Design quote automation** - Based on GuestWisely pattern
2. **Guest app strategy** - Build vs partner
3. **Report builder UX** - Self-service analytics
4. **Webhook implementation** - Real-time events


