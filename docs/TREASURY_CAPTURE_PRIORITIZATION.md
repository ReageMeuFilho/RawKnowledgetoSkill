# Treasury Capture Prioritization Guide

> **Purpose**: Prioritize Phase 3 Property Finance skills by treasury capture value
> **Date**: January 2026
> **Total Skills**: 43 (Group 9: Property Finance)
> **Strategic Goal**: Own the financial control plane for property management

---

## 📊 Executive Summary

This document prioritizes the 43 Property Finance skills based on their **treasury capture value**—the ability for Citadel OS to own critical financial workflows, approvals, and fund movements. Skills with higher treasury capture value should be built first.

---

## 🎯 Treasury Capture Value Framework

### Value Rating Definitions

| Rating | Symbol | Description | Revenue Impact | Build Priority |
|--------|--------|-------------|----------------|----------------|
| **CRITICAL** | 🔴 | Direct control over money movement | High recurring | **Build First** |
| **HIGH** | 🟠 | Approval/validation of transactions | Medium | Build Second |
| **MEDIUM** | 🟡 | Financial visibility & reporting | Low direct | Build Third |
| **FOUNDATION** | 🟢 | Enables other treasury functions | Indirect | Build as dependency |

### Treasury Capture Hooks Identified

From the 31 PMS vendor research, we identified these **critical treasury hooks**:

| Hook | Description | Skill(s) | Value |
|------|-------------|----------|-------|
| **AP Approval Ownership** | AI owns invoice approval decisions | SKILL-210 | 🔴 |
| **Owner Payout Execution** | AI calculates and triggers distributions | SKILL-231, 235 | 🔴 |
| **Payment Batch Control** | AI batches and schedules payments | SKILL-232 | 🔴 |
| **Fund Segregation Monitoring** | AI enforces trust compliance | SKILL-220, 225 | 🔴 |
| **Collections Escalation** | AI owns collections workflow | SKILL-216 | 🔴 |
| **Reconciliation Posting** | AI proposes and posts adjustments | SKILL-204 | 🔴 |

---

## 🏆 TIER 1: CRITICAL (Build First) - 11 Skills

These skills provide **direct control over money movement**. They represent the highest revenue potential and competitive moat.

### Tier 1A: Payment Execution (Build Week 1-2)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| **#1** | SKILL-235 | ACH Payment Execution | Execute batch ACH payments | Transaction fee per ACH |
| **#2** | SKILL-231 | Owner Payout Calculation | Calculate and trigger distributions | % of payout volume |
| **#3** | SKILL-232 | Payment Batch Preparation | Group payments for efficiency | Batch processing fee |
| **#4** | SKILL-236 | Payment Reconciliation | Match sent payments to cleared | Included in payment fee |

**Implementation Order Rationale**: 
- SKILL-235 (ACH Execution) enables all other payment skills
- SKILL-231 (Owner Payouts) is the most requested feature by property managers
- SKILL-232 (Batching) reduces costs and improves efficiency
- SKILL-236 (Reconciliation) closes the payment loop

**Code Example - Owner Payout Calculation**:
```python
class OwnerPayoutCalculator:
    def calculate_distribution(self, owner_id: str, period_end: date) -> PayoutResult:
        # Step 1: Get ending cash balance
        cash_balance = self.ledger.get_balance(
            account_type="operating",
            owner_id=owner_id,
            as_of=period_end
        )
        
        # Step 2: Subtract property reserve
        reserve_requirement = self.get_reserve_requirement(owner_id)
        
        # Step 3: Subtract outstanding liabilities
        outstanding_bills = self.ap.get_outstanding_bills(owner_id)
        pending_expenses = self.ap.get_pending_expenses(owner_id)
        
        # Step 4: Calculate available for payout
        available = (
            cash_balance
            - reserve_requirement
            - outstanding_bills
            - pending_expenses
        )
        
        return PayoutResult(
            owner_id=owner_id,
            gross_income=self.get_gross_income(owner_id, period_end),
            total_expenses=self.get_total_expenses(owner_id, period_end),
            reserve_held=reserve_requirement,
            available_for_payout=max(0, available),
            payout_date=self.get_next_payout_date()
        )
```

### Tier 1B: Approval Ownership (Build Week 3-4)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| **#5** | SKILL-210 | Approval Workflow Engine | Own AP approval decisions | Subscription tier feature |
| **#6** | SKILL-201 | Threshold & Limit Config | Set approval thresholds | Enables auto-approval |
| **#7** | SKILL-216 | Collections Workflow Engine | Own collections escalation | Reduces bad debt |

**Implementation Order Rationale**:
- SKILL-210 (Approval Engine) is the core of AP automation
- SKILL-201 (Thresholds) enables auto-approval for routine invoices
- SKILL-216 (Collections) protects AR and reduces write-offs

