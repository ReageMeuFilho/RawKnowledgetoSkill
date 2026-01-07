# Property Finance Research → Citadel OS Architecture Mapping

> **Purpose**: Map competitor research findings to our established Citadel OS architecture
> **Date**: January 2026
> **Source Research**: `How to Automate Research and Extract Know-How/` folder
> **Companies Analyzed**: 31 PMS vendors

---

## 📊 Executive Summary

This document maps the **350+ skill candidates** and **85+ treasury hooks** identified from competitor research to our **6-layer Citadel OS architecture**. This ensures all new Phase 3 Property Finance skills integrate seamlessly with our existing infrastructure.

---

## 🏗️ Citadel OS Architecture Reminder

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                          CITADEL OS 6-LAYER STACK                               │
├─────────────────────────────────────────────────────────────────────────────────┤
│ Layer 6: APPLICATIONS      │ React/Next.js Dashboards, Mobile Apps             │
├─────────────────────────────────────────────────────────────────────────────────┤
│ Layer 5: DOMAIN BUNDLES    │ STR, LTR, HOA, Hospitality, Finance Bundles       │
├─────────────────────────────────────────────────────────────────────────────────┤
│ Layer 4: SKILLS LAYER      │ AI Agent Skills (SKILL.md), MCP Servers           │
├─────────────────────────────────────────────────────────────────────────────────┤
│ Layer 3: HOT PATH          │ FastAPI, Real-time AI, Sub-second responses       │
├─────────────────────────────────────────────────────────────────────────────────┤
│ Layer 2: COLD PATH         │ TigerBeetle, Formance, Temporal Workflows         │
├─────────────────────────────────────────────────────────────────────────────────┤
│ Layer 1: INFRASTRUCTURE    │ PostgreSQL, Redis, Redpanda, AWS ECS/Fargate      │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🗺️ Research → Architecture Mapping

### Layer 6: Applications (UI/UX)

| Research Finding | Competitor Source | Citadel OS Implementation |
|------------------|-------------------|---------------------------|
| Owner Portal | Guesty, Hostfully, Buildium | React dashboard with real-time updates |
| Owner Statement PDF | AppFolio, RealPage | Server-side PDF generation (react-pdf) |
| Approval Mobile App | AvidXchange | React Native with push notifications |
| Bank Reconciliation UI | AppFolio | Interactive matching interface |
| Collections Dashboard | Vantaca | Kanban-style collections board |
| Invoice Upload | Buildium | Drag-drop with OCR preview |

**Technology Stack**:
- React 19 + TypeScript + Next.js 15
- TailwindCSS 4.1
- React Native (mobile)
- WebSocket for real-time updates

---

### Layer 5: Domain Bundles

| Research Skill Category | Domain Bundle | Skills Included |
|-------------------------|---------------|-----------------|
| **Control Plane** | `finance-core` | SKILL-194 to SKILL-202 |
| **Property Finance Core** | `finance-core` | SKILL-203 to SKILL-207 |
| **Accounts Payable** | `finance-ap` | SKILL-208 to SKILL-213 |
| **Accounts Receivable** | `finance-ar` | SKILL-214 to SKILL-219 |
| **Trust/Reserves** | `finance-trust` | SKILL-220 to SKILL-225 |
| **Owner Reporting** | `finance-reporting` | SKILL-226 to SKILL-230 |
| **Treasury Operations** | `finance-treasury` | SKILL-231 to SKILL-236 |

**Bundle Structure**:
```
skills/
└── finance/
    ├── finance-core/
    │   ├── SKILL-194-policy-permissioning/
    │   ├── SKILL-203-transaction-categorization/
    │   └── SKILL-204-three-way-reconciliation/
    ├── finance-ap/
    │   ├── SKILL-208-invoice-ocr/
    │   └── SKILL-210-approval-workflow/
    ├── finance-ar/
    │   ├── SKILL-214-rent-roll/
    │   └── SKILL-216-collections-workflow/
    ├── finance-trust/
    │   ├── SKILL-220-trust-compliance/
    │   └── SKILL-225-trust-liability-recon/
    ├── finance-reporting/
    │   └── SKILL-226-owner-statements/
    └── finance-treasury/
        ├── SKILL-231-owner-payouts/
        └── SKILL-235-ach-execution/
```

---

### Layer 4: Skills Layer (MCP Servers)

