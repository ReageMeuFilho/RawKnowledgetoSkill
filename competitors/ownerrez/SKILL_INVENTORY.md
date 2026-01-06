# OwnerRez - Skill Inventory

> **Source**: OWNERREZ (v2)PRD.md
> **Analysis Date**: January 2026
> **Focus**: Accounting-First Mid-Market Platform (5-150 properties)

---

## 🎯 **CRITICAL: OwnerRez = Accounting Excellence**

OwnerRez fills the **mid-market accounting** gap:
- **QuickBooks-First** philosophy (deep QB Online integration)
- **Trust accounting workflows** via PM module + QB sync
- **5-150 properties** sweet spot (10-60 core)
- **Power-user orientation** (complexity for capability trade-off)

This is the platform for **accounting-focused PMCs**.

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 55+ |
| **New Unique Skills** | 7 |
| **Overlapping with Registry** | 45+ |
| **Knowledge Gaps Identified** | 6 |

---

## 🆕 Unique Skills (New to Registry)

### 1. SKILL-200: quickbooks-first-accounting 🎉

**Priority**: P0
**Category**: accounting-integration

**Description**: 
Platform designed to offload full accounting to QuickBooks Online while providing detailed sync rules and deposit syncing.

**Philosophy**:
- OwnerRez = operational ledger
- QuickBooks = double-entry accounting
- Deposit syncing = to-the-penny bank reconciliation
- Owner payouts sync as checks/bills in QB

**Key Differentiator**: Not "integrates with QB" - **DESIGNED FOR QB** from the ground up.

**Components**:
- Bookings auto-synced to QB
- Payments auto-synced to QB
- Deposits synced for reconciliation
- Owner payouts as QB checks/bills
- Tax summaries for filing

**Strategic Note**: For accounting-heavy PMCs, this is the killer feature.

---

### 2. SKILL-201: deposit-syncing-reconciliation

**Priority**: P0
**Category**: accounting-integration

**Description**: 
Deposit syncing for to-the-penny bank reconciliations in QuickBooks Online.

**How It Works**:
1. Guest makes payment
2. OwnerRez records in ledger
3. Auto-sync to QuickBooks
4. QB matches bank deposit exactly
5. Reconciliation complete

**Key Differentiator**: **To-the-penny** accuracy - no manual journal entries.

**Critical For**: Audit compliance, owner trust, accountant efficiency.

---

### 3. SKILL-202: modular-pricing-architecture

**Priority**: P1
**Category**: commercial-model

**Description**: 
Base PMS plus add-on modules allowing granular control over cost structure.

**Modules**:
- **Base PMS**: Calendar, reservations, basic features
- **PM Module**: Owner statements, commissions
- **QuickBooks Integration**: Premium sync features
- **Hosted Websites**: Direct booking sites
- **WordPress Plugin**: WP integration
- **SMS Messaging**: Metered/add-on

**Key Differentiator**: Pay only for what you need.

**Strategic Note**: Good for cost-conscious operators who don't need everything.

---

### 4. SKILL-203: channel-rate-testing

**Priority**: P1
**Category**: pricing-optimization

**Description**: 
Tools to compare actual OTA listings vs expected nightly prices to verify rate accuracy.

**Use Cases**:
- Verify channel sync is working correctly
- Compare markup across channels
- Identify pricing discrepancies
- Test before going live

**Key Differentiator**: **Audit capability** for pricing integrity.

---

### 5. SKILL-204: quote-to-booking-workflow

**Priority**: P1
**Category**: booking-operations

**Description**: 
Create quotes with taxes/fees, send to guests, and convert to bookings upon acceptance.

**Flow**:
1. Guest inquires
2. PM creates quote with all charges
3. Quote sent to guest
4. Guest reviews and accepts
5. Quote converts to booking
6. Payment collected

**Key Differentiator**: **Formal quote process** vs immediate booking.

**Use Cases**:
- Custom pricing negotiations
- Group bookings
- Long-stay inquiries
- Corporate clients

---

### 6. SKILL-205: digital-rental-agreements

**Priority**: P0
**Category**: legal-compliance

**Description**: 
Custom rental agreements per property/channel with digital signature collection and booking automation.

**Features**:
- Custom agreements per property
- Different agreements per channel
- Digital signature collection
- Auto-send on booking creation
- Require signature before check-in
- Store signed agreements

**Key Differentiator**: **Legal protection** built into booking flow.

---

### 7. SKILL-206: owner-stay-tracking

**Priority**: P2
**Category**: owner-management

**Description**: 
Special reservation status for owner stays that appear appropriately in calendars and financials.

**How It Works**:
- Owner stay blocks calendar
- No revenue recorded
- Separate from guest bookings
- Appears in owner reports
- Cleaning tasks can still trigger

**Key Differentiator**: **Clean accounting** for owner use vs rental income.

---

## 🔄 Overlapping Skills (Enhanced by OwnerRez)

