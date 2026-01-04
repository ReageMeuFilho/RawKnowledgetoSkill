# Master Skill Registry: STR PMS

> **Single Source of Truth** for all skills across competitors
> **Last Updated**: January 2026
> **Competitors Analyzed**: 1 (Guesty)
> **Total Skills**: 67

---

## 📊 Registry Statistics

| Metric | Count |
|--------|-------|
| Total Skills | 67 |
| MVP Skills (P0) | 24 |
| Phase 1 Skills (P1) | 22 |
| Phase 2 Skills (P2) | 15 |
| Phase 3 Skills (P3) | 6 |
| Unique Skills (1 competitor) | 67 |
| Universal Skills (all competitors) | TBD |

---

## 🏷️ Skill Categories

| Category | Skills | Description |
|----------|--------|-------------|
| `communication` | 10 | Guest messaging, inquiries, reviews |
| `booking` | 8 | Reservations, calendar, availability |
| `pricing` | 6 | Rates, revenue management, discounts |
| `operations` | 10 | Cleaning, maintenance, vendors |
| `financial` | 12 | Payments, payouts, accounting |
| `compliance` | 4 | Taxes, ID verification, regulations |
| `channel` | 6 | OTA integrations, calendar sync |
| `owner` | 4 | Statements, reporting, communication |
| `analytics` | 4 | Performance, forecasting, insights |
| `cross-cutting` | 3 | Notifications, permissions, audit |

---

## 📋 Registry Entries

<!-- COMMUNICATION SKILLS -->

### SKILL-001: unified-inbox-management

**Category**: communication
**Priority**: P0
**Status**: NEEDED

**Description**: 
Aggregate and manage guest messages across all OTA channels (Airbnb, Booking.com, Vrbo, email, SMS) into a single interface.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Unified Inbox | ⭐⭐⭐⭐⭐ | Best-in-class, real-time aggregation |
| Hostaway | | | | |
| Hospitable | | | | |
| Lodgify | | | | |

**Best Implementation**: Guesty
**Why Best**: Real-time sync, thread management, search

**Capabilities**:
- [x] Aggregate from Airbnb, Booking.com, Vrbo
- [x] Email and SMS integration
- [x] Search and filter messages
- [x] Read/unread tracking
- [x] Thread management
- [ ] AI-suggested responses

**Knowledge Sources**:
- Primary: KG-001 (Guest Message Response Patterns)

**Related Skills**: SKILL-002, SKILL-003

---

### SKILL-002: message-triage-routing

**Category**: communication
**Priority**: P0
**Status**: NEEDED

**Description**: 
Categorize inbound messages (question, issue, complaint, positive, checkout, booking change) and route to appropriate handler.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | AI Suite | ⭐⭐⭐⭐ | Sentiment + category detection |

**Capabilities**:
- [x] Message categorization
- [x] Urgency detection
- [x] Priority flagging
- [ ] Auto-routing to team members

**Knowledge Sources**:
- Primary: KG-001 (Guest Message Response Patterns)

---

### SKILL-003: ai-response-suggestion

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Generate contextually appropriate guest responses based on message content, property info, and host communication style.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guesty AI Suite™ | ⭐⭐⭐⭐ | GPT-powered, tone-matching |

**Capabilities**:
- [x] Context-aware response generation
- [x] Tone matching (professional/friendly/casual)
- [x] One-click approval
- [x] Learning from host feedback

**Knowledge Sources**:
- Primary: KG-001 (Guest Message Response Patterns)

---

### SKILL-004: message-translation

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Detect guest language and translate messages bidirectionally for multi-language communication.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | AI Translation | ⭐⭐⭐⭐ | Google Translate integration |

**Capabilities**:
- [x] Language detection
- [x] Inbound translation
- [x] Outbound translation
- [ ] Translation memory

---

### SKILL-005: sentiment-analysis

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Analyze guest sentiment and flag negative/urgent messages for priority response.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | AI Suite | ⭐⭐⭐ | Basic sentiment (positive/neutral/negative) |

**Capabilities**:
- [x] Sentiment scoring
- [x] Urgency flagging
- [x] Priority queue
- [ ] Trend analysis

---

### SKILL-006: automated-messaging

**Category**: communication
**Priority**: P0
**Status**: NEEDED

**Description**: 
Send automated messages on triggers (pre-arrival, check-in, checkout, review request).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Automation Tools | ⭐⭐⭐⭐⭐ | Flexible triggers, templates |

