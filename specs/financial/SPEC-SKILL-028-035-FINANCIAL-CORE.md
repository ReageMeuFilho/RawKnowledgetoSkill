# Final Skill Specification: Financial Core System

**Skills**: SKILL-028, SKILL-029, SKILL-030, SKILL-031, SKILL-032, SKILL-035
**Category**: Financial Core
**Priority**: P0 (MVP Critical)
**Status**: SPECIFIED
**Date**: January 7, 2026
**Source**: ES-PHASE1-GROUP4-financial-core.md (7,568 lines)

---

## Executive Summary

This specification covers six foundational financial skills that form the Treasury Operating System (Treasury OS) for property management platforms. Built on **TigerBeetle** (1M+ TPS financial database) and **Formance** (programmable double-entry ledger), these skills deliver mission-critical payment processing, trust accounting, and automated payouts.

**Business Impact**: 
- Saves property managers **150 hours/year** through automation
- Handles **8,000+ transactions per query** with zero locks
- Ensures **100% trust account segregation** for compliance
- Supports **135+ currencies** and **40+ payment methods**

---

## SKILL-028: Payment Collection

### Overview
Multi-method payment collection system supporting credit cards, ACH, PIX (Brazil), SEPA (EU), and wire transfers with split payment capabilities across methods, guests, and installments.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Multi-Method Splitting** | Single booking across multiple cards/methods | Real-time processing |
| **Regional Payment Support** | ACH, PIX, SEPA, credit cards | 135+ currencies |
| **Automated Scheduling** | 50% at booking, 50% 30 days before | Configurable rules |
| **Failed Payment Retry** | Intelligent dunning sequences | 3-5 retry attempts |

### Technical Implementation

```python
# Payment Collection Service Architecture
class PaymentCollectionEngine:
    """
    TigerBeetle-backed payment collection with atomic transactions.
    Supports split payments, regional methods, and automated scheduling.
    """
    
    supported_methods = {
        'credit_card': ['visa', 'mastercard', 'amex', 'discover'],
        'debit': ['ach', 'sepa', 'bacs'],
        'instant': ['pix', 'apple_pay', 'google_pay'],
        'wire': ['domestic', 'international']
    }
    
    performance_targets = {
        'transaction_throughput': '8,000+ per query',
        'processing_latency': '<100ms (95th percentile)',
        'availability': '99.9%',
        'split_payment_limit': '10 methods per booking'
    }
```

### Database Schema (TigerBeetle)

```sql
-- TigerBeetle Account Structure
-- Native debit/credit schema ensuring double-entry compliance

Account {
    id: UUID,                    -- Unique account identifier
    ledger: uint32,              -- Currency/asset type partition
    code: uint16,                -- Account type (asset, liability, etc.)
    flags: uint16,               -- Account behavior flags
    debits_pending: uint128,     -- Pending debit amount
    debits_posted: uint128,      -- Posted debit amount
    credits_pending: uint128,    -- Pending credit amount
    credits_posted: uint128,     -- Posted credit amount
    user_data: bytes[128]        -- Custom metadata
}

Transfer {
    id: UUID,                    -- Idempotent transfer ID
    debit_account_id: UUID,      -- Source account
    credit_account_id: UUID,     -- Destination account
    amount: uint128,             -- Transfer amount (immutable)
    pending_id: UUID,            -- For two-phase commits
    user_data: bytes[128],       -- Custom metadata
    timeout: uint32,             -- Pending transfer timeout
    ledger: uint32,              -- Must match account ledgers
    code: uint16,                -- Transfer type code
    flags: uint16                -- Transfer behavior flags
}
```

### Integration Points

| Provider | Integration Type | Purpose | Compliance |
|----------|-----------------|---------|------------|
| **Stripe Connect** | REST API + Webhooks | Card processing, Apple/Google Pay | PCI DSS Level 1 |
| **Plaid** | REST API | ACH verification, bank linking | SOC 2 Type II |
| **PIX (Brazil)** | QR Code + API | Instant payments | BACEN regulated |
| **SEPA (EU)** | XML messages | Euro transfers | PSD2 compliant |