**Code Example - Approval Workflow Routing**:
```python
class ApprovalRouter:
    def route_invoice(self, invoice: Invoice) -> ApprovalRoute:
        # Rule 1: PO Match - auto-approve if matches PO
        if invoice.po_number:
            po = self.po_service.get(invoice.po_number)
            if po and self.matches_po(invoice, po):
                return ApprovalRoute(
                    type="auto_approve",
                    reason="PO_MATCH",
                    approvers=[]
                )
        
        # Rule 2: Amount-based routing
        thresholds = self.get_thresholds(invoice.property_id)
        
        if invoice.amount <= thresholds.auto_approve_limit:
            return ApprovalRoute(
                type="auto_approve",
                reason="UNDER_THRESHOLD",
                approvers=[]
            )
        
        if invoice.amount <= thresholds.single_approver_limit:
            return ApprovalRoute(
                type="single_approval",
                approvers=[self.get_property_manager(invoice.property_id)]
            )
        
        # Rule 3: High-value requires multi-level
        return ApprovalRoute(
            type="multi_level",
            approvers=[
                self.get_property_manager(invoice.property_id),
                self.get_regional_manager(invoice.property_id),
                self.get_owner(invoice.property_id)
            ]
        )
```

### Tier 1C: Compliance & Trust (Build Week 5-6)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| **#8** | SKILL-220 | Trust Account Compliance | Prevent fund commingling | Compliance = trust |
| **#9** | SKILL-225 | Trust Liability Reconciliation | Validate trust = liabilities | Risk mitigation |
| **#10** | SKILL-204 | Three-Way Bank Reconciliation | Validate all fund movements | Audit requirement |
| **#11** | SKILL-224 | State-Specific Compliance | Apply state trust rules | Legal requirement |

**Implementation Order Rationale**:
- SKILL-220 (Trust Compliance) is legally required in most states
- SKILL-225 (Trust Liability) is the key validation for trust accounting
- SKILL-204 (Three-Way Recon) is the gold standard per AppFolio
- SKILL-224 (State Rules) handles jurisdiction-specific requirements

**Code Example - Three-Way Reconciliation**:
```python
class ThreeWayReconciliation:
    def reconcile(self, bank_account_id: str, as_of_date: date) -> ReconciliationResult:
        # Checkpoint 1: Bank Statement Balance
        bank_statement = self.bank.get_statement(bank_account_id, as_of_date)
        checkpoint_1 = (
            bank_statement.ending_balance
            + bank_statement.deposits_in_transit
            - bank_statement.outstanding_checks
        )
        
        # Checkpoint 2: Bank Book Balance (our ledger)
        book_balance = self.ledger.get_balance(bank_account_id, as_of_date)
        undeposited = self.ledger.get_undeposited_receipts(bank_account_id)
        checkpoint_2 = book_balance + undeposited
        
        # Checkpoint 3: Trust Liability Total (for trust accounts)
        if self.is_trust_account(bank_account_id):
            checkpoint_3 = self.get_trust_liability_total(bank_account_id)
        else:
            checkpoint_3 = checkpoint_2  # For operating accounts, CP2 = CP3
        
        # Validate all three match
        is_balanced = (
            abs(checkpoint_1 - checkpoint_2) < 0.01 and
            abs(checkpoint_2 - checkpoint_3) < 0.01
        )
        
        return ReconciliationResult(
            bank_statement_balance=checkpoint_1,
            book_balance=checkpoint_2,
            trust_liability_total=checkpoint_3,
            is_balanced=is_balanced,
            variance=abs(checkpoint_1 - checkpoint_3),
            exceptions=self.identify_exceptions(bank_account_id, as_of_date)
        )
```

---

## 🟠 TIER 2: HIGH VALUE (Build Second) - 12 Skills

These skills provide **approval and validation** of financial transactions.

### Tier 2A: Invoice Processing (Build Week 7-8)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| #12 | SKILL-208 | Invoice OCR Extraction | Auto-extract invoice data | Time savings |
| #13 | SKILL-209 | Invoice Triage & Coding | Auto-assign GL codes | Accuracy improvement |
| #14 | SKILL-211 | Duplicate Invoice Detection | Prevent double payments | Cost avoidance |
| #15 | SKILL-212 | Vendor Payment Optimization | Recommend best payment method | Fee reduction |

### Tier 2B: AR Management (Build Week 9-10)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| #16 | SKILL-215 | Automated Late Fee Assessment | Policy-based fee calculation | Revenue generation |
| #17 | SKILL-217 | Tenant Ledger Management | Track charges/payments | AR accuracy |
| #18 | SKILL-218 | NSF/Bounced Payment Handler | Reverse + fee assessment | Loss prevention |
| #19 | SKILL-221 | Security Deposit Lifecycle | Receipt → hold → refund | Compliance |

