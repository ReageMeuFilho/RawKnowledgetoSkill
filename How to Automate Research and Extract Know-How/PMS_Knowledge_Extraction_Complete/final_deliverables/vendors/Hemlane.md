


# Hemlane Knowledge Document

## 1. Company Overview

Hemlane is a property management platform catering primarily to the long-term residential rental (LTR) market. It offers a hybrid model that combines a self-service software platform with optional, human-in-the-loop managed services. This allows Hemlane to serve a wide range of users, from DIY landlords with a few properties to professional property managers and real estate brokerages.

The platform aims to automate and simplify the entire rental lifecycle, including marketing, tenant screening, lease management, rent collection, maintenance coordination, and financial accounting. Hemlane's tiered pricing model provides a scalable solution, starting with a free tier and extending to a full-service offering.

**Products and Services:**

*   **Software Platform:** Core features include listing syndication, applicant screening, lease management with e-signatures, online rent collection, automated late fees, document storage, and tenant messaging.
*   **Managed Services:** Optional, human-powered services such as 24/7 repair coordination, full tenant communication handling, tenant placement, and eviction support.

**Market Position:**

Hemlane targets DIY landlords with 1-10 units as its primary market. Secondary markets include small property managers (10-50 units) and landlords seeking a more passive investment approach. Its competitive advantages include its tiered service model, 24/7 repair coordination without vendor markup, a functional free tier, integrated state-specific legal compliance, and a user-friendly interface.

**Strengths:**

*   Hybrid software and service model offers flexibility.
*   Strong focus on automation of the rental lifecycle.
*   Comprehensive feature set covering financials, maintenance, and leasing.
*   Positive user reviews often highlight customer service and ease of use.

**Limitations:**

*   Some user reviews mention a decline in service quality.
*   The platform is primarily focused on the LTR market, with less support for other verticals like STR or HOA/Condo.

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

Hemlane provides several financial reports that serve as owner statements. These reports can be generated and downloaded from the 'Reports' tab in the platform.

**Generating Owner Statements:**

*   **Statement of Cash Flow:** This report details income and operating expenses, mortgages and loans, capital expenses, and liabilities. It can be filtered by a specific user and time frame.
*   **Income Statement:** This report shows income and expenses for paid or in-transit transactions. It can also be filtered by user and time frame.
*   **Lease Ledger:** This report shows the balance due from tenants.
*   **Schedule E:** This report reflects income/losses for the rental property and can be used for tax purposes.
*   **Rent Roll:** This report provides an overview of rental income.

**Validation and Distribution:**

*   The reports are generated based on the financial data within the Hemlane platform.
*   Owners can download these reports and have them sent to their email inbox.
*   Hemlane does not automatically send monthly statements, but it does send a monthly summary email to subscription bill-to users.

**Payouts:**

*   Hemlane uses ACH payment processing, which generally takes 3 business days for paying customers with verified accounts.
*   Owners can set up automatic payments for recurring expenses.
*   The platform provides a reference ID for each transaction to help match payments to bank account statements.

### Bank Reconciliation

Hemlane's bank reconciliation process is centered around its "Bank Sync" feature, which uses Plaid to connect to users' bank accounts.

**Matching:**

*   **Bank Sync:** Users can connect their bank accounts to Hemlane, which then automatically imports transactions. This feature can sync up to two years of historical data, although some banks have shorter limits.
*   **Transaction Matching:** Once transactions are imported, users can assign them to specific properties and categorize them. For payments processed through Hemlane, a unique Reference ID is provided to facilitate matching with bank statements.
*   **Manual Entry:** For transactions that occur outside of Hemlane, users can manually enter them and mark them as "offline transactions." The Bank Sync feature can also help automate the tracking of these offline transactions.

**Exceptions:**

*   The documentation does not explicitly detail a process for handling exceptions. However, the ability to manually categorize and assign transactions provides a way to manage discrepancies.

**Posting Plans:**

*   The documentation does not mention specific "posting plans." The system appears to rely on the user to categorize and assign transactions as they are imported.

### AP: Invoice Intake → Coding → Approvals → Payments

Hemlane's accounts payable workflow is integrated with its maintenance and repair features.

**Invoice Intake:**

*   Service professionals (vendors) can be added to the Hemlane account.
*   When a maintenance request is initiated, a work order can be created and assigned to a service professional.
*   The service professional can then upload an invoice directly to the work order.

**Coding:**

*   Once an invoice is received, the user can record it as a transaction in Hemlane.
*   During this process, the transaction can be assigned to one or more properties and categorized for accounting purposes.

**Approvals:**

*   The property owner or manager reviews the invoice within the work order.
*   The documentation does not specify a formal, multi-step approval process. The review of the invoice by the owner serves as the primary approval.

**Payments:**

