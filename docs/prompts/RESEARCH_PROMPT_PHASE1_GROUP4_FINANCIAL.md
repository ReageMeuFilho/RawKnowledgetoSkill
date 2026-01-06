# Research Prompt: Phase 1 Group 4 - Financial Core

## 🎯 RESEARCH OBJECTIVE

Research and document the **6 financial core skills**. This is CRITICAL as it directly integrates with our Treasury OS (TigerBeetle + Formance) deployment in Q2 2025.

---

## ⚠️ IMPORTANT CONTEXT

**We already have Treasury OS infrastructure:**
- **TigerBeetle**: High-throughput ledger (1M+ TPS)
- **Formance**: Programmable double-entry accounting
- **Temporal**: Workflow orchestration for financial operations

The research should focus on **WHAT** these skills do (business logic, user flows, rules) rather than **HOW** to build a ledger (we have that).

---

## 📋 SKILLS TO RESEARCH

| Skill ID | Name | Priority | Category |
|----------|------|----------|----------|
| SKILL-028 | payment-collection | P0 | financial |
| SKILL-029 | refund-processing | P0 | financial |
| SKILL-030 | security-deposit-handling | P0 | financial |
| SKILL-031 | payment-reconciliation | P0 | financial |
| SKILL-032 | owner-ledger-management | P0 | financial |
| SKILL-035 | payout-processing | P0 | financial |

---

## 🏢 PLATFORMS TO ANALYZE

### Primary (Best-in-Class)
| Platform | Why | Focus Areas |
|----------|-----|-------------|
| **Guesty** | Enterprise payment flows | Multi-currency, split payments |
| **OwnerRez** | Trust accounting excellence | Owner statements, reconciliation |
| **Baselane** | Fintech-native | Integrated banking, auto-categorization |

### Secondary
| Platform | Focus |
|----------|-------|
| Hostaway | Payment automation |
| Lodgify | Direct payment processing |
| Hemlane | Hybrid PM financials |

### Payment Processors (Technical Sources)
| Provider | Focus |
|----------|-------|
| Stripe Connect | Platform payments, split payouts |
| Plaid | Bank verification, ACH |
| PayPal/Braintree | Alternative payment methods |

---

## 📚 RESEARCH QUESTIONS BY SKILL

### SKILL-028: Payment Collection

**Core Questions:**
1. What payment methods are supported (card, ACH, wire, PIX)?
2. How is the payment flow structured (booking → invoice → payment)?
3. How are partial payments handled?
4. What's the payment reminder/dunning sequence?
5. How are failed payments retried?

**Technical Questions:**
- Payment processor integration patterns?
- PCI compliance requirements?
- How is card tokenization handled?
- Webhook handling for payment events?

**Regional Considerations:**
- ACH (US) timing and limits?
- PIX (Brazil) instant payments?
- SEPA (EU) direct debit?
- Credit card processing fees by region?

**Sources to Check:**
- [ ] Guesty payment documentation
- [ ] Stripe Connect platform documentation
- [ ] OwnerRez payment settings
- [ ] YouTube: "vacation rental payment processing"
- [ ] PCI DSS requirements
- [ ] Plaid ACH documentation

---

### SKILL-029: Refund Processing

**Core Questions:**
1. What refund policies can be configured?
2. How are partial refunds calculated?
3. What's the refund approval workflow?
4. How long do refunds take by payment method?
5. How are refunds tracked and reported?

**Technical Questions:**
- Refund API calls per processor?
- How are chargebacks vs refunds distinguished?
- Refund to original payment method vs alternative?
- Refund fee handling?

**Business Rules:**
- Cancellation policy enforcement?
- Service fee retention on refunds?
- Cleaning fee refund rules?
- Tax refund calculations?

**Sources to Check:**
- [ ] Stripe refund documentation
- [ ] Airbnb cancellation policy types
- [ ] Guesty refund workflows
- [ ] YouTube: "vacation rental cancellation policy"
- [ ] Chargeback prevention best practices

---

### SKILL-030: Security Deposit Handling

**Core Questions:**
1. How are security deposits collected (hold vs charge)?
2. What's the deposit release workflow?
3. How are damage claims processed?
4. What documentation is required for claims?
5. How are disputes handled?

**Technical Questions:**
- Pre-authorization vs actual charge?
- Hold duration limits by card network?
- Deposit escrow requirements?
- Photo documentation integration?

**Compliance Considerations:**
- State-by-state deposit regulations?
- Maximum deposit amounts?
- Interest on deposits?
- Return timeline requirements?

**Sources to Check:**
- [ ] Guesty security deposit options
- [ ] Stripe pre-authorization documentation
- [ ] State landlord-tenant laws (security deposits)
- [ ] YouTube: "vacation rental security deposit"
- [ ] Airbnb damage protection vs deposit

---

### SKILL-031: Payment Reconciliation

**Core Questions:**
1. How are payments matched to bookings?
2. How are OTA payouts reconciled?
3. What's the reconciliation frequency?
4. How are discrepancies flagged and resolved?
5. What reports are generated?

**Technical Questions:**
- Matching algorithm for payment → booking?
- OTA payout report parsing (Airbnb, Vrbo)?
- Bank statement import (OFX, CSV)?
- Reconciliation status workflow?

