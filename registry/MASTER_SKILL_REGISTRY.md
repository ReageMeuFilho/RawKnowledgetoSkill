# Master Skill Registry: STR/LTR PMS + Maintenance + Housing Ops

> **Single Source of Truth** for all skills across competitors
> **Last Updated**: January 2026
> **Competitors Analyzed**: 14 (Guesty, Host OS, Mews, Besty AI, Boom AI, Inntelo AI, Visito AI, Cloudbeds, RentalReady, PriceLabs, Vendoroo, EliseAI, **Hostaway**)
> **Total Skills**: 186
> **BENCHMARKS**: EliseAI (LTR leader), Guesty & Hostaway (STR enterprise leaders)

---

## 📊 Registry Statistics

| Metric | Count |
|--------|-------|
| Total Skills | 186 |
| MVP Skills (P0) | 60 |
| Phase 1 Skills (P1) | 83 |
| Phase 2 Skills (P2) | 35 |
| Phase 3 Skills (P3) | 8 |
| Universal Skills (all 14) | 26 |
| Unique Skills (Guesty only) | 41 |
| Unique Skills (Host OS only) | 12 |
| Unique Skills (Mews only) | 15 |
| Unique Skills (Besty only) | 11 |
| Unique Skills (Boom only) | 7 |
| Unique Skills (Inntelo only) | 9 |
| Unique Skills (Visito only) | 8 |
| Unique Skills (Cloudbeds only) | 6 |
| Unique Skills (RentalReady only) | 9 |
| Unique Skills (PriceLabs only) | 12 |
| Unique Skills (Vendoroo only) | 11 |
| Unique Skills (EliseAI only) | 10 |
| Unique Skills (Hostaway only) | 9 |

---

## 🏷️ Skill Categories

| Category | Skills | Description |
|----------|--------|-------------|
| `communication` | 13 | Guest messaging, inquiries, reviews |
| `booking` | 8 | Reservations, calendar, availability |
| `pricing` | 8 | Rates, revenue management, discounts |
| `operations` | 12 | Cleaning, maintenance, vendors |
| `financial` | 14 | Payments, payouts, accounting |
| `compliance` | 6 | Taxes, ID verification, regulations |
| `channel` | 6 | OTA integrations, calendar sync |
| `owner` | 4 | Statements, reporting, communication |
| `analytics` | 4 | Performance, forecasting, insights |
| `cross-cutting` | 3 | Notifications, permissions, audit |
| `inventory` | 1 | Polymorphic inventory management |
| `hospitality` | 8 | Hotel-grade kiosk, digital key, concierge |
| `revenue` | 4 | Inquiry winback, direct booking, extended stay |
| `ai-control` | 4 | Confidence, co-pilot, brand voice |
| `voice` | 3 | Voice AI, call recording, voicemail |
| `agentic` | 5 | Multi-function agent, predictive outreach, multi-agent |
| `cdp` | 2 | Customer data platform, identity resolution |
| `retention` | 2 | Churn prediction, proactive detection |
| `builder` | 2 | No-code agent builder, templates |
| `retrieval` | 2 | RAG hybrid, knowledge gap detection |
| `ai-foundation` | 3 | Foundation model, time surface, causal AI |
| `distribution` | 2 | 300+ channels, marketplace |
| `ai-routing` | 2 | Confidence scoring, human-in-loop |
| `grouping` | 2 | Property grouping, multi-office |
| `quality` | 2 | Quality audit, review replies |
| `contractor` | 1 | Service provider ecosystem |
| `pricing-algorithm` | 3 | HLP, elasticity, demand forecast |
| `event-detection` | 1 | 4-way redundant detection |
| `price-customization` | 2 | 12 options, stacking logic |
| `pacing` | 1 | YoY trajectory analysis |
| `investment` | 1 | Revenue estimation |
| `integrations-mgmt` | 1 | 161+ PMS sync management |
| `maintenance-agents` | 2 | Specialized maintenance AI agents |
| `maintenance-intelligence` | 3 | Brain, memory, troubleshooting |
| `emergency-handling` | 2 | Classification, after-hours flow |
| `invoice-compliance` | 1 | AI validation, fraud detection |
| `policy-engine` | 1 | Granular rules with simulation |
| `work-orchestration` | 2 | State machine, campaigns |
| `housing-crm` | 1 | Purpose-built CRM hub |
| `leasing` | 1 | Full funnel lead-to-lease |
| `resident-lifecycle` | 2 | Renewals, delinquency |
| `field-service` | 1 | Technician app, routing |
| `compliance` | 1 | Fair housing AI guardrails |
| `ai-collaboration` | 2 | Human handoff, status updates |
| `training-data` | 1 | Conversation training moat |
| `enterprise-ops` | 1 | Centralized multi-portfolio |
| `white-label` | 1 | Reseller, custom branding |
| `trust-accounting` | 1 | Legal fund separation |
| `cleaner-ops` | 1 | Mobile portal, checklists |
| `workflow-builder` | 1 | Visual automation builder |
| `multi-engine` | 1 | Multiple booking sites |
| `rbac` | 1 | Granular permissions |
| `ai-messaging` | 1 | Suggestions, sentiment |
| `scale` | 1 | 1000+ property proven |

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

<!-- HOST OS UNIQUE SKILLS (068-079) -->

### SKILL-068: polymorphic-inventory-management

**Category**: inventory
**Priority**: P0
**Status**: NEEDED

**Description**: 
Manage multiple inventory types (accommodation, parking, meeting rooms, event spaces) with parent/child dependency rules where booking a parent blocks children and vice versa.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Flat inventory only |
| Host OS | ✅ | Polymorphic Inventory | ⭐⭐⭐⭐⭐ | Full hierarchy |

**Best Implementation**: Host OS (Derived from Cloudbeds & Mews)

**Capabilities**:
- [x] Multiple inventory types (Accommodation, Parking, Meeting, Event)
- [x] Parent/Child unit dependency
- [x] Booking parent blocks all children
- [x] Booking child blocks parent
- [x] Multi-unit clustering

**Knowledge Sources**:
- Primary: KG-NEW-001 (Split Inventory Management Patterns)

---

### SKILL-069: gap-night-revenue-optimization

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Automatically detect "orphan" 1-2 night gaps between bookings and message adjacent guests with extension offers at discounted rates.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No gap detection |
| Host OS | ✅ | Gap Night Logic | ⭐⭐⭐⭐⭐ | BestyAI derived |

**Best Implementation**: Host OS (Derived from BestyAI)

**Capabilities**:
- [x] Orphan night detection
- [x] Adjacent guest messaging
- [x] Discount calculation
- [x] Acceptance tracking

**Knowledge Sources**:
- Primary: KG-NEW-002 (Gap Night Discount Optimization)

---

### SKILL-070: attribute-based-room-upgrade

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Proactively offer room upgrades 72h pre-arrival based on vacant superior room inventory.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Upsells | ⭐⭐⭐ | Generic upsells only |
| Host OS | ✅ | Attribute-Based Upselling | ⭐⭐⭐⭐⭐ | Vacancy-aware |

**Best Implementation**: Host OS

**Capabilities**:
- [x] Vacant superior room detection
- [x] Optimal upgrade price calculation
- [x] Timed offer delivery (72h pre-arrival)
- [x] Conversion tracking

**Knowledge Sources**:
- Primary: KG-NEW-003 (Room Upgrade Timing/Pricing)

---

### SKILL-071: auto-review-posting

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Automatically post 5-star review for guest immediately to trigger Airbnb's "review blind" mechanism.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Request only, no auto-post |
| Host OS | ✅ | Auto-Review Posting | ⭐⭐⭐⭐ | Review blind optimization |

**Best Implementation**: Host OS

**Capabilities**:
- [x] Randomized review template generation
- [x] Automatic posting timing
- [x] Review blind trigger optimization

**Knowledge Sources**:
- Primary: KG-NEW-004 (Airbnb Review Blind Mechanics)

---

### SKILL-072: bad-review-defense-drafting

**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI drafts professional, factual rebuttals for reviews < 4 stars for manager approval.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No rebuttal assistance |
| Host OS | ✅ | Bad Review Defense | ⭐⭐⭐⭐ | AI-drafted |

**Best Implementation**: Host OS

**Capabilities**:
- [x] Sentiment-aware rebuttal drafting
- [x] Fact-based response generation
- [x] Manager approval workflow

**Knowledge Sources**:
- Primary: KG-NEW-005 (Negative Review Response Patterns)

---

### SKILL-073: magic-link-housekeeping-app

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Cleaners access task app via SMS magic link without username/password, with GPS geofencing validation.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Task App | ⭐⭐⭐ | Login required |
| Host OS | ✅ | No-Login App | ⭐⭐⭐⭐⭐ | Magic link + GPS |

**Best Implementation**: Host OS (Derived from Breezeway)

**Capabilities**:
- [x] Magic link authentication (no login)
- [x] GPS geofence validation for clock-in
- [x] Photo gate (cannot mark ready without photos)
- [x] Automatic payment calculation on clock-out

**Knowledge Sources**:
- Primary: KG-003 (Cleaning Task Workflow) - ENHANCED

---

### SKILL-074: emergency-guest-relocation

**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Automatic protocol when critical maintenance issue detected with incoming guest - reassign unit and communicate.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Manual process |
| Host OS | ✅ | Emergency Relocation | ⭐⭐⭐⭐ | Automated protocol |

**Best Implementation**: Host OS

**Capabilities**:
- [x] Critical issue detection
- [x] Guest arrival check
- [x] Alternative unit assignment
- [x] Automated guest communication
- [x] Compensation calculation

**Knowledge Sources**:
- Primary: KG-NEW-006 (Emergency Relocation Protocols)

---

### SKILL-075: guest-folio-management

**Category**: financial
**Priority**: P1
**Status**: NEEDED

**Description**: 
Hotel-style tab allowing charges to be added after initial booking (minibar, room service, damage fees).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No post-booking charges |
| Host OS | ✅ | Guest Folio | ⭐⭐⭐⭐⭐ | Full folio (Mews derived) |

**Best Implementation**: Host OS (Derived from Mews)

**Capabilities**:
- [x] Post-booking charge addition
- [x] Card-on-file tokenization
- [x] Pre-authorization holds ($200)
- [x] Auto-release timing (24h post-checkout)

**Knowledge Sources**:
- Primary: KG-NEW-007 (Hotel Folio Management)

---

### SKILL-076: multi-stakeholder-payment-split

**Category**: financial
**Priority**: P0
**Status**: NEEDED

**Description**: 
Automatically split each payment into Tax, Vendor, Manager, and Owner portions with segregated accounts.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Trust Accounting | ⭐⭐⭐⭐ | Basic splits |
| Host OS | ✅ | Auto-Split Payments | ⭐⭐⭐⭐⭐ | 4-way real-time |

**Best Implementation**: Host OS

**Capabilities**:
- [x] Real-time split calculation
- [x] Segregated liability accounts
- [x] Auto-routing to recipient wallets
- [x] Audit trail per split

**Knowledge Sources**:
- Primary: KG-004 (Owner Statement Format) - ENHANCED

---

### SKILL-077: police-reporting-api

**Category**: compliance
**Priority**: P1
**Status**: NEEDED