**Capabilities**:
- [x] Pre-arrival sequence
- [x] Check-in instructions
- [x] Post-checkout follow-up
- [x] Review requests
- [x] Template variables

**Knowledge Sources**:
- Primary: KG-008 (Pre-Arrival Guest Communication)

---

<!-- BOOKING/CALENDAR SKILLS -->

### SKILL-007: calendar-sync-management

**Category**: booking
**Priority**: P0
**Status**: NEEDED

**Description**: 
Maintain unified calendar across all OTA channels with real-time sync.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Multi-Calendar | ⭐⭐⭐⭐⭐ | Real-time, multi-property |

**Capabilities**:
- [x] Airbnb sync
- [x] Booking.com sync
- [x] Vrbo sync
- [x] iCal import/export
- [x] Real-time updates

**Knowledge Sources**:
- Primary: KG-005 (OTA Channel Sync Edge Cases)

---

### SKILL-008: double-booking-prevention

**Category**: booking
**Priority**: P0
**Status**: NEEDED

**Description**: 
Detect and prevent calendar conflicts in real-time across all channels.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Conflict Detection | ⭐⭐⭐⭐⭐ | Real-time blocking |

**Capabilities**:
- [x] Conflict detection
- [x] Auto-blocking
- [x] Conflict resolution
- [x] Alert notifications

---

### SKILL-009: date-blocking

**Category**: booking
**Priority**: P0
**Status**: NEEDED

**Description**: 
Block dates for owner stays, maintenance windows, and cleaning buffers.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Calendar Blocking | ⭐⭐⭐⭐ | Multiple block types |

**Capabilities**:
- [x] Owner stay blocks
- [x] Maintenance windows
- [x] Cleaning buffers
- [x] Custom block reasons

---

### SKILL-010: direct-reservation-creation

**Category**: booking
**Priority**: P0
**Status**: NEEDED

**Description**: 
Create manual bookings outside OTA channels (phone, email, repeat guests).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Direct Reservations | ⭐⭐⭐⭐ | Full integration with system |

**Capabilities**:
- [x] Manual entry
- [x] Payment collection
- [x] Source tracking
- [x] Full automation integration

---

<!-- PRICING SKILLS -->

### SKILL-011: dynamic-pricing

**Category**: pricing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Optimize nightly rates based on demand signals, seasonality, and market data.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | PriceOptimizer™ | ⭐⭐⭐⭐ | AI-powered, multi-factor |

**Capabilities**:
- [x] Demand-based pricing
- [x] Seasonal adjustments
- [x] Day-of-week modifiers
- [x] Lead time pricing
- [x] Min/max constraints

**Knowledge Sources**:
- Primary: KG-002 (Dynamic Pricing Logic)

---

### SKILL-012: competitor-price-monitoring

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Track competitor rates in the market for pricing intelligence.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Competitor Benchmarking | ⭐⭐⭐ | AirDNA integration |

**Knowledge Sources**:
- Primary: KG-016 (Competitor Rate Monitoring)

---

### SKILL-013: seasonal-pricing-rules

**Category**: pricing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Apply seasonal rate modifiers (high season, low season, holidays).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Rate Cards | ⭐⭐⭐⭐ | Flexible rules engine |

**Knowledge Sources**:
- Primary: KG-002 (Dynamic Pricing Logic)

---

### SKILL-014: event-based-pricing

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Adjust prices for local events (festivals, sports, concerts).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Event Pricing | ⭐⭐⭐ | Manual event entry |

**Knowledge Sources**:
- Primary: KG-002 (Dynamic Pricing Logic)

---

### SKILL-015: occupancy-based-pricing

**Category**: pricing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Adjust rates based on current and forecasted occupancy levels.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Occupancy Rules | ⭐⭐⭐⭐ | Auto-adjustment |

---

### SKILL-016: los-discount-management

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Manage length-of-stay discounts (weekly, monthly rates).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | LOS Discounts | ⭐⭐⭐⭐ | Percentage or fixed |

---

<!-- OPERATIONS SKILLS -->

### SKILL-017: task-auto-generation

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Automatically create cleaning/maintenance tasks from reservation events.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Task Management | ⭐⭐⭐⭐⭐ | Event-driven, templates |

**Capabilities**:
- [x] Post-checkout cleaning
- [x] Pre-arrival inspection
- [x] Linen change
- [x] Deep clean scheduling
- [x] Custom templates

**Knowledge Sources**:
- Primary: KG-003 (Cleaning Task Workflow)

---

### SKILL-018: task-assignment

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Assign tasks to staff/vendors with notifications and tracking.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Task Assignment | ⭐⭐⭐⭐ | Staff management |