### Acceptance Criteria
- [ ] Process credit card payments with <3s response time
- [ ] Support split payments across up to 10 methods
- [ ] Handle regional payments (ACH, PIX, SEPA)
- [ ] Implement intelligent retry logic for failed payments
- [ ] All transactions recorded in TigerBeetle with immutable audit trail

---

## SKILL-029: Refund Processing

### Overview
Automated refund workflows with configurable cancellation policies, approval workflows, and partial refund calculations including tax handling.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Policy Engine** | Strict, moderate, flexible policies | Instant calculation |
| **Partial Refunds** | Pro-rata with fee retention | Accurate to cent |
| **Approval Workflows** | Threshold-based routing | <24 hour processing |
| **Tax Handling** | Jurisdiction-aware refunds | Multi-state compliant |

### Refund Policy Configuration

```python
# Refund Policy Engine
class RefundPolicyEngine:
    """
    Configurable refund policies with Formance Numscript DSL.
    Immutable refund records in TigerBeetle.
    """
    
    policies = {
        'strict': {
            'full_refund_window': 0,      # No full refunds
            'partial_refund_window': 7,    # 7 days before
            'cancellation_fee': 0.50       # 50% fee
        },
        'moderate': {
            'full_refund_window': 7,       # 7 days before
            'partial_refund_window': 3,    # 3 days before
            'cancellation_fee': 0.25       # 25% fee
        },
        'flexible': {
            'full_refund_window': 24,      # 24 hours before
            'partial_refund_window': 0,    # Up to check-in
            'cancellation_fee': 0.10       # 10% fee
        }
    }
```

### Formance Numscript Example

```numscript
// Partial refund with fee retention
vars {
  account $guest
  account $platform
  account $owner
  monetary $refund_amount
  monetary $platform_fee
}

send $refund_amount (
  source = $platform
  destination = $guest
)

// Retain platform fee
send $platform_fee (
  source = $owner
  destination = $platform
)
```

### Acceptance Criteria
- [ ] Automatically calculate refunds based on policy and timing
- [ ] Support partial refunds with fee retention logic
- [ ] Route refunds through approval workflow when above threshold
- [ ] Handle tax refunds based on jurisdiction
- [ ] Maintain immutable refund audit trail

---

## SKILL-030: Security Deposit Handling

### Overview
Advanced pre-authorization management with Virtual Credit Card processing, authorization holds, and damage claim workflows with evidence documentation.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Authorization Holds** | Card network compliant | 5-second response |
| **VCC Processing** | Virtual Credit Cards | Full lifecycle |
| **Damage Claims** | Evidence-based workflow | Photo documentation |
| **Hold Extensions** | Before expiration | Network limits |

### Authorization Hold Lifecycle

```python
# Security Deposit State Machine
class SecurityDepositStateMachine:
    """
    Manages authorization holds with card network compliance.
    """
    
    states = [
        'PENDING_AUTHORIZATION',
        'AUTHORIZED',
        'EXTENDED',
        'CAPTURED',          # Damage claim
        'RELEASED',          # No damage
        'EXPIRED',           # Auto-release
        'DISPUTED'           # Guest dispute
    ]
    
    hold_limits = {
        'visa': {'max_days': 31, 'extension': True},
        'mastercard': {'max_days': 30, 'extension': True},
        'amex': {'max_days': 90, 'extension': False},
        'discover': {'max_days': 10, 'extension': True}
    }
```

### Damage Claim Schema

```json
{
  "claim_id": "uuid",
  "deposit_id": "uuid",
  "property_id": "uuid",
  "guest_id": "uuid",
  "claim_amount": 500.00,
  "currency": "USD",
  "evidence": [
    {
      "type": "photo",
      "url": "s3://evidence/claim-123/damage-1.jpg",
      "description": "Broken window in bedroom",
      "timestamp": "2026-01-07T10:30:00Z"
    }
  ],
  "status": "PENDING_REVIEW",
  "created_at": "2026-01-07T10:30:00Z"
}
```

### Acceptance Criteria
- [ ] Place authorization holds with <5s response time
- [ ] Track and extend holds before expiration
- [ ] Convert holds to charges for damage claims
- [ ] Require photo evidence for damage claims
- [ ] Handle guest disputes with evidence trail

