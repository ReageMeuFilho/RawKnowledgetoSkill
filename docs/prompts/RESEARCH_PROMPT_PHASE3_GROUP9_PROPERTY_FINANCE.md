# Research Prompt: Phase 3 Group 9 - Advanced Property Finance

> **Target Agent**: AI Research Analyst
> **Output Location**: `knowledge/finance/KD-PHASE3-G9-property-finance.md`
> **Skills to Research**: SKILL-194 through SKILL-236 (43 skills)
> **Priority**: P3 (Advanced) - **HIGHEST TREASURY VALUE**
> **Estimated Research Time**: 12-16 hours

---

## 🎯 RESEARCH OBJECTIVE

Research and document comprehensive engineering specifications for **Advanced Property Finance** capabilities that enable property managers to automate the complete financial lifecycle: accounts payable, accounts receivable, bank reconciliation, trust accounting, owner reporting, and treasury operations.

**Strategic Importance**: This skill group represents the **highest treasury capture value** of any Phase 3 group. These skills enable Citadel OS to own the financial control plane for property management operations.

---

## 📋 SKILLS TO SPECIFY (43 Total)

### Control Plane Foundation (9 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-194** | Policy & Permissioning | Control Plane | Role-based access control for financial operations |
| **SKILL-195** | Entity Hierarchy Management | Control Plane | Property → Unit → Owner → Tenant relationships |
| **SKILL-196** | GL Account Configuration | Control Plane | Chart of accounts setup and mapping |
| **SKILL-197** | Fund Type Definition | Control Plane | Operating vs. Trust vs. Reserve fund setup |
| **SKILL-198** | Fiscal Period Management | Control Plane | Open/close accounting periods |
| **SKILL-199** | Bank Account Configuration | Control Plane | Link bank accounts to entities/funds |
| **SKILL-200** | Audit Log & Decision Trace | Control Plane | Immutable audit trail for all financial actions |
| **SKILL-201** | Threshold & Limit Configuration | Control Plane | Set approval thresholds, payment limits |
| **SKILL-202** | Integration Credential Management | Control Plane | Secure API key/OAuth management |

### Property Finance Core (5 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-203** | Transaction Categorization AI | Finance Core | ML-based automatic GL coding |
| **SKILL-204** | Three-Way Bank Reconciliation | Finance Core | Bank statement + Bank ledger + Trust liability |
| **SKILL-205** | Reconciliation Exception Handler | Finance Core | Smart resolution of unmatched transactions |
| **SKILL-206** | Month-End Close Automation | Finance Core | Period locking, accruals, validation |
| **SKILL-207** | Year-End/Tax Preparation | Finance Core | Schedule E generation, 1099 prep |

### Accounts Payable Automation (6 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-208** | Invoice Data Extraction (OCR/AI) | AP | Auto-extract vendor, amount, date from PDF |
| **SKILL-209** | Invoice Triage & Coding | AP | Auto-assign GL codes based on vendor/content |
| **SKILL-210** | Approval Workflow Engine | AP | Configurable multi-level approval routing |
| **SKILL-211** | Duplicate Invoice Detection | AP | Prevent paying same invoice twice |
| **SKILL-212** | Vendor Payment Optimization | AP | Recommend best payment method |
| **SKILL-213** | 1099 Vendor Management | AP | Track W-9s, calculate 1099 thresholds |

### Accounts Receivable & Collections (6 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-214** | Rent Roll Generation | AR | Comprehensive rental income reporting |
| **SKILL-215** | Automated Late Fee Assessment | AR | Policy-based fee calculation |
| **SKILL-216** | Collections Workflow Engine | AR | Escalation from reminder → notice → legal |
| **SKILL-217** | Tenant Ledger Management | AR | Track charges, payments, adjustments |
| **SKILL-218** | NSF/Bounced Payment Handler | AR | Reverse payment, assess fees |
| **SKILL-219** | Payment Plan Management | AR | Set up and track installment plans |

### Trust/Reserves/Compliance (6 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-220** | Trust Account Compliance Monitor | Trust | Prevent fund commingling |
| **SKILL-221** | Security Deposit Lifecycle Manager | Trust | Receipt → hold → interest → refund/apply |
| **SKILL-222** | HOA Reserve Fund Management | Trust | Operating vs. reserves segregation |
| **SKILL-223** | Reserve Study Integration | Trust | Track component funding status |
| **SKILL-224** | State-Specific Compliance Engine | Trust | Apply state trust/deposit rules |
| **SKILL-225** | Trust Liability Reconciliation | Trust | Validate trust balance = sum of liabilities |