**Knowledge Sources**:
- Primary: KG-003 (Cleaning Task Workflow)

---

### SKILL-019: task-progress-tracking

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Track task completion with photo verification and checklists.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Task Tracking | ⭐⭐⭐⭐ | Photo required, checklists |

**Knowledge Sources**:
- Primary: KG-003 (Cleaning Task Workflow)

---

### SKILL-020: task-escalation

**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Escalate overdue or failed tasks to manager.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | SLA Escalation | ⭐⭐⭐ | Timer-based |

---

### SKILL-021: maintenance-request-handling

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Handle guest-reported maintenance issues with vendor coordination.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Maintenance Tasks | ⭐⭐⭐ | Basic workflow |

**Knowledge Sources**:
- Primary: KG-009 (Maintenance Request Handling)

---

### SKILL-022: smart-lock-integration

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Manage smart lock access codes with automatic generation and delivery.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | LocksManager™ | ⭐⭐⭐⭐⭐ | Multi-lock support |

**Capabilities**:
- [x] August support
- [x] Level Lock support
- [x] Nuki support
- [x] Yale support
- [x] Auto-generation
- [x] Auto-delivery
- [x] Auto-revocation

**Knowledge Sources**:
- Primary: KG-007 (Smart Lock Integration)

---

### SKILL-023: access-code-management

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Generate, deliver, and revoke unique access codes per reservation.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Access Codes | ⭐⭐⭐⭐⭐ | Full lifecycle management |

**Knowledge Sources**:
- Primary: KG-007 (Smart Lock Integration)

---

<!-- CHANNEL SKILLS -->

### SKILL-024: channel-connection

**Category**: channel
**Priority**: P0
**Status**: NEEDED

**Description**: 
Connect and authenticate OTA accounts (Airbnb, Booking.com, Vrbo).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Channel Manager | ⭐⭐⭐⭐⭐ | 60+ channels |

**Knowledge Sources**:
- Primary: KG-005 (OTA Channel Sync Edge Cases)

---

### SKILL-025: listing-content-sync

**Category**: channel
**Priority**: P0
**Status**: NEEDED

**Description**: 
Sync listing title, description, photos, and amenities to all channels.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Content Sync | ⭐⭐⭐⭐ | Bidirectional |

---

### SKILL-026: rate-distribution

**Category**: channel
**Priority**: P0
**Status**: NEEDED

**Description**: 
Distribute rates across all connected channels with real-time updates.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Rate Distribution | ⭐⭐⭐⭐⭐ | <5 min sync |

---

### SKILL-027: sync-status-monitoring

**Category**: channel
**Priority**: P0
**Status**: NEEDED

**Description**: 
Track sync status and alert on failures with retry logic.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Sync Monitoring | ⭐⭐⭐⭐ | Error handling |

---

<!-- FINANCIAL SKILLS -->

### SKILL-028: payment-collection

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Collect and process guest payments via card and bank transfer.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guesty Pay™ | ⭐⭐⭐⭐⭐ | PCI compliant, multi-method |

**Capabilities**:
- [x] Credit/debit cards
- [x] Bank transfers
- [x] PayPal
- [x] Split payments
- [x] Auto-retry

---

### SKILL-029: refund-processing

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Process partial or full refunds with reason tracking.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Refunds | ⭐⭐⭐⭐ | Partial support |

---

### SKILL-030: security-deposit-handling

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Hold and release security deposits with damage claim integration.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Deposits | ⭐⭐⭐⭐ | Escrow management |

---

### SKILL-031: payment-reconciliation

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Match payments to bank deposits with discrepancy detection.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Reconciliation | ⭐⭐⭐⭐ | Auto-matching |

**Knowledge Sources**:
- Primary: KG-004 (Owner Statement Format)

---

### SKILL-032: owner-ledger-management

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Track owner account balances with revenue and deductions.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Trust Accounting | ⭐⭐⭐⭐⭐ | Full ledger |

**Knowledge Sources**:
- Primary: KG-004 (Owner Statement Format)

---

### SKILL-033: escrow-management

**Category**: financial
**Priority**: P1
**Status**: NEEDED

**Description**: 
Hold funds in escrow for deposits and dispute resolution.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Escrow | ⭐⭐⭐⭐ | Auto-release |

---

### SKILL-034: tax-collection-tracking

**Category**: compliance
**Priority**: P0
**Status**: NEEDED

**Description**: 
Collect and track guest taxes by jurisdiction.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Tax Handling | ⭐⭐⭐⭐ | Multi-jurisdiction |