**Description**: 
Auto-generate and submit guest registration reports to local authorities (e.g., Schede Alloggiati in Italy, EU requirements).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No police reporting |
| Host OS | ✅ | Police Reporting | ⭐⭐⭐⭐ | CheKin derived |

**Best Implementation**: Host OS (Derived from CheKin)

**Capabilities**:
- [x] Country-specific report generation
- [x] API submission to authorities
- [x] Compliance tracking
- [x] Record retention

**Knowledge Sources**:
- Primary: KG-NEW-008 (Country Guest Registration Requirements)

---

### SKILL-078: party-prevention-grid

**Category**: compliance
**Priority**: P1
**Status**: NEEDED

**Description**: 
Noise monitoring with automated escalation sequence (SMS → Voice Call → Security Dispatch).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No noise monitoring |
| Host OS | ✅ | Party Prevention Grid | ⭐⭐⭐⭐⭐ | Full escalation |

**Best Implementation**: Host OS (Derived from Minut)

**Capabilities**:
- [x] Minut/NoiseAware integration
- [x] WiFi device counting (crowd detection)
- [x] 3-step escalation (SMS → Call → Dispatch)
- [x] Security dispatch integration

**Knowledge Sources**:
- Primary: KG-NEW-009 (Party Prevention Thresholds)

---

### SKILL-079: knowledge-graph-rag-answers

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Answer guest questions using property-specific knowledge base (house manuals, local guides) with RAG retrieval.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | AI Suite | ⭐⭐⭐ | Generic responses |
| Host OS | ✅ | Knowledge Graph RAG | ⭐⭐⭐⭐⭐ | Property-specific |

**Best Implementation**: Host OS (Derived from BoomAI)

**Capabilities**:
- [x] Property-specific document retrieval
- [x] Context-aware answers with photos
- [x] Multi-document synthesis
- [x] Source citation

**Knowledge Sources**:
- Primary: KG-001 (Guest Message Response) - ENHANCED

---

<!-- MEWS UNIQUE SKILLS (080-094) -->

### SKILL-080: self-service-checkin-kiosk

**Category**: hospitality
**Priority**: P1
**Status**: NEEDED

**Description**: 
Tablet-based self-service check-in with payment processing, upselling, and key activation.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No kiosk |
| Host OS | ❌ | - | - | No kiosk |
| Mews | ✅ | Digital Check-In Kiosk | ⭐⭐⭐⭐⭐ | 2.6x upsell conversion |

**Best Implementation**: Mews

**Capabilities**:
- [x] Hardware integration (iPad/Android)
- [x] Card reader for payments
- [x] NFC for Digital Key activation
- [x] Camera for photo capture
- [x] Thermal printer for receipts
- [x] Accessibility features

**Knowledge Sources**:
- Primary: KG-MEWS-001 (Kiosk Hardware)
- Secondary: KG-MEWS-002 (Kiosk Upsell)

---

### SKILL-081: digital-key-apple-wallet

**Category**: hospitality
**Priority**: P1
**Status**: NEEDED

**Description**: 
Contactless room access via smartphone with BLE/NFC and Apple Wallet integration.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | LocksManager | ⭐⭐⭐⭐ | Code-based only |
| Host OS | ⚠️ | Smart Lock | ⭐⭐⭐⭐ | Code-based only |
| Mews | ✅ | Digital Key | ⭐⭐⭐⭐⭐ | Apple Wallet + BLE |

**Best Implementation**: Mews

**Capabilities**:
- [x] App clip (no app store required)
- [x] Apple Wallet integration
- [x] Key sharing between guests
- [x] Auto-revocation at checkout
- [x] Offline BLE operation
- [x] Access audit logging
- [x] Remote lock control

**Knowledge Sources**:
- Primary: KG-MEWS-003 (Digital Key Hardware)
- Secondary: KG-MEWS-004 (Apple Wallet Integration)

---

### SKILL-082: hourly-flexible-booking

**Category**: booking
**Priority**: P1
**Status**: NEEDED

**Description**: 
Price and book spaces by hour, day, week, or month (not just nightly).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Nightly only |
| Host OS | ❌ | - | - | Nightly only |
| Mews | ✅ | Flexible Booking | ⭐⭐⭐⭐⭐ | Hourly to monthly |

**Best Implementation**: Mews

**Capabilities**:
- [x] Hourly rate plans
- [x] Day-use bookings
- [x] Weekly/monthly rates
- [x] Meeting room booking
- [x] Co-working desk booking
- [x] Event space rentals

**Knowledge Sources**:
- Primary: KG-MEWS-005 (Flexible Pricing Models)

---

### SKILL-083: ml-revenue-management

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Machine learning-powered pricing with demand forecasting (Atomize RMS).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | PriceOptimizer | ⭐⭐⭐ | Rules-based |
| Host OS | ⚠️ | Revenue Agent | ⭐⭐⭐⭐ | Gap nights |
| Mews | ✅ | Atomize RMS | ⭐⭐⭐⭐⭐ | Full ML, 20-37% RevPAR |

**Best Implementation**: Mews (Atomize)

**Capabilities**:
- [x] Real-time demand forecasting
- [x] Automated 24/7 rate recommendations
- [x] Competitive intelligence
- [x] 90-day forward forecasting
- [x] Sensitivity analysis
- [x] 20-37% RevPAR improvement

**Knowledge Sources**:
- Primary: KG-MEWS-006 (ML Revenue Management)

---

### SKILL-084: conversion-optimized-booking-engine

**Category**: channel
**Priority**: P0
**Status**: NEEDED

**Description**: 
Direct booking website with A/B testing, smart recommendations, and upsell orchestration.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Guesty Websites | ⭐⭐⭐ | Basic templates |
| Host OS | ⚠️ | Website Builder | ⭐⭐⭐ | SEO focus |
| Mews | ✅ | Booking Engine | ⭐⭐⭐⭐⭐ | A/B testing, conversion |

**Best Implementation**: Mews

**Capabilities**:
- [x] Mobile-first (<2s load on 3G)
- [x] Built-in A/B testing
- [x] Resume booking after 48h
- [x] Social proof notifications
- [x] Dynamic bundling
- [x] Gift card integration

**Knowledge Sources**:
- Primary: KG-MEWS-007 (Booking Conversion)

---

### SKILL-085: no-app-guest-messaging

**Category**: communication
**Priority**: P0
**Status**: NEEDED

**Description**: 
Real-time guest messaging via SMS/email link without app download required.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Guest App | ⭐⭐⭐ | App required |
| Host OS | ⚠️ | Guest App | ⭐⭐⭐ | App required |
| Mews | ✅ | Virtual Concierge | ⭐⭐⭐⭐⭐ | No app, SMS link |

**Best Implementation**: Mews

**Capabilities**:
- [x] SMS link access (no app)
- [x] WebSocket (<2s latency)
- [x] FAQ bot automation
- [x] Bulk room announcements
- [x] In-stay service ordering

**Knowledge Sources**:
- Primary: KG-001 (Guest Message Response) - ENHANCED

---

### SKILL-086: pre-arrival-data-capture

**Category**: compliance
**Priority**: P0
**Status**: NEEDED

**Description**: 
Collect payment info, ID, signatures, and preferences digitally before arrival.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Pre-Check-in | ⭐⭐⭐ | Basic form |
| Host OS | ⚠️ | Pre-Check-in Link | ⭐⭐⭐ | ID + selfie |
| Mews | ✅ | Online Check-In | ⭐⭐⭐⭐⭐ | Full data capture |

**Best Implementation**: Mews

**Capabilities**:
- [x] Digital signature capture
- [x] Passport/ID scan
- [x] Card pre-authorization
- [x] Emergency contact collection
- [x] Group member management
- [x] GDPR compliance

**Knowledge Sources**:
- Primary: KG-MEWS-008 (Pre-Arrival Data)

---

### SKILL-087: front-desk-command-center

**Category**: hospitality
**Priority**: P2
**Status**: NEEDED

**Description**: 
Centralized reception interface with occupancy map, queues, and alerts.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No front desk focus |
| Host OS | ❌ | - | - | No front desk focus |
| Mews | ✅ | Front Office | ⭐⭐⭐⭐⭐ | Hotel-grade |

**Best Implementation**: Mews

**Capabilities**:
- [x] Visual occupancy map
- [x] Arrival/departure queues
- [x] Wait time tracking
- [x] Priority alerts
- [x] 3-5 min check-in vs 10-15
- [x] Offline capability

**Knowledge Sources**:
- Primary: KG-MEWS-009 (Front Desk Workflow)

---

### SKILL-088: overbooking-management

**Category**: booking
**Priority**: P2
**Status**: NEEDED

**Description**: 
Controlled overbooking with waitlist and relocation tools.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No overbooking |
| Host OS | ❌ | - | - | No overbooking |
| Mews | ✅ | Overbooking Mgmt | ⭐⭐⭐⭐ | Full workflow |

**Best Implementation**: Mews

**Capabilities**:
- [x] Overbooking thresholds
- [x] Waitlist functionality
- [x] Cancellation prediction
- [x] Relocation workflow
- [x] Compensation tracking

**Knowledge Sources**:
- Primary: KG-MEWS-010 (Overbooking Strategies)

---

### SKILL-089: staff-shift-planning

**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
Housekeeping shift scheduling with capacity planning.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No shift planning |
| Host OS | ❌ | - | - | No shift planning |
| Mews | ✅ | Shift Planning | ⭐⭐⭐⭐ | Full scheduling |

**Best Implementation**: Mews

**Capabilities**:
- [x] Shift creation/assignment
- [x] Capacity planning
- [x] Shift swapping
- [x] Overtime alerts
- [x] Payroll integration

**Knowledge Sources**:
- Primary: KG-MEWS-011 (Staff Scheduling)

---

### SKILL-090: housekeeping-performance-analytics

**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
Track cleaner performance with metrics and leaderboards.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Task Reports | ⭐⭐ | Basic metrics |
| Host OS | ⚠️ | Task Analytics | ⭐⭐⭐ | Photo verification |
| Mews | ✅ | HK Performance | ⭐⭐⭐⭐⭐ | Full analytics |

**Best Implementation**: Mews

**Capabilities**:
- [x] Rooms per shift per cleaner
- [x] Average turnover time
- [x] Quality scores
- [x] Guest satisfaction correlation
- [x] Leaderboards
- [x] Labor cost per room

**Knowledge Sources**:
- Primary: KG-003 (Cleaning Workflow) - ENHANCED

---

### SKILL-091: goppar-reporting

**Category**: analytics
**Priority**: P1
**Status**: NEEDED

**Description**: 
Gross Operating Profit Per Available Room including costs.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Analytics | ⭐⭐⭐ | Revenue only |
| Host OS | ❌ | - | - | No GOPPAR |
| Mews | ✅ | GOPPAR Reports | ⭐⭐⭐⭐⭐ | True profitability |

**Best Implementation**: Mews

**Capabilities**:
- [x] Revenue minus operational costs
- [x] Property profitability
- [x] Expense breakdown
- [x] Trend analysis
- [x] Benchmark comparison

**Knowledge Sources**:
- Primary: KG-MEWS-012 (Hotel Financial Metrics)

---

### SKILL-092: integration-marketplace

**Category**: channel
**Priority**: P1
**Status**: NEEDED