**OTA Payout Complexity:**
| OTA | Payout Timing | Data Available |
|-----|---------------|----------------|
| Airbnb | 24h after check-in | Detailed breakdown |
| Vrbo | After checkout | Summary + fees |
| Booking.com | Monthly | Invoice format |

**Sources to Check:**
- [ ] OwnerRez reconciliation features
- [ ] Baselane auto-categorization
- [ ] Airbnb payout report format
- [ ] Accounting reconciliation best practices
- [ ] YouTube: "vacation rental bookkeeping"

---

### SKILL-032: Owner Ledger Management

**Core Questions:**
1. How is owner income/expenses tracked?
2. What's the chart of accounts structure?
3. How are multi-owner properties handled?
4. What expense categories are standard?
5. How is owner equity tracked?

**Technical Questions:**
- Double-entry accounting model?
- Account hierarchy?
- Journal entry automation?
- Period closing process?

**Trust Accounting Requirements:**
- Separation of owner funds?
- Interest-bearing trust accounts?
- Audit trail requirements?
- State CAM regulations?

**Sources to Check:**
- [ ] OwnerRez owner accounting
- [ ] Guesty owner portal
- [ ] Trust accounting regulations (by state)
- [ ] NARPM best practices
- [ ] YouTube: "property management accounting"

---

### SKILL-035: Payout Processing

**Core Questions:**
1. What's the payout schedule (weekly, monthly)?
2. How are payout amounts calculated (income - expenses - fees)?
3. What approval workflows exist?
4. How are payouts to multiple owners split?
5. What payout methods are supported?

**Technical Questions:**
- Payout calculation formula?
- Reserve withholding logic?
- Minimum payout thresholds?
- ACH batch processing?
- International wire requirements?

**Numscript Integration (Formance):**
```numscript
// Example: Monthly owner payout
send [USD remaining] (
  source = @owner:john_smith:operating
  destination = @owner:john_smith:bank_account
)
```

**Sources to Check:**
- [ ] Guesty owner payout documentation
- [ ] OwnerRez payout settings
- [ ] Stripe Connect payout API
- [ ] ACH batch file format (NACHA)
- [ ] YouTube: "property manager owner payouts"

---

## 📄 OUTPUT REQUIREMENTS

### Document Structure

```markdown
# Knowledge Document: Financial Core
## Phase 1 Group 4 | Skills: SKILL-028, 029, 030, 031, 032, 035

## 1. Executive Summary
   - Key financial flows
   - Treasury OS integration points
   - Compliance requirements

## 2. Financial Architecture Overview
   - Money flow diagram (guest → platform → owner)
   - Account structure (Chart of Accounts)
   - Integration with TigerBeetle/Formance

## 3. SKILL-028: Payment Collection
   ### 3.1 Payment Methods by Region
   ### 3.2 Collection Flow & States
   ### 3.3 Failed Payment Handling
   ### 3.4 PCI Compliance Requirements
   ### 3.5 Processor Integration Patterns

## 4. SKILL-029: Refund Processing
   ### 4.1 Refund Policies
   ### 4.2 Calculation Logic
   ### 4.3 Approval Workflow
   ### 4.4 Accounting Entries

## 5. SKILL-030: Security Deposit Handling
   ### 5.1 Hold vs Charge Strategies
   ### 5.2 Release Workflow
   ### 5.3 Damage Claim Process
   ### 5.4 Compliance by State

## 6. SKILL-031: Payment Reconciliation
   ### 6.1 Matching Algorithm
   ### 6.2 OTA Payout Parsing
   ### 6.3 Discrepancy Resolution
   ### 6.4 Reconciliation Reports

## 7. SKILL-032: Owner Ledger Management
   ### 7.1 Chart of Accounts
   ### 7.2 Transaction Categories
   ### 7.3 Multi-Owner Properties
   ### 7.4 Trust Accounting Requirements

## 8. SKILL-035: Payout Processing
   ### 8.1 Payout Calculation Formula
   ### 8.2 Schedule & Frequency
   ### 8.3 Reserve Management
   ### 8.4 Multi-Currency Payouts

## 9. Numscript Examples
   - Payment collection
   - Fee splits
   - Owner payout
   - Refund processing

## 10. References
   - 35+ citations
```

### Quality Targets

| Metric | Target |
|--------|--------|
| Document Length | 500-700 lines |
| Citations | 35+ sources |
| Data Models | Ledger account structure, transaction types |
| Numscript Examples | 4-6 examples |
| Compliance Coverage | US, Brazil, EU |

---

## 💾 SAVE LOCATION

```
knowledge/financial/KD-PHASE1-G4-financial-core.md
```

---

## ✅ COMPLETION CHECKLIST

- [ ] All 6 skills researched
- [ ] Money flow documented end-to-end
- [ ] Trust accounting requirements identified
- [ ] Regional payment methods covered (ACH, PIX, SEPA)
- [ ] Numscript examples provided
- [ ] 35+ sources cited

---

## 🚀 AFTER COMPLETING

```bash
git add -A
git commit -m "Stage 1 COMPLETE: Phase 1 Group 4 - Financial Core (6 skills)"
git push
```