### Tier 2C: Treasury Management (Build Week 11-12)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| #20 | SKILL-233 | Negative Balance Handler | Handle owner negative cash flow | Risk management |
| #21 | SKILL-234 | Cash Flow Forecasting | Predict future cash needs | Planning tool |
| #22 | SKILL-205 | Reconciliation Exception Handler | Smart exception resolution | Efficiency |
| #23 | SKILL-206 | Month-End Close Automation | Period locking, accruals | Time savings |

---

## 🟡 TIER 3: MEDIUM VALUE (Build Third) - 11 Skills

These skills provide **financial visibility and reporting**.

### Tier 3A: Reporting (Build Week 13-14)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| #24 | SKILL-226 | Owner Statement Generation | Itemized income/expense report | Expected feature |
| #25 | SKILL-227 | Owner Packet Automation | Bundle multiple reports | Efficiency |
| #26 | SKILL-228 | Owner Portal Management | Self-service access | Reduces support |
| #27 | SKILL-229 | Scheduled Report Distribution | Auto-generate and email | Automation |
| #28 | SKILL-230 | Budget vs. Actuals Reporting | Variance analysis | Insights |

### Tier 3B: Finance Core (Build Week 15-16)

| Rank | Skill ID | Name | Treasury Hook | Revenue Model |
|------|----------|------|---------------|---------------|
| #29 | SKILL-203 | Transaction Categorization AI | ML-based GL coding | Time savings |
| #30 | SKILL-214 | Rent Roll Generation | Comprehensive rental report | Expected feature |
| #31 | SKILL-219 | Payment Plan Management | Track installment plans | Collections tool |
| #32 | SKILL-222 | HOA Reserve Fund Management | Operating vs. reserves | HOA compliance |
| #33 | SKILL-223 | Reserve Study Integration | Track component funding | HOA planning |
| #34 | SKILL-207 | Year-End/Tax Preparation | Schedule E, 1099 prep | Tax compliance |

---

## 🟢 TIER 4: FOUNDATION (Build as Dependencies) - 9 Skills

These skills **enable other treasury functions** and should be built when needed.

| Rank | Skill ID | Name | Dependency For | Build When |
|------|----------|------|----------------|------------|
| #35 | SKILL-194 | Policy & Permissioning | All skills | Before Week 1 |
| #36 | SKILL-195 | Entity Hierarchy Management | All skills | Before Week 1 |
| #37 | SKILL-196 | GL Account Configuration | SKILL-209, 203 | Before Week 7 |
| #38 | SKILL-197 | Fund Type Definition | SKILL-220, 222 | Before Week 5 |
| #39 | SKILL-198 | Fiscal Period Management | SKILL-206 | Before Week 11 |
| #40 | SKILL-199 | Bank Account Configuration | SKILL-204 | Before Week 5 |
| #41 | SKILL-200 | Audit Log & Decision Trace | All skills | Before Week 1 |
| #42 | SKILL-202 | Integration Credential Management | Bank feeds | Before Week 5 |
| #43 | SKILL-213 | 1099 Vendor Management | SKILL-207 | Before Week 15 |

---

## 📅 Recommended Build Schedule

### Phase 3 Group 9: 16-Week Implementation Plan

