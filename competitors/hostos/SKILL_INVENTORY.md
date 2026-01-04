# Host OS STR PMS - Skill Inventory

> **Source**: `hostos_str_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: STR (Short-Term Rental)
> **Type**: Synthesized Best-of-Breed (Guesty + Cloudbeds + Mews + BoomAI + BestyAI)

---

## 📊 Extraction Summary

| Category | Count | New vs Guesty |
|----------|-------|---------------|
| Skills | 38 | 12 NEW, 26 overlap |
| Tools | 18 | 6 NEW |
| Memory Types | 8 | 2 NEW |
| Integrations | 12 | 4 NEW |

---

## 🆕 NEW Skills (Not in Guesty)

These are **unique capabilities** that Host OS adds beyond Guesty:

### NEW-001: Polymorphic Inventory Management
**Category**: inventory
**Priority**: P0
**Description**: Manage multiple inventory types (accommodation, parking, meeting rooms, event spaces) in one unified system with parent/child dependency rules.

**Unique Capabilities**:
- Parent/Child unit dependency (Villa = Suite A + Suite B)
- Booking parent blocks all children
- Booking child blocks parent but not siblings
- Multi-unit clustering for identical units

**Knowledge Required**:
- KG-NEW-001: How do hotels/resorts manage split inventory?

---

### NEW-002: Gap Night Revenue Optimization
**Category**: pricing
**Priority**: P1
**Description**: Automatically detect "orphan" 1-2 night gaps in calendar and message adjacent guests with extension offers.

**Unique Capabilities**:
- Detect orphan nights between bookings
- Auto-message adjacent guests with discounts
- Track acceptance rate

**Knowledge Required**:
- KG-NEW-002: What discount percentages work for gap night offers?

---

### NEW-003: Attribute-Based Room Upgrade Upselling
**Category**: pricing
**Priority**: P1
**Description**: Proactively offer room upgrades 72h pre-arrival based on vacant inventory of superior rooms.

**Unique Capabilities**:
- Detect vacant superior rooms
- Calculate optimal upgrade price
- Auto-send upgrade offers
- Track conversion

**Knowledge Required**:
- KG-NEW-003: What's the optimal timing and pricing for upgrade offers?

---

### NEW-004: Auto-Review Posting (Airbnb Review Blind)
**Category**: communication
**Priority**: P1
**Description**: Automatically post 5-star review for guest immediately to trigger Airbnb's "review blind" mechanism.

**Unique Capabilities**:
- Randomized review template generation
- Automatic posting timing
- Review blind trigger optimization

**Knowledge Required**:
- KG-NEW-004: Airbnb review blind mechanics and best templates

---

### NEW-005: Bad Review Defense Drafting
**Category**: communication
**Priority**: P2
**Description**: AI drafts professional, factual rebuttals for reviews < 4 stars for manager approval.

**Unique Capabilities**:
- Sentiment-aware rebuttal drafting
- Fact-based response generation
- Manager approval workflow

**Knowledge Required**:
- KG-NEW-005: Best practices for responding to negative reviews

---

### NEW-006: No-Login Housekeeping App (Magic Link)
**Category**: operations
**Priority**: P0
**Description**: Cleaners access task app via SMS magic link without username/password, with GPS geofencing.

**Unique Capabilities**:
- Magic link authentication (no login)
- GPS geofence validation for clock-in
- Photo gate (cannot mark ready without photos)
- Automatic payment calculation on clock-out

**Knowledge Required**:
- KG-003 (Cleaning Task Workflow) - ENHANCED

---

### NEW-007: Emergency Guest Relocation Protocol
**Category**: operations
**Priority**: P1
**Description**: Automatic protocol when critical maintenance issue detected with incoming guest.

**Unique Capabilities**:
- Critical issue detection
- Guest arrival check
- Alternative unit assignment
- Automated guest communication
- Compensation calculation

**Knowledge Required**:
- KG-NEW-006: How do PMs handle emergency relocations?

---

### NEW-008: Guest Folio (Hotel-Style Tab)
**Category**: financial
**Priority**: P1
**Description**: Add charges to reservation after initial booking (minibar, room service, damage fees).

**Unique Capabilities**:
- Post-booking charge addition
- Card-on-file tokenization
- Pre-authorization holds
- Auto-release timing

**Knowledge Required**:
- KG-NEW-007: Hotel folio management best practices

---

### NEW-009: Multi-Stakeholder Auto-Split Payments
**Category**: financial
**Priority**: P0
**Description**: Automatically split each payment into Tax, Vendor, Manager, and Owner portions.

**Unique Capabilities**:
- Real-time split calculation
- Segregated liability accounts
- Auto-routing to recipient wallets
- Audit trail per split

**Knowledge Required**:
- KG-004 (Owner Statement Format) - ENHANCED

---

### NEW-010: Police Reporting API (EU/Asia Compliance)
**Category**: compliance
**Priority**: P1
**Description**: Auto-generate and submit guest registration reports to local authorities (e.g., Schede Alloggiati in Italy).

**Unique Capabilities**:
- Country-specific report generation
- API submission to authorities
- Compliance tracking
- Record retention

**Knowledge Required**:
- KG-NEW-008: Country-specific guest registration requirements

---

### NEW-011: Party Prevention Grid
**Category**: compliance
**Priority**: P1
**Description**: Noise monitoring with automated escalation sequence (SMS → Voice Call → Security Dispatch).

**Unique Capabilities**:
- NoiseAware/Minut integration
- WiFi device counting (crowd detection)
- Multi-step escalation sequence
- Security dispatch integration

**Knowledge Required**:
- KG-NEW-009: Party prevention best practices and thresholds

---

### NEW-012: Knowledge Graph RAG for Guest Queries
**Category**: communication
**Priority**: P1
**Description**: Answer guest questions using property-specific knowledge base (house manuals, local guides).

**Unique Capabilities**:
- Property-specific document retrieval
- Context-aware answers with photos
- Multi-document synthesis
- Source citation

**Knowledge Required**:
- KG-001 (Guest Message Response) - ENHANCED

---

## 🔄 Skills Overlapping with Guesty

These skills exist in both systems - Host OS provides enhanced versions:

| Host OS Feature | Guesty Equivalent | Enhancement |
|-----------------|-------------------|-------------|
| Unified Inbox | Unified Inbox | + WhatsApp native, RAG answers |
| Intent Recognition | AI Suite | + More categories (Complaint, Review) |
| Sentiment Guardrails | Sentiment Analysis | + Hard stop threshold |
| Channel Manager | Channel Manager | + Google Hotels, < 30s sync |
| Rate Distribution | Rate Distribution | + Derived rates |
| Task Auto-Generation | Task Management | + GPS, Photo gate |
| Trust Accounting | Trust Accounting | + Multi-stakeholder splits |
| Guest Verification | Guesty Verify | + Police reporting |
| Smart Lock Integration | LocksManager | + Seam/Igloohome |
| Direct Booking Website | Guesty Websites | + SEO engine |
| Dynamic Pricing | PriceOptimizer | + Gap night logic |
| Review Request | Automation | + Auto-posting |

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-NEW-001 | detect_gap_nights | Find orphan nights in calendar | BUILD |
| TOOL-NEW-002 | calculate_upgrade_price | Determine optimal upgrade offer | BUILD |
| TOOL-NEW-003 | post_airbnb_review | Post review via Airbnb API | BUILD |
| TOOL-NEW-004 | submit_police_report | Submit guest data to authorities | BUILD |
| TOOL-NEW-005 | monitor_noise_level | Get readings from noise sensors | BUY (Minut API) |
| TOOL-NEW-006 | count_wifi_devices | Crowd detection via WiFi | BUY (Minut API) |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-NEW-001 | Folio Transactions | Post-booking charges per guest | 7 years |
| MEM-NEW-002 | Police Report Log | Submitted guest registrations | Forever (legal) |

---

## 🔌 NEW Integrations Required

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-NEW-001 | Google Hotels | OTA distribution | API |
| INT-NEW-002 | Minut | Noise monitoring | API |
| INT-NEW-003 | NoiseAware | Noise monitoring | API |
| INT-NEW-004 | Seam | Smart lock (universal) | API |
| INT-NEW-005 | Igloohome | Smart lock | API |
| INT-NEW-006 | Channex | OTA middleware | API |
| INT-NEW-007 | Rentals United | OTA middleware | API |
| INT-NEW-008 | Police Authority APIs | Guest registration | API |

---

## 📊 Comparison: Host OS vs Guesty

| Dimension | Guesty | Host OS | Winner |
|-----------|--------|---------|--------|
| **Inventory Model** | Flat | Polymorphic (Parent/Child) | Host OS |
| **AI Automation** | Suggestions | Autonomous Agents | Host OS |
| **Channel Sync Speed** | < 5 min | < 30 sec | Host OS |
| **Revenue Optimization** | Basic | Gap Night + Upgrades | Host OS |
| **Operations App** | Login required | Magic Link + GPS | Host OS |
| **Financial Model** | Trust Accounting | Trust + Folio + Splits | Host OS |
| **Compliance** | ID Verification | ID + Police Reporting | Host OS |
| **Party Prevention** | None | Full Grid | Host OS |
| **Documentation Depth** | Comprehensive | Synthesized | Guesty |

---

## 🎯 Knowledge Gaps (NEW)

| ID | Knowledge Needed | Skills Blocked |
|----|------------------|----------------|
| KG-NEW-001 | Split inventory management patterns | NEW-001 |
| KG-NEW-002 | Gap night discount optimization | NEW-002 |
| KG-NEW-003 | Room upgrade offer timing/pricing | NEW-003 |
| KG-NEW-004 | Airbnb review blind mechanics | NEW-004 |
| KG-NEW-005 | Negative review response patterns | NEW-005 |
| KG-NEW-006 | Emergency relocation protocols | NEW-007 |
| KG-NEW-007 | Hotel folio management | NEW-008 |
| KG-NEW-008 | Country guest registration requirements | NEW-010 |
| KG-NEW-009 | Party prevention thresholds | NEW-011 |

---

## ✅ Recommendation

**Host OS represents the "Target State"** for our STR vertical. It takes everything Guesty does and adds:

1. **More autonomous AI** (agents vs. suggestions)
2. **Better financial controls** (splits, folios)
3. **Stronger compliance** (police reporting)
4. **Enhanced operations** (magic link, GPS, photo gates)
5. **Revenue optimization** (gap nights, upgrades)
6. **Asset protection** (noise monitoring)

**Action**: Use Host OS as the PRIMARY PRD and Guesty as supplementary detail.