**Description**: 
1000+ certified integrations with no connection fees.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Marketplace | ⭐⭐⭐ | 200+ integrations |
| Host OS | ❌ | - | - | Limited |
| Mews | ✅ | Marketplace | ⭐⭐⭐⭐⭐ | 1000+ no fees |

**Best Implementation**: Mews

**Capabilities**:
- [x] 1000+ integrations
- [x] No connection fees
- [x] Partner certification
- [x] Native SDKs
- [x] Zapier integration

---

### SKILL-093: loyalty-tier-management

**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
VIP tier management with automatic recognition.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | CRM Segments | ⭐⭐⭐ | Manual tagging |
| Host OS | ❌ | - | - | No loyalty tiers |
| Mews | ✅ | Loyalty Management | ⭐⭐⭐⭐ | Full tier system |

**Best Implementation**: Mews

**Capabilities**:
- [x] Loyalty program integration
- [x] VIP flagging on arrival
- [x] Tier-based service
- [x] Repeat guest recognition
- [x] Lifetime value tracking

**Knowledge Sources**:
- Primary: KG-MEWS-013 (Loyalty Program Design)

---

### SKILL-094: package-deal-bundling

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Bundle rooms with services as packages.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Upsells | ⭐⭐⭐ | Add-ons only |
| Host OS | ⚠️ | Upsells | ⭐⭐⭐ | Add-ons only |
| Mews | ✅ | Package Deals | ⭐⭐⭐⭐⭐ | True bundling |

**Best Implementation**: Mews

**Capabilities**:
- [x] Room + service bundles
- [x] Dynamic bundle pricing
- [x] Occupancy-based bundling
- [x] Package promotions
- [x] Bundle revenue tracking

**Knowledge Sources**:
- Primary: KG-MEWS-014 (Package Pricing)

---

<!-- BESTY AI UNIQUE SKILLS (095-105) -->

### SKILL-095: inquiry-winback-automation

**Category**: revenue
**Priority**: P0
**Status**: NEEDED

**Description**: 
Automatically follow up on abandoned inquiries to recover lost bookings with 3-message sequence.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No winback |
| Host OS | ❌ | - | - | No winback |
| Mews | ❌ | - | - | No winback |
| Besty | ✅ | Inquiry Winback | ⭐⭐⭐⭐⭐ | 8-20% recovery |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Track inquiry dropoff points
- [x] 3-message sequence (24h, 48h, 72h)
- [x] Objection-based messaging
- [x] Progressive escalation
- [x] Stop after 3 (avoid spam)

**Knowledge Sources**:
- Primary: KG-BESTY-001 (Inquiry Objection Patterns)

---

### SKILL-096: direct-booking-conversion

**Category**: revenue
**Priority**: P1
**Status**: NEEDED

**Description**: 
Convert OTA inquiries to direct bookings to save 15% commission.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No conversion |
| Host OS | ❌ | - | - | No conversion |
| Mews | ⚠️ | Booking Engine | ⭐⭐⭐ | For hotels |
| Besty | ✅ | Direct Conversion | ⭐⭐⭐⭐⭐ | OTA → Direct |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Respond on OTA first
- [x] Suggest direct with discount
- [x] Show savings calculation
- [x] WhatsApp pivot
- [x] 5-15% conversion rate

**Knowledge Sources**:
- Primary: KG-BESTY-002 (Direct Booking Tactics)

---

### SKILL-097: confidence-threshold-system

**Category**: ai-control
**Priority**: P0
**Status**: NEEDED

**Description**: 
Route messages to human when AI confidence is below threshold.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | AI Suite | ⭐⭐ | Basic filtering |
| Host OS | ⚠️ | Agent Control | ⭐⭐⭐ | Some control |
| Mews | ❌ | - | - | No AI control |
| Besty | ✅ | Confidence System | ⭐⭐⭐⭐⭐ | Production-ready |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] 0-100% confidence scoring
- [x] Configurable threshold by message type
- [x] Auto-escalation logic
- [x] Learning curve tracking
- [x] Safety categories always escalate

**Knowledge Sources**:
- Primary: KG-BESTY-006 (Confidence Threshold Tuning)

---

### SKILL-098: visual-journey-builder

**Category**: automation
**Priority**: P1
**Status**: NEEDED

**Description**: 
Drag-and-drop builder for multi-step guest communication sequences.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Automation Rules | ⭐⭐⭐ | Basic rules |
| Host OS | ⚠️ | Workflows | ⭐⭐⭐ | Less visual |
| Mews | ⚠️ | Journeys | ⭐⭐⭐⭐ | Hotel-focused |
| Besty | ✅ | Journey Builder | ⭐⭐⭐⭐⭐ | No-code, 30+ templates |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] No coding required
- [x] Branching logic (if/then)
- [x] A/B testing built-in
- [x] 30+ pre-built templates
- [x] Multi-channel delivery

**Knowledge Sources**:
- Primary: KG-BESTY-005 (Journey Timing)

---

### SKILL-099: review-response-by-sentiment

**Category**: communication
**Priority**: P0
**Status**: NEEDED

**Description**: 
Generate contextual review responses matched to sentiment level.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Review Response | ⭐⭐⭐ | Basic |
| Host OS | ⚠️ | Auto-Review | ⭐⭐⭐⭐ | Template-based |
| Mews | ⚠️ | Review Management | ⭐⭐⭐⭐ | Hotel-grade |
| Besty | ✅ | Sentiment Response | ⭐⭐⭐⭐⭐ | 100% rate |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Templates per sentiment (5★ to 1★)
- [x] Reference specific review details
- [x] Maintain brand voice
- [x] Auto-post or queue
- [x] 100% response rate

**Knowledge Sources**:
- Primary: KG-BESTY-004 (Review Response Templates)

---

### SKILL-100: copilot-to-autopilot-progression

**Category**: ai-control
**Priority**: P0
**Status**: NEEDED

**Description**: 
Graduated automation from human-review (Co-Pilot) to full automation (Autopilot).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No progression |
| Host OS | ⚠️ | Agent Control | ⭐⭐⭐ | Some control |
| Mews | ❌ | - | - | No AI control |
| Besty | ✅ | Co-Pilot/Autopilot | ⭐⭐⭐⭐⭐ | Trust-building |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] AI drafts, human reviews
- [x] Feedback trains model
- [x] Progressive trust-building
- [x] Override always available
- [x] Audit trail

---

### SKILL-101: real-time-sentiment-alerts

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Detect negative guest sentiment and alert property manager immediately.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | AI Suite | ⭐⭐ | Limited |
| Host OS | ⚠️ | Sentiment | ⭐⭐⭐ | Basic |
| Mews | ❌ | - | - | No alerts |
| Besty | ✅ | Sentiment Alerts | ⭐⭐⭐⭐⭐ | Real-time |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] 0-100 sentiment scoring
- [x] Emotion detection
- [x] Automatic flag < 40
- [x] Alert to manager
- [x] Tone adaptation

---

### SKILL-102: brand-voice-training

**Category**: ai-control
**Priority**: P1
**Status**: NEEDED

**Description**: 
Train AI to match property's unique communication style.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Templates | ⭐⭐ | Manual |
| Host OS | ❌ | - | - | No training |
| Mews | ⚠️ | Brand Settings | ⭐⭐⭐ | Basic |
| Besty | ✅ | Voice Training | ⭐⭐⭐⭐⭐ | Learning |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Tone setting (formal/casual)
- [x] Example message learning
- [x] Signature greetings
- [x] Phrases to avoid
- [x] Per-property customization

---

### SKILL-103: extended-stay-discount-automation

**Category**: revenue
**Priority**: P1
**Status**: NEEDED

**Description**: 
Proactively offer tiered discounts for 7+ night stays.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Length Discount | ⭐⭐⭐ | Manual setup |
| Host OS | ⚠️ | Long Stay | ⭐⭐⭐ | Basic |
| Mews | ⚠️ | Weekly Rates | ⭐⭐⭐⭐ | Hotel-grade |
| Besty | ✅ | Extended Stay | ⭐⭐⭐⭐⭐ | Proactive offers |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Tiered discounts (7d=10%, 14d=20%, 30d=30%)
- [x] Mid-stay extension offers
- [x] Prospect targeting
- [x] Dynamic pricing integration

---

### SKILL-104: knowledge-base-auto-population

**Category**: ai-control
**Priority**: P1
**Status**: NEEDED

**Description**: 
Auto-populate AI knowledge from PMS property data.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Property Sync | ⭐⭐⭐ | Partial |
| Host OS | ⚠️ | Knowledge Sync | ⭐⭐⭐ | Limited |
| Mews | ⚠️ | Property Data | ⭐⭐⭐⭐ | Hotel-focused |
| Besty | ✅ | Auto-Population | ⭐⭐⭐⭐⭐ | Full PMS sync |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Auto-import from PMS
- [x] Amenities, rules, rates
- [x] House manual upload
- [x] Local guide upload
- [x] Brand voice examples

---

### SKILL-105: conversation-summary-intelligence

**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
Auto-generate summaries of conversation threads with issue identification.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | AI Summary | ⭐⭐⭐ | Basic |
| Host OS | ⚠️ | Thread Summary | ⭐⭐⭐ | Some |
| Mews | ❌ | - | - | No summary |
| Besty | ✅ | Conv Intelligence | ⭐⭐⭐⭐⭐ | Actionable |

**Best Implementation**: Besty AI

**Capabilities**:
- [x] Key points extraction
- [x] Issue identification
- [x] Pattern detection across properties
- [x] Resolution tracking
- [x] Actionable insights

---

<!-- BOOM AI UNIQUE SKILLS (106-112) -->

### SKILL-106: voice-ai-concierge

**Category**: voice
**Priority**: P1
**Status**: NEEDED

**Description**: 
24/7 AI-powered phone answering for guest support and reservations.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No voice AI |
| Host OS | ⚠️ | Voice mention | ⭐⭐⭐ | Concept only |
| Mews | ❌ | - | - | No voice AI |
| Besty | ❌ | - | - | Coming Q1 2026 |
| Boom | ✅ | Voice AI Concierge | ⭐⭐⭐⭐⭐ | Full implementation |

**Best Implementation**: Boom AI (BAM)

**Capabilities**:
- [x] 24/7 call answering
- [x] Natural language understanding
- [x] Make reservations via phone
- [x] Process payments by voice
- [x] 5+ language support
- [x] Sentiment detection
- [x] Human escalation
- [x] Call transcription

**Knowledge Sources**:
- Primary: KG-BOOM-001 (Voice AI Implementation)

---

### SKILL-107: multi-function-agentic-execution

**Category**: agentic
**Priority**: P0
**Status**: NEEDED

**Description**: 
AI agent that handles messaging, reviews, and reporting simultaneously.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Isolated tasks |
| Host OS | ⚠️ | Agentic | ⭐⭐⭐⭐ | Concept aligned |
| Mews | ❌ | - | - | No agentic |
| Besty | ⚠️ | Automation | ⭐⭐⭐ | Sequential |
| Boom | ✅ | BAM | ⭐⭐⭐⭐⭐ | True agentic |

**Best Implementation**: Boom AI (BAM)

**Capabilities**:
- [x] Simultaneous multi-function execution
- [x] Cross-function context awareness
- [x] Pattern learning across operations
- [x] Autonomous decision-making
- [x] Transparent reasoning
- [x] Continuous learning