| Existing Skill | OwnerRez Enhancement |
|----------------|---------------------|
| SKILL-180 (trust-accounting) | + QuickBooks-first design |
| SKILL-192 (owner-statements) | + Commission splits, payout rules |
| SKILL-028 (owner-reports) | + QB payout sync |
| SKILL-XXX (channel-mgmt) | + Rate testing/comparison |
| SKILL-XXX (direct-booking) | + WordPress plugin |
| SKILL-XXX (task-automation) | + Turno/Breezeway integration |

---

## 🏆 Best-in-Class Features

| Feature | Why Best | For Whom |
|---------|----------|----------|
| **QuickBooks Integration** | Deepest in market | Accounting-focused PMs |
| **Deposit Syncing** | To-the-penny | Audit compliance |
| **Owner Statements** | Full PM module | Multi-owner portfolios |
| **Rate Testing** | Verify pricing | Channel-heavy operators |
| **Rental Agreements** | Digital e-sign | Legal protection |

---

## 📊 Mid-Market Positioning

### OwnerRez vs Competitors

| Dimension | OwnerRez | Hostaway | Hospitable | Lodgify |
|-----------|----------|----------|------------|---------|
| **Focus** | Accounting | Enterprise | Automation | Website |
| **QB Depth** | **DEEP** | Moderate | Basic | Basic |
| **Trust Accounting** | **STRONG** | Strong | Limited | None |
| **AI Messaging** | None | Partial | **STRONG** | Minimal |
| **Website** | Secondary | Basic | Simple | **STRONG** |
| **Complexity** | High | High | Low | Low |

### Market Segmentation Complete!

```
                    LOW                    HIGH
                    ACCOUNTING DEPTH
              ┌─────────────────────────────┐
    SIMPLE    │                    │        │
    UX        │     Lodgify       │        │
              │     Hospitable     │        │
              ├────────────────────┼────────┤
    COMPLEX   │                    │OwnerRez│
    UX        │     Guesty        │Hostaway│
              │                    │        │
              └─────────────────────────────┘
```

---

## 📈 Architectural Insights

### OwnerRez Architecture Pattern
```
┌─────────────────────────────────────────────────────────────────┐
│                    OWNERREZ PLATFORM                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ┌──────────────────────────────────────────────────────────┐  │
│   │              OPERATIONAL LEDGER (Primary)                 │  │
│   │  ┌────────────┐ ┌────────────┐ ┌────────────┐            │  │
│   │  │ Bookings   │ │ Payments   │ │ Expenses   │            │  │
│   │  │ & Quotes   │ │ & Deposits │ │ & Fees     │            │  │
│   │  └────────────┘ └────────────┘ └────────────┘            │  │
│   └──────────────────────────────────────────────────────────┘  │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              QUICKBOOKS SYNC ENGINE                        │ │
│   │  ┌────────────┐ ┌────────────┐ ┌────────────┐             │ │
│   │  │ Invoices   │ │ Deposits   │ │ Payouts    │             │ │
│   │  │ → QB       │ │ → QB       │ │ → QB       │             │ │
│   │  └────────────┘ └────────────┘ └────────────┘             │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │                   PM MODULE (Add-On)                       │ │
│   │  Owner Statements │ Commission Splits │ Payout Rules      │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              CHANNEL MANAGER + OPERATIONS                  │ │
│   │  Airbnb | Vrbo | Booking.com | Tasks | Agreements         │ │
│   └───────────────────────────────────────────────────────────┘ │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Key Insight for Our Platform

OwnerRez validates that **accounting-first architecture** works for mid-market:
- Operational ledger separate from GL
- QuickBooks as external accounting engine
- Modular pricing for cost efficiency
- Power-user automations for flexibility

For our platform:
- Consider QB integration as premium feature
- Support accounting export at minimum
- Modular pricing for different segments

---

## 🎯 Strategic Implications

### What OwnerRez Teaches Us

1. **QuickBooks integration is critical** for US mid-market
2. **Modular pricing** attracts cost-conscious operators
3. **Power-user complexity** acceptable for capable users
4. **Trust accounting** is legal requirement in many states
5. **Rate testing** prevents pricing errors at scale

### Our Competitive Response

| OwnerRez Strength | Our Counter |
|-------------------|-------------|
| QuickBooks-first | QB integration + multi-accounting |
| Modular pricing | Tiered plans with flexibility |
| Trust accounting | Match via Hostaway-level |
| Rate testing | Built-in pricing audit |
| Rental agreements | Digital signature integration |

### Market Gap Analysis

| Segment | Champion | Our Opportunity |
|---------|----------|-----------------|
| SMB Website | Lodgify | Match builder |
| SMB AI | Hospitable | Match Knowledge Hub |
| Mid-Market Accounting | **OwnerRez** | Match QB depth |
| Enterprise | Guesty/Hostaway | Full feature parity |
| LTR | EliseAI | Multi-vertical approach |

**Full market coverage now documented!**

---

## Next Steps

1. **Document QB sync requirements** - What data flows needed?
2. **Quote-to-booking UX** - How to implement formal quotes?
3. **Digital signature integration** - E-sign providers?
4. **Rate testing tool** - Automated pricing audit?


