# Final Skill Specification: Booking & Calendar System

**Skills**: SKILL-007, SKILL-008, SKILL-009, SKILL-010
**Category**: Booking Core
**Priority**: P0 (MVP Critical)
**Status**: SPECIFIED
**Date**: January 7, 2026
**Source**: ES-PHASE1-GROUP2-booking-calendar.md (6,532 lines)

---

## Executive Summary

This specification covers four foundational booking system skills that form the core of multi-channel vacation rental management. These skills work together to prevent double bookings, synchronize calendars across 60+ OTA platforms, manage date blocking, and enable direct reservations with PCI-compliant payment processing.

**Business Impact**: On average, operators switching to comprehensive property management systems see a **33% revenue boost** in their first year. Double bookings occur in **25% of first-year short-term rentals** (Booking.com data).

---

## SKILL-007: Calendar Sync Management

### Overview
Multi-calendar management system that prevents double bookings by managing reservations and availability across all listings and channels from a single, intuitive calendar dashboard.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Real-time API Sync** | Instant synchronization with OTA platforms | <1 minute latency |
| **iCal Fallback** | Hourly sync for non-API platforms | 1-12 hour sync cycle |
| **Multi-Channel Consolidation** | Single view of all bookings | 60+ channels supported |
| **Timezone Management** | Property-specific timezone handling | UTC normalization |

### Technical Implementation

```python
# Calendar Sync Service Architecture
class CalendarSyncEngine:
    """
    Hybrid synchronization supporting both API and iCal protocols.
    API connections update instantly; iCal syncs hourly.
    """
    
    sync_methods = {
        'airbnb': 'API',      # Real-time
        'vrbo': 'API',        # Real-time  
        'booking_com': 'API', # Real-time
        'google_calendar': 'iCal',  # Hourly
        'external': 'iCal'    # Hourly
    }
    
    performance_targets = {
        'api_sync_latency': '<60 seconds',
        'ical_sync_frequency': '1 hour',
        'conflict_detection': '<100ms',
        'channel_coverage': '60+ platforms'
    }
```

### Database Schema

```sql
-- Calendar events table for sync management
CREATE TABLE calendar_events (
    event_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    source VARCHAR(20) NOT NULL CHECK (source IN ('airbnb', 'vrbo', 'booking_com', 'direct', 'block')),
    external_id VARCHAR(255),
    status event_status DEFAULT 'CONFIRMED',
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    guest_name VARCHAR(255),
    ical_uid VARCHAR(255),
    sync_timestamp TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
    conflict_status conflict_status DEFAULT 'NONE'
);

-- Index for sync performance
CREATE INDEX idx_calendar_events_property_sync ON calendar_events (property_id, sync_timestamp);
```

### Integration Points

| Platform | Integration Type | Sync Method | Rate Limit |
|----------|-----------------|-------------|------------|
| Airbnb | OAuth 2.0 API | Real-time webhooks | 1000 req/hr |
| Vrbo | REST API | Webhook + polling | 500 req/hr |
| Booking.com | XML API | Push notifications | 2000 req/hr |
| Google Calendar | OAuth 2.0 | iCal feed | Hourly |

### Acceptance Criteria
- [ ] API connections update availability within 60 seconds
- [ ] iCal feeds sync at minimum hourly intervals
- [ ] Single calendar view consolidates all channels
- [ ] No duplicate events from same source
- [ ] Timezone correctly handled per property

---

## SKILL-008: Double-Booking Prevention

### Overview
Automated availability checking software that prevents double bookings by cross-referencing incoming reservations with existing bookings in real-time, alerting owners if conflicts arise.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Atomic Availability Locking** | Database-level prevention | <100ms lock acquisition |
| **Concurrent Booking Handling** | Race condition prevention | Zero conflicts |
| **Buffer Time Management** | Cleaning gaps between stays | Configurable 0-48 hours |
| **Conflict Resolution** | Automated handling workflow | <5 minute resolution |

### Technical Implementation

```sql
-- PostgreSQL EXCLUSION constraint for double-booking prevention
CREATE TABLE bookings (
    booking_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    user_id UUID NOT NULL REFERENCES users(user_id),
    check_in_date DATE NOT NULL,
    check_out_date DATE NOT NULL,
    status booking_status DEFAULT 'INQUIRY',
    total_amount DECIMAL(10,2),
    currency VARCHAR(3) DEFAULT 'USD',
    source_channel VARCHAR(50) DEFAULT 'direct',
    
    -- Ensure check-in is before check-out
    CONSTRAINT check_dates_valid CHECK (check_in_date < check_out_date),
    
    -- CRITICAL: Prevent overlapping bookings for the same property
    EXCLUDE USING gist (
        property_id WITH =,
        daterange(check_in_date, check_out_date, '[)') WITH &&
    ) WHERE (status NOT IN ('CANCELLED_BY_GUEST', 'CANCELLED_BY_HOST'))
);

-- Required extension for exclusion constraint
CREATE EXTENSION IF NOT EXISTS "btree_gist";
```