---

## SKILL-031: Payment Reconciliation

### Overview
Automated settlement and payout reconciliation with OTA payout parsing, intelligent matching algorithms, and discrepancy flagging.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Automated Matching** | 95%+ auto-match rate | Real-time |
| **OTA Parsing** | Airbnb, Vrbo, Booking.com | All major formats |
| **Discrepancy Flagging** | Within 24 hours | Prioritized queue |
| **Variance Analysis** | Daily/monthly reports | Automated generation |

### Reconciliation Engine

```python
# Formance Native Reconciliation
class ReconciliationEngine:
    """
    Integrated account-based reconciliation providing automated
    monitoring of funds under management in ledger vs their
    accurate and exact existence on financial partners.
    """
    
    matching_rules = [
        {'field': 'amount', 'tolerance': 0.01},
        {'field': 'date', 'tolerance_days': 3},
        {'field': 'reference', 'fuzzy_match': 0.85},
        {'field': 'guest_name', 'fuzzy_match': 0.90}
    ]
    
    ota_parsers = {
        'airbnb': AirbnbPayoutParser,
        'vrbo': VrboPayoutParser,
        'booking_com': BookingComPayoutParser
    }
    
    performance = {
        'auto_match_rate': '>95%',
        'processing_rate': '10,000 transactions/hour',
        'discrepancy_sla': '<24 hours'
    }
```

### Reconciliation Workflow

```
Bank Statement Import → Parse OTA Payouts → Match Transactions
        ↓                      ↓                    ↓
   Validate Format       Extract Details      Confidence Score
        ↓                      ↓                    ↓
   Store in System       Map to Bookings     Auto-Match (>95%)
                                                   ↓
                              ┌─────────────────────┴─────────────────────┐
                              ↓                                           ↓
                         Matched (✓)                              Unmatched (?)
                              ↓                                           ↓
                      Update Ledger                           Flag for Review
                              ↓                                           ↓
                      Generate Report                         Manual Resolution
```

### Acceptance Criteria
- [ ] Automatically match 95%+ of bank transactions to bookings
- [ ] Flag unmatched transactions within 24 hours
- [ ] Generate daily/monthly reconciliation reports
- [ ] Parse OTA payout files from all major platforms
- [ ] Eliminate data drifts between systems

---

## SKILL-032: Owner Ledger Management

### Overview
Trust/escrow accounting model with separate bank accounts ensuring compliance with state landlord-tenant laws, plus professional owner statement generation.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Trust Account Segregation** | 100% fund separation | Legal compliance |
| **Owner Statements** | Professional monthly reports | <24hr generation |
| **Multi-Owner Support** | Profit sharing splits | Percentage-based |
| **Expense Tracking** | Property-level costs | Real-time updates |

### Trust Account Architecture

```python
# Trust Account Segregation Model
class TrustAccountManager:
    """
    TigerBeetle ensures sum of debits and credits over all
    accounts is zero at all times - perfect for trust accounting.
    """
    
    account_structure = {
        'operating': 'Platform operational funds',
        'trust': {
            'escrow': 'Guest deposits held in trust',
            'owner_funds': 'Per-owner segregated balances',
            'security_deposits': 'Held security deposits'
        }
    }
    
    compliance = {
        'fund_commingling': 'PROHIBITED',
        'segregation_audit': 'DAILY',
        'statement_frequency': 'MONTHLY'
    }
```

### Owner Statement Schema

```json
{
  "statement_id": "uuid",
  "owner_id": "uuid",
  "period": {
    "start": "2026-01-01",
    "end": "2026-01-31"
  },
  "properties": [
    {
      "property_id": "uuid",
      "name": "Beach House #1",
      "income": {
        "rental_income": 5000.00,
        "cleaning_fees": 300.00,
        "pet_fees": 100.00,
        "total": 5400.00
      },
      "expenses": {
        "platform_fee": 540.00,
        "cleaning_cost": 200.00,
        "maintenance": 150.00,
        "total": 890.00
      },
      "net_income": 4510.00
    }
  ],
  "summary": {
    "total_income": 5400.00,
    "total_expenses": 890.00,
    "net_payout": 4510.00,
    "payout_date": "2026-02-01"
  }
}
```

