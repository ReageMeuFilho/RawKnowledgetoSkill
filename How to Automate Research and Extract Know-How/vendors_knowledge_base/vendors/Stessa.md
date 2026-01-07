# Stessa Knowledge Document

## 1. Company Overview

Stessa is a property management software platform designed for real estate investors. It is a subsidiary of Roofstock and aims to provide an all-in-one solution for managing the entire real estate investment lifecycle, from acquisition to exit. The platform is primarily focused on the LTR (Long-Term Rental) and Finance verticals, catering to a wide range of investors, from those with a single property to those with large portfolios. Stessa's core value proposition is to replace spreadsheets and fragmented tools with an intelligent, automated system that simplifies property management, accounting, and financial tracking.

### Products and Services

Stessa offers a freemium SaaS model with three tiers: Essentials (free), Manage, and Pro. The platform's key features include:

*   **Property Acquisition:** An investment property marketplace powered by Roofstock, providing institutional-grade data for property evaluation.
*   **Accounting and Bookkeeping:** Automated income and expense tracking, smart receipt scanning, and a real estate-specific chart of accounts.
*   **Financial Reporting:** A suite of investor-focused reports, including Net Cash Flow, Income Statement, Schedule of Real Estate Owned (SREO), and a tax-ready Schedule E.
*   **Landlord Banking:** High-yield business checking accounts for each property, offered in partnership with Thread Bank, with features like property-specific debit cards and competitive APY.
*   **Rent Collection:** Automated online rent collection with tenant reminders and late fee enforcement.
*   **Leasing and Tenant Management:** Tools for vacancy marketing, tenant screening (via RentPrep), and e-signing of lease agreements (via DocuSign).
*   **Maintenance Tracking:** A system for logging, tracking, and managing maintenance requests.

### Market Position, Strengths, and Limitations

Stessa positions itself as a unique, vertically integrated platform for real estate investors, competing with spreadsheets, generic accounting software, and traditional property management software. Its key strengths include:

*   **Investor-Centric Focus:** The platform is specifically designed for the needs of real estate investors, offering relevant metrics and reports.
*   **Integrated Ecosystem:** Stessa combines property management, accounting, and banking in a single platform, providing a seamless user experience.
*   **Freemium Model:** The free Essentials tier provides a powerful entry point for new investors, driving user acquisition.
*   **Data-Driven Insights:** The platform provides valuable data and analytics to help investors make informed decisions.

However, Stessa also has some limitations:

*   **Limited Customization:** The platform's reporting and features are not as customizable as some of its competitors.
*   **Customer Support:** Some users have reported slow response times from customer support.
*   **Dependence on Integrations:** The platform relies on third-party integrations for some of its key features, which can sometimes lead to issues.

## 2. Workflow Deep Dives

This section provides a detailed analysis of the key operational workflows within the Stessa platform, based on the available documentation and user feedback.

### 2.1. Owner Statements / Owner Payouts

Stessa does not have a traditional "owner statement" in the same way a third-party property manager would. Instead, it provides a suite of reports that an owner can use to understand their portfolio's performance. The primary reports that serve this function are the **Income Statement**, **Net Cash Flow Report**, and the **Schedule of Real Estate Owned (SREO)**. For tax purposes, Stessa generates a **Schedule E** report. The process for generating these reports is as follows:

1.  **Data Aggregation:** All income and expense transactions are automatically collected through linked bank accounts (via Plaid) or manually entered.
2.  **Categorization:** Transactions are categorized according to a real estate-specific chart of accounts.
3.  **Report Generation:** The user can generate the desired reports from the "Reports" tab in the application. Reports can be filtered by date range and property.
4.  **Distribution:** Reports can be exported to PDF or Excel for sharing with partners, accountants, or for personal records.

There is no explicit "owner payout" workflow within Stessa, as the platform is designed for the property owner to manage their own finances. Payouts would be handled through the owner's own bank accounts, which are linked to Stessa for tracking purposes.

### 2.2. Bank Reconciliation

Stessa's bank reconciliation process is largely automated through its bank connection feature, which uses Plaid to link to users' bank accounts. The workflow is as follows:

1.  **Bank Connection:** The user links their bank accounts, credit cards, and mortgage accounts to Stessa.
2.  **Transaction Import:** Stessa automatically imports all transactions from the linked accounts.
3.  **Transaction Review:** New transactions appear in the "Needs Review" tab, where the user can categorize them.
4.  **Matching:** Stessa's system automatically matches transactions to properties based on the user's rules and past behavior. The user can also manually match transactions.
5.  **Reconciliation:** While there isn't a formal reconciliation feature in the traditional accounting sense, the continuous import and categorization of transactions effectively keeps the user's books reconciled with their bank statements in real-time.

**Edge Cases and Exception Handling:**

*   **Connection Issues:** Bank connections can sometimes break, requiring the user to re-authenticate or troubleshoot the connection.
*   **Duplicate Transactions:** Occasionally, duplicate transactions may be imported, which need to be manually deleted.
*   **Missing Transactions:** If transactions are missing, the user can manually add them or upload a CSV file from their bank.

### 2.3. AP: Invoice Intake → Coding → Approvals → Payments

Stessa's accounts payable workflow is more focused on expense tracking than a full-cycle AP process. It does not have a formal approval workflow for invoices. The process is as follows:

1.  **Invoice Intake:** Invoices and receipts can be captured in several ways:
    *   **Smart Receipt Scanning:** Using the mobile app's camera to scan and OCR the document.
    *   **Email Forwarding:** Forwarding receipt emails to a dedicated Stessa email address.
    *   **Manual Entry:** Manually entering the expense details.
    *   **File Upload:** Uploading a CSV/Excel file of transactions.
2.  **Coding:** Once a transaction is created, it needs to be categorized using Stessa's chart of accounts. This is done in the "Transactions" tab.
3.  **Approvals:** There is no approval workflow in Stessa. The property owner is responsible for reviewing and approving all expenses.
4.  **Payments:** Stessa does not directly handle bill payments. Payments are made through the user's linked bank accounts, and the transactions are then imported into Stessa for tracking.

### 2.4. AR: Rent Roll → Collections → Notices → Adjustments

Stessa has a relatively robust accounts receivable workflow, centered around its rent collection and tenant management features.

1.  **Rent Roll:** The **Rent Roll** report provides a comprehensive overview of all units, leases, and tenants. It is automatically populated from the lease information entered by the user.
2.  **Collections:** Stessa automates the rent collection process:
    *   **Online Payments:** Tenants can pay rent online via ACH, credit card, or debit card.
    *   **Reminders:** Automated reminders are sent to tenants before rent is due.
    *   **Late Fees:** Late fees can be automatically assessed and added to the tenant's ledger.
3.  **Notices:** While Stessa does not generate legal notices, it does provide lease agreement templates and allows for e-signing via DocuSign.
4.  **Adjustments:** The **Tenant Ledger** tracks all charges, payments, and balances for each tenant. Adjustments, such as prorated rent or concessions, can be manually added to the ledger.

### 2.5. Trust/Escrow/Security Deposit Handling

Stessa provides a clear workflow for handling security deposits:

1.  **Recording the Deposit:** When a security deposit is received, it is recorded as a liability. The transaction is categorized as "Security Deposit" in Stessa.
2.  **Holding the Deposit:** The deposit is held in a separate bank account, which can be one of Stessa's Landlord Banking accounts.
3.  **Applying or Returning the Deposit:** At the end of the lease, the deposit can be either applied to unpaid rent or damages, or returned to the tenant. Stessa provides two distinct workflows for this:
    *   **Applying the Deposit:** A new income transaction is created to offset the expense of the damages or unpaid rent. The security deposit liability is then reduced by the same amount.
    *   **Returning the Deposit:** A new expense transaction is created to record the return of the deposit to the tenant. The security deposit liability is then zeroed out.

### 2.6. Reserves (HOA/Condo)

Stessa's features are not specifically designed for HOA/Condo management, and there is no mention of operating vs. reserves management in the documentation. This is a key limitation of the platform for this vertical.