### Conflict Detection Algorithm

```python
async def check_availability(property_id: UUID, check_in: date, check_out: date) -> bool:
    """
    Atomic availability check with row-level locking.
    Returns True if property is available, False otherwise.
    """
    async with database.transaction():
        # Lock the property row to prevent concurrent modifications
        result = await database.execute("""
            SELECT 1 FROM bookings
            WHERE property_id = $1
              AND status NOT IN ('CANCELLED_BY_GUEST', 'CANCELLED_BY_HOST')
              AND daterange(check_in_date, check_out_date, '[)') && 
                  daterange($2, $3, '[)')
            FOR UPDATE NOWAIT
        """, property_id, check_in, check_out)
        
        return result.rowcount == 0
```

### Buffer Time Configuration

| Scenario | Default Buffer | Use Case |
|----------|---------------|----------|
| Same-day turnover | 4 hours | High-demand properties |
| Standard cleaning | 8 hours | Most properties |
| Deep clean | 24 hours | Premium properties |
| Maintenance window | 48+ hours | Scheduled repairs |

### Acceptance Criteria
- [ ] Zero double bookings occur under any circumstances
- [ ] Concurrent booking attempts handled atomically
- [ ] Buffer time configurable per property
- [ ] Conflict alerts sent within 5 minutes
- [ ] Database-level protection via EXCLUSION constraint

---

## SKILL-009: Date Blocking

### Overview
Date blocking system for managing maintenance windows, personal use, and seasonal closures with automatic cross-channel synchronization.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Manual Date Blocking** | One-click block creation | Instant application |
| **Recurring Block Patterns** | Weekly/monthly schedules | RFC 5545 compliant |
| **Block Type Categorization** | Maintenance, owner use, seasonal | Clean reporting |
| **Cross-Channel Sync** | Blocks propagate to all OTAs | <1 minute sync |

### Block Types

```sql
CREATE TYPE block_type AS ENUM (
    'MAINTENANCE',   -- Deep cleans, repairs, inspections
    'OWNER_USE',     -- Personal stays, private events
    'SEASONAL',      -- Off-season closures
    'BUFFER',        -- Turnaround time between guests
    'COMPLIANCE'     -- Permit/license restrictions
);

CREATE TABLE date_blocks (
    block_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    property_id UUID NOT NULL REFERENCES properties(property_id),
    type block_type NOT NULL,
    reason VARCHAR(255),
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    recurrence_rule VARCHAR(255), -- RFC 5545 RRULE format
    revenue_impact DECIMAL(10,2),
    created_by UUID REFERENCES users(user_id),
    approval_status VARCHAR(20) DEFAULT 'PENDING',
    sync_status VARCHAR(20) DEFAULT 'PENDING',
    
    -- Prevent overlapping blocks of the same type
    EXCLUDE USING gist (
        property_id WITH =,
        type WITH =,
        daterange(start_date, end_date, '[)') WITH &&
    )
);
```

### Recurring Block Examples

| Pattern | RRULE | Use Case |
|---------|-------|----------|
| Weekly cleaning | `RRULE:FREQ=WEEKLY;BYDAY=TH` | Every Thursday |
| Monthly inspection | `RRULE:FREQ=MONTHLY;BYMONTHDAY=1` | 1st of month |
| Quarterly deep clean | `RRULE:FREQ=MONTHLY;INTERVAL=3` | Every 3 months |
| Seasonal closure | `RRULE:FREQ=YEARLY;BYMONTH=12` | December annually |

### Acceptance Criteria
- [ ] Blocks sync to all connected channels within 1 minute
- [ ] Recurring patterns support RFC 5545 RRULE format
- [ ] Block types tracked for reporting purposes
- [ ] Existing bookings flagged when creating overlapping blocks
- [ ] Revenue impact calculated automatically

---

## SKILL-010: Direct Reservation Creation

### Overview
Embeddable booking widget that enables direct reservations with PCI-compliant payment processing, supporting multiple payment methods and currencies.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Embeddable Widget** | Copy-paste integration | <200ms page load |
| **PCI-Compliant Processing** | Stripe/PayPal tokenization | Level 1 PCI DSS |
| **Multiple Payment Methods** | Cards, wallets, manual | 12+ gateways |
| **Multi-Currency Support** | International guests | All major currencies |

### Payment Gateway Integration