*   **Offline Payments:** The user can pay the service professional outside of Hemlane and then record the payment in the system as an "offline transaction."
*   **Repair Billing (Complete Package Only):** For users on the "Complete" plan, Hemlane offers a "Repair Billing" service that manages and initiates payments to service professionals.



### AR: Rent Roll → Collections → Notices → Adjustments

Hemlane's accounts receivable process is primarily focused on rent collection.

**Rent Roll:**

*   Hemlane provides a "Rent Roll" report that gives an overview of rental income.
*   The "Lease Ledger" report also tracks the balance due from tenants.

**Collections:**

*   Users can set up recurring or one-time payment requests for rent.
*   Tenants can pay online via ACH or credit/debit card.
*   The platform sends automatic reminders for upcoming and late payments.

**Notices:**

*   Hemlane sends automatic late payment reminders one day after the due date and every Monday thereafter until the payment is made.
*   The system can be configured to automatically assess late fees.

**Adjustments:**

*   Users can make rent adjustments, such as concessions or other one-time changes.
*   The platform allows for partial payments to be enabled on recurring payment requests.

### Trust/Escrow/Security Deposit Handling

Hemlane's model aims to eliminate the need for traditional trust accounts for property managers.

**Security Deposits:**

*   Hemlane allows landlords to request security deposits from tenants as a one-time payment.
*   The platform can also be used to refund security deposits to tenants.

**Trust and Escrow:**

*   Hemlane's core philosophy is to have rent and other payments flow directly to the property owner's bank account, bypassing the need for a property manager to hold funds in a trust account.
*   For property managers managing rentals on behalf of other owners, Hemlane's platform is designed to facilitate direct payments from tenants to owners.
*   The platform's "Allocate Rent" feature allows property management fees to be automatically split off and routed to the manager's account.
*   Similarly, for maintenance and repairs, the owner can be set as the billing contact, so that repair bills are paid directly from the owner's account.

_The following sections are based on the analysis of the available information and the Hemlane PRD. Direct documentation on some of these topics is limited, so some aspects are inferred from the platform's overall functionality._

### Reserves (HOA/Condo): Operating vs. Reserves Management

Hemlane's primary focus is on the long-term residential rental market, and there is no specific information available regarding features for managing HOA or condo reserves. The platform's accounting features are geared towards individual landlords and property managers, not the more complex financial management required for HOAs.

### Month-End Close Checklist + Reporting Pack

Hemlane does not provide a formal month-end close checklist. However, the platform offers a suite of financial reports that can be used to create a reporting pack:

*   **Income Statement:** Provides a P&L report for a selected period.
*   **Statement of Cash Flow:** Reports on income, expenses, and liabilities.
*   **Rent Roll:** Summarizes rental income.
*   **Lease Ledger:** Shows tenant balances.

These reports can be downloaded and compiled to form a comprehensive month-end reporting package.

## 3. Data Model and Artifacts

**Data Model Entities:**

*   **Property:** Represents a rental property, including details like address and unit information.
*   **Unit:** A specific unit within a property.
*   **Owner:** The property owner.
*   **Tenant:** The individual residing in a unit.
*   **Vendor:** Service professionals who perform maintenance and repairs.
*   **GL Account:** Transactions can be categorized, implying an underlying chart of accounts.
*   **Bank Account:** User's bank accounts are connected for payments and reconciliation.

**Artifacts:**

*   **Reports:** Income Statement, Statement of Cash Flow, Rent Roll, Lease Ledger, Schedule E.
*   **Exports:** Financial reports can be downloaded.
*   **Statements:** While not automatically generated, the financial reports serve as owner statements.

## 4. Skill Candidates

Based on the analysis of Hemlane's workflows, the following skill candidates have been identified:

*   **CP-001:** Generate Owner Statement
*   **CP-002:** Process Owner Payout
*   **FIN-001:** Reconcile Bank Account
*   **AP-001:** Process Invoice
*   **AP-002:** Approve Invoice
*   **AP-003:** Pay Invoice
*   **AR-001:** Collect Rent
*   **AR-002:** Assess Late Fees
*   **TR-001:** Manage Security Deposits

## 5. Treasury Capture Opportunities

*   **Approvals:** The review and approval of maintenance invoices present an opportunity for an AI agent to manage this process.
*   **Payouts:** The initiation of owner payouts and vendor payments could be automated by an AI agent.
*   **Fund Segregation:** While Hemlane's model avoids trust accounts, an AI agent could monitor and manage the flow of funds to ensure proper allocation.

## 6. Training Data Candidates

*   **Example Artifacts:** Sample financial reports (Income Statement, Rent Roll, etc.) can be used to train an AI to understand and generate these documents.
*   **Edge Cases:** Scenarios like partial payments, rent adjustments, and disputed charges can be used to train the AI on exception handling.
*   **Evaluation Scenarios:** The AI can be evaluated on its ability to accurately reconcile bank statements, generate owner statements, and process invoices.