### Owner Reporting & Payouts (5 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-226** | Owner Statement Generation | Reporting | Itemized income/expense report |
| **SKILL-227** | Owner Packet Automation | Reporting | Bundle multiple reports for distribution |
| **SKILL-228** | Owner Portal Management | Reporting | Self-service access to statements/documents |
| **SKILL-229** | Scheduled Report Distribution | Reporting | Auto-generate and email monthly reports |
| **SKILL-230** | Budget vs. Actuals Reporting | Reporting | Variance analysis for owners/boards |

### Treasury Operations (6 skills)

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-231** | Owner Payout Calculation | Treasury | Net distribution = income - expenses - reserves |
| **SKILL-232** | Payment Batch Preparation | Treasury | Group payments for efficient processing |
| **SKILL-233** | Negative Balance Handler | Treasury | Handle owner accounts with negative cash flow |
| **SKILL-234** | Cash Flow Forecasting | Treasury | Predict future cash needs |
| **SKILL-235** | ACH Payment Execution | Treasury | Execute batch ACH payments |
| **SKILL-236** | Payment Reconciliation | Treasury | Match sent payments to bank cleared |

---

## 🔍 DETAILED RESEARCH QUESTIONS BY CATEGORY

### Control Plane Foundation

#### SKILL-194: Policy & Permissioning

**Core Questions**:
1. What permission models do property finance systems use (RBAC, ABAC)?
2. What are the standard roles in property management finance?
   - Property Manager, Bookkeeper, Owner, Approver, Auditor
3. What granular permissions are needed?
   - View vs. Edit vs. Approve vs. Execute
   - By entity (property, owner, fund)
   - By transaction type (AP, AR, payouts)
4. How do platforms like AppFolio and Buildium implement role hierarchies?
5. What approval matrices exist (amount-based, entity-based)?
6. How to implement segregation of duties?

**Technical Requirements**:
- RBAC with hierarchical roles
- Permission inheritance patterns
- Audit logging of permission changes
- Multi-tenant isolation

#### SKILL-196: GL Account Configuration

**Core Questions**:
1. What is a real estate-specific chart of accounts?
2. What GL accounts are required for property management?
   - Income: Rent, Late Fees, Pet Fees, Application Fees
   - Expense: Maintenance, Utilities, Management Fees, Insurance
   - Liability: Security Deposits, Prepaid Rent
   - Equity: Owner Draws, Owner Contributions
3. How do platforms like Stessa structure their chart of accounts?
4. What account numbering conventions are used?
5. How to handle multi-property GL mapping?
6. What account types are needed (Asset, Liability, Equity, Income, Expense)?

#### SKILL-197: Fund Type Definition

**Core Questions**:
1. What fund types are required for property management?
   - Operating Fund
   - Trust/Security Deposit Fund
   - Reserve Fund (HOA)
   - Escrow Fund
2. What are the legal requirements for fund segregation by state?
3. How do platforms prevent commingling?
4. How to map funds to bank accounts?
5. What reporting requirements exist per fund type?

---

### Property Finance Core

#### SKILL-204: Three-Way Bank Reconciliation

**Core Questions**:
1. What is AppFolio's three-way reconciliation methodology?
   - Checkpoint 1: Bank Reconciliation Report (statement balance + deposits - outstanding checks)
   - Checkpoint 2: Bank Account Activity Report (ending book balance + undeposited receipts)
   - Checkpoint 3: Bank Balance Detail (trust liability total)
2. Why is three-way reconciliation the gold standard for trust accounting?
3. What matching algorithms are used (exact, fuzzy, reference-based)?
4. How to handle timing differences (deposits in transit, outstanding checks)?
5. What exception categories exist?
   - Unmatched bank transactions
   - Unmatched ledger entries
   - Amount mismatches
   - Duplicate transactions
6. What reports are generated after reconciliation?

**Technical Requirements**:
- Multi-source data ingestion (OFX, CSV, API)
- Configurable matching rules
- Confidence scoring for proposed matches
- Exception workflow with manual resolution
- Posting plan generation
- Complete audit trail

#### SKILL-203: Transaction Categorization AI