**Knowledge Sources**:
- Primary: KG-011 (Tax Collection & Remittance)

---

### SKILL-035: payout-processing

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Process scheduled or on-demand payouts to property owners.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Payouts | ⭐⭐⭐⭐⭐ | Multi-currency |

---

### SKILL-036: owner-statement-generation

**Category**: owner
**Priority**: P0
**Status**: NEEDED

**Description**: 
Generate monthly owner statements with revenue breakdown.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Owner Statements | ⭐⭐⭐⭐⭐ | Detailed breakdown |

**Knowledge Sources**:
- Primary: KG-004 (Owner Statement Format)

---

<!-- COMPLIANCE SKILLS -->

### SKILL-037: guest-verification

**Category**: compliance
**Priority**: P1
**Status**: NEEDED

**Description**: 
Verify guest identity before check-in with ID and face verification.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guesty Verify | ⭐⭐⭐⭐ | Third-party integration |

**Knowledge Sources**:
- Primary: KG-006 (Guest Verification Process)

---

### SKILL-038: risk-scoring

**Category**: compliance
**Priority**: P1
**Status**: NEEDED

**Description**: 
Calculate risk score for bookings based on multiple factors.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Risk Scoring | ⭐⭐⭐ | 0-100 scale |

**Knowledge Sources**:
- Primary: KG-006 (Guest Verification Process)

---

### SKILL-039: damage-claim-processing

**Category**: compliance
**Priority**: P1
**Status**: NEEDED

**Description**: 
Handle damage claims with documentation and approval workflow.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Damage Protection | ⭐⭐⭐⭐ | Claims portal |

**Knowledge Sources**:
- Primary: KG-012 (Damage Claim Processing)

---

<!-- OWNER SKILLS -->

### SKILL-040: owner-portal-access

**Category**: owner
**Priority**: P1
**Status**: NEEDED

**Description**: 
Provide owners view-only access to reservations and financials.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Owners Portal | ⭐⭐⭐⭐ | Dedicated portal |

---

### SKILL-041: owner-stay-management

**Category**: owner
**Priority**: P1
**Status**: NEEDED

**Description**: 
Allow owners to block dates for personal use.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Owner Stays | ⭐⭐⭐⭐ | Calendar integration |

---

<!-- ANALYTICS SKILLS -->

### SKILL-042: analytics-dashboard

**Category**: analytics
**Priority**: P0
**Status**: NEEDED

**Description**: 
Display KPIs and performance metrics (occupancy, ADR, RevPAR).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Analytics | ⭐⭐⭐⭐⭐ | Comprehensive dashboards |

---

### SKILL-043: report-generation

**Category**: analytics
**Priority**: P1
**Status**: NEEDED

**Description**: 
Generate exportable reports (revenue, occupancy, tax).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Reports | ⭐⭐⭐⭐ | PDF/CSV export |

---

### SKILL-044: performance-forecasting

**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
Forecast revenue and occupancy based on booking pipeline.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Forecasting | ⭐⭐⭐ | Basic forecasting |

---

### SKILL-045: benchmarking

**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
Compare performance vs. previous periods and market.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Benchmarking | ⭐⭐⭐ | Period comparison |

---

<!-- GUEST MANAGEMENT SKILLS -->

### SKILL-046: guest-profile-management

**Category**: communication
**Priority**: P0
**Status**: NEEDED

**Description**: 
Maintain unified guest profiles across all channels.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guesty CRM | ⭐⭐⭐⭐⭐ | Cross-channel merge |

---

### SKILL-047: guest-segmentation

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Categorize guests by value, frequency, and preferences.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guest Segments | ⭐⭐⭐⭐ | Auto-tagging |

**Knowledge Sources**:
- Primary: KG-015 (Guest Segmentation Strategies)

---

### SKILL-048: duplicate-profile-merging

**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
Identify and merge duplicate guest records across channels.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Profile Merge | ⭐⭐⭐ | Fuzzy matching |

---

<!-- GUEST APP SKILLS -->

### SKILL-049: guest-app-management

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Manage white-label guest portal with property information.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guest App | ⭐⭐⭐⭐⭐ | Full customization |

---

### SKILL-050: upsell-management

**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
Present and track upsell offers to guests (late checkout, experiences).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Upsells | ⭐⭐⭐⭐ | Analytics included |

---

### SKILL-051: pre-arrival-questionnaire

**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
Collect guest preferences and needs before arrival.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Questionnaire | ⭐⭐⭐ | Customizable questions |