### Acceptance Criteria
- [ ] Maintain separate trust accounts for each owner
- [ ] Record all property-related financial transactions
- [ ] Generate monthly statements within 24 hours
- [ ] Support multi-owner properties with profit sharing
- [ ] Prevent fund commingling at all times

---

## SKILL-035: Payout Processing

### Overview
Automated disbursement calculations (income - expenses - fees) with rolling reserve management, multi-currency support, and international wire capabilities.

### Key Features

| Feature | Description | Performance Target |
|---------|-------------|-------------------|
| **Automated Calculations** | Income - expenses - fees | Real-time |
| **Rolling Reserves** | Risk-based holdbacks | Configurable % |
| **Multi-Currency** | 135+ currencies | FX optimization |
| **International Wires** | 118+ countries | Stripe Connect |

### Payout Calculation Engine

```python
# Payout Processing Engine
class PayoutEngine:
    """
    Automated payout calculations with Temporal workflow orchestration.
    Supports multi-currency with 135+ currencies via Stripe Connect.
    """
    
    calculation_formula = """
    PAYOUT = GROSS_INCOME 
           - PLATFORM_FEE 
           - OWNER_EXPENSES 
           - ROLLING_RESERVE 
           - UNPAID_BALANCES
    """
    
    payout_schedules = {
        'weekly': {'day': 'monday', 'minimum': 100.00},
        'biweekly': {'day': '1st,15th', 'minimum': 250.00},
        'monthly': {'day': '1st', 'minimum': 500.00}
    }
    
    reserve_rules = {
        'new_owner': {'percentage': 0.10, 'duration_days': 90},
        'established': {'percentage': 0.05, 'duration_days': 30},
        'premium': {'percentage': 0.00, 'duration_days': 0}
    }
```

### Temporal Payout Workflow

```python
@workflow.defn
class PayoutWorkflow:
    """
    Temporal treats API interactions as Activities that retry
    automatically and recover seamlessly.
    """
    
    @workflow.run
    async def run(self, owner_id: str, period_end: date):
        # Step 1: Calculate payout amount
        payout = await workflow.execute_activity(
            calculate_payout,
            owner_id, period_end,
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        # Step 2: Check minimum threshold
        if payout.amount < payout.minimum_threshold:
            return PayoutResult(status='BELOW_MINIMUM', held=True)
        
        # Step 3: Apply rolling reserve
        reserve = await workflow.execute_activity(
            apply_reserve,
            owner_id, payout.amount,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        # Step 4: Execute disbursement
        disbursement = await workflow.execute_activity(
            execute_disbursement,
            owner_id, payout.amount - reserve.amount,
            start_to_close_timeout=timedelta(minutes=10)
        )
        
        # Step 5: Record in TigerBeetle
        await workflow.execute_activity(
            record_payout,
            disbursement,
            start_to_close_timeout=timedelta(minutes=2)
        )
        
        return PayoutResult(status='COMPLETED', transaction_id=disbursement.id)
```

### Acceptance Criteria
- [ ] Calculate payouts as income minus expenses minus fees
- [ ] Support weekly/biweekly/monthly payout schedules
- [ ] Handle minimum payout thresholds
- [ ] Support multi-currency international payouts
- [ ] Manage rolling reserves based on owner risk profile

---

## Technology Stack Summary

