# Property Management System (PMS) Knowledge Extraction Plan

**Document Version:** 1.0  
**Date:** January 7, 2026  
**Author:** Manus AI  
**Purpose:** Comprehensive plan for automating research and extracting know-how from PMS companies to build a "Harvey for Property Finance" skill library

---

## 1. Executive Summary

This document provides a comprehensive plan for systematically extracting operational know-how from Property Management System (PMS) companies across the Short-Term Rental (STR), Long-Term Rental (LTR), and HOA/Condo verticals. The extracted knowledge will form the foundation for building an AI-powered "Digital Workforce Manager + Treasury OS" skill library.

The plan identifies **31 companies** for analysis, defines **8 skill domains** containing **35+ individual skills**, and provides a standardized research methodology to ensure consistent, high-quality knowledge extraction across all vendors.

---

## 2. Companies Identified for Research

Based on the provided content and project shared files, the following companies have been identified for knowledge extraction. They are organized by their primary vertical focus and role in the property finance ecosystem.

### 2.1 Core PMS Platforms (Integration Targets)

| Company | Vertical | Primary Focus | PRD Available |
|---------|----------|---------------|---------------|
| AppFolio | LTR | Accounting, Trust Accounting, Reporting | No |
| Buildium | LTR | AP, Bank Recs, Trust Accounting | No |
| Yardi (Breeze/Voyager) | LTR/Commercial | Trust Accounting, CAM Automation | No |
| Entrata | LTR (Enterprise) | Full-stack PM Operations | No |
| RealPage | LTR (Enterprise) | Portfolio Management | No |
| MRI | LTR (Enterprise) | Enterprise PM Software | No |
| Guesty | STR | Accounting, Owner Statements, Payouts | Yes |
| Hostaway | STR | PMS Ecosystem | No |
| Lodgify | STR | PMS Ecosystem | No |
| OwnerRez | STR | PMS Ecosystem | No |
| Hostfully | STR | PMS Ecosystem | No |
| Vantaca | HOA/Condo | Accounting Workflows, Reconciliation | No |
| CINC Systems | HOA/Condo | Unified Platform with Accounting + Banking | No |
| Enumerate | HOA/Condo | Community Association Management + Accounting | No |
| Amenitiz | Hospitality | Hotel/Property Management | Yes |
| Cloudbeds | Hospitality | Hotel PMS with Finance Features | Yes |
| Mews | Hospitality | Modern PMS with Payments | Yes |

### 2.2 Payments and Treasury Layer

| Company | Focus Area | Role in Ecosystem |
|---------|------------|-------------------|
| Zego | Rent Payments, Utilities | PMS Integration Layer |
| PayLease | Rent Payments | Property Payment Processing |
| ClickPay | Payments Platform | Ledger Integration |
| Stripe | Payment Rails | Generic Reference Patterns |
| BILT Rewards | Rent Payments/Rewards | Consumer Payment Innovation |

### 2.3 Back-Office Automation

| Company | Focus Area | Relevance |
|---------|------------|-----------|
| AvidXchange | AP Automation | Community Association Management |

### 2.4 AI-Native PMS Solutions (Project Shared Files)

| Company | PRD File | Focus Area |
|---------|----------|------------|
| BetsyAI | BetsyAI.pdf | AI Property Management |
| BoomAI | BoomAI.pdf | AI Property Operations |
| InnteloAIPMS | InnteloAIPMS.pdf | AI-Powered PMS |
| VisitoAIPMS | VisitoAIPRDPMS.pdf | AI Visitor/Guest Management |
| Hemlane | Hemlane_PRD.md.pdf | Property Management |
| Stessa | Stessa_PRD.md (1).pdf | Real Estate Investing/Finance |
| Landlord Finance OS | Landlord_Finance_OS_PRD.md.pdf | Landlord Financial Operations |
| Project Citadel | Project Citadel.pdf | Property Finance Platform |

---

## 3. Skill Domains and Skills to Extract

The knowledge extraction will focus on building skills across **8 primary domains**. Each domain contains specific skills that require vendor-specific workflow knowledge.

### 3.1 Skill Domain Taxonomy