**Knowledge Sources**:
- Primary: KG-BOOM-002 (Agentic Architecture)

---

### SKILL-108: predictive-guest-outreach

**Category**: agentic
**Priority**: P1
**Status**: NEEDED

**Description**: 
Proactively reach guests with offers based on profile analysis.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Segments | ⭐⭐⭐ | Manual triggers |
| Host OS | ⚠️ | AI Outreach | ⭐⭐⭐⭐ | Some prediction |
| Mews | ⚠️ | Upselling | ⭐⭐⭐⭐ | At kiosk |
| Besty | ⚠️ | Journeys | ⭐⭐⭐⭐ | Time-based |
| Boom | ✅ | Predictive | ⭐⭐⭐⭐⭐ | Profile-based |

**Best Implementation**: Boom AI (BAM)

**Capabilities**:
- [x] Predict guest needs before asking
- [x] Timing optimization
- [x] Content personalization
- [x] Dynamic pricing per segment

---

### SKILL-109: call-recording-transcription

**Category**: voice
**Priority**: P2
**Status**: NEEDED

**Description**: 
Automatic call recording with searchable transcription.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| All Others | ❌ | - | - | No call recording |
| Boom | ✅ | Call Recording | ⭐⭐⭐⭐⭐ | Full implementation |

**Best Implementation**: Boom AI

**Capabilities**:
- [x] Compliance-aware recording
- [x] Real-time transcription
- [x] Searchable history
- [x] Sentiment analysis
- [x] Follow-up task creation

---

### SKILL-110: voicemail-to-sms-email

**Category**: voice
**Priority**: P2
**Status**: NEEDED

**Description**: 
Convert voicemails to text and route to appropriate channel.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| All Others | ❌ | - | - | No voicemail handling |
| Boom | ✅ | Voicemail Conversion | ⭐⭐⭐⭐⭐ | Full implementation |

**Best Implementation**: Boom AI

**Capabilities**:
- [x] Voicemail transcription
- [x] SMS delivery
- [x] Email backup
- [x] Priority routing
- [x] Callback scheduling

---

### SKILL-111: beyond-dynamic-pricing-integration

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Native integration with Beyond for ML-powered dynamic pricing.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | PriceOptimizer | ⭐⭐⭐ | Basic |
| Host OS | ⚠️ | Pricing Agent | ⭐⭐⭐⭐ | Gap focus |
| Mews | ✅ | Atomize RMS | ⭐⭐⭐⭐⭐ | ML pricing |
| Besty | ❌ | - | - | Relies on PMS |
| Boom | ✅ | Beyond | ⭐⭐⭐⭐⭐ | STR-specific |

**Best Implementation**: Boom + Beyond (STR) or Mews + Atomize (Hotels)

**Capabilities**:
- [x] Direct data flow
- [x] <15 min rate sync
- [x] Decade of STR data
- [x] Competitor monitoring
- [x] Seasonal optimization

---

### SKILL-112: causal-ai-understanding

**Category**: agentic
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI that understands cause-and-effect, not just correlations.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| All Others | ❌ | - | - | Correlation only |
| Boom | ✅ | Causal AI | ⭐⭐⭐⭐ | Advanced |

**Best Implementation**: Boom AI

**Capabilities**:
- [x] Understand WHY guests ask
- [x] Predict impact of actions
- [x] Root cause analysis
- [x] Outcome forecasting

---

<!-- INNTELO AI UNIQUE SKILLS (113-121) -->

### SKILL-113: ai-customer-data-platform

**Category**: cdp
**Priority**: P1
**Status**: NEEDED

**Description**: 
Unified first-party guest data foundation with identity resolution and predictive analytics.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Guest Profile | ⭐⭐⭐ | Basic |
| Host OS | ⚠️ | Guest Data | ⭐⭐⭐ | Concept |
| Mews | ⚠️ | Guest Profiles | ⭐⭐⭐⭐ | Good |
| Besty | ❌ | - | - | No CDP |
| Boom | ⚠️ | Unified Guest | ⭐⭐⭐ | Basic |
| Inntelo | ✅ | AI CDP | ⭐⭐⭐⭐⭐ | Full stack |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] Identity resolution (single guest across systems)
- [x] Deduplication and normalization
- [x] Real-time event streaming
- [x] Lifetime value tracking
- [x] Price sensitivity analysis
- [x] GDPR/CCPA compliance built-in

**Knowledge Sources**:
- Primary: KG-INN-001 (CDP Architecture)

---

### SKILL-114: multi-agent-architecture

**Category**: agentic
**Priority**: P0
**Status**: NEEDED

**Description**: 
5 specialized AI agents coordinating on complex tasks.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Single system |
| Host OS | ⚠️ | Agents | ⭐⭐⭐⭐ | Concept |
| Mews | ❌ | - | - | No agents |
| Besty | ❌ | - | - | Single AI |
| Boom | ⚠️ | BAM | ⭐⭐⭐⭐ | Multi-function |
| Inntelo | ✅ | Multi-Agent | ⭐⭐⭐⭐⭐ | 5 specialized |

**Best Implementation**: Inntelo AI

**Agent Types**:
1. Guest Communication Agent
2. Task Execution Agent
3. Operations Planning Agent
4. Revenue Optimization Agent
5. Escalation Agent

**Capabilities**:
- [x] Agent-to-agent communication
- [x] Shared state management
- [x] Clean handoff protocols
- [x] Conflict resolution
- [x] Parallel execution

**Knowledge Sources**:
- Primary: KG-INN-002 (Multi-Agent Coordination)

---

### SKILL-115: cross-department-workflow-orchestration

**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
Guest requests flow seamlessly across departments with coordinated timing.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Task Mgmt | ⭐⭐⭐⭐ | Manual |
| Host OS | ⚠️ | Workflows | ⭐⭐⭐⭐ | Concept |
| Mews | ⚠️ | Operations | ⭐⭐⭐⭐ | Basic |
| Besty | ❌ | - | - | No ops |
| Boom | ⚠️ | Operations | ⭐⭐⭐⭐ | Basic |
| Inntelo | ✅ | Cross-Dept | ⭐⭐⭐⭐⭐ | Full |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] Single notification (all parts complete)
- [x] Coordinated timing (sequential dependencies)
- [x] Shared context across departments
- [x] Real-time priority adjustment

---

### SKILL-116: predictive-housekeeping

**Category**: operations
**Priority**: P1
**Status**: NEEDED

**Description**: 
AI anticipates room needs before requests are made.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Auto Tasks | ⭐⭐⭐ | Trigger-based |
| Mews | ⚠️ | Housekeeping | ⭐⭐⭐⭐ | Good |
| Inntelo | ✅ | Predictive HK | ⭐⭐⭐⭐⭐ | Full AI |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] Anticipate needs from guest profile
- [x] Schedule deep cleans optimally
- [x] Predict linen needs
- [x] Optimize cleaning sequences
- [x] Dynamic re-prioritization

---

### SKILL-117: 40-plus-language-support

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive multilingual support with context-aware translation.

**Competitor Coverage**:
| Competitor | Has | Languages | Quality | Notes |
|------------|-----|-----------|---------|-------|
| Guesty | ⚠️ | 10+ | ⭐⭐⭐ | Basic |
| Boom | ⚠️ | 5+ | ⭐⭐⭐ | Voice focus |
| Besty | ⚠️ | 5+ | ⭐⭐⭐ | Basic |
| Mews | ⚠️ | 10+ | ⭐⭐⭐⭐ | Good |
| Inntelo | ✅ | 40+ | ⭐⭐⭐⭐⭐ | Full |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] 40+ languages native
- [x] Dialect awareness
- [x] Context translation (intent, not words)
- [x] Slang and colloquialism
- [x] Hospitality terminology

---

### SKILL-118: churn-prediction-retention

**Category**: retention
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI identifies at-risk guests and triggers retention interventions.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| All Others | ❌ | - | - | No churn AI |
| Inntelo | ✅ | Churn Pred | ⭐⭐⭐⭐⭐ | Full |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] Churn score per guest
- [x] Retention intervention triggers
- [x] Win-back campaigns
- [x] Loyalty tier conversion
- [x] LTV optimization

---

### SKILL-119: predictive-maintenance-advanced

**Category**: operations
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI predicts equipment failures before guest impact.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Maintenance | ⭐⭐⭐ | Reactive |
| Mews | ⚠️ | Maintenance | ⭐⭐⭐⭐ | Basic |
| Inntelo | ✅ | Predictive | ⭐⭐⭐⭐⭐ | Full AI |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] MTBF tracking
- [x] MTTR analytics
- [x] Predictive failure detection
- [x] Equipment lifecycle analysis
- [x] Warranty tracking

---

### SKILL-120: intent-recognition-system

**Category**: ai-control
**Priority**: P0
**Status**: NEEDED

**Description**: 
50+ hospitality intents with 95% accuracy target.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ⚠️ | Basic NLU | ⭐⭐⭐ | Limited |
| Boom | ⚠️ | BAM NLU | ⭐⭐⭐⭐ | Good |
| Besty | ⚠️ | AI NLU | ⭐⭐⭐⭐ | Good |
| Inntelo | ✅ | Intent System | ⭐⭐⭐⭐⭐ | 95% accuracy |

**Best Implementation**: Inntelo AI

**Capabilities**:
- [x] 50+ hospitality intents
- [x] 95% accuracy target
- [x] Emotion detection
- [x] Ambiguity handling
- [x] Sarcasm detection
- [x] Confidence thresholds

---

### SKILL-121: proactive-issue-detection

**Category**: retention
**Priority**: P2
**Status**: NEEDED

**Description**: 
AI detects issues from patterns and proactively offers help.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| All Others | ❌ | - | - | Reactive only |
| Inntelo | ✅ | Proactive | ⭐⭐⭐⭐⭐ | Pattern-based |

**Best Implementation**: Inntelo AI

**Example**: "We noticed you struggled with WiFi yesterday. Can we help?"

**Capabilities**:
- [x] Pattern detection across interactions
- [x] Proactive outreach for recurring issues
- [x] Pre-emptive problem resolution
- [x] Guest satisfaction protection

---

<!-- VISITO AI UNIQUE SKILLS (122-129) -->

### SKILL-122: no-code-agent-builder

**Category**: builder
**Priority**: P1
**Status**: NEEDED

**Description**: 
Drag-and-drop interface to create AI agents in 2 minutes without coding.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | Code required |
| Boom | ⚠️ | Basic | ⭐⭐ | Limited |
| Besty | ⚠️ | Quick Setup | ⭐⭐⭐⭐ | Good |
| Inntelo | ⚠️ | Config | ⭐⭐⭐ | Limited |
| Visito | ✅ | No-Code Builder | ⭐⭐⭐⭐⭐ | Full |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] 5-step guided wizard
- [x] Pre-built templates (6 types)
- [x] Personality/tone config
- [x] Boundary settings
- [x] One-click launch
- [x] 95%+ no-code usage

---

### SKILL-123: 100-plus-language-support

**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive multilingual support (100+ languages).