| Layer | Technology | Version | Purpose |
|-------|------------|---------|---------|
| **Financial Database** | TigerBeetle | 0.16.67 | 1M+ TPS, immutable ledger |
| **Programmable Accounting** | Formance | Latest | Numscript DSL, reconciliation |
| **Workflow Orchestration** | Temporal | 1.8.0+ | Durable execution, 99.9% SLA |
| **Payment Processing** | Stripe Connect | Latest | 15,000+ platforms, 135+ currencies |
| **Banking Integration** | Plaid | 12.0+ | ACH, bank verification |
| **API Framework** | FastAPI | 0.104+ | High-performance async |
| **Infrastructure** | Kubernetes | 1.31+ | Multi-cloud deployment |

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        FINANCIAL CORE SYSTEM (Treasury OS)                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐                  │
│  │   Stripe     │    │    Plaid     │    │  OTA APIs    │  Integrations   │
│  │   Connect    │    │   Banking    │    │ (Airbnb,etc) │                  │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘                  │
│         │                   │                   │                          │
│         └───────────────────┼───────────────────┘                          │
│                             │                                              │
│                    ┌────────▼────────┐                                     │
│                    │  Temporal       │                                     │
│                    │  Workflows      │   Orchestration Layer               │
│                    └────────┬────────┘                                     │
│                             │                                              │
│  ┌──────────────────────────┼──────────────────────────┐                  │
│  │                          │                          │                  │
│  │  ┌──────────┐   ┌────────▼────────┐   ┌──────────┐ │                  │
│  │  │ Payment  │   │   Formance      │   │  Payout  │ │  Financial      │
│  │  │Collection│   │   Ledger        │   │Processing│ │  Skills Layer   │
│  │  │(SKILL-28)│   │(Programmable)   │   │(SKILL-35)│ │                  │
│  │  └────┬─────┘   └────────┬────────┘   └────┬─────┘ │                  │
│  │       │                  │                  │       │                  │
│  │  ┌────▼─────┐   ┌────────▼────────┐   ┌────▼─────┐ │                  │
│  │  │ Refund   │   │   TigerBeetle   │   │  Owner   │ │                  │
│  │  │Processing│   │    (1M+ TPS)    │   │  Ledger  │ │                  │
│  │  │(SKILL-29)│   │  Immutable DB   │   │(SKILL-32)│ │                  │
│  │  └────┬─────┘   └────────┬────────┘   └────┬─────┘ │                  │
│  │       │                  │                  │       │                  │
│  │  ┌────▼─────┐            │            ┌────▼─────┐ │                  │
│  │  │ Security │            │            │ Recon-   │ │                  │
│  │  │ Deposits │            │            │ ciliation│ │                  │
│  │  │(SKILL-30)│            │            │(SKILL-31)│ │                  │
│  │  └──────────┘            │            └──────────┘ │                  │
│  │                          │                          │                  │
│  └──────────────────────────┼──────────────────────────┘                  │
│                             │                                              │
│                    ┌────────▼────────┐                                     │
│                    │  Trust Accounts │                                     │
│                    │  (Segregated)   │   Compliance Layer                  │
│                    └─────────────────┘                                     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Performance SLAs

| Metric | Target | Critical Threshold |
|--------|--------|-------------------|
| Transaction Throughput | 8,000+ per query | <1,000 |
| Processing Latency | <100ms (95th) | >500ms |
| Reconciliation Accuracy | 99.99% auto-match | <95% |
| System Availability | 99.9% | <99% |
| Payout Processing | <10 seconds | >60 seconds |
| Trust Account Segregation | 100% | Any commingling |

---

## Compliance Requirements

| Regulation | Scope | Implementation |
|------------|-------|----------------|
| **PCI DSS Level 1** | Card data handling | Stripe tokenization |
| **SOC 2 Type II** | Data security | Plaid integration |
| **State Trust Laws** | Fund segregation | Separate accounts |
| **PSD2 (EU)** | European payments | SEPA compliance |
| **BACEN (Brazil)** | PIX payments | Central bank API |
| **AML/KYC** | Identity verification | Alloy integration |

---

## Implementation Timeline

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Week 1-2** | Foundation | TigerBeetle + Formance setup |
| **Week 3-4** | Payment Collection | Stripe Connect, multi-method |
| **Week 5-6** | Refund & Deposits | Policy engine, holds |
| **Week 7-8** | Reconciliation | OTA parsing, matching |
| **Week 9-10** | Owner Ledger | Trust accounting, statements |
| **Week 11-12** | Payouts | Calculations, scheduling |
| **Week 13-14** | Integration | Temporal workflows, testing |
| **Week 15-16** | Compliance | Audit, security review |

**Total: 16 weeks to production-ready MVP**