```python
# Payment Processor Factory
class PaymentProcessorFactory:
    """
    PCI-compliant payment processing with multiple gateway support.
    Tokenization ensures no raw card data touches our servers.
    """
    
    supported_gateways = {
        'stripe': StripeProcessor,      # Cards, Apple Pay, Google Pay
        'paypal': PayPalProcessor,      # PayPal, Venmo
        'authorize_net': AuthorizeNet,  # Credit cards
    }
    
    supported_methods = [
        'credit_card',      # Visa, MC, Amex, Discover
        'apple_pay',        # iOS devices
        'google_pay',       # Android devices
        'paypal',           # PayPal account
        'bank_transfer',    # ACH, wire
        'custom'            # Cash, Zelle, Venmo instructions
    ]
```

### PCI DSS Compliance

```sql
-- Payment tokens table (no raw card data stored)
CREATE TABLE payment_methods (
    payment_method_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id UUID NOT NULL REFERENCES users(user_id),
    token VARCHAR(255) NOT NULL,           -- Gateway-provided token
    last_four_digits VARCHAR(4),           -- For display only
    card_type VARCHAR(20),                 -- visa, mastercard, etc.
    expiry_month INTEGER,
    expiry_year INTEGER,
    gateway_name VARCHAR(50) NOT NULL,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);

-- Transaction audit trail (7-year retention for PCI)
CREATE TABLE payment_transactions (
    transaction_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    booking_id UUID NOT NULL REFERENCES bookings(booking_id),
    payment_method_token VARCHAR(255) NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'USD',
    status payment_status DEFAULT 'PENDING',
    gateway_transaction_id VARCHAR(255),
    processed_at TIMESTAMPTZ,
    audit_log JSONB DEFAULT '{}'
);
```

### Booking Widget Architecture

```html
<!-- Embeddable Booking Widget -->
<div id="citadel-booking-widget" 
     data-property-id="uuid" 
     data-api-key="public_key">
</div>
<script src="https://cdn.citadelos.com/widget.js"></script>
```

### Acceptance Criteria
- [ ] Widget embeds in any CMS with copy-paste
- [ ] PCI Level 1 DSS compliant (no raw card data)
- [ ] Supports credit cards, Apple Pay, Google Pay
- [ ] Multi-currency pricing displayed
- [ ] Booking confirmation within 30 seconds

---

## Technology Stack Summary

| Layer | Technology | Version | Purpose |
|-------|------------|---------|---------|
| **Backend** | Python/Flask | 3.11+ | Core booking logic |
| **Real-time** | Node.js/Express | 18+ | Calendar sync services |
| **Frontend** | React/TypeScript | 18+ | Booking widget |
| **Database** | PostgreSQL | 15+ | EXCLUSION constraints |
| **Cache** | Redis | 7+ | Session, availability |
| **Payments** | Stripe | v2023-10 | PCI tokenization |
| **Infrastructure** | AWS ECS Fargate | - | Serverless containers |

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        BOOKING & CALENDAR SYSTEM                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐                  │
│  │   Airbnb     │    │    Vrbo      │    │ Booking.com  │  OTA Channels   │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘                  │
│         │                   │                   │                          │
│         └───────────────────┼───────────────────┘                          │
│                             │                                              │
│                    ┌────────▼────────┐                                     │
│                    │  API Gateway    │                                     │
│                    │  (Rate Limit)   │                                     │
│                    └────────┬────────┘                                     │
│                             │                                              │
│         ┌───────────────────┼───────────────────┐                          │
│         │                   │                   │                          │
│  ┌──────▼──────┐    ┌───────▼───────┐    ┌─────▼─────┐                    │
│  │ Calendar    │    │ Double-Book   │    │ Payment   │   Core Services    │
│  │ Sync Engine │    │ Prevention    │    │ Processor │                    │
│  │ (SKILL-007) │    │ (SKILL-008)   │    │(SKILL-010)│                    │
│  └──────┬──────┘    └───────┬───────┘    └─────┬─────┘                    │
│         │                   │                   │                          │
│         └───────────────────┼───────────────────┘                          │
│                             │                                              │
│                    ┌────────▼────────┐                                     │
│                    │   PostgreSQL    │                                     │
│                    │ EXCLUSION CONST │   Database Layer                    │
│                    │  (Zero Double   │                                     │
│                    │   Bookings)     │                                     │
│                    └─────────────────┘                                     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Performance SLAs

| Metric | Target | Critical Threshold |
|--------|--------|-------------------|
| API Response Time | <500ms (95th percentile) | >3 seconds |
| Calendar Sync Latency | <1 minute (API) | >15 minutes |
| Double-Booking Rate | 0% | Any occurrence |
| Payment Processing | <30 seconds | >120 seconds |
| System Availability | 99.95% | <99.5% |