| Research Pattern | MCP Server | Operations |
|------------------|------------|------------|
| **Bank Reconciliation** | `mcp://finance/reconciliation` | `match_transactions`, `propose_matches`, `post_adjustments` |
| **Transaction Categorization** | `mcp://finance/categorization` | `categorize`, `suggest_gl_code`, `train_model` |
| **Invoice Processing** | `mcp://ap/invoice-intake` | `extract_ocr`, `validate`, `create_bill` |
| **Approval Routing** | `mcp://ap/workflow` | `route`, `approve`, `reject`, `escalate` |
| **Collections** | `mcp://ar/collections` | `escalate`, `send_notice`, `create_payment_plan` |
| **Trust Monitoring** | `mcp://trust/compliance` | `check_commingling`, `validate_balances`, `alert` |
| **Owner Payouts** | `mcp://treasury/payouts` | `calculate`, `batch`, `execute`, `reconcile` |
| **Payment Execution** | `mcp://treasury/ach` | `generate_nacha`, `submit`, `track_status` |

**MCP Server Architecture**:
```yaml
# New MCP servers for Property Finance
mcp_servers:
  # Finance Core
  finance-reconciliation:
    protocol: mcp://finance/reconciliation
    methods:
      - ingest_bank_transactions
      - ingest_ledger_entries
      - propose_matches
      - resolve_exception
      - post_adjustments
      - generate_report
    
  finance-categorization:
    protocol: mcp://finance/categorization
    methods:
      - categorize_transaction
      - suggest_gl_code
      - retrain_model
      - get_confidence_score
    
  # Accounts Payable
  ap-invoice:
    protocol: mcp://ap/invoice-intake
    methods:
      - extract_invoice_data
      - validate_invoice
      - detect_duplicate
      - create_bill
    
  ap-workflow:
    protocol: mcp://ap/workflow
    methods:
      - route_for_approval
      - approve
      - reject
      - escalate
      - get_approval_status
    
  # Accounts Receivable
  ar-collections:
    protocol: mcp://ar/collections
    methods:
      - check_delinquency
      - escalate_stage
      - generate_notice
      - create_payment_plan
      - log_activity
    
  # Trust Accounting
  trust-compliance:
    protocol: mcp://trust/compliance
    methods:
      - check_fund_segregation
      - validate_trust_balance
      - detect_commingling
      - generate_compliance_report
    
  # Treasury Operations
  treasury-payouts:
    protocol: mcp://treasury/payouts
    methods:
      - calculate_owner_distribution
      - create_batch
      - execute_batch
      - reconcile_payments
```

---

### Layer 3: Hot Path (Real-time Processing)

| Research Pattern | Hot Path Service | Response Time | Implementation |
|------------------|------------------|---------------|----------------|
| Invoice OCR | `invoice-ocr-service` | < 2s | FastAPI + Amazon Textract |
| Transaction Categorization | `categorization-service` | < 100ms | FastAPI + XGBoost model |
| Approval Routing | `approval-router` | < 50ms | FastAPI + Redis rules cache |
| Delinquency Check | `delinquency-checker` | < 100ms | FastAPI + PostgreSQL |
| Trust Balance Check | `trust-monitor` | < 50ms | FastAPI + TigerBeetle |

**Hot Path Architecture**:
```
┌──────────────────────────────────────────────────────────────────┐
│                      HOT PATH SERVICES                           │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  │
│  │ Invoice OCR     │  │ Categorization  │  │ Approval Router │  │
│  │ FastAPI         │  │ FastAPI + ML    │  │ FastAPI + Redis │  │
│  │ < 2s response   │  │ < 100ms         │  │ < 50ms          │  │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘  │
│           │                    │                    │            │
│           └────────────────────┼────────────────────┘            │
│                                │                                 │
│                    ┌───────────┴───────────┐                    │
│                    │    Rust/Axum Gateway  │                    │
│                    │    (Rate Limiting)    │                    │
│                    └───────────────────────┘                    │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

### Layer 2: Cold Path (Financial Guarantees)

| Research Pattern | Cold Path Component | Guarantee | Implementation |
|------------------|---------------------|-----------|----------------|
| **Three-Way Reconciliation** | TigerBeetle | Exact balance matching | VSR consensus |
| **Trust Fund Segregation** | Formance Ledger | Fund isolation | Numscript DSL |
| **Approval Workflows** | Temporal | Durable execution | Workflow as code |
| **Payment Batching** | Temporal | Reliable delivery | Activity retries |
| **ACH Execution** | Temporal + TigerBeetle | Double-entry guarantee | Saga pattern |
| **Owner Payouts** | Formance | Audit trail | Numscript transactions |

**Cold Path Architecture**:
```
┌──────────────────────────────────────────────────────────────────┐
│                      COLD PATH SERVICES                          │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    TIGERBEETLE LEDGER                       ││
│  │  • 1M+ TPS financial transactions                          ││
│  │  • Strict serializability (VSR consensus)                  ││
│  │  • Trust account balances                                  ││
│  │  • Owner distributions                                     ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    FORMANCE LEDGER                          ││
│  │  • Bank-grade double-entry accounting                      ││
│  │  • Numscript DSL for transactions                          ││
│  │  • Fund segregation enforcement                            ││
│  │  • Audit trail (immutable)                                 ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    TEMPORAL WORKFLOWS                       ││
│  │  • Approval workflow orchestration                         ││
│  │  • Payment batch processing                                ││
│  │  • Collections escalation                                  ││
│  │  • Month-end close automation                              ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Numscript Example (Fund Segregation)**:
```numscript
// Prevent commingling - only allow transfers within same fund type
vars {
  account $source
  account $destination
  monetary $amount
}

precondition {
  // Source and destination must be same fund type
  $source.metadata.fund_type == $destination.metadata.fund_type
}

send $amount (
  source = $source
  destination = $destination
)
```