**Competitor Coverage**:
| Competitor | Has | Languages | Quality |
|------------|-----|-----------|---------|
| Inntelo | ⚠️ | 40+ | ⭐⭐⭐⭐ |
| Boom | ⚠️ | 5+ | ⭐⭐⭐ |
| Guesty | ⚠️ | 10+ | ⭐⭐⭐ |
| Visito | ✅ | **100+** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] 100+ languages native
- [x] Auto-detection
- [x] Native fluency
- [x] Language-based routing

---

### SKILL-124: knowledge-gap-detection

**Category**: retrieval
**Priority**: P1
**Status**: NEEDED

**Description**: 
AI identifies questions it can't answer and suggests content to add.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| All Others | ❌ | - | - |
| Visito | ✅ | Gap Detection | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] Auto-identify unanswered questions
- [x] Suggestions for missing info
- [x] FAQ recommendations
- [x] Coverage metrics
- [x] Preview before publish

---

### SKILL-125: back-to-bot-handoff

**Category**: escalation
**Priority**: P2
**Status**: NEEDED

**Description**: 
After human resolves, hand conversation back to AI with context.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| All Others | ❌ | - | - |
| Visito | ✅ | Back-to-Bot | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] Human resolves issue
- [x] Hands back to AI
- [x] Full context preserved
- [x] Prevents re-escalation
- [x] System learns from resolution

---

### SKILL-126: pre-chat-survey

**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
Collect customer information before first message.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Mews | ⚠️ | Pre-arrival | ⭐⭐⭐⭐ | Different context |
| Visito | ✅ | Pre-Chat Survey | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] Custom survey fields
- [x] Required vs optional
- [x] Conditional logic
- [x] CRM integration

---

### SKILL-127: widget-analytics

**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
Track web chat widget engagement and conversion.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Mews | ⚠️ | Booking Analytics | ⭐⭐⭐⭐ | Different |
| Visito | ✅ | Widget Analytics | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] Open/close tracking
- [x] Initiation vs abandonment
- [x] Entry point analysis
- [x] Bounce rate
- [x] Conversion tracking

---

### SKILL-128: rag-hybrid-retrieval

**Category**: retrieval
**Priority**: P1
**Status**: NEEDED

**Description**: 
Combine semantic search + keyword matching for best results.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Inntelo | ⚠️ | Semantic | ⭐⭐⭐⭐ | Semantic only |
| Boom | ⚠️ | Basic | ⭐⭐⭐ | Basic |
| Visito | ✅ | RAG Hybrid | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] Semantic search (embeddings)
- [x] BM25 keyword matching
- [x] Hybrid combination
- [x] Source citation
- [x] Hallucination reduction

---

### SKILL-129: tool-calling-custom-actions

**Category**: integrations
**Priority**: P1
**Status**: NEEDED

**Description**: 
AI agent can call external APIs autonomously during conversation.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Inntelo | ⚠️ | Integrations | ⭐⭐⭐⭐ | Pre-built |
| Boom | ⚠️ | Integrations | ⭐⭐⭐⭐ | Pre-built |
| Visito | ✅ | Tool Calling | ⭐⭐⭐⭐⭐ | Custom |

**Best Implementation**: Visito AI

**Capabilities**:
- [x] Define tools (name, params)
- [x] AI decides when to call
- [x] Parameter extraction
- [x] Response parsing
- [x] Error handling

---

<!-- CLOUDBEDS UNIQUE SKILLS (130-135) -->

### SKILL-130: signals-foundation-ai-model

**Category**: ai-foundation
**Priority**: P0
**Status**: NEEDED

**Description**: 
Hospitality-specific foundation AI trained on 13+ years of data from 31,000+ hotels.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality | Notes |
|------------|-----|--------------|---------|-------|
| Guesty | ❌ | - | - | No foundation AI |
| Boom | ⚠️ | BAM | ⭐⭐⭐⭐ | Multi-function |
| Inntelo | ⚠️ | Multi-Agent | ⭐⭐⭐⭐ | Agent-based |
| Cloudbeds | ✅ | Signals | ⭐⭐⭐⭐⭐ | True foundation |

**Best Implementation**: Cloudbeds (Signals)

**Capabilities**:
- [x] 96%+ demand forecasting
- [x] Causal AI (cause-effect)
- [x] 4B data points/hour
- [x] 13+ years training data
- [x] Weekly retraining
- [x] Multi-task learning

**Knowledge Sources**:
- Primary: KG-CB-001 (Foundation AI Architecture)

---

### SKILL-131: time-surface-technology

**Category**: ai-foundation
**Priority**: P1
**Status**: NEEDED

**Description**: 
Proprietary 2D analysis of correlated booking days for higher accuracy.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| All Others | ❌ | - | - |
| Cloudbeds | ✅ | Time Surface | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Cloudbeds

**Capabilities**:
- [x] 2D pattern analysis
- [x] Correlated day detection
- [x] Seasonal pattern recognition
- [x] Higher accuracy than 1D

---

### SKILL-132: 180-day-demand-forecasting

**Category**: pricing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Predict booking demand for 180 days out with 96%+ accuracy.

**Competitor Coverage**:
| Competitor | Has | Horizon | Accuracy |
|------------|-----|---------|----------|
| Traditional | ⚠️ | 30-60 days | 50-70% |
| Mews (Atomize) | ⚠️ | 90 days | 85% |
| Cloudbeds | ✅ | **180 days** | **96%+** |

**Best Implementation**: Cloudbeds (Signals)

**Capabilities**:
- [x] 180-day horizon
- [x] 96%+ accuracy
- [x] Demand peak/trough ID
- [x] ADR potential forecast
- [x] Segment-specific demand

---

### SKILL-133: 300-plus-channel-distribution

**Category**: distribution
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive channel distribution with 300+ OTA integrations.

**Competitor Coverage**:
| Competitor | Has | Channels | Quality |
|------------|-----|----------|---------|
| Guesty | ⚠️ | 200+ | ⭐⭐⭐⭐ |
| Mews | ⚠️ | 150+ | ⭐⭐⭐⭐ |
| Boom | ⚠️ | 100+ | ⭐⭐⭐ |
| Cloudbeds | ✅ | **300+** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Cloudbeds

**Capabilities**:
- [x] 300+ channels
- [x] <5 min sync
- [x] Zero commission
- [x] 99.99% overbooking prevention
- [x] Metasearch (Google, Kayak)

---

### SKILL-134: event-impact-analysis

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Predict booking surge from local events (concerts, conferences, sports).

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Mews | ⚠️ | Event basic | ⭐⭐⭐ |
| Cloudbeds | ✅ | Event Impact | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Cloudbeds

**Capabilities**:
- [x] Event detection
- [x] Demand increase quantification
- [x] Rate adjustment recommendations
- [x] Weather impact correlation

---

### SKILL-135: integration-marketplace-200-plus

**Category**: distribution
**Priority**: P1
**Status**: NEEDED

**Description**: 
Pre-built marketplace with 200+ partner integrations.

**Competitor Coverage**:
| Competitor | Has | Integrations | Quality |
|------------|-----|--------------|---------|
| Guesty | ⚠️ | 100+ | ⭐⭐⭐⭐ |
| Mews | ⚠️ | 100+ | ⭐⭐⭐⭐ |
| Cloudbeds | ✅ | **200+** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Cloudbeds

**Categories**:
- Accounting (QuickBooks, Xero)
- Housekeeping (Zenvie, Alice)
- Guest Experience (Visito, Inntelo)
- Revenue Management
- CRM (HubSpot, Salesforce)

---

<!-- RENTALREADY UNIQUE SKILLS (136-144) -->

### SKILL-136: flexible-property-grouping

**Category**: grouping
**Priority**: P1
**Status**: NEEDED

**Description**: 
Group properties by location, type, ownership with different rules, policies, and staff per group.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| All Others | ⚠️ | Basic groups | ⭐⭐⭐ |
| RentalReady | ✅ | Flexible Grouping | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady (UNIQUE!)

**Capabilities**:
- [x] Group by location (city/region)
- [x] Group by type (villa/apt/studio)
- [x] Group by ownership model
- [x] Different rules per group
- [x] Different staff per group
- [x] Different pricing per group

---

### SKILL-137: ai-confidence-based-routing

**Category**: ai-routing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Route AI-generated messages based on confidence score (high/medium/low).

**Competitor Coverage**:
| Competitor | Has | Confidence | Human-in-Loop |
|------------|-----|------------|---------------|
| Cloudbeds | ⚠️ | Basic | ⭐⭐⭐ |
| Visito | ⚠️ | Limited | ⭐⭐ |
| RentalReady | ✅ | **Full** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady (Maia AI)

**Routing Logic**:
- HIGH (>90%): Auto-send (configurable)
- MEDIUM (70-90%): Human review OR auto+notify
- LOW (<70%): ALWAYS human review

---

### SKILL-138: ai-property-quality-audit

**Category**: quality
**Priority**: P1
**Status**: NEEDED

**Description**: 
Monitor property quality from guest reviews and generate improvement recommendations.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Cloudbeds | ⚠️ | Basic | ⭐⭐⭐ |
| Inntelo | ⚠️ | CDP insights | ⭐⭐⭐ |
| RentalReady | ✅ | Quality Audit | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady

**Workflow**:
1. Review ingestion from OTAs
2. Sentiment & issue extraction
3. Quality scoring by category
4. Trend detection
5. Recommendation generation

---

### SKILL-139: ai-review-reply-generation

**Category**: quality
**Priority**: P1
**Status**: NEEDED

**Description**: 
Auto-generate public replies to guest reviews on OTAs.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Others | ⚠️ | Manual | ⭐⭐ |
| RentalReady | ✅ | Review Replies | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady

**Capabilities**:
- [x] Positive review responses
- [x] Negative review handling
- [x] Tone matching
- [x] Manager edit/approve

---

### SKILL-140: dynamic-min-stay-optimization

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Auto-adjust minimum stay requirements to fill calendar gaps.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Besty | ⚠️ | Gap Fill | ⭐⭐⭐⭐ |
| RentalReady | ✅ | Min-Stay Opt | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady + Besty combined

**Result**: Fill 2-night gaps when 3-night minimum blocked

---

### SKILL-141: lead-time-based-pricing

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Set different prices based on booking advance window.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Cloudbeds | ⚠️ | Basic | ⭐⭐⭐⭐ |
| RentalReady | ✅ | Lead-Time | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady

**Example**:
- 90+ days: +20% (premium early bookers)
- 0-14 days: -15% (last-minute fill)

---

### SKILL-142: service-provider-ecosystem

**Category**: contractor
**Priority**: P0
**Status**: NEEDED

**Description**: 
Complete ecosystem for managing cleaners, maintenance, key handlers.

**Competitor Coverage**:
| Competitor | Has | Mobile App | Offline |
|------------|-----|------------|---------|
| Guesty | ⚠️ | Basic | ❌ |
| Cloudbeds | ⚠️ | Good | ❌ |
| RentalReady | ✅ | **Full** | ✅ |

**Best Implementation**: RentalReady (UNIQUE offline support!)

**Mobile App Features**:
- [x] Task list (today/tomorrow/upcoming)
- [x] Checklist execution
- [x] Photo evidence
- [x] Problem reporting
- [x] Navigation/maps
- [x] In-app messaging
- [x] **Offline-first** (UNIQUE!)
- [x] Payment tracking

---