```
skills/
├── control_plane/           # Manager-Orchestrator (THE MOAT)
├── integrations/            # Vendor Knowledge → Actionability
├── property_finance_core/   # The "Harvey" Layer
├── ap_ar/                   # AP/AR Workforce
├── trust_reserves_compliance/  # Property-Specific Finance
├── reporting_owner_board/   # Owner/Board Artifacts
├── treasury_payments/       # Monetization Ladder
└── risk_audit/              # CFO Confidence Layer
```

### 3.2 Complete Skill List by Domain

#### Domain 1: Control Plane (Manager-Orchestrator)

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| CP-001 | Policy & Permissioning | Define role-based permissions, spend caps, allowed vendors, approval requirements |
| CP-002 | Task Decomposition & Routing | Convert outcome requests into tasks; route to worker skills |
| CP-003 | Approval Chain Orchestration | Create approval workflows with SLAs and reminders |
| CP-004 | Work Queue & SLA Management | Prioritize tasks, manage due dates, escalations |
| CP-005 | Evidence Pack Builder | Bundle proof into ready-to-approve packets |
| CP-006 | Exception Triage & Human Escalation | Detect ambiguity/failure; route to human |
| CP-007 | Audit Log & Decision Trace | Immutable action log with policy checks |
| CP-008 | ROI Ledger & Outcome Reporting | Track baseline vs achieved metrics |
| CP-009 | Runbooks & Playbook Versioning | Version-controlled procedures |

#### Domain 2: Integrations

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| INT-001 | Vendor Export Ingestion | Import CSV/XLSX/PDF exports; map fields |
| INT-002 | Chart of Accounts & Entity Model Mapper | Canonicalize COA, properties, units, owners |
| INT-003 | Bank Feed / Statement Import | OFX/CSV/PDF parsing; normalize transactions |
| INT-004 | Document Intake | Extract invoice/receipt header/line items |
| INT-005 | Identity & Access Connector | Connect to email, drive, ticketing for evidence |

#### Domain 3: Property Finance Core

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| FIN-001 | Month-End Close Orchestration | Close checklist, dependencies, completeness checks |
| FIN-002 | Bank Reconciliation | Match bank ↔ ledger; produce exceptions + posting plan |
| FIN-003 | Journal Entry Drafting & Posting Plan | Create JE proposals with rationale |
| FIN-004 | Accruals & Prepaids | Identify recurring expenses; draft accrual recommendations |
| FIN-005 | Variance Explanation | Compare MoM/YoY; explain drivers |

#### Domain 4: AP/AR Workforce

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| AP-001 | Vendor Onboarding & Compliance | W-9/VAT info, payment method, COI/insurance |
| AP-002 | Invoice Triage & Coding | GL coding by rules + history |
| AP-003 | Duplicate/Overbilling Detection | Detect same invoice twice, inflated items |
| AP-004 | Payables Approval & Scheduling | Route for approvals; recommend pay date |
| AR-001 | Rent Roll & Collections Monitor | Identify delinquencies; generate notices |
| AR-002 | Charge/Adjustment Management | Late fees, credits, owner charges |

#### Domain 5: Trust/Reserves/Compliance

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| TR-001 | Client/Trust Ledger Segregation | Enforce separation of operating vs client funds |
| TR-002 | Security Deposit Ledger & Compliance Pack | Track deposits, deductions, refund timing |
| TR-003 | Owner Draws & Reserve Policy Enforcement | Enforce min reserves; flag policy violations |
| TR-004 | HOA Reserve Fund Management | Reserve schedules, contribution policy |

#### Domain 6: Reporting (Owner/Board)

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| REP-001 | Owner Statement Generation | Produce owner statement packet + narrative |
| REP-002 | HOA Board Pack | Operating vs reserve summary, delinquency |
| REP-003 | Vendor Spend & Maintenance Analytics | Top vendors, cost per unit, anomalies |

#### Domain 7: Treasury & Payments

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| TRE-001 | Cash Position & Forecast | 30/60/90 day forecast from rent schedule |
| TRE-002 | Payment Rail Selection | Decide ACH/SEPA vs card vs wire |
| TRE-003 | Payment Batch Preparation | Generate payment file; attach approval pack |
| TRE-004 | Payment Initiation | Trigger payments via partner rails |
| TRE-005 | Payouts to Owners | Compute distributions; apply reserve rules |
| TRE-006 | Yield/Sweep/Reserve Optimization | Sweep idle balances; maintain liquidity |