**Temporal Workflow Example (AP Approval)**:
```python
@workflow.defn
class InvoiceApprovalWorkflow:
    @workflow.run
    async def run(self, invoice_id: str) -> ApprovalResult:
        # Step 1: Route invoice based on rules
        routing = await workflow.execute_activity(
            route_invoice,
            invoice_id,
            start_to_close_timeout=timedelta(minutes=5)
        )
        
        # Step 2: Wait for approval (with timeout)
        approval = await workflow.wait_condition(
            lambda: self.approval_received,
            timeout=timedelta(days=7)
        )
        
        # Step 3: If approved, execute payment
        if approval.approved:
            payment = await workflow.execute_activity(
                execute_payment,
                invoice_id,
                start_to_close_timeout=timedelta(minutes=30)
            )
            return ApprovalResult(approved=True, payment_id=payment.id)
        
        return ApprovalResult(approved=False, reason=approval.reason)
```

---

### Layer 1: Infrastructure

| Research Requirement | Infrastructure Component | Configuration |
|---------------------|--------------------------|---------------|
| **Bank Transaction Data** | PostgreSQL | `bank_transactions` table |
| **Ledger Entries** | TigerBeetle | Account balances |
| **Invoice Documents** | AWS S3 | `invoices/` bucket |
| **Approval States** | PostgreSQL | `approval_workflows` table |
| **Collections History** | PostgreSQL | `collections_activities` table |
| **Trust Balances** | TigerBeetle | Trust fund accounts |
| **Audit Logs** | PostgreSQL (partitioned) | `audit_events` table |
| **ML Models** | S3 + SageMaker | Categorization model |
| **Event Streaming** | Redpanda | Financial events |
| **Caching** | Redis | GL codes, vendor lookups |