---

## Implementation Timeline

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Week 1-2** | Foundation | PostgreSQL schema, EXCLUSION constraints |
| **Week 3-4** | Calendar Sync | API integrations, iCal parser |
| **Week 5-6** | Double-Booking | Atomic locking, conflict resolution |
| **Week 7-8** | Date Blocking | Block management, recurring patterns |
| **Week 9-10** | Direct Booking | Widget, payment integration |
| **Week 11-12** | Testing | E2E tests, load testing, security audit |

**Total: 12 weeks to production-ready MVP**

---

## Testing Requirements

| Test Type | Coverage Target | Focus Areas |
|-----------|-----------------|-------------|
| Unit Tests | 90% | Double-booking logic, payment processing |
| Integration Tests | 85% | OTA API sync, database constraints |
| E2E Tests | Critical paths | Complete booking flow |
| Load Tests | 1000 concurrent | Peak booking season simulation |
| Security Tests | PCI DSS | Payment tokenization, data encryption |

---

## Dependencies

| Dependency | Type | Status |
|------------|------|--------|
| SKILL-261-268 (AI Workforce) | Optional | Can operate standalone |
| Treasury OS (TigerBeetle) | Integration | Financial recording |
| Auth0 | Required | User authentication |
| Stripe | Required | Payment processing |
| AWS ECS | Required | Infrastructure |

---

## Risk Mitigation

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| OTA API changes | Medium | High | Version pinning, webhook monitoring |
| Payment gateway outage | Low | Critical | Multi-gateway failover |
| Database deadlock | Low | High | Optimistic locking, retry logic |
| Calendar sync delays | Medium | Medium | Circuit breaker, queue management |

---

## 📐 Architecture Alignment Notes

### Citadel OS Layer Mapping

| Spec Component | Citadel Layer | Technology | Aligned |
|----------------|---------------|------------|---------|
| Calendar Sync Engine | Layer 4 (Skills) | Python/Node.js scripts | ✅ |
| Double-Booking Logic | Layer 2 (Database) | PostgreSQL EXCLUSION | ✅ (app data, not financial) |
| Payment Processing | Layer 3B (Cold Path) | TigerBeetle via Stripe | ✅ |
| Real-time Updates | Layer 2 | Redis Pub/Sub | ✅ |
| API Gateway | Layer 2 | Rust/Axum | ✅ |

### Execution Path Classification

| Operation | Path | Rationale |
|-----------|------|-----------|
| Calendar Sync | **Hot Path** | API orchestration, no financial guarantee |
| Double-Booking Check | **Cold Path** | Database constraint, ACID required |
| Date Blocking | **Hybrid** | User action (Hot) → DB write (Cold) |
| Payment Collection | **Cold Path** | Financial transaction via TigerBeetle |
| Booking Creation | **Hybrid** | Validation (Hot) → Transaction (Cold) |

### MCP Server Requirements

```yaml
# Required MCP servers for Booking & Calendar skills
mcp_servers:
  - uri: mcp://treasury/create_transfer
    purpose: Payment processing via TigerBeetle
  - uri: mcp://temporal/trigger_workflow
    purpose: Booking workflow orchestration
  - uri: mcp://vector/query
    purpose: Property availability RAG
  - uri: mcp://ota/sync_calendar
    purpose: OTA channel synchronization
```

### Database Alignment Clarification

| Data Type | Database | Rationale |
|-----------|----------|-----------|
| Booking metadata | PostgreSQL | Non-financial app data |
| Calendar events | PostgreSQL | Operational data |
| **Payment transactions** | **TigerBeetle** | Financial data (via Formance) |
| Sync status cache | Redis | Ephemeral cache |

> **IMPORTANT**: PostgreSQL is correctly used for booking/calendar **metadata** only. 
> All **payment transactions** flow through TigerBeetle via the Cold Path.

### Infrastructure Alignment

| Incoming Spec | Our Decision | Status |
|---------------|--------------|--------|
| AWS ECS Fargate | ECS/Fargate | ✅ Aligned |
| PostgreSQL 15+ | PostgreSQL (app data) | ✅ Aligned |
| Redis 7+ | Redis | ✅ Aligned |
| Stripe | Stripe Connect | ✅ Aligned |

### Compliance Verification

- ✅ Booking metadata in PostgreSQL (appropriate for non-financial)
- ✅ Payment data routes to TigerBeetle (immutable, auditable)
- ✅ PCI DSS via Stripe tokenization
- ✅ EXCLUSION constraints for data integrity
- ✅ Targets ECS/Fargate deployment

---

*Specification complete. Architecture aligned with Citadel OS reference. Ready for implementation.*