```
Week 1-2:   Foundation + Payment Execution (Tier 1A)
            ├── SKILL-194 (Permissions) - Foundation
            ├── SKILL-195 (Entity Hierarchy) - Foundation
            ├── SKILL-200 (Audit Log) - Foundation
            ├── SKILL-235 (ACH Execution) - CRITICAL
            ├── SKILL-231 (Owner Payouts) - CRITICAL
            └── SKILL-232 (Payment Batching) - CRITICAL

Week 3-4:   Approval Ownership (Tier 1B)
            ├── SKILL-210 (Approval Workflow) - CRITICAL
            ├── SKILL-201 (Thresholds) - CRITICAL
            └── SKILL-216 (Collections) - CRITICAL

Week 5-6:   Compliance & Trust (Tier 1C)
            ├── SKILL-197 (Fund Types) - Foundation
            ├── SKILL-199 (Bank Config) - Foundation
            ├── SKILL-220 (Trust Compliance) - CRITICAL
            ├── SKILL-225 (Trust Liability) - CRITICAL
            ├── SKILL-204 (Three-Way Recon) - CRITICAL
            └── SKILL-224 (State Rules) - CRITICAL

Week 7-8:   Invoice Processing (Tier 2A)
            ├── SKILL-196 (GL Config) - Foundation
            ├── SKILL-208 (Invoice OCR) - HIGH
            ├── SKILL-209 (Invoice Coding) - HIGH
            ├── SKILL-211 (Duplicate Detection) - HIGH
            └── SKILL-212 (Payment Optimization) - HIGH

Week 9-10:  AR Management (Tier 2B)
            ├── SKILL-215 (Late Fees) - HIGH
            ├── SKILL-217 (Tenant Ledger) - HIGH
            ├── SKILL-218 (NSF Handler) - HIGH
            └── SKILL-221 (Security Deposits) - HIGH

Week 11-12: Treasury Management (Tier 2C)
            ├── SKILL-198 (Fiscal Periods) - Foundation
            ├── SKILL-233 (Negative Balance) - HIGH
            ├── SKILL-234 (Cash Flow Forecast) - HIGH
            ├── SKILL-205 (Exception Handler) - HIGH
            └── SKILL-206 (Month-End Close) - HIGH

Week 13-14: Reporting (Tier 3A)
            ├── SKILL-226 (Owner Statements) - MEDIUM
            ├── SKILL-227 (Owner Packets) - MEDIUM
            ├── SKILL-228 (Owner Portal) - MEDIUM
            ├── SKILL-229 (Scheduled Reports) - MEDIUM
            └── SKILL-230 (Budget vs. Actuals) - MEDIUM

Week 15-16: Finance Core (Tier 3B)
            ├── SKILL-203 (Categorization AI) - MEDIUM
            ├── SKILL-214 (Rent Roll) - MEDIUM
            ├── SKILL-219 (Payment Plans) - MEDIUM
            ├── SKILL-222 (HOA Reserves) - MEDIUM
            ├── SKILL-223 (Reserve Studies) - MEDIUM
            ├── SKILL-213 (1099 Management) - Foundation
            └── SKILL-207 (Year-End/Tax) - MEDIUM
```

---

## 💰 Treasury Capture Revenue Model

### Revenue Streams by Skill Tier

| Tier | Revenue Model | Example Pricing | Potential ARR (1000 properties) |
|------|---------------|-----------------|--------------------------------|
| **Tier 1 (Critical)** | Transaction fees + Premium tier | $0.50/ACH + $10/property/mo | $180K/year |
| **Tier 2 (High)** | Premium tier unlock | $5/property/mo premium | $60K/year |
| **Tier 3 (Medium)** | Included in base tier | - | Retention value |
| **Tier 4 (Foundation)** | Platform requirement | - | Enables other tiers |

### Treasury Capture Value by Skill

| Skill | Annual Transaction Volume (est.) | Fee Model | Revenue/1000 Properties |
|-------|----------------------------------|-----------|------------------------|
| SKILL-235 (ACH) | 12,000 payments/year | $0.50/payment | $6,000/year |
| SKILL-231 (Payouts) | 12,000 distributions/year | 0.1% of volume | $12,000/year @ $1M volume |
| SKILL-210 (Approvals) | 24,000 invoices/year | Premium tier | Included |
| SKILL-216 (Collections) | 1,200 delinquent/year | Bad debt reduction | 2% of AR recovered |

---

## 🎯 Quick Reference: Build Order

### Must Build First (Week 1-6)
1. SKILL-194 (Permissions) - Foundation
2. SKILL-195 (Entity Hierarchy) - Foundation
3. SKILL-200 (Audit Log) - Foundation
4. **SKILL-235 (ACH Execution)** - 🔴 CRITICAL
5. **SKILL-231 (Owner Payouts)** - 🔴 CRITICAL
6. **SKILL-232 (Payment Batching)** - 🔴 CRITICAL
7. **SKILL-210 (Approval Workflow)** - 🔴 CRITICAL
8. **SKILL-216 (Collections)** - 🔴 CRITICAL
9. **SKILL-220 (Trust Compliance)** - 🔴 CRITICAL
10. **SKILL-204 (Three-Way Recon)** - 🔴 CRITICAL
11. **SKILL-225 (Trust Liability)** - 🔴 CRITICAL

### Total CRITICAL Skills: 11 (26% of Group 9)
### Total HIGH Skills: 12 (28% of Group 9)
### Total Build Time: 16 weeks

---

## ✅ Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| **AP Automation Rate** | 70% auto-approved | Invoices auto-approved / total |
| **AR Collection Rate** | 98% collected within 30 days | On-time payments / total |
| **Trust Compliance** | 100% fund segregation | Zero commingling incidents |
| **Reconciliation Time** | < 2 hours/month/property | Time spent on recon |
| **Owner Payout Accuracy** | 99.9% | Correct payouts / total |
| **Payment Processing Cost** | < $0.30/transaction | Avg cost per payment |

---

**Document Version**: 1.0
**Last Updated**: January 2026
**Next Review**: After Week 6 implementation