**Core Questions**:
1. How do Stessa and Landlord Finance OS implement AI-powered categorization?
2. What features predict the correct GL account?
   - Vendor name/type
   - Transaction description
   - Amount patterns
   - Historical categorization
3. What ML models work best (NLP, classification)?
4. How to handle new vendors/transaction types?
5. What is the target accuracy rate?
6. How to implement user feedback loop for model improvement?

**Technical Requirements**:
- NLP for transaction description parsing
- Vendor matching/lookup
- Classification model (XGBoost, BERT)
- Confidence thresholds for auto-categorization
- Human-in-the-loop for low confidence
- Model retraining pipeline

---

### Accounts Payable Automation

#### SKILL-208: Invoice Data Extraction (OCR/AI)

**Core Questions**:
1. How do AvidXchange and Buildium AI Bill Scan extract invoice data?
2. What fields are extracted?
   - Vendor name and address
   - Invoice number
   - Invoice date
   - Due date
   - Line items (description, quantity, amount)
   - Total amount
   - Tax
3. What OCR technologies are used (Tesseract, Amazon Textract, Google Document AI)?
4. How to handle different invoice formats?
5. What is the accuracy rate for structured vs. unstructured invoices?
6. How to validate extracted data?

**Technical Requirements**:
- PDF/image ingestion
- OCR engine integration
- Template learning for repeat vendors
- Field validation rules
- Confidence scoring
- Human review workflow for low confidence

#### SKILL-210: Approval Workflow Engine

**Core Questions**:
1. How does AvidXchange implement approval workflows?
2. What routing logic is configurable?
   - Manual workflow selection
   - PO matching
   - Vendor-specific defaults
   - Property/entity defaults
   - Amount thresholds
3. How to implement multi-level approvals (sequential, parallel)?
4. How to handle approval delegation and escalation?
5. What notifications are sent at each stage?
6. How to track approval history and SLAs?

**Technical Requirements**:
- Workflow definition DSL
- Multi-step routing engine
- Threshold-based routing
- Delegation and escalation rules
- Email/SMS notifications
- Approval SLA tracking
- Mobile approval capability

---

### Accounts Receivable & Collections

#### SKILL-216: Collections Workflow Engine

**Core Questions**:
1. How does AppFolio implement the collections workflow?
   - Day 5: Generate delinquency report
   - Day 5: Send "Notice of Late Rent" via email
   - Day 10: Send "Notice to Vacate" if still unpaid
2. How does Vantaca's action item system work?
3. What triggers move accounts through collections stages?
   - Days past due
   - Balance threshold
   - Number of missed payments
4. What notices are generated at each stage?
5. How to track and document all collection activities?
6. What integration with legal/eviction services exists?

**Technical Requirements**:
- State machine for collections stages
- Configurable triggers (days, amount, count)
- Notice template system
- Document generation (PDF)
- Activity logging
- Integration with legal providers
- Escalation workflows

#### SKILL-214: Rent Roll Generation

**Core Questions**:
1. What data is included in a comprehensive rent roll?
   - Property/Unit details
   - Tenant name
   - Lease start/end dates
   - Market rent vs. actual rent
   - Current balance (charges, credits)
   - Payment status
2. How do RealPage and AppFolio structure their rent rolls?
3. What calculations are performed?
   - Loss-to-lease (market rent - actual rent)
   - Occupancy rate
   - Collection rate
4. How to filter/sort rent rolls (by property, status, date)?
5. What export formats are needed (PDF, Excel, CSV)?

---

### Trust/Reserves/Compliance

#### SKILL-220: Trust Account Compliance Monitor

**Core Questions**:
1. What are state-specific trust accounting requirements?
   - California: Broker Trust Fund handling
   - New York: Security deposit interest requirements
   - Florida: Advance rent handling
2. What constitutes commingling of funds?
3. How do platforms detect and prevent commingling?
4. What alerts should be generated for compliance violations?
5. How to audit trust account activity?
6. What documentation is required for compliance?

**Technical Requirements**:
- State rules engine
- Real-time fund monitoring
- Commingling detection algorithm
- Compliance alerts
- Audit report generation
- Remediation workflow

#### SKILL-225: Trust Liability Reconciliation

**Core Questions**:
1. How does AppFolio's three-way reconciliation validate trust liabilities?
2. What is the calculation: Trust Bank Balance = Sum of Individual Trust Liabilities?
3. How to handle discrepancies?
4. What reports show trust liability by tenant/owner?
5. How often should trust liability reconciliation occur?