### SKILL-143: occupancy-based-pricing-rules

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Automatically adjust rates based on portfolio occupancy.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Cloudbeds | ⚠️ | Signals | ⭐⭐⭐⭐⭐ |
| RentalReady | ✅ | Occupancy Rules | ⭐⭐⭐⭐ |

**Best Implementation**: Cloudbeds (Signals) + RentalReady (Rules)

**Example**:
- Occupancy >80%: +10% all unsold
- Occupancy <50%: -15% discount

---

### SKILL-144: multi-office-staff-separation

**Category**: grouping
**Priority**: P1
**Status**: NEEDED

**Description**: 
Large portfolio management with city managers who only see/manage their properties.

**Competitor Coverage**:
| Competitor | Has | Feature Name | Quality |
|------------|-----|--------------|---------|
| Cloudbeds | ⚠️ | Multi-property | ⭐⭐⭐⭐ |
| RentalReady | ✅ | Multi-Office | ⭐⭐⭐⭐⭐ |

**Best Implementation**: RentalReady

**Capabilities**:
- [x] City managers per group
- [x] Staff visibility restricted
- [x] Central finance read-only
- [x] CEO aggregated dashboard

---

<!-- PRICELABS UNIQUE SKILLS (145-156) -->

### SKILL-145: hyper-local-pulse-algorithm

**Category**: pricing-algorithm
**Priority**: P0
**Status**: NEEDED

**Description**: 
Proprietary algorithm generating optimized daily pricing based on hyper-local (0.5-5km radius) market conditions.

**Competitor Coverage**:
| Competitor | Has | Granularity | Quality |
|------------|-----|-------------|---------|
| Cloudbeds | ⚠️ | Market-wide | ⭐⭐⭐⭐ |
| All Others | ⚠️ | Market-wide | ⭐⭐⭐ |
| PriceLabs | ✅ | **0.5-5km** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs (MOST GRANULAR!)

**Components**:
- [x] Demand forecasting (365 days, <12% MAPE)
- [x] Price elasticity estimation
- [x] Competitive benchmarking (20-350 comps)
- [x] 4-way event detection
- [x] Daily market-driven recalculation
- [x] Lead time optimization

---

### SKILL-146: four-way-event-detection

**Category**: event-detection
**Priority**: P0
**Status**: NEEDED

**Description**: 
Industry-first redundant event detection using 4 independent signals.

**Competitor Coverage**:
| Competitor | Has | Detection Methods | Quality |
|------------|-----|-------------------|---------|
| Cloudbeds | ⚠️ | AI-based | ⭐⭐⭐⭐ |
| Others | ⚠️ | Single source | ⭐⭐⭐ |
| PriceLabs | ✅ | **4-way** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs

**4 Detection Methods**:
1. YoY Pacing comparison
2. Early demand signals (booking surge)
3. Competitor pricing spikes (60%+ raise)
4. Hotel price indicators (Booking.com)

**Confidence Scoring**:
- 1 method: 40%
- 2 methods: 70%
- 3+ methods: 85%+

---

### SKILL-147: price-elasticity-estimation

**Category**: pricing-algorithm
**Priority**: P1
**Status**: NEEDED

**Description**: 
Determine how sensitive demand is to price changes at neighborhood level.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| PriceLabs | ✅ | Elasticity | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs (UNIQUE!)

**Output**: Elasticity coefficient (-0.5 to -2.0)

**Examples**:
- Premium beachfront: -0.4 (can raise prices)
- Mid-tier interior: -1.2 (needs competitive pricing)

---

### SKILL-148: dynamic-min-stay-4-methods

**Category**: pricing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive min-stay optimization with 4 adjustment methods.

**Competitor Coverage**:
| Competitor | Has | Methods | Quality |
|------------|-----|---------|---------|
| RentalReady | ⚠️ | 1 | ⭐⭐⭐⭐ |
| Others | ⚠️ | 1-2 | ⭐⭐⭐ |
| PriceLabs | ✅ | **4** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs (MOST COMPLETE!)

**4 Methods**:
1. Gap-filling (detect & fill short gaps)
2. Lead-time based (far-out vs last-minute)
3. Demand-based (high occ → raise, low → lower)
4. Adjacent day consideration (extension opportunity)

---

### SKILL-149: twelve-price-customization-options

**Category**: price-customization
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive price customization framework with 12 options.

**Competitor Coverage**:
| Competitor | Has | Options | Quality |
|------------|-----|---------|---------|
| RentalReady | ⚠️ | 6-8 | ⭐⭐⭐⭐ |
| Cloudbeds | ⚠️ | 5-6 | ⭐⭐⭐⭐ |
| PriceLabs | ✅ | **12** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs

**12 Options**:
1. Base Price Setting
2. Seasonal Profiles
3. Lead-Time Pricing
4. Day-of-Week
5. LOS Discounts
6. OTA-Specific Markup
7. Event-Based
8. Occupancy-Based
9. Weekday/Peak Strategy
10. Foreign Currency
11. Cleaning Fee Factor
12. Bulk Updates

---

### SKILL-150: automation-rules-engine

**Category**: automation
**Priority**: P1
**Status**: NEEDED

**Description**: 
Conditional logic for pricing/availability without manual intervention.

**Competitor Coverage**:
| Competitor | Has | Rule Types | Quality |
|------------|-----|------------|---------|
| RentalReady | ⚠️ | Basic | ⭐⭐⭐⭐ |
| PriceLabs | ✅ | **6 types** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs

**Rule Types**:
1. Occupancy-based (IF occ > 80% THEN +15%)
2. Pacing rules (YoY comparison)
3. Event rules (auto-apply markup)
4. Booking window (lead-time triggers)
5. Channel-specific (per-OTA strategy)
6. Time-based (seasons/days active)

---

### SKILL-151: pacing-analysis-yoy

**Category**: pacing
**Priority**: P1
**Status**: NEEDED

**Description**: 
Forward-looking booking trajectory and YoY forecast analysis.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Cloudbeds | ⚠️ | Basic | ⭐⭐⭐ |
| PriceLabs | ✅ | **Full** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs

**Metrics**:
- Current vs prior year booking pace
- Booking window analysis
- Lead-time distribution
- Revenue projection
- Risk zone identification

---

### SKILL-152: revenue-estimator-pro

**Category**: investment
**Priority**: P2
**Status**: NEEDED

**Description**: 
Investment analysis tool for new properties or portfolio evaluation.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| PriceLabs | ✅ | Full | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs (UNIQUE!)

**Features**:
- Monthly/annual revenue projection
- ADR recommendation
- Occupancy forecast
- ROI calculation
- Payback period
- Comp-set analysis (50-350 properties)

---

### SKILL-153: pms-integration-management-161

**Category**: integrations-mgmt
**Priority**: P0
**Status**: NEEDED

**Description**: 
Most extensive PMS/channel manager integration ecosystem.

**Competitor Coverage**:
| Competitor | Has | Count | Quality |
|------------|-----|-------|---------|
| Cloudbeds | ✅ | 200+ | ⭐⭐⭐⭐⭐ |
| PriceLabs | ✅ | **161+** | ⭐⭐⭐⭐⭐ |
| Others | ⚠️ | 20-50 | ⭐⭐⭐ |

**Best Implementation**: Cloudbeds (200+) + PriceLabs (161+)

**Integration Types**:
1. Native Direct (real-time)
2. API-Based Custom
3. Bulk Multi-PMS

---

### SKILL-154: team-management-6-roles

**Category**: access-control
**Priority**: P1
**Status**: NEEDED

**Description**: 
Enterprise-grade role-based access control with 6 distinct roles.

**Competitor Coverage**:
| Competitor | Has | Roles | Quality |
|------------|-----|-------|---------|
| Guesty | ✅ | 4-5 | ⭐⭐⭐⭐ |
| RentalReady | ⚠️ | 3-4 | ⭐⭐⭐ |
| PriceLabs | ✅ | **6** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs

**6 Roles**:
1. Account Owner
2. Account Administrator
3. Revenue Manager
4. Property Manager
5. View-Only/Analyst
6. Integration Manager

---

### SKILL-155: comp-set-management

**Category**: competitive-intelligence
**Priority**: P1
**Status**: NEEDED

**Description**: 
Sophisticated comparable property selection and monitoring.

**Competitor Coverage**:
| Competitor | Has | Max Comps | Quality |
|------------|-----|-----------|---------|
| Cloudbeds | ⚠️ | Unknown | ⭐⭐⭐⭐ |
| PriceLabs | ✅ | **350** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs

**Selection Criteria**:
- Proximity (0.5-15 km)
- Property type match
- Bedroom count (±1)
- Amenity similarity
- Price range (±20-30%)
- Review score (4.5+)

---

### SKILL-156: market-dashboards-free

**Category**: analytics
**Priority**: P1
**Status**: NEEDED

**Description**: 
Free competitive benchmarking and market analysis dashboards.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Cloudbeds | ⚠️ | Paid | ⭐⭐⭐⭐ |
| PriceLabs | ✅ | **Free** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: PriceLabs (FREE!)

**8 KPIs**:
1. ADR
2. Occupancy Rate
3. RevPAR
4. Annual Revenue Estimate
5. Booking Velocity
6. Occupancy Heatmap
7. ADR Trends
8. Competitive Positioning

---

<!-- VENDOROO UNIQUE SKILLS (157-167) - MAINTENANCE SPECIALIZED -->

### SKILL-157: specialized-maintenance-agents

**Category**: maintenance-agents
**Priority**: P0
**Status**: NEEDED

**Description**: 
Role-based AI agent architecture with 5 specialized "Roos" for maintenance operations.

**Competitor Coverage**:
| Competitor | Has | Approach | Quality |
|------------|-----|----------|---------|
| Guesty | ⚠️ | General AI | ⭐⭐⭐ |
| All Others | ⚠️ | Generic chatbot | ⭐⭐ |
| **Vendoroo** | ✅ | **5 specialized agents** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo (ONLY ONE!)

**5 Agent Types**:
| Agent | Role | Hard Constraints |
|-------|------|------------------|
| Receptionist Roo | Intake, identity verify | Cannot promise times/costs |
| Triage Roo | Classification, urgency | Cannot downgrade emergency |
| Coordinator Roo | Vendor, scheduling | Cannot exceed budget |
| Invoice Roo | Validation, compliance | Cannot auto-approve > threshold |
| Assistant Roo | NL queries | Read-only, cannot mutate |

---

### SKILL-158: maintenance-brain-memory

**Category**: maintenance-intelligence
**Priority**: P0
**Status**: NEEDED

**Description**: 
Persistent per-property/unit maintenance knowledge base that learns over time.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **Vendoroo** | ✅ | **MaintenanceBook** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo (UNIQUE!)

**Components**:
- MaintenanceBookEntry per property/unit/system
- Asset info: model, age, warranty_expiry
- Recurring issues and patterns
- Recommendations and last service date
- Preferred vendor per system type
- Historical decision training

---

### SKILL-159: emergency-classification-engine

**Category**: emergency-handling
**Priority**: P0
**Status**: NEEDED

**Description**: 
High-accuracy emergency detection with <0.5% false negative rate target.