#### Domain 8: Risk & Audit

| Skill ID | Skill Name | Description |
|----------|------------|-------------|
| RA-001 | Controls Testing & Evidence | Validate approvals, segregation, policy adherence |
| RA-002 | Fraud/Anomaly Detection | Vendor fraud patterns, unusual spend |

---

## 4. Research Methodology

### 4.1 Knowledge Sources (Priority Order)

For each company, knowledge will be extracted from the following sources in order of priority:

1. **Project PRD Files** (if available) — Highest signal, most structured
2. **Official Help Centers / Knowledge Bases** — Vendor-documented workflows
3. **API Documentation** — Data models, endpoints, integration patterns
4. **Vendor Webinars / Product Updates** — Recent feature announcements
5. **Third-Party Implementation Guides** — Partner best practices
6. **Community Forums / Reddit / Blogs** — Edge cases and real-world hacks

### 4.2 Information to Extract Per Company

For each company, the research agent will extract:

#### A) Workflow Primitives (Step-by-Step)

For each of these 7 core workflows:
- Owner statements / owner payouts
- Bank reconciliation
- AP: invoice intake → coding → approvals → payments
- AR: rent roll → collections → notices → adjustments
- Trust/escrow/security deposit handling
- Reserves (HOA/Condo): operating vs reserves
- Month-end close checklist + reporting pack

Extract:
- Exact steps
- Required inputs
- Outputs/artifacts produced
- Roles/permissions involved
- Edge cases and exception handling
- Common failure modes

#### B) Data Model + Exports

- Key entities (property, unit, owner, tenant, vendor, GL account, fund, bank account)
- Report/export formats (CSV/XLSX/PDF)
- Required fields for each report
- Naming conventions and unique identifiers

#### C) Permissions + Governance

- User roles and permissions model
- Approval workflows
- Audit logging capabilities
- Controls and segregation concepts

#### D) Integrations + APIs

- API endpoints or integration guides
- Webhooks/events
- Import/export methods
- Rate limits

#### E) Edge-Case Intelligence

- Common forum/community issues
- Vendor best practices
- Implementation pitfalls

### 4.3 Output Format Per Company

Each company's research will produce a structured markdown file:

```
knowledge/vendors/{VENDOR_NAME}/KD-{VENDOR_NAME}-property-finance.md
```

With the following sections:

1. **Vendor Overview** — Products, verticals, finance capabilities
2. **Workflow Deep Dives** — Detailed procedure for each workflow
3. **Artifacts Catalog** — Training data with example formats
4. **Skill Candidates** — Mapped to skill library with inputs/outputs
5. **Canonical Mapping Notes** — Field mappings to canonical model
6. **Treasury Capture Hooks** — Where approvals, payouts, and fund segregation occur

---

## 5. Automated Research Execution Plan

### 5.1 Phase 1: PRD Document Analysis

Process the 15 available PRD documents from the project shared files using parallel research agents. Each agent will:

1. Read and analyze the complete PRD document
2. Extract all workflow information
3. Map features to skill candidates
4. Identify data models and integration patterns
5. Document treasury capture opportunities

**Companies with PRDs:**
- Amenitiz, BetsyAI, BoomAI, Cloudbeds, Guesty, Hemlane, InnteloAIPMS, Landlord Finance OS, Mews, Project Citadel, Stessa, VisitoAIPMS, BILT Rewards, AI Property Management Platform

### 5.2 Phase 2: Public Knowledge Extraction

For companies without PRDs, conduct web research to extract:

1. Help center documentation
2. API documentation
3. Community forum discussions
4. Implementation guides

**Companies requiring web research:**
- AppFolio, Buildium, Yardi, Entrata, RealPage, MRI, Hostaway, Lodgify, OwnerRez, Hostfully, Vantaca, CINC Systems, Enumerate, Zego, PayLease, ClickPay, AvidXchange

### 5.3 Phase 3: Knowledge Synthesis

After individual company research:

1. Merge findings into unified skill definitions
2. Create canonical data model mappings
3. Generate synthetic training cases
4. Define evaluation tests for each skill

---

## 6. Universal Vendor Research Prompt

The following prompt template will be used for each company research task:

```markdown
# RESEARCH_PROMPT_PROPERTY_FINANCE_SKILLS_V1

You are a Research Analyst building a Skills Library for an AI "Digital Workforce 
Manager + Treasury OS" in the property management vertical:
- STR (short-term rental)
- LTR (long-term rental property management)
- HOA/Condo (community association management)

## INPUTS
Vendor Name: {{VENDOR_NAME}}
Vendor Product(s): {{VENDOR_PRODUCTS}}
Vertical Coverage: {{STR|LTR|HOA_CONDO|MULTI}}
PRD File Path: {{PRD_PATH}} (if available)

## MISSION
1) Extract the best "how-to" operational knowledge from the vendor ecosystem
2) Convert the knowledge into executable Skills (Claude Skills format)
3) Produce training-grade artifacts and evaluation tests

## WORKFLOWS TO ANALYZE
1) Owner statements / owner payouts
2) Bank reconciliation
3) AP: invoice intake → coding → approvals → payments
4) AR: rent roll → collections → notices → adjustments
5) Trust/escrow/security deposit handling
6) Reserves (HOA/Condo): operating vs reserves
7) Month-end close checklist + reporting pack

## OUTPUT STRUCTURE
Create: knowledge/vendors/{{VENDOR_NAME}}/KD-{{VENDOR_NAME}}-property-finance.md

Sections:
1. Vendor Overview
2. Workflow Deep Dives (for each workflow)
3. Artifacts Catalog
4. Skill Candidates (mapped to skill library)
5. Canonical Mapping Notes
6. Treasury Capture Hooks
```

---

## 7. Priority Skill Set (P0 — Build First)

Based on the analysis, the following skills should be built first to create the "treasury wedge":

### P0 Control Plane
- **CP-001** Policy & Permissioning
- **CP-003** Approval Chain Orchestration
- **CP-005** Evidence Pack Builder
- **CP-007** Audit Log & Decision Trace

### P0 Finance
- **FIN-002** Bank Reconciliation
- **REP-001** Owner Statement Generation
- **AP-002** Invoice Triage & Coding
- **AP-004** Payables Approval & Scheduling

### P0 Treasury (Non-Custodial)
- **TRE-003** Payment Batch Preparation

---

## 8. Expected Deliverables

Upon completion of the research automation, the following deliverables will be produced:

| Deliverable | Description |
|-------------|-------------|
| Knowledge Documents | One KD-{VENDOR}-property-finance.md per company |
| Skill Manifest | skill_manifest.yaml with complete skill enumeration |
| Skill Folders | 35+ skill folders with README, tool_definition, examples, evals |
| Canonical Data Model | canonical_model.json for cross-vendor field mapping |
| Training Cases | 20+ synthetic training cases per skill |
| Evaluation Tests | 5+ eval tests per skill |

---

## 9. Recommended Next Steps

1. **Confirm Scope** — Review the company list and skill domains; add or remove as needed
2. **Prioritize Verticals** — Select STR, LTR, or HOA/Condo as the starting vertical
3. **Initiate Research** — Begin parallel research execution for PRD documents
4. **Review Outputs** — Validate extracted knowledge against skill requirements
5. **Build Skills** — Convert knowledge into executable skill definitions

---

## Appendix A: Project Shared Files Inventory

| File Name | Company/Topic |
|-----------|---------------|
| BetsyAI.pdf | BetsyAI |
| Stessa_PRD.md (1).pdf | Stessa |
| Amenitiz Platform PRD PMS.pdf | Amenitiz |
| MewsPMSProductRequirementSoftware.pdf | Mews |
| cloudbedsai.pdf | Cloudbeds |
| Guesty.pdf | Guesty |
| Hemlane_PRD.md.pdf | Hemlane |
| InnteloAIPMS.pdf | InnteloAIPMS |
| Landlord_Finance_OS_PRD.md.pdf | Landlord Finance OS |
| VisitoAIPRDPMS.pdf | VisitoAIPMS |
| AI_Property_Management_Platform_PRD.md.pdf | AI Property Management |
| BILT_Rewards_PRD.md (1).pdf | BILT Rewards |
| BoomAI.pdf | BoomAI |
| Project Citadel.pdf | Project Citadel |
| ai_property_management_prd.md.pdf | AI Property Management |

---

*Document prepared by Manus AI — January 7, 2026*
