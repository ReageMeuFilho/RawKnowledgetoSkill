# Property Management System (PMS) Research Summary

**Document Version:** 1.0  
**Date:** January 7, 2026  
**Author:** Manus AI  
**Purpose:** Summary of automated research across 31 PMS companies for building a "Harvey for Property Finance" skill library

---

## Executive Summary

This document summarizes the results of comprehensive parallel research conducted across **31 Property Management System (PMS) companies**. The research extracted operational know-how from PRD documents, company websites, help centers, Reddit discussions, YouTube channels, and other public forums to build a foundation for an AI-powered "Digital Workforce Manager + Treasury OS" skill library.

The research successfully identified **7 core workflows**, mapped findings to **35+ skill candidates**, and discovered **multiple treasury capture opportunities** across the STR, LTR, and HOA/Condo verticals.

---

## Research Results Overview

| Metric | Value |
|--------|-------|
| Companies Researched | 31 |
| PRD Documents Analyzed | 14 |
| Knowledge Documents Generated | 31 |
| Total Workflows Documented | 130+ |
| Skill Candidates Identified | 350+ |
| Treasury Hooks Found | 85+ |
| Average Data Quality Score | 6.7/10 |

---

## Company Research Summary by Vertical

### Short-Term Rental (STR)

| Company | Workflows Found | Skill Candidates | Treasury Hooks | Data Quality | Key Insight |
|---------|-----------------|------------------|----------------|--------------|-------------|
| Guesty | 5 | 9 | 3 | 8/10 | Strong trust accounting features; AP workflow opportunity |
| Hostaway | 4 | 5 | 3 | 6/10 | Relies on third-party integrations for accounting |
| Lodgify | 1 | 4 | 3 | 6/10 | Owner statement generation is well-defined workflow |
| OwnerRez | 5 | 11 | 3 | 8/10 | Heavily reliant on QuickBooks integration |
| Hostfully | 5 | 8 | 2 | 7/10 | Strong focus on automation and Owner Portal |
| Cloudbeds | 5 | 26 | 3 | 8/10 | Hotel-focused; core financial workflows are manual |
| Amenitiz | 4 | 5 | 3 | 7/10 | All-in-one for hoteliers; limited AP functionality |
| Mews | 5 | 5 | 3 | 8/10 | Strong API; robust reporting capabilities |

### Long-Term Rental (LTR)

| Company | Workflows Found | Skill Candidates | Treasury Hooks | Data Quality | Key Insight |
|---------|-----------------|------------------|----------------|--------------|-------------|
| AppFolio | 4 | 20 | 3 | 8/10 | Strong AI focus; three-way reconciliation is key |
| Buildium | 5 | 9 | 3 | 8/10 | AvidXchange integration for AP automation |
| Yardi | 3 | 4 | 2 | 6/10 | Dominant player; complex workflow engine |
| Entrata | 2 | 5 | 3 | 7/10 | Open API provides integration opportunities |
| RealPage | 7 | 15 | 4 | 8/10 | Extensive API; strong trust accounting |
| MRI Software | - | - | - | 4/10 | Limited public documentation available |
| Hemlane | 5 | 9 | 3 | 8/10 | Hybrid model; eliminates traditional trust accounts |
| Stessa | 6 | 29 | 3 | 8/10 | Investor-centric; lacks formal approval workflows |
| Landlord Finance OS | 7 | 11 | 3 | 9/10 | AI-powered bookkeeping; integrated banking |

### HOA/Condo

| Company | Workflows Found | Skill Candidates | Treasury Hooks | Data Quality | Key Insight |
|---------|-----------------|------------------|----------------|--------------|-------------|
| Vantaca | 7 | 9 | 3 | 8/10 | Strong workflow automation; global settings limitation |
| CINC Systems | 4 | 11 | 3 | 7/10 | AI-powered "Cephai"; AvidXchange integration |
| Enumerate | 4 | 25 | 3 | 5/10 | SmartBanking feature for AI-powered reconciliation |

### Payments Layer

| Company | Workflows Found | Skill Candidates | Treasury Hooks | Data Quality | Key Insight |
|---------|-----------------|------------------|----------------|--------------|-------------|
| Zego | 5 | 25 | 3 | 6/10 | Comprehensive payment platform; strong integrations |
| PayLease | 4 | 9 | 3 | 5/10 | Payment processing focused; limited workflow docs |
| ClickPay | 4 | 10 | 3 | 6/10 | Receivables platform; no AP functionality |
| BILT Rewards | 1 | 3 | 1 | 3/10 | Renter-focused; limited PM features |
| AvidXchange | 1 | 6 | 3 | 7/10 | Highly configurable AP approval workflow |

### AI-Native PMS Solutions