---

<!-- AUTOMATION SKILLS -->

### SKILL-052: automation-rule-builder

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Create if-then automation rules for workflows.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Automation Tools | ⭐⭐⭐⭐⭐ | Visual builder |

---

### SKILL-053: pricing-automation

**Category**: pricing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Apply pricing rules automatically based on triggers.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Auto-pricing | ⭐⭐⭐⭐⭐ | Nightly calculation |

---

<!-- DIRECT BOOKING SKILLS -->

### SKILL-054: direct-booking-website

**Category**: channel
**Priority**: P1
**Status**: NEEDED

**Description**: 
Manage branded direct booking website.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Guesty Websites | ⭐⭐⭐⭐ | Template-based |

**Knowledge Sources**:
- Primary: KG-014 (Direct Booking Website Optimization)

---

### SKILL-055: website-seo

**Category**: channel
**Priority**: P2
**Status**: NEEDED

**Description**: 
Optimize website for search engines.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | SEO Tools | ⭐⭐⭐ | Basic meta tags |

---

<!-- MULTI-UNIT SKILLS -->

### SKILL-056: multi-unit-management

**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Manage buildings with multiple units and shared amenities.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Multi-Unit | ⭐⭐⭐⭐ | Building hierarchy |

**Knowledge Sources**:
- Primary: KG-013 (Multi-Unit Building Management)

---

<!-- ENTERPRISE SKILLS -->

### SKILL-057: multi-brand-management

**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
Support multiple brands in one account with consolidated reporting.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Enterprise Hub | ⭐⭐⭐⭐⭐ | Full separation |

---

### SKILL-058: regional-access-control

**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
Limit user access by region or property group.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Permissions | ⭐⭐⭐⭐ | Granular control |

---

### SKILL-059: permission-management

**Category**: cross-cutting
**Priority**: P0
**Status**: NEEDED

**Description**: 
Manage user roles and access permissions.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | RBAC | ⭐⭐⭐⭐⭐ | Comprehensive roles |

---

### SKILL-060: audit-logging

**Category**: cross-cutting
**Priority**: P0
**Status**: NEEDED

**Description**: 
Track all user actions for compliance and debugging.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Audit Trail | ⭐⭐⭐⭐ | Immutable logs |

---

### SKILL-061: notification-management

**Category**: cross-cutting
**Priority**: P0
**Status**: NEEDED

**Description**: 
Send push, email, and SMS notifications with preferences.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Notifications | ⭐⭐⭐⭐⭐ | Multi-channel |

---

<!-- API SKILLS -->

### SKILL-062: api-key-management

**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
Manage API access credentials for integrations.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Open API | ⭐⭐⭐⭐⭐ | Full REST API |

---

### SKILL-063: webhook-management

**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
Configure event webhooks for external integrations.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Webhooks | ⭐⭐⭐⭐ | Retry logic |

---

<!-- DATA SKILLS -->

### SKILL-064: data-export

**Category**: analytics
**Priority**: P1
**Status**: NEEDED

**Description**: 
Export data in various formats (CSV, PDF).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Export | ⭐⭐⭐⭐ | Multiple formats |

---

### SKILL-065: bulk-operations

**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Perform batch updates across multiple properties.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Bulk Import | ⭐⭐⭐⭐ | CSV templates |

---

### SKILL-066: search-filter

**Category**: cross-cutting
**Priority**: P0
**Status**: NEEDED

**Description**: 
Search across all data types with advanced filtering.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Search | ⭐⭐⭐⭐⭐ | Full-text search |

---

### SKILL-067: review-request-management

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Request and track guest reviews post-checkout.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ✅ | Review Requests | ⭐⭐⭐⭐ | Automated timing |

**Knowledge Sources**:
- Primary: KG-010 (Review Request Strategy)

---

## 📈 How to Add New Skills

When processing a new competitor PRD:

1. **Extract features** from PRD
2. **Search this registry** for matching skill
3. **If match**: Update competitor coverage
4. **If no match**: Add new entry using template above
5. **Update statistics** at top

### Matching Rules

- Same **primary function** = Same skill
- Different **name** doesn't matter
- Look at **what it does**, not what it's called

---

## 📊 Priority Breakdown

### P0 - MVP (24 skills)
Core functionality for basic STR management

### P1 - Phase 1 (22 skills)
Enhanced features for professional managers

### P2 - Phase 2 (15 skills)
Advanced features for scaling operations

### P3 - Phase 3 (6 skills)
Enterprise and specialized features
