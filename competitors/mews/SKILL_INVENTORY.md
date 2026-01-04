# Mews Hospitality Platform - Skill Inventory

> **Source**: `mews_hospitality_pms_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: Hospitality (Hotels, Hostels, Serviced Apartments)
> **Type**: Hotel-Grade PMS (adaptable to STR)

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 52 | 15 NEW, 37 overlap |
| Tools | 22 | 8 NEW |
| Memory Types | 12 | 4 NEW |
| Integrations | 18 | 6 NEW |

---

## 🏨 Mews Context

Mews is a **hotel-grade PMS** focused on:
- Hotels (50-500 rooms)
- Hostels
- Serviced apartments
- Mixed-use properties

**Key Differentiators from STR platforms**:
- Check-in KIOSK hardware
- Digital Key (BLE, NFC, Apple Wallet)
- Hourly bookings (not just nightly)
- Front desk workflow optimization
- Revenue Management System (Atomize RMS)
- Enterprise multi-property management

---

## 🆕 NEW Skills (Not in Guesty or Host OS)

### NEW-MEWS-001: Self-Service Check-In Kiosk
**Category**: operations
**Priority**: P1
**Description**: Tablet-based self-service check-in with payment processing, upselling, and key activation.

**Unique Capabilities**:
- Hardware integration (iPad/Android tablet)
- Card reader for payments
- NFC reader for Digital Key activation
- Camera for photo capture
- Thermal printer for receipts
- 2.6x higher upsell conversion vs staff check-in
- Accessibility features (large text, text-to-speech)

**Knowledge Required**:
- KG-MEWS-001: Kiosk hardware selection and setup
- KG-MEWS-002: Kiosk upsell optimization

---

### NEW-MEWS-002: Digital Key with Apple Wallet
**Category**: operations
**Priority**: P1
**Description**: Contactless room access via smartphone with BLE/NFC and Apple Wallet integration.

**Unique Capabilities**:
- App clip (no app store required)
- Apple Wallet integration
- Key sharing between guests
- Automatic revocation at checkout
- Offline operation (BLE)
- Access audit logging
- Remote lock control by staff

**Knowledge Required**:
- KG-MEWS-003: Digital key hardware requirements
- KG-MEWS-004: Apple Wallet integration

---

### NEW-MEWS-003: Hourly/Flexible Space Booking
**Category**: booking
**Priority**: P1
**Description**: Price and book spaces by hour, day, week, or month (not just nightly).

**Unique Capabilities**:
- Hourly rate plans
- Day-use bookings
- Weekly/monthly discounts
- Meeting room booking
- Co-working desk booking
- Event space hourly rentals

**Knowledge Required**:
- KG-MEWS-005: Flexible pricing models

---

### NEW-MEWS-004: AI Revenue Management (Atomize RMS)
**Category**: pricing
**Priority**: P1
**Description**: Machine learning-powered pricing optimization with demand forecasting.

**Unique Capabilities**:
- Real-time demand forecasting
- Automated rate recommendations 24/7
- Competitive intelligence monitoring
- 90-day forward forecasting
- Sensitivity analysis (test before applying)
- 20-37% RevPAR improvement reported

**Knowledge Required**:
- KG-MEWS-006: ML-based revenue management

---

### NEW-MEWS-005: Conversion-Optimized Booking Engine
**Category**: channel
**Priority**: P0
**Description**: Direct booking website with A/B testing, smart recommendations, and upsell orchestration.

**Unique Capabilities**:
- Mobile-first (60% of bookings)
- <2 second load time on 3G
- A/B testing framework built-in
- Resume booking after 48 hours
- Social proof (real-time booking notifications)
- Dynamic bundling based on occupancy
- Gift card integration

**Knowledge Required**:
- KG-MEWS-007: Booking engine conversion optimization

---

### NEW-MEWS-006: Real-Time Messaging (No App Required)
**Category**: communication
**Priority**: P0
**Description**: Web-based real-time messaging via SMS/email link, no app download needed.

**Unique Capabilities**:
- SMS link access (no app)
- WebSocket-based (<2 second latency)
- FAQ bot for common questions
- Staff sees guest location (outdoor venues)
- Bulk announcements to rooms

**Knowledge Required**:
- KG-001 (Guest Message Response) - ENHANCED

---

### NEW-MEWS-007: Guest Data Capture at Pre-Arrival
**Category**: compliance
**Priority**: P0
**Description**: Collect payment info, personal data, signatures, and preferences before arrival.

**Unique Capabilities**:
- Digital signature capture
- Passport/ID scan
- Payment card pre-authorization
- Emergency contact collection
- Group member management
- GDPR-compliant data handling

**Knowledge Required**:
- KG-MEWS-008: Pre-arrival data collection best practices

---

### NEW-MEWS-008: Front Desk Command Center
**Category**: operations
**Priority**: P0
**Description**: Centralized interface for reception with real-time occupancy map, queues, and alerts.

**Unique Capabilities**:
- Visual occupancy map (color-coded)
- Arrival/departure queues with wait times
- Check-in queue management
- Priority alerts (overbooking, VIP)
- 3-5 minute check-in vs 10-15 traditional
- Offline check-in capability

**Knowledge Required**:
- KG-MEWS-009: Front desk workflow optimization

---

### NEW-MEWS-009: Overbooking Management
**Category**: booking
**Priority**: P1
**Description**: Controlled overbooking to maximize occupancy with waitlist and relocation tools.

**Unique Capabilities**:
- Overbooking thresholds per property
- Waitlist functionality
- Cancellation prediction
- Relocation workflow
- Compensation tracking

**Knowledge Required**:
- KG-MEWS-010: Overbooking strategies and relocation

---

### NEW-MEWS-010: Staff Shift Planning
**Category**: operations
**Priority**: P2
**Description**: Housekeeping shift scheduling with capacity planning and overtime tracking.

**Unique Capabilities**:
- Shift creation and assignment
- Capacity planning (rooms per shift)
- Shift swapping between staff
- Overtime alerts
- Break tracking compliance
- Payroll integration

**Knowledge Required**:
- KG-MEWS-011: Staff scheduling best practices

---

### NEW-MEWS-011: Housekeeping Performance Analytics
**Category**: analytics
**Priority**: P2
**Description**: Track individual cleaner performance with leaderboards and quality scores.

**Unique Capabilities**:
- Rooms cleaned per shift
- Average turnover time per cleaner
- Quality score from inspections
- Guest satisfaction correlation
- Leaderboards for motivation
- Labor cost per room

**Knowledge Required**:
- KG-003 (Cleaning Workflow) - ENHANCED

---

### NEW-MEWS-012: GOPPAR Reporting
**Category**: analytics
**Priority**: P1
**Description**: Gross Operating Profit Per Available Room metric including operational costs.

**Unique Capabilities**:
- Revenue minus operational costs
- Property-level profitability
- Expense category breakdown
- Trend analysis
- Benchmark comparison

**Knowledge Required**:
- KG-MEWS-012: Hotel financial metrics

---

### NEW-MEWS-013: 1000+ Integration Marketplace
**Category**: channel
**Priority**: P1
**Description**: Open API ecosystem with 1000+ certified integrations and no connection fees.

**Unique Capabilities**:
- No connection fees (vs competitors)
- Pre-built connectors
- Partner certification process
- Native SDKs (JS, Python, Ruby, Go)
- Zapier integration

**Knowledge Required**:
- Technical (no domain knowledge needed)

---

### NEW-MEWS-014: Loyalty Tier Management
**Category**: communication
**Priority**: P2
**Description**: VIP tier management with automatic recognition and service delivery.

**Unique Capabilities**:
- Loyalty program integration
- VIP flagging on arrival
- Tier-based service delivery
- Repeat guest recognition
- Lifetime value tracking

**Knowledge Required**:
- KG-MEWS-013: Loyalty program design

---

### NEW-MEWS-015: Package Deal Bundling
**Category**: pricing
**Priority**: P1
**Description**: Bundle rooms with services (spa, dining, experiences) as packages.

**Unique Capabilities**:
- Room + service bundles
- Dynamic bundle pricing
- Occupancy-based bundling
- Package promotion management
- Bundle revenue tracking

**Knowledge Required**:
- KG-MEWS-014: Package pricing strategies

---

## 🔄 Skills Overlapping with Guesty/Host OS

Mews has these capabilities but with HOTEL-grade detail:

| Mews Feature | STR Equivalent | Mews Enhancement |
|--------------|----------------|------------------|
| Reservation Management | Calendar Sync | Hourly bookings, overbooking |
| Guest Profile | Guest CRM | Cross-property history, VIP tiers |
| Rate Management | Dynamic Pricing | Atomize RMS, ML forecasting |
| Housekeeping App | Task Management | Shift planning, performance metrics |
| Payment Processing | Guesty Pay | Embedded platform, PCI L1 |
| Multi-Property | Enterprise Hub | Portfolio dashboard, bulk ops |
| Virtual Concierge | Guest App | No-app messaging, in-stay services |
| Digital Key | Smart Lock | Apple Wallet, BLE, NFC |
| Upselling | Upsell Management | Kiosk conversion, A/B testing |
| Analytics | Dashboard | GOPPAR, cohort analysis |

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-MEWS-001 | render_kiosk_ui | Display kiosk check-in flow | BUILD |
| TOOL-MEWS-002 | process_kiosk_payment | Process card at kiosk | BUY (Stripe) |
| TOOL-MEWS-003 | activate_digital_key | Provision key to phone | BUILD |
| TOOL-MEWS-004 | add_to_apple_wallet | Push key to Apple Wallet | BUY (Apple) |
| TOOL-MEWS-005 | forecast_demand | ML demand prediction | BUILD/BUY |
| TOOL-MEWS-006 | calculate_goppar | Compute GOPPAR metric | BUILD |
| TOOL-MEWS-007 | schedule_staff_shift | Create/manage shifts | BUILD |
| TOOL-MEWS-008 | capture_digital_signature | Capture guest signature | BUILD |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-MEWS-001 | Kiosk Transactions | Kiosk check-in records | 2 years |
| MEM-MEWS-002 | Digital Key Log | Key issuance/access log | 1 year |
| MEM-MEWS-003 | Demand Forecasts | ML prediction history | 1 year |
| MEM-MEWS-004 | Staff Performance | Cleaner metrics | 2 years |

---

## 🔌 NEW Integrations Required

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-MEWS-001 | ASSA ABLOY | Digital key locks | API |
| INT-MEWS-002 | Salto | Digital key locks | API |
| INT-MEWS-003 | Apple Wallet | Key delivery | API |
| INT-MEWS-004 | Atomize | Revenue management | Native |
| INT-MEWS-005 | Adyen | Payment processing | API |
| INT-MEWS-006 | Zapier | No-code automation | API |

---

## 📊 Comparison: Mews vs STR Platforms

| Dimension | Guesty | Host OS | Mews | Best For |
|-----------|--------|---------|------|----------|
| **Target** | STR hosts | STR operators | Hotels | - |
| **Booking Unit** | Nightly | Nightly | Hourly+ | Mews (flexibility) |
| **Check-In** | Smart lock | Smart lock | Kiosk + Key | Mews (options) |
| **AI Pricing** | Basic | Gap nights | Atomize RMS | Mews (ML) |
| **Operations** | Good | Better | Best | Mews (hotel-grade) |
| **Guest Comms** | Good | RAG | No-app | Host OS + Mews |
| **Analytics** | Good | Basic | GOPPAR | Mews (finance) |
| **Scale** | 1-1000 | 1-1000 | 50-10000 | Mews (enterprise) |

---

## 🎯 What Mews Adds to Our Solution

**ADOPT for STR**:
1. **Digital Key with Apple Wallet** - Better than code-only smart lock
2. **No-App Messaging** - Guest portal without app download
3. **Conversion-Optimized Booking Engine** - A/B testing, smart recommendations
4. **Housekeeping Performance Metrics** - Labor cost optimization
5. **GOPPAR Reporting** - True profitability metrics

**CONSIDER for Premium STR**:
1. **Self-Service Kiosk** - For buildings with 10+ units
2. **Hourly Bookings** - For day-use / meeting space
3. **Atomize RMS** - For portfolios wanting ML pricing

**SKIP for STR**:
1. Front desk command center (not needed for STR)
2. Overbooking management (STR doesn't overbook)
3. Staff shift planning (STR uses contractors)

---

## 📋 Knowledge Gaps (NEW from Mews)

| ID | Knowledge Needed | Skills Blocked |
|----|------------------|----------------|
| KG-MEWS-001 | Kiosk hardware selection | Kiosk Check-In |
| KG-MEWS-002 | Kiosk upsell optimization | Kiosk Check-In |
| KG-MEWS-003 | Digital key hardware requirements | Digital Key |
| KG-MEWS-004 | Apple Wallet integration | Digital Key |
| KG-MEWS-005 | Flexible pricing models | Hourly Booking |
| KG-MEWS-006 | ML revenue management | Atomize RMS |
| KG-MEWS-007 | Booking engine conversion | Direct Booking |
| KG-MEWS-008 | Pre-arrival data collection | Guest Data Capture |
| KG-MEWS-009 | Front desk optimization | Front Desk (skip) |
| KG-MEWS-010 | Overbooking strategies | Overbooking (skip) |
| KG-MEWS-011 | Staff scheduling | Shift Planning (skip) |
| KG-MEWS-012 | Hotel financial metrics | GOPPAR |
| KG-MEWS-013 | Loyalty program design | Loyalty Tiers |
| KG-MEWS-014 | Package pricing | Bundle Deals |

---

## ✅ Recommendation

**Mews provides HOTEL-GRADE depth** in areas where Guesty and Host OS are lighter:

| Area | Value for STR | Priority |
|------|---------------|----------|
| Digital Key (Apple Wallet) | HIGH | P1 |
| No-App Guest Messaging | HIGH | P0 |
| Booking Engine A/B Testing | HIGH | P1 |
| Housekeeping Performance | MEDIUM | P2 |
| GOPPAR Analytics | MEDIUM | P2 |
| Kiosk Check-In | LOW (premium) | P3 |
| Hourly Bookings | LOW (niche) | P3 |

**Bottom Line**: Mews fills gaps in **conversion optimization**, **digital key UX**, and **financial analytics** that neither Guesty nor Host OS fully address.