**Competitor Coverage**:
| Competitor | Has | Accuracy Target | Quality |
|------------|-----|-----------------|---------|
| All Others | ⚠️ | Undefined | ⭐⭐⭐ |
| **Vendoroo** | ✅ | **<0.5% FN** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo (ONLY MEASURABLE TARGET!)

**Features**:
- Conservative classification (err toward emergency)
- Auditable logic trail
- Safety-first triage instructions
- Post-incident review workflow
- False negative tracking

---

### SKILL-160: vendor-intelligence-ranking

**Category**: operations
**Priority**: P0
**Status**: NEEDED

**Description**: 
Multi-factor vendor scoring and tiered assignment with performance metrics.

**Competitor Coverage**:
| Competitor | Has | Depth | Quality |
|------------|-----|-------|---------|
| Guesty | ⚠️ | Basic list | ⭐⭐⭐ |
| RentalReady | ⚠️ | Service providers | ⭐⭐⭐⭐ |
| **Vendoroo** | ✅ | **Full intelligence** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo

**Performance Metrics**:
- jobs_completed
- on_time_rate
- avg_rating (tenant feedback)
- rework_rate
- reliability_score (composite)

**Tier System**: Bronze → Silver → Gold with auto-promotion/demotion

---

### SKILL-161: remote-troubleshooting-flows

**Category**: maintenance-intelligence
**Priority**: P1
**Status**: NEEDED

**Description**: 
Category-specific guided troubleshooting before dispatch.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **Vendoroo** | ✅ | **Category scripts** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo (UNIQUE!)

**Flow**:
1. Classify issue category
2. Check MaintenanceBook for patterns
3. Run category-specific troubleshooting
4. If resolved: log steps, mark "monitor"
5. If unresolved: dispatch

**Goal**: Resolve without dispatch when safe and appropriate

---

### SKILL-162: invoice-validation-ai

**Category**: invoice-compliance
**Priority**: P1
**Status**: NEEDED

**Description**: 
Automated invoice compliance checking against policy and history.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Guesty | ⚠️ | Manual review | ⭐⭐⭐ |
| Cloudbeds | ⚠️ | Basic validation | ⭐⭐⭐⭐ |
| **Vendoroo** | ✅ | **AI compliance** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo

**Validation Checks**:
- Line items match WorkOrder scope
- Rates within standard for vendor
- Parts/labor reasonable for job type
- Historical pattern comparison
- Fraud/waste detection signals

---

### SKILL-163: maintenance-policy-engine

**Category**: policy-engine
**Priority**: P0
**Status**: NEEDED

**Description**: 
Granular, scope-based policy rules with simulation mode.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| PriceLabs | ⚠️ | Automation rules | ⭐⭐⭐⭐ |
| **Vendoroo** | ✅ | **Full policy + simulation** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo

**Rule Types**: budget, escalation, safety, communication

**Scope Levels**:
- Account-wide (company default)
- Property-level override
- Unit-level exception

**Unique Feature**: Simulation mode - "Show me how this rule would change decisions"

---

### SKILL-164: preventive-maintenance-campaigns

**Category**: work-orchestration
**Priority**: P1
**Status**: NEEDED

**Description**: 
Rule-based scheduled maintenance with batch vendor assignment.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **Vendoroo** | ✅ | **Campaign system** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo (UNIQUE!)

**Features**:
- Rule: "HVAC inspection every 6 months for region X"
- Auto-generate WorkOrders with `job_type=preventive`
- Batch vendor assignment
- Campaign-level tracking
- Aggregated reporting

---

### SKILL-165: work-order-state-machine

**Category**: work-orchestration
**Priority**: P0
**Status**: NEEDED

**Description**: 
Idempotent, pausable orchestration with defined state transitions.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Guesty | ⚠️ | Task status | ⭐⭐⭐ |
| **Vendoroo** | ✅ | **Formal state machine** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo

**States**:
```
received → triaged → awaiting_approval → awaiting_vendor → 
scheduled → in_progress → completed → [rework] → cancelled
```