---

## Testing Requirements

| Test Type | Coverage Target | Focus Areas |
|-----------|-----------------|-------------|
| Unit Tests | 90% | Financial calculations, policy logic |
| Integration Tests | 85% | Stripe, Plaid, OTA APIs |
| E2E Tests | Critical paths | Payment → Statement → Payout |
| Load Tests | 10,000 TPS | TigerBeetle stress testing |
| Security Tests | PCI DSS | Tokenization, encryption |
| Compliance Tests | 100% | Trust account segregation |

---

## Cost Estimates

| Environment | Compute | Storage | Network | Total/Month |
|-------------|---------|---------|---------|-------------|
| Development | $2,500 | $500 | $200 | $3,200 |
| Staging | $5,000 | $1,000 | $500 | $6,500 |
| Production | $15,000 | $3,000 | $2,000 | $20,000 |
| DR | $3,000 | $1,500 | $500 | $5,000 |
| **Total** | $25,500 | $6,000 | $3,200 | **$34,700** |

---

## Risk Mitigation

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| Payment processor outage | Low | Critical | Multi-processor failover |
| Trust account commingling | Very Low | Critical | Database-level constraints |
| OTA API changes | Medium | High | Version monitoring, adapters |
| Currency conversion errors | Low | High | Real-time rate validation |
| Reconciliation failures | Medium | Medium | Manual review queue |

---

## 📐 Architecture Alignment Notes

### Citadel OS Layer Mapping

| Spec Component | Citadel Layer | Technology | Aligned |
|----------------|---------------|------------|---------|
| Payment Processing | Layer 3B (Cold Path) | TigerBeetle via Formance | ✅ |
| Workflow Orchestration | Layer 3B (Cold Path) | Temporal | ✅ |
| API Gateway | Layer 2 | Rust/Axum (external), FastAPI (internal) | ✅ |
| Business Logic | Layer 4 (Skills) | Skill Scripts (Python) | ✅ |
| Event Streaming | Layer 2 | Redpanda | ✅ |

### Execution Path Classification

| Operation | Path | Rationale |
|-----------|------|-----------|
| Payment Collection | **Cold Path** | Financial guarantee required, TigerBeetle |
| Refund Calculation | **Hybrid** | Policy logic (Hot) → Transaction (Cold) |
| Authorization Holds | **Cold Path** | Card network compliance |
| Reconciliation | **Cold Path** | Formance Native, audit trail |
| Owner Statements | **Hybrid** | Report generation (Hot) → Ledger (Cold) |
| Payout Processing | **Cold Path** | Temporal workflow, TigerBeetle |

### MCP Server Requirements

```yaml
# Required MCP servers for Financial Core skills
mcp_servers:
  - uri: mcp://treasury/create_transfer
    purpose: TigerBeetle transfer creation
  - uri: mcp://treasury/query_balance
    purpose: Account balance queries
  - uri: mcp://formance/execute_numscript
    purpose: Programmable accounting logic
  - uri: mcp://temporal/trigger_workflow
    purpose: Payout workflow initiation
  - uri: mcp://temporal/query_workflow
    purpose: Workflow status queries
```

### Infrastructure Alignment

| Incoming Spec | Our Decision | Adjustment Needed |
|---------------|--------------|-------------------|
| Kubernetes 1.31+ | **ECS/Fargate** | ✅ Use ECS/Fargate, not EKS |
| TigerBeetle | TigerBeetle on EC2 | ✅ Aligned (EC2 for TigerBeetle) |
| Formance | Formance Cloud | ✅ Aligned |
| Temporal | Temporal Cloud | ✅ Aligned |
| Multi-cloud | AWS Primary | ✅ AWS with Brazil edge |

### Compliance Verification

- ✅ Financial data stored in TigerBeetle (immutable, auditable)
- ✅ Accounting logic in Formance Numscript (compliance as code)
- ✅ Workflows in Temporal (durable, recoverable)
- ✅ Trust accounting via Formance segregation
- ✅ PCI DSS via Stripe tokenization (no raw card data)

---

*Specification complete. Architecture aligned with Citadel OS reference. Ready for implementation.*

