# VisitoAIPMS: Analogous Research for AI Skill Library

## 1. Company Overview

VisitoAIPMS is presented as a no-code, multi-channel conversational AI platform designed for businesses to create and manage intelligent AI agents. The primary focus of the platform, as detailed in the provided Product Requirements Document (PRD), is on automating customer communication across various channels like WhatsApp, Instagram, and web chat. While the PRD positions VisitoAIPMS within the hospitality vertical, its core functionality is centered on conversational AI rather than the operational and financial workflows typically found in a dedicated Property Management System (PMS).

To fulfill the research requirements for building a comprehensive AI skills library for the property management vertical, this document presents findings from an analogous study of two leading PMS platforms: **Buildium** and **AppFolio**. This approach allows for the extraction of detailed operational know-how that can be translated into the required skill candidates.

| Feature | VisitoAIPMS (from PRD) | Buildium (Analogous Research) | AppFolio (Analogous Research) |
| :--- | :--- | :--- | :--- |
| **Primary Focus** | Conversational AI | Full-service PMS | Full-service PMS |
| **Target Audience** | SMBs in hospitality, e-commerce, etc. | Residential, commercial, HOA, student housing | Residential, commercial, HOA, student housing, investment management |
| **Core Strength** | No-code AI agent builder | Comprehensive property accounting and management | AI-powered automation and unified platform |

## 2. Workflow Deep Dives

The following sections provide a detailed analysis of the seven key property management workflows, based on the features and capabilities of Buildium and AppFolio.

### Owner Statements & Payouts

| Feature | Buildium | AppFolio |
| :--- | :--- | :--- |
| **Owner Statements** | Generates owner statements, but some users on Reddit have reported them to be confusing. | Provides a clear owner statement report. |
| **Owner Payouts** | Implied through accounting features. | Supports owner payouts via eCheck. |

### Bank Reconciliation

| Feature | Buildium | AppFolio |
| :--- | :--- | :--- |
| **Automation** | Automatic bank reconciliation. | Automated bank reconciliation with Plaid integration. |
| **Process** | Manual matching of transactions against bank statements. | Automated transaction matching. |
| **Reporting** | Generates a reconciliation report. | Generates a reconciliation report. |

### Accounts Payable (AP)

| Feature | Buildium | AppFolio |
| :--- | :--- | :--- |
| **Invoice Intake** | Can turn work orders into bills. | Smart Bill Entry feature for automated intake. |
| **Approvals** | Not explicitly mentioned. | Bill Approval Flows for streamlined approvals. |
| **Payments** | Online bill pay, including recurring payments. | Payments via eCheck. |

### Accounts Receivable (AR)

| Feature | Buildium | AppFolio |
| :--- | :--- | :--- |
| **Rent Collection** | Online rent collection. | Online rent collection with automated late fees. |
| **Adjustments** | Implied through financial reporting. | Bulk tenant charges and payment plans. |
| **Collections** | Not explicitly mentioned. | Standardized tenant debt collection workflows. |

### Trust/Escrow/Security Deposit Handling

| Feature | Buildium | AppFolio |
| :--- | :--- | :--- |
| **Trust Accounting** | Supports trust accounting rules. | Supports trust accounting. |
| **Deposits** | Tracks fees, deposits, and refunds. | Allows for holding and refunding deposits from escrow. |

### Reserves Management (HOA/Condo)

Neither Buildium nor AppFolio provide specific, detailed information on their public-facing websites regarding the management of operating versus reserve funds for HOAs and Condos.

### Month-End Close & Reporting

| Feature | Buildium | AppFolio |
| :--- | :--- | :--- |
| **Reporting Suite** | Full suite of financial reports. | Customizable reports including income statements, cash flow statements, and balance sheets. |

## 3. Data Model and Artifacts

Based on the features of Buildium and AppFolio, the following data model entities and artifacts can be inferred:

*   **Data Model Entities:** Property, Unit, Owner, Tenant, Vendor, GL Account, Fund, Bank Account.
*   **Artifacts:** Owner Statements, Bank Reconciliation Reports, Invoices, Bills, Work Orders, Leases, Rent Rolls, 1099s, Financial Statements.

## 4. Skill Candidates

The following skill candidates have been identified based on the research findings:

*   **CP-001:** Owner Statement Generation
*   **CP-002:** Owner Payout Processing
*   **FIN-001:** Bank Reconciliation
*   **AP-001:** Invoice Intake & Coding
*   **AP-002:** Invoice Approval Routing
*   **AP-003:** Invoice Payment Processing
*   **AR-001:** Rent Roll Processing & Collections
*   **AR-002:** Late Fee Assessment & Notice Generation
*   **TR-001:** Security Deposit Handling
*   **REP-001:** Month-End Reporting Package Generation

## 5. Treasury Capture Opportunities

The following are key areas where an AI agent could provide significant value in treasury management:

*   **Approvals:** Automating the approval process for invoices and owner payouts, based on predefined rules and thresholds.
*   **Payouts:** Initiating and tracking owner and vendor payments, ensuring timely and accurate disbursements.
*   **Fund Segregation:** Monitoring and maintaining the segregation of funds between operating accounts, reserve accounts, and tenant security deposits.

## 6. Training Data Candidates

To train an AI agent on these skills, the following types of data would be required:

*   Sample owner statements from various PMS platforms.
*   Anonymized bank statements and transaction data for reconciliation practice.
*   A diverse set of invoices and bills, including different formats and line items.
*   Sample lease agreements and rent rolls with various scenarios (e.g., prorated rent, mid-cycle move-ins).
*   Examples of month-end reporting packages from different property management companies.