**Database Schema (PostgreSQL)**:
```sql
-- Bank Reconciliation
CREATE TABLE bank_transactions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    bank_account_id UUID NOT NULL REFERENCES bank_accounts(id),
    transaction_date DATE NOT NULL,
    amount DECIMAL(15,2) NOT NULL,
    description TEXT,
    reference_number VARCHAR(100),
    status VARCHAR(20) DEFAULT 'pending', -- pending, matched, exception
    matched_ledger_entry_id UUID,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- AP Invoices
CREATE TABLE invoices (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    vendor_id UUID NOT NULL REFERENCES vendors(id),
    property_id UUID REFERENCES properties(id),
    invoice_number VARCHAR(100),
    invoice_date DATE NOT NULL,
    due_date DATE,
    amount DECIMAL(15,2) NOT NULL,
    gl_account_id UUID REFERENCES gl_accounts(id),
    status VARCHAR(20) DEFAULT 'draft', -- draft, pending_approval, approved, paid
    ocr_confidence DECIMAL(5,2),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Approval Workflows
CREATE TABLE approval_workflows (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    entity_type VARCHAR(50) NOT NULL, -- invoice, payout, adjustment
    entity_id UUID NOT NULL,
    current_stage INT DEFAULT 1,
    status VARCHAR(20) DEFAULT 'pending', -- pending, approved, rejected
    temporal_workflow_id VARCHAR(255),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE TABLE approval_stages (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    workflow_id UUID NOT NULL REFERENCES approval_workflows(id),
    stage_number INT NOT NULL,
    approver_id UUID NOT NULL REFERENCES users(id),
    status VARCHAR(20) DEFAULT 'pending',
    decision_at TIMESTAMP WITH TIME ZONE,
    comments TEXT
);

-- Collections
CREATE TABLE collections_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL REFERENCES tenants(id),
    property_id UUID NOT NULL REFERENCES properties(id),
    current_stage VARCHAR(50) DEFAULT 'current', -- current, late, notice, legal
    balance_due DECIMAL(15,2) NOT NULL,
    days_past_due INT DEFAULT 0,
    last_payment_date DATE,
    next_action_date DATE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE TABLE collections_activities (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    collections_account_id UUID NOT NULL REFERENCES collections_accounts(id),
    activity_type VARCHAR(50) NOT NULL, -- notice_sent, call_made, payment_plan_created
    activity_date TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    notes TEXT,
    document_id UUID REFERENCES documents(id)
);

-- Trust Accounting
CREATE TABLE trust_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    bank_account_id UUID NOT NULL REFERENCES bank_accounts(id),
    fund_type VARCHAR(50) NOT NULL, -- operating, security_deposit, reserve
    property_id UUID REFERENCES properties(id),
    balance DECIMAL(15,2) NOT NULL DEFAULT 0,
    last_reconciled_at TIMESTAMP WITH TIME ZONE
);

CREATE TABLE trust_liabilities (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    trust_account_id UUID NOT NULL REFERENCES trust_accounts(id),
    entity_type VARCHAR(50) NOT NULL, -- tenant, owner
    entity_id UUID NOT NULL,
    amount DECIMAL(15,2) NOT NULL,
    description TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

---

## 🔄 Execution Path Classification

| Skill | Execution Path | Rationale |
|-------|----------------|-----------|
| **SKILL-203** Transaction Categorization | **HOT** | ML inference < 100ms |
| **SKILL-204** Three-Way Reconciliation | **HYBRID** | Hot: matching; Cold: posting |
| **SKILL-208** Invoice OCR | **HOT** | OCR service, sub-2s |
| **SKILL-210** Approval Workflow | **COLD** | Durable, multi-day workflows |
| **SKILL-216** Collections Workflow | **COLD** | State machine, notifications |
| **SKILL-220** Trust Compliance | **COLD** | Financial guarantee required |
| **SKILL-231** Owner Payouts | **COLD** | Financial transaction |
| **SKILL-235** ACH Execution | **COLD** | Bank integration, audit |

---

## 🔗 Integration Points with Existing Skills

| New Skill | Integrates With | Integration Pattern |
|-----------|-----------------|---------------------|
| SKILL-204 (Reconciliation) | SKILL-031 (Payment Reconciliation) | Extends with three-way |
| SKILL-210 (AP Workflow) | SKILL-059 (Permission Management) | Uses RBAC for approvers |
| SKILL-216 (Collections) | SKILL-061 (Notifications) | Sends collection notices |
| SKILL-220 (Trust Compliance) | SKILL-060 (Audit Logging) | Logs compliance events |
| SKILL-231 (Owner Payouts) | SKILL-035 (Payout Processing) | Extends with calculation |
| SKILL-226 (Owner Statements) | SKILL-042 (Analytics Dashboard) | Data source |

---

## 📈 Research Source → Architecture Mapping Summary

| Research Source | Skill IDs | Layer 2 (Cold) | Layer 3 (Hot) | Layer 4 (MCP) |
|-----------------|-----------|----------------|---------------|---------------|
| **AppFolio** | 204, 206, 220 | TigerBeetle, Formance | - | finance/reconciliation |
| **AvidXchange** | 208-213 | Temporal | FastAPI OCR | ap/workflow |
| **Buildium/RealPage** | 214-219, 220-225 | Formance | - | ar/collections |
| **Stessa** | 203, 207 | - | FastAPI ML | finance/categorization |
| **Landlord Finance OS** | 231-236 | TigerBeetle, Temporal | - | treasury/payouts |
| **Vantaca** | 222, 223 | Formance | - | trust/reserves |
| **Zego** | 232, 235 | Temporal | - | treasury/ach |

---

## ✅ Architecture Alignment Checklist

For each Phase 3 Group 9 skill, verify:

- [ ] **Layer Assignment**: Skill assigned to correct layer
- [ ] **MCP Server**: Protocol and methods defined
- [ ] **Execution Path**: Hot/Cold/Hybrid classified
- [ ] **Data Storage**: PostgreSQL vs TigerBeetle determined
- [ ] **Workflow Orchestration**: Temporal workflow if Cold path
- [ ] **Integration**: Connected to existing skills
- [ ] **Compliance**: Audit logging, fund segregation enforced

---

**Document Version**: 1.0
**Last Updated**: January 2026
**Author**: Cursor AI