---

### Owner Reporting & Payouts

#### SKILL-226: Owner Statement Generation

**Core Questions**:
1. What sections are included in an owner statement?
   - Management company info
   - Owner info
   - Property/unit summary
   - Income summary (rent, fees)
   - Expense summary (maintenance, management fee)
   - Net cash flow
   - Beginning/ending balance
   - Reserve/prepaid items
   - Outstanding bills
2. How do AppFolio and Buildium structure owner statements?
3. What customization options are needed?
4. How to handle multi-property owner statements?
5. What delivery methods are supported (portal, email, mail)?

#### SKILL-231: Owner Payout Calculation

**Core Questions**:
1. How is the "Available for Payment" calculated?
   - Ending cash balance
   - MINUS: Property reserve
   - MINUS: Outstanding liabilities
   - MINUS: Pending expenses
   - EQUALS: Available for payout
2. How do platforms like Buildium handle negative balances?
3. What reserve policies are configurable?
4. How to handle owner contributions for negative cash flow?
5. What approval workflow exists for payouts?

---

### Treasury Operations

#### SKILL-232: Payment Batch Preparation

**Core Questions**:
1. How does AvidXchange prepare payment batches?
2. What payment methods are supported?
   - ACH
   - Check
   - Virtual Card
   - Wire
3. How to optimize for cost (virtual card rebates vs. ACH fees)?
4. What vendor preferences are stored?
5. How to validate bank details before payment?
6. What batch approval workflow exists?

#### SKILL-235: ACH Payment Execution

**Core Questions**:
1. What is the ACH payment flow?
   - Batch creation
   - NACHA file generation
   - Bank submission
   - Confirmation
   - Settlement
2. What error handling exists (NSF, invalid account)?
3. How to track payment status?
4. What reconciliation occurs after settlement?
5. What compliance requirements exist (NACHA rules)?

---

## 🏢 COMPETITOR RESEARCH SOURCES

### Primary Sources (from your research)

| Company | Key Strengths | Skills to Learn |
|---------|---------------|-----------------|
| **AppFolio** | Three-way reconciliation, AI | FIN-002, AP-002, TR-001 |
| **AvidXchange** | AP workflow engine | AP-001 through AP-006 |
| **Buildium/RealPage** | Trust accounting, rent roll | TR-001 to TR-006, AR-001 |
| **Stessa** | AI categorization, investor reports | FIN-001, REP-001 to REP-003 |
| **Landlord Finance OS** | Integrated banking, AI bookkeeping | TRE-001 to TRE-006 |
| **Vantaca** | HOA reserves, collections workflow | TR-003, AR-003 |
| **Zego** | Payment processing | TRE-002, TRE-005 |

### Research Sources to Use

1. **AppFolio Help Center**: https://help.appfolio.com/
2. **Buildium Help Center**: https://www.buildium.com/help/
3. **AvidXchange Documentation**: https://www.avidxchange.com/
4. **Stessa Help Center**: https://support.stessa.com/
5. **Vantaca Library**: https://support.vantaca.com/
6. **Industry Standards**: NARPM, IREM, CAI
7. **State Regulations**: Trust accounting laws by state
8. **NACHA Rules**: ACH payment standards

---

## 🏗️ ARCHITECTURE ALIGNMENT

### Citadel OS Layer Mapping

| Component | Layer | Implementation |
|-----------|-------|----------------|
| Finance Dashboards | Layer 6: Applications | React + TypeScript |
| Property Finance Bundle | Layer 5: Domain Bundles | Finance domain |
| Finance Skills | Layer 4: Skills Layer | SKILL.md files |
| Calculations/Workflows | Layer 3: Hot Path | FastAPI + Temporal |
| Financial Ledger | Layer 2: Cold Path | TigerBeetle + Formance |
| Data Storage | Layer 1: Infrastructure | PostgreSQL + TigerBeetle |

### Required MCP Servers