| Company | Workflows Found | Skill Candidates | Treasury Hooks | Data Quality | Key Insight |
|---------|-----------------|------------------|----------------|--------------|-------------|
| BetsyAI | 2 | 8 | 2 | 7/10 | AI-layer on existing PMS; revenue from upsells |
| BoomAI | 5 | 15 | 3 | 7/10 | Agentic AI for property management |
| InnteloAIPMS | 2 | 13 | 3 | 3/10 | Guest experience focused; limited finance features |
| VisitoAIPMS | 7 | 10 | 3 | 7/10 | Conversational AI; needs deep workflow integration |
| Project Citadel | 3 | 15 | 4 | 6/10 | Tokenization model; AI Operator for zero staff |
| AI Property Management | 7 | 35 | 3 | 8/10 | Comprehensive AI platform; unified data model |

---

## Key Insights Across All Companies

### Common Patterns

1. **Trust Accounting is Foundational**: Nearly all LTR and STR platforms emphasize the separation of operating and trust funds. This is a regulatory requirement and a key differentiator for property finance.

2. **Three-Way Reconciliation**: AppFolio's three-way reconciliation (bank statement, bank ledger, trust liability balances) is a best practice that should be incorporated into the Bank Reconciliation skill.

3. **AvidXchange Integration**: Multiple platforms (Buildium, AppFolio, Vantaca, CINC) integrate with AvidXchange for AP automation, indicating it is a de facto standard in the industry.

4. **Owner Portal is Critical**: Guesty, Hostfully, and others highlight the Owner Portal as a key feature for distributing statements and managing owner relationships.

5. **AI is Emerging**: Platforms like AppFolio (Realm-X AI), CINC (Cephai), and the AI-native solutions are investing heavily in AI for automation and data-driven insights.

### Treasury Capture Opportunities

The research identified the following primary treasury capture hooks across vendors:

| Hook | Description | Companies with Strong Implementation |
|------|-------------|--------------------------------------|
| AP Approvals | Owning the approval workflow for vendor invoices | AppFolio, Buildium, AvidXchange, Vantaca |
| Owner Payouts | Calculating and initiating owner distributions | Guesty, Hemlane, Landlord Finance OS |
| Fund Segregation | Managing the separation of operating vs. trust/reserve funds | AppFolio, Buildium, Vantaca, Guesty |
| Payment Batch Preparation | Creating ready-to-pay batches for vendor and owner payments | AvidXchange, Zego |

---

## Skill Library Structure

The extracted knowledge has been organized into a skill library with the following structure:

```
skills/
├── control_plane/           # 9 skills (CP-001 to CP-009)
├── integrations/            # 5 skills (INT-001 to INT-005)
├── property_finance_core/   # 5 skills (FIN-001 to FIN-005)
├── ap_ar/                   # 6 skills (AP-001 to AP-004, AR-001 to AR-002)
├── trust_reserves_compliance/  # 4 skills (TR-001 to TR-004)
├── reporting_owner_board/   # 3 skills (REP-001 to REP-003)
├── treasury_payments/       # 6 skills (TRE-001 to TRE-006)
└── risk_audit/              # 2 skills (RA-001 to RA-002)
```

### P0 Skills (Build First)

| Skill ID | Skill Name | Priority Rationale |
|----------|------------|-------------------|
| FIN-002 | Bank Reconciliation | Highest pain point; most standardized workflow |
| REP-001 | Owner Statement Generation | Recurring monthly artifact; high owner visibility |
| AP-002 | Invoice Triage & Coding | High volume; significant time savings |
| AP-004 | Payables Approval & Scheduling | Treasury capture hook; approval ownership |
| TRE-003 | Payment Batch Preparation | Non-custodial treasury entry point |
| CP-001 | Policy & Permissioning | Foundation for all other skills |
| CP-007 | Audit Log & Decision Trace | Required for compliance and trust |

---

## Deliverables

The following files are included in this research package:

| File | Description |
|------|-------------|
| `pms_company_research.csv` | Raw research results for all 31 companies |
| `knowledge/vendors/*.md` | Individual knowledge documents for each company |
| `vendors_knowledge_base.zip` | Compressed archive of all vendor knowledge documents |
| `skill_manifest.yaml` | YAML manifest defining the skill library structure |
| `skills/` | Skill library folder structure with P0 skill templates |
| `skills_library.zip` | Compressed archive of the skill library |

---

## Recommended Next Steps

1. **Review Vendor Knowledge Documents**: Examine the individual knowledge documents for each company to validate the extracted workflows and identify additional details.

2. **Prioritize by Vertical**: Based on your go-to-market strategy, select STR, LTR, or HOA/Condo as the initial focus and prioritize skills accordingly.

3. **Build P0 Skills**: Start with the P0 skills (Bank Reconciliation, Owner Statement Generation, Invoice Triage) to create the "digital workforce in production" starter pack.

4. **Create Training Data**: Use the "Training Data Candidates" sections in each knowledge document to create synthetic training cases and evaluation tests.

5. **Integrate with Target Platforms**: Prioritize integrations with the most common platforms (AppFolio, Buildium, Guesty, Yardi) to maximize market coverage.

---

*Research completed by Manus AI — January 7, 2026*