**Guarantees**:
- Invariant enforcement (can't skip states)
- Idempotency (safe to retry)
- Pause/resume per account/property/work_order
- AuditLog every transition

---

### SKILL-166: owner-cost-defensibility

**Category**: financial
**Priority**: P1
**Status**: NEEDED

**Description**: 
Every maintenance dollar traceable and justifiable to owners.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Guesty | ⚠️ | Owner reports | ⭐⭐⭐ |
| **Vendoroo** | ✅ | **Full defensibility** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo

**Components**:
- Invoice-to-policy mapping
- Historical pattern comparison
- Fraud/waste detection signals
- Per-property spend analysis
- Executive summary generation

---

### SKILL-167: after-hours-emergency-flow

**Category**: emergency-handling
**Priority**: P0
**Status**: NEEDED

**Description**: 
Specialized workflow for after-hours emergency handling.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Boom AI | ⚠️ | 24/7 availability | ⭐⭐⭐⭐ |
| **Vendoroo** | ✅ | **Dedicated flow** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Vendoroo

**Flow**:
1. After-hours flag detection
2. Stricter emergency classification
3. Safety script for tenant (shut-off valves, etc.)
4. Emergency-capable vendor dispatch
5. PM on-call notification (Slack/SMS)
6. Human override capability
7. Post-incident review tagging

---

<!-- ELISEAI UNIQUE SKILLS (168-177) - INDUSTRY BENCHMARK -->

### SKILL-168: purpose-built-housing-crm

**Category**: housing-crm
**Priority**: P0
**Status**: NEEDED

**Description**: 
EliseCRM as the "nervous system" - a CRM purpose-built for multifamily as system-of-engagement (while PMS = system-of-record).

**Competitor Coverage**:
| Competitor | Has | Approach | Quality |
|------------|-----|----------|---------|
| Guesty | ⚠️ | Basic CRM | ⭐⭐⭐ |
| All Others | ⚠️ | No CRM or generic | ⭐⭐ |
| **EliseAI** | ✅ | **Purpose-built** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI (MARKET LEADER!)

**Components**:
- Unified inbox across all channels
- Full prospect/resident profiles
- Automated workflows for all modules
- Cross-portfolio dashboards
- Real-time AI + human collaboration

---

### SKILL-169: leasing-ai-full-funnel

**Category**: leasing
**Priority**: P0
**Status**: NEEDED

**Description**: 
Complete lead-to-lease AI automation covering the entire prospect journey.

**Competitor Coverage**:
| Competitor | Has | Coverage | Quality |
|------------|-----|----------|---------|
| Besty AI | ⚠️ | Inquiry response | ⭐⭐⭐⭐ |
| Inntelo AI | ⚠️ | Guest messaging | ⭐⭐⭐⭐ |
| **EliseAI** | ✅ | **Full funnel** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI

**Capabilities**:
- 24/7 prospect response (all channels)
- Real-time PMS availability/pricing
- Preference capture + unit recommendation
- Tour scheduling (including self-tours)
- Lead nurturing campaigns
- Pre-screening questions

---

### SKILL-170: resident-lifecycle-ai

**Category**: resident-lifecycle
**Priority**: P0
**Status**: NEEDED

**Description**: 
Proactive resident engagement for renewals, questions, and lifecycle events.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **EliseAI** | ✅ | **Full lifecycle** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI (UNIQUE!)

**Capabilities**:
- Answer resident questions (rent, policies, amenities)
- Proactive renewal outreach
- Explain pricing changes and terms
- Handle inbound renewal questions
- Escalation to human when needed

---

### SKILL-171: delinquency-empathy-automation

**Category**: resident-lifecycle
**Priority**: P0
**Status**: NEEDED

**Description**: 
AI-managed payment reminders with empathetic messaging and promises-to-pay capture.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **EliseAI** | ✅ | **Empathy + effectiveness** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI (UNIQUE!)

**Features**:
- Payment reminders at configured intervals
- Late fee explanations
- Promises-to-pay capture
- Note updates in CRM
- Empathetic tone protection
- Escalation for complex cases

**Key Metric**: Reduces bad debt while protecting relationships

---

### SKILL-172: maintenance-technician-app

**Category**: field-service
**Priority**: P0
**Status**: NEEDED

**Description**: 
Dedicated mobile/web app for technicians and supervisors with AI-powered auto-assignment.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Vendoroo | ⚠️ | Vendor portal | ⭐⭐⭐⭐ |
| **EliseAI** | ✅ | **Full field service** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI

**Features**:
- Work order management (priority, timeline)
- Smart auto-assignment by skills/location
- Real-time time tracking
- Geo-fenced location tracking (privacy-compliant)
- Offline mode with sync
- Supervisor dashboard

---

### SKILL-173: fair-housing-compliance-ai

**Category**: compliance
**Priority**: P0
**Status**: NEEDED

**Description**: 
Built-in guardrails for fair housing and non-discrimination in all leasing interactions.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **EliseAI** | ✅ | **Built into AI** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI (CRITICAL FOR US MARKET!)

**Components**:
- Compliance checks in conversation flows
- Phrasing templates for sensitive topics
- Equal treatment enforcement
- Audit logging for compliance review
- Regulatory constraint enforcement

---

### SKILL-174: 30m-conversation-training

**Category**: training-data
**Priority**: P1
**Status**: ASPIRATIONAL

**Description**: 
Models trained on 30+ million real conversations with prospects and residents.

**Competitor Coverage**:
| Competitor | Has | Scale | Quality |
|------------|-----|-------|---------|
| All Others | ⚠️ | <1M | ⭐⭐⭐ |
| **EliseAI** | ✅ | **30M+** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI (MASSIVE MOAT!)

**Training Coverage**:
- Domain-specific NLU
- Leasing conversations
- Maintenance requests
- Payment discussions
- Community policies

**Note**: This is a **data moat** - we need to start collecting conversations now.

---

### SKILL-175: centralized-operations-model

**Category**: enterprise-ops
**Priority**: P1
**Status**: NEEDED

**Description**: 
Built for centralized operations across large portfolios with role specialization.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| RentalReady | ⚠️ | Multi-office | ⭐⭐⭐⭐ |
| **EliseAI** | ✅ | **Enterprise-grade** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI

**Features**:
- Multi-portfolio support
- Role-based access (central vs on-site)
- Consistent service across properties
- Standardized workflows across regions
- Enterprise governance

---

### SKILL-176: ai-human-realtime-collaboration

**Category**: ai-collaboration
**Priority**: P0
**Status**: NEEDED

**Description**: 
Humans can jump into AI conversations at any time and override decisions.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Guesty | ⚠️ | Basic escalation | ⭐⭐⭐ |
| **EliseAI** | ✅ | **Real-time collab** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI

**Capabilities**:
- Real-time conversation handoff
- Override AI decisions
- Human takeover for complex cases
- Seamless transition (resident doesn't notice)
- Full audit trail

---

### SKILL-177: automated-status-updates

**Category**: ai-collaboration
**Priority**: P1
**Status**: NEEDED

**Description**: 
Proactive notifications to residents at every work order milestone.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Vendoroo | ⚠️ | Basic updates | ⭐⭐⭐⭐ |
| **EliseAI** | ✅ | **Full lifecycle** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: EliseAI

**Milestones**:
1. Work order created
2. Assigned to technician
3. Scheduled time
4. In-progress
5. Completed

**Impact**: Reduces "where's my repair?" calls by proactively communicating.

---

<!-- HOSTAWAY UNIQUE SKILLS (178-186) - ENTERPRISE STR COMPETITOR -->

### SKILL-178: 93-percent-message-automation

**Category**: communication
**Priority**: P0
**Status**: NEEDS VALIDATION

**Description**: 
Platform claims 93% of guest communications can be automated (vs competitors' 30-50%).

**Competitor Coverage**:
| Competitor | Has | Claim | Quality |
|------------|-----|-------|---------|
| EliseAI | ✅ | ~99% work orders | ⭐⭐⭐⭐⭐ |
| All Others | ⚠️ | 30-50% | ⭐⭐⭐ |
| **Hostaway** | ✅ | **93%** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway (claimed)

**How Achieved**:
- AI message suggestions and auto-replies
- Trigger-based scheduled messages
- Auto-responses for common inquiries
- AI classification by intent/type
- Sentiment analysis
- Smart quick replies

**Validation Needed**: How is 93% measured? What's in the 7%?

---

### SKILL-179: white-label-platform

**Category**: white-label
**Priority**: P0
**Status**: NEEDED

**Description**: 
Full white-label capabilities for agencies and resellers to build custom branded solutions.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❌ | None | N/A |
| **Hostaway** | ✅ | **Full white-label** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway (UNIQUE!)

**Features**:
- Rebrand with client logos/colors
- Host on custom domain
- Multi-tenant support
- Reseller program with markup
- Custom branding throughout

**Strategic Note**: Our open-source approach = infinite customization (better than white-label?)

---

### SKILL-180: trust-accounting

**Category**: trust-accounting
**Priority**: P1
**Status**: NEEDED

**Description**: 
Separate trust accounts for owner funds, maintaining legal separation from operating funds.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ❓ | Unknown | N/A |
| **Hostaway** | ✅ | **Full trust** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway

**Features**:
- Separate owner trust accounts
- Commission holds for expenses/damages
- Full reconciliation
- Legal compliance
- Automated owner payouts

**COMPLIANCE NOTE**: Required in many US states and jurisdictions!

---

### SKILL-181: cleaner-portal-mobile

**Category**: cleaner-ops
**Priority**: P1
**Status**: NEEDED

**Description**: 
Dedicated mobile portal for cleaners/vendors with task management, checklists, and photo documentation.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| EliseAI | ✅ | Maintenance App | ⭐⭐⭐⭐⭐ |
| Vendoroo | ⚠️ | Vendor portal | ⭐⭐⭐⭐ |
| **Hostaway** | ✅ | **Cleaner portal** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway (cleaner-specific), EliseAI (technician-specific)

**Features**:
- Task assignment with notifications
- Digital checklists
- Required photo uploads
- Time tracking per task
- Quality rating system

---

### SKILL-182: custom-workflow-builder

**Category**: workflow-builder
**Priority**: P0
**Status**: NEEDED

**Description**: 
Visual workflow builder for complex business process automation with conditional logic.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Guesty | ⚠️ | Templates | ⭐⭐⭐⭐ |
| All Others | ⚠️ | Basic rules | ⭐⭐⭐ |
| **Hostaway** | ✅ | **Visual builder** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway

**Capabilities**:
- Define triggers (booking created, payment, etc.)
- Perform actions (message, task, field update)
- Complex conditional logic (if/then/else)
- Multi-step sequential workflows
- Approval chains
- Escalation rules

---

### SKILL-183: multi-booking-engine

**Category**: multi-engine
**Priority**: P2
**Status**: NEEDED

**Description**: 
Create multiple separate booking websites for different property groups.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| All Others | ⚠️ | Single site | ⭐⭐⭐ |
| **Hostaway** | ✅ | **Multiple engines** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway (UNIQUE!)

**Use Cases**:
- Different brands for locations
- Separate sites for property types
- White-label sites for different owners

---

### SKILL-184: granular-rbac

**Category**: rbac
**Priority**: P1
**Status**: NEEDED

**Description**: 
Fine-grained role-based access control at property, feature, and action level.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Guesty | ⚠️ | Role-based | ⭐⭐⭐⭐ |
| EliseAI | ⚠️ | Multi-portfolio | ⭐⭐⭐⭐ |
| **Hostaway** | ✅ | **Granular** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Hostaway

**Permission Levels**:
- Property-level (assign to specific properties)
- Feature-level (which features per role)
- Action-level (CRUD per feature)
- Data visibility controls
- **Custom Roles** (create your own)

---

### SKILL-185: ai-message-generation

**Category**: ai-messaging
**Priority**: P0
**Status**: NEEDED

**Description**: 
AI-powered message suggestions, auto-drafting, and sentiment analysis.

**Competitor Coverage**:
| Competitor | Has | Feature | Quality |
|------------|-----|---------|---------|
| Besty AI | ✅ | AI responses | ⭐⭐⭐⭐⭐ |
| EliseAI | ✅ | 30M trained | ⭐⭐⭐⭐⭐ |
| **Hostaway** | ✅ | **Full AI suite** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Tied (Besty, EliseAI, Hostaway all strong)

**Capabilities**:
- AI suggestions for response content
- Auto-generate response drafts
- AI classification by intent
- Sentiment analysis
- Smart reply suggestions

---

### SKILL-186: 1000-property-scale

**Category**: scale
**Priority**: P1
**Status**: DOCUMENTED

**Description**: 
Platform tested and proven to handle 1000+ property portfolios.

**Competitor Coverage**:
| Competitor | Has | Scale | Quality |
|------------|-----|-------|---------|
| Guesty | ✅ | 5000+ | ⭐⭐⭐⭐⭐ |
| EliseAI | ✅ | Enterprise | ⭐⭐⭐⭐⭐ |
| **Hostaway** | ✅ | **1000+** | ⭐⭐⭐⭐⭐ |

**Best Implementation**: Guesty (largest scale documented)

**Enterprise Features**:
- Sub-second channel sync
- Database optimized for large datasets
- Multi-region deployment
- Auto-scaling
- 99.9% uptime SLA
- SOC 2 Type II

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

### P0 - MVP (30 skills)
Core functionality for basic STR management
- Includes: Polymorphic Inventory, Magic Link App, Multi-Stakeholder Splits
- NEW: Booking Engine, No-App Messaging, Pre-Arrival Data

### P1 - Phase 1 (36 skills)
Enhanced features for professional managers
- Includes: Gap Night, Upgrades, RAG, Party Prevention, Police Reporting
- NEW: Digital Key, Kiosk, ML Pricing, GOPPAR, Package Bundling

### P2 - Phase 2 (21 skills)
Advanced features for scaling operations
- Includes: Bad Review Defense
- NEW: Front Desk, Overbooking, Shift Planning, HK Performance, Loyalty

### P3 - Phase 3 (7 skills)
Enterprise and specialized features
- NEW: Hourly Bookings

---

## 🏆 Best-of-Breed Sources

| Feature Area | Best Source | Why |
|--------------|-------------|-----|
| STR Operations | Guesty | Comprehensive task management, OTA sync |
| Agentic AI | Host OS (BoomAI) | Autonomous agents, RAG |
| Compliance | Host OS (CheKin) | ID + Police reporting |
| Protection | Host OS (Minut) | Noise monitoring |
| Digital Key | Mews | Apple Wallet, BLE |
| Booking Engine | Mews | A/B testing, conversion |
| Analytics | Mews | GOPPAR, performance |
| Revenue ML | Mews (Atomize) | ML-powered pricing |
| Guest Portal | Mews | No-app messaging |
| **Gap Nights** | **Besty AI** | **Full workflow, 40-60% fill rate** |
| **Inquiry Winback** | **Besty AI** | **8-20% recovery rate** |
| **AI Control** | **Besty AI** | **Confidence thresholds, Co-Pilot** |
| **Guest Journeys** | **Besty AI** | **Visual builder, 30+ templates** |
| **Review Response** | **Besty AI** | **100% rate, sentiment-matched** |
| **Voice AI** | **Boom AI** | **24/7 phone answering, 5+ languages** |
| **Agentic Architecture** | **Boom AI** | **Multi-function simultaneous execution** |
| **Predictive Outreach** | **Boom AI** | **Proactive offers based on profile** |
| **CDP** | **Inntelo AI** | **Full stack, identity resolution, 97% capture** |
| **Multi-Agent** | **Inntelo AI** | **5 specialized agents, clean handoffs** |
| **Cross-Dept Orchestration** | **Inntelo AI** | **Seamless workflow coordination** |
| **40+ Languages** | **Inntelo AI** | **Most comprehensive multilingual** |
| **Churn Prediction** | **Inntelo AI** | **Full retention AI, intervention triggers** |
| **Upsell Conversion** | **Inntelo AI** | **30-40% rate (highest)** |
| **100+ Languages** | **Visito AI** | **Most comprehensive multilingual (100+)** |
| **2-Min Setup** | **Visito AI** | **Fastest agent creation** |
| **No-Code Builder** | **Visito AI** | **Full drag-and-drop, templates** |
| **Knowledge Gaps** | **Visito AI** | **Auto-detection of missing content** |
| **RAG Hybrid** | **Visito AI** | **Semantic + keyword retrieval** |
| **Foundation AI** | **Cloudbeds** | **Signals - hospitality-specific foundation model** |
| **Demand Forecast** | **Cloudbeds** | **96% accuracy @ 180 days (BEST!)** |
| **Time Surface** | **Cloudbeds** | **Proprietary 2D booking analysis** |
| **Channel Distribution** | **Cloudbeds** | **300+ channels (MOST!)** |
| **Event Impact** | **Cloudbeds** | **Automatic event detection & pricing** |
| **Marketplace** | **Cloudbeds** | **200+ pre-built integrations** |
| **AI Confidence Routing** | **RentalReady** | **High/Medium/Low + human-in-loop (MOST CONTROL!)** |
| **Property Grouping** | **RentalReady** | **Location/type/ownership (UNIQUE!)** |
| **Service Provider App** | **RentalReady** | **Offline-first mobile app** |
| **Quality Audit** | **RentalReady** | **Reviews → Scores → Recommendations** |
| **Review Replies** | **RentalReady** | **Auto-generate public responses** |
| **Min-Stay Optimization** | **RentalReady** | **Fill calendar gaps dynamically** |
| **Lead-Time Pricing** | **RentalReady** | **Price by booking window** |
| **Multi-Office** | **RentalReady** | **Staff separation by city/group** |
| **Offline Support** | **RentalReady** | **Field worker reliability (UNIQUE!)** |
| **Dynamic Pricing Algorithm** | **PriceLabs** | **HLP - hyper-local 0.5-5km (BEST GRANULARITY!)** |
| **Event Detection** | **PriceLabs** | **4-way redundancy (MOST RELIABLE!)** |
| **Price Customization** | **PriceLabs** | **12 options with stacking (MOST COMPREHENSIVE!)** |
| **Min-Stay Optimization** | **PriceLabs** | **4 methods (MOST COMPLETE!)** |
| **Price Elasticity** | **PriceLabs** | **Economic demand modeling (UNIQUE!)** |
| **Pacing Analysis** | **PriceLabs** | **YoY trajectory forecasting** |
| **Revenue Estimation** | **PriceLabs** | **Investment analysis tool** |
| **PMS Integrations Count** | **PriceLabs** | **161+ systems (MOST!)** |