```yaml
mcp_servers:
  # Core Treasury (existing)
  - mcp://treasury-read              # Financial data read
  - mcp://treasury-write             # Financial transactions
  
  # Property Finance (new)
  - mcp://finance/reconciliation     # Bank reconciliation
  - mcp://finance/categorization     # AI transaction coding
  - mcp://finance/period-close       # Month/year end close
  
  # Accounts Payable (new)
  - mcp://ap/invoice-intake          # OCR extraction
  - mcp://ap/workflow                # Approval routing
  - mcp://ap/payment                 # Payment execution
  
  # Accounts Receivable (new)
  - mcp://ar/rent-roll               # Rent roll generation
  - mcp://ar/collections             # Collections workflow
  - mcp://ar/ledger                  # Tenant ledger
  
  # Trust/Compliance (new)
  - mcp://trust/compliance           # Trust monitoring
  - mcp://trust/deposits             # Security deposits
  - mcp://trust/reserves             # Reserve management
  
  # Reporting (new)
  - mcp://reporting/owner-statements # Owner reports
  - mcp://reporting/batch            # Report bundles
  
  # Treasury Ops (new)
  - mcp://treasury/payouts           # Owner payouts
  - mcp://treasury/batch             # Payment batching
  - mcp://treasury/forecast          # Cash forecasting
```

### Technology Stack Requirements

- **Backend**: Python 3.12+ (FastAPI), Rust (TigerBeetle)
- **Financial Ledger**: TigerBeetle (1M+ TPS)
- **Accounting Engine**: Formance (Numscript DSL)
- **Workflow Orchestration**: Temporal
- **ML/AI**: scikit-learn, XGBoost, BERT for categorization
- **OCR**: Amazon Textract or Google Document AI
- **Database**: PostgreSQL (metadata), TigerBeetle (transactions)
- **Caching**: Redis for GL lookups
- **Streaming**: Redpanda for transaction events
- **Container**: AWS ECS/Fargate

---

## 📊 OUTPUT FORMAT REQUIREMENTS

### Document Structure

```markdown
# Engineering Specification: Advanced Property Finance Platform

## 1. Executive Summary
## 2. Skills Overview (43 skills in 7 categories)
## 3. Technical Architecture
## 4. Detailed Skill Specifications
   - For each skill:
     - Purpose and business value
     - Treasury capture opportunity
     - Technical implementation
     - API endpoints
     - Data models
     - Workflow diagrams
     - Integration requirements
## 5. Database Schema
## 6. Compliance Framework
## 7. Security Requirements
## 8. Testing Strategy
## 9. Implementation Roadmap (prioritized by treasury value)
```

### Code Example Requirements

```python
# Include working code examples for:
# - Three-way reconciliation algorithm
# - Invoice OCR extraction
# - Approval workflow engine
# - Collections state machine
# - Owner payout calculation
# - Payment batch generation
```

```sql
-- Include schema for:
-- - Trust accounts and balances
-- - Transaction categorization
-- - Approval workflows
-- - Collections stages
```

---

## ✅ QUALITY CHECKLIST

Before submitting, verify:

- [ ] All 43 skills have detailed specifications
- [ ] Three-way reconciliation fully documented
- [ ] AP workflow engine matches AvidXchange capability
- [ ] Collections workflow matches AppFolio capability
- [ ] Trust accounting compliance by state documented
- [ ] Owner statement format matches industry standard
- [ ] Treasury capture hooks clearly identified
- [ ] Integration with TigerBeetle/Formance specified
- [ ] NACHA/ACH compliance documented
- [ ] State-specific regulations addressed

---

## 💰 TREASURY CAPTURE VALUE ASSESSMENT

Rate each skill for treasury capture potential:

| Rating | Description | Example Skills |
|--------|-------------|----------------|
| **🔴 Critical** | Direct control of money movement | AP-003, TRE-001, TRE-005 |
| **🟠 High** | Approval/validation of financial transactions | AP-002, TR-001 |
| **🟡 Medium** | Financial visibility and reporting | REP-001, FIN-002 |
| **🟢 Foundation** | Enables other treasury functions | CP-001, CP-004 |

---

## 📚 ADDITIONAL RESEARCH AREAS

1. **State Trust Regulations**: Document requirements for CA, TX, FL, NY, AZ
2. **NACHA Compliance**: ACH file formats, return codes
3. **1099 Reporting**: IRS requirements, thresholds, e-filing
4. **SOC 2 Compliance**: Security controls for financial data
5. **PCI DSS**: If handling card payments
6. **Bank Integration Patterns**: Plaid, MX, Finicity

---

**Expected Output**: A comprehensive engineering specification document of **4,000-5,000 lines** covering all 43 property finance skills with production-ready technical details, treasury capture analysis, and compliance framework.

**This is the highest-value Phase 3 skill group for the Citadel OS platform.**