### 2.7. Month-End Close Checklist + Reporting Pack

Stessa does not have a formal month-end close checklist. However, the platform's real-time nature and suite of reports make the month-end process relatively straightforward. A typical month-end process in Stessa would involve:

1.  **Reviewing Transactions:** Ensuring all transactions for the month have been imported and categorized correctly.
2.  **Reviewing the Rent Roll:** Verifying that all rent payments have been received and recorded.
3.  **Generating Reports:** Generating the month-end reporting pack, which would typically include:
    *   **Income Statement**
    *   **Net Cash Flow Report**
    *   **Balance Sheet**
    *   **Tenant Ledger**

These reports can be exported to PDF or Excel for record-keeping and analysis.

## 3. Data Model and Artifacts

This section outlines the core data entities that make up the Stessa platform, as well as the key artifacts that are produced.

### 3.1. Data Model Entities

The Stessa platform is built around a set of interconnected data entities:

*   **User:** Represents the account holder, their subscription tier, and authentication credentials.
*   **Property:** The central entity, containing address, specifications, valuation, and associations to other entities.
*   **Transaction:** Represents a single financial event (income or expense) linked to a property.
*   **Tenant/Lease:** Contains tenant information and the terms of their lease agreement.
*   **Banking Account:** Represents a Landlord Banking account linked to a property.
*   **Report:** Stores the configuration and generated output of a financial report.

### 3.2. Artifacts

The Stessa platform produces a variety of artifacts that are used for financial management, reporting, and record-keeping:

*   **Reports:** The primary artifacts produced by Stessa are its financial reports, which include:
    *   Income Statement
    *   Net Cash Flow Report
    *   Schedule of Real Estate Owned (SREO)
    *   Schedule E (for tax purposes)
    *   Tenant Ledger
*   **Exports:** Reports and other data can be exported in both **Excel** and **PDF** formats.
*   **Invoices/Receipts:** Scanned or uploaded invoices and receipts are stored as digital artifacts linked to their corresponding transactions.
*   **Lease Agreements:** Executed lease agreements are stored as digital documents within the platform.

## 4. Skill Candidates

This section maps the findings from the research to the predefined skill IDs for the AI Digital Workforce Manager.

| Skill ID | Skill Name | Stessa Platform Mapping |
|---|---|---|
| **Core Property** | | |
| CP-001 | Property Onboarding | Stessa has a guided onboarding process for adding new properties. |
| CP-002 | Unit Onboarding | For multi-family properties, users can add and manage individual units. |
| CP-003 | Lease Abstracting | Lease details such as term dates, rent amount, and security deposit are tracked. |
| CP-004 | Tenant Onboarding | Stessa supports tenant screening and lease signing. |
| CP-005 | Tenant Move-Out | The platform has a workflow for applying or returning security deposits. |
| CP-006 | Maintenance Request Handling | A maintenance tracking feature allows for logging and managing requests. |
| CP-007 | Vendor Management | Implied in the maintenance workflow, but not an explicit feature. |
| CP-008 | Owner Onboarding | The entire platform is designed for owner onboarding and use. |
| CP-009 | Portfolio Setup | Users can create and manage multiple portfolios (Pro feature). |
| **Integrations** | | |
| INT-001 | Bank Feed Integration | Core feature, powered by Plaid. |
| INT-002 | PMS Integration | AppFolio integration is mentioned for syncing owner statements. |
| INT-003 | Insurance Integration | Partnership for insurance referrals is mentioned. |
| INT-004 | Lending/Mortgage Integration | Mortgage details and payments can be tracked. |
| INT-005 | Legal/Forms Integration | DocuSign integration for e-signing and access to legal forms. |
| **Financial Ops** | | |
| FIN-001 | Bank Reconciliation | Automated through bank feeds and transaction categorization. |
| FIN-002 | Chart of Accounts Mgmt | Uses a real estate-specific chart of accounts. |
| FIN-003 | Journal Entry Creation | Manual transaction entry serves this purpose. |
| FIN-004 | Month-End Close | Supported by a suite of on-demand financial reports. |
| FIN-005 | Year-End Close / Tax Prep | The Schedule E report is a key feature for tax preparation. |
| **Accounts Payable**| | |
| AP-001 | Invoice Processing | Supported by receipt scanning, email forwarding, and manual entry. |
| AP-002 | Bill Payment | Not directly supported; payments are tracked after the fact. |
| AP-003 | Vendor Payment | Not directly supported. |
| AP-004 | Approval Workflows | No formal approval workflows are available. |
| **Accounts Receivable**| | |
| AR-001 | Rent Collection | Fully automated online rent collection is a core feature. |
| AR-002 | Late Fee Management | Late fees can be automatically assessed. |
| **Trust Accounting**| | |
| TR-001 | Security Deposit Mgmt | A clear workflow for recording and handling security deposits exists. |
| TR-002 | Escrow Management | Escrow payments are mentioned as a transaction category. |
| TR-003 | Owner Contributions | Tracked as a transaction category. |
| TR-004 | Trust Account Reconciliation | Handled as part of the general bank reconciliation process. |
| **Reporting** | | |
| REP-001 | Owner Statements | Generated through a combination of reports like the Income Statement. |
| REP-002 | Financial Reporting Package | A full suite of financial reports is available. |
| REP-003 | Performance Dashboards | Real-time dashboards with key performance metrics are a central feature. |
| **Treasury** | | |
| TRE-001 | Cash Management | The Landlord Banking feature provides high-yield accounts. |
| TRE-002 | Payment Approval | Not supported. |
| TRE-003 | Payout Automation | Not supported. |
| TRE-004 | Fund Segregation | Landlord Banking allows for separate accounts per property. |
| TRE-005 | Yield Optimization | High-yield APY on cash balances is a key feature. |
| TRE-006 | Fraud Detection | Not explicitly mentioned, but implied through secure banking partnerships. |
| **Risk & Audit** | | |
| RA-001 | Approval Policy Enforcement | Not supported due to the lack of approval workflows. |
| RA-002 | Audit Trail | Not explicitly mentioned, but transaction history serves as a basic audit trail. |

## 5. Treasury Capture Opportunities

This section identifies key points in the Stessa workflow where an AI agent could potentially take ownership of approvals, payouts, and fund segregation to create a more robust treasury management system.

*   **Payment Approvals:** Stessa currently lacks any formal approval workflows. An AI agent could be integrated to review and approve payments based on predefined rules, such as invoice amount, vendor history, and budget compliance. This would be particularly valuable for larger portfolios with multiple properties and vendors.
*   **Payout Automation:** While Stessa tracks expenses, it does not automate the payment process. An AI agent could be used to automate bill payments, owner distributions, and other payouts, triggered by approved invoices or scheduled events. This would streamline the payment process and reduce manual effort.
*   **Fund Segregation:** Stessa's Landlord Banking feature allows for separate bank accounts for each property, which is a good first step towards fund segregation. However, an AI agent could further enhance this by automatically allocating funds to different reserves (e.g., operating, capital expenditures, security deposits) based on predefined rules and cash flow projections.

## 6. Training Data Candidates

This section identifies potential sources of training data from the Stessa ecosystem that could be used to build and evaluate the AI skills.

*   **Example Artifacts:**
    *   **Financial Reports:** The various financial reports generated by Stessa (Income Statement, Net Cash Flow, Schedule E) can be used as examples of well-structured financial data.
    *   **Transaction Data:** The categorized transaction data from users' accounts can be used to train models for automated expense categorization and anomaly detection.
    *   **Lease Agreements:** Anonymized lease agreements can be used to train models for lease abstraction and key data extraction.
*   **Edge Cases and Evaluation Scenarios:**
    *   **Bank Connection Errors:** The user-reported issues with bank connections can be used to create scenarios for testing the robustness of the bank feed integration.
    *   **Complex Transactions:** Transactions that are split between multiple properties or categories can be used to test the model's ability to handle complex accounting scenarios.
    *   **Tenant Disputes:** Scenarios involving tenant disputes over rent, fees, or security deposits can be used to evaluate the model's ability to handle exception cases in the accounts receivable workflow.
