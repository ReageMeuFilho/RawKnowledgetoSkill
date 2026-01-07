# Landlord Finance OS Knowledge Document

## 1. Company Overview

**Products:** Landlord Finance OS is a financial platform for real estate investors that combines banking, bookkeeping, rent collection, tenant management, and financial services into a single, integrated solution.

**Verticals:** The primary vertical is LTR (Long-Term Rentals), with a focus on individual landlords and small property management companies.

**Market Position:** The platform aims to be an all-in-one financial operating system for real estate investors, differentiating itself by offering real banking accounts, property-specific organization, AI-powered bookkeeping, and a focus on IRS Schedule E for tax preparation.

**Strengths:**
*   Integrated platform combining banking, bookkeeping, and property management.
*   Real FDIC-insured bank accounts.
*   AI-powered bookkeeping and automated transaction categorization.
*   Freemium model to drive user adoption.

**Limitations:**
*   As a new product, it may lack the feature depth and brand recognition of established competitors.
*   The reliance on a partner bank introduces a dependency on a third party for core banking functionalities.


## 2. Workflow Deep Dives

## 3. Data Model and Artifacts

## 4. Skill Candidates

## 5. Treasury Capture Opportunities

## 6. Training Data Candidates

### 2.1 Owner Statements / Owner Payouts

**Procedure:**
1.  **Data Aggregation:** The system aggregates all income (rent, fees) and expenses (management fees, maintenance costs) for each property owner over a specified period (typically monthly).
2.  **Statement Generation:** A detailed owner statement is generated, itemizing all transactions. This statement includes rental income, other income, management fees, maintenance expenses, and any other relevant charges.
3.  **Validation:** The system (and potentially a property manager) validates the statement for accuracy, ensuring all transactions are correctly categorized and allocated to the right property and owner.
4.  **Distribution:** The owner statement is made available to the owner through the owner portal. The owner receives a notification (email or in-app) that their statement is ready.
5.  **Payout Calculation:** The net payout to the owner is calculated by subtracting total expenses from total income.
6.  **Payout Execution:** The calculated payout amount is transferred to the owner's designated bank account via ACH transfer.

**Inputs:**
*   Rental income data
*   Fee income data
*   Maintenance and other expense data
*   Owner and property information
*   Owner bank account details

**Outputs:**
*   Owner Statement (PDF or digital view)
*   Owner Payout (ACH transfer)

**Roles/Permissions:**
*   **Property Manager:** Can view, generate, and validate owner statements. Can initiate owner payouts.
*   **Owner:** Can view and download their own statements. Can view payout history.

**Edge Cases & Exception Handling:**
*   **Negative Balance:** If an owner's property has a negative cash flow for the period, the payout is zero, and the negative balance may be carried over to the next period or require a contribution from the owner.
*   **Disputes:** Owners may dispute charges on their statement. A process for reviewing and resolving disputes is required.

**Common Failure Modes:**
*   **Incorrect Transaction Categorization:** Miscategorized expenses can lead to inaccurate statements and payouts.
*   **Delayed Payouts:** Delays in ACH processing can cause owner dissatisfaction.

### 2.2 Bank Reconciliation

**Procedure:**
1.  **Transaction Syncing:** The platform automatically syncs bank transactions from the user's connected bank accounts (both internal Landlord Finance OS accounts and external accounts connected via Plaid).
2.  **Automated Matching:** The system's AI-powered engine attempts to automatically match synced bank transactions with transactions recorded in the bookkeeping module (e.g., rent payments, expense entries).
3.  **Exception Handling:** Transactions that cannot be automatically matched are flagged as 'unreconciled' and presented to the user for manual review and categorization.
4.  **Reconciliation Reporting:** The system provides a reconciliation report that shows the reconciled and unreconciled transactions for a given period, helping the user to identify discrepancies.

**Inputs:**
*   Bank transaction data (from internal and external accounts)
*   Bookkeeping transaction data

**Outputs:**
*   Reconciliation Report
*   List of unreconciled transactions

**Roles/Permissions:**
*   **Bookkeeper/Property Manager:** Can perform bank reconciliation, categorize transactions, and view reconciliation reports.

**Edge Cases & Exception Handling:**
*   **Duplicate Transactions:** The system should be able to detect and flag potential duplicate transactions.
*   **Timing Differences:** The system should account for timing differences between when a transaction is recorded and when it clears the bank.

**Common Failure Modes:**
*   **Sync Errors:** Connectivity issues with the bank can lead to incomplete or delayed transaction syncing.
*   **Incorrect Matching:** The AI may incorrectly match transactions, requiring manual correction.

### 2.3 AP: Invoice Intake → Coding → Approvals → Payments
**Procedure:**
1.  **Invoice Intake:** Invoices can be received via email forwarding or by uploading a file (PDF, JPG, PNG) into the system.
2.  **AI-Powered Data Extraction:** The system uses AI to automatically extract key information from the invoice, such as vendor name, invoice number, amount, and due date.
3.  **Coding:** The user (or an AI assistant) codes the invoice to the appropriate property, unit, and expense category. The system may suggest a category based on the vendor and invoice details.
4.  **Approval Workflow:** If an approval workflow is configured, the invoice is routed to the designated approver(s) for review. Approvers are notified via email or in-app notification.
5.  **Payment:** Once approved, the invoice can be paid directly from the platform via ACH, wire transfer, or by mailing a check.

**Inputs:**
*   Invoice file (PDF, JPG, PNG)
*   Vendor information
*   Property and unit details
*   Expense categories

**Outputs:**
*   Bill payment (ACH, wire, check)
*   Updated expense records in the bookkeeping module

**Roles/Permissions:**
*   **Bookkeeper/Property Manager:** Can upload, code, and pay invoices.
*   **Approver:** Can approve or reject invoices.

**Edge Cases & Exception Handling:**
*   **Duplicate Invoices:** The system should detect and flag potential duplicate invoices from the same vendor for the same amount and date range.
*   **Approval Rejection:** If an invoice is rejected, it is sent back to the submitter with a reason for rejection.

**Common Failure Modes:**
*   **Incorrect Data Extraction:** The AI may fail to extract information from the invoice correctly, requiring manual correction.
*   **Approval Bottlenecks:** Delays in the approval process can lead to late payments.

### 2.4 AR: Rent Roll → Collections → Notices → Adjustments

**Procedure:**
1.  **Rent Roll Generation:** The system generates a rent roll for each property, showing the status of each tenant's rent payment for the current period.
2.  **Automated Invoicing and Reminders:** The system automatically sends rent invoices and payment reminders to tenants via email or in-app notification.
3.  **Online Rent Collection:** Tenants can pay their rent online via ACH or credit/debit card through the tenant portal.
4.  **Automated Late Fees:** If rent is not paid by the due date, the system automatically assesses a late fee according to the terms of the lease.
5.  **Notices:** The system can generate and send various notices to tenants, such as late rent notices or notices to quit, based on pre-defined templates.
6.  **Adjustments:** The property manager can make adjustments to a tenant's ledger, such as waiving a late fee or applying a credit.

**Inputs:**
*   Lease agreements (rent amount, due date, late fee policy)
*   Tenant information
*   Payment data

**Outputs:**
*   Rent Roll report
*   Tenant statements
*   Notices to tenants

**Roles/Permissions:**
*   **Property Manager:** Can view the rent roll, send notices, and make adjustments.
*   **Tenant:** Can view their payment history, make payments, and receive notices.

**Edge Cases & Exception Handling:**
*   **Partial Payments:** The system should be able to handle partial rent payments and track the remaining balance.
*   **Bounced Payments:** If a tenant's payment is returned (e.g., due to insufficient funds), the system should reverse the payment and assess any applicable fees.

**Common Failure Modes:**
*   **Incorrect Lease Terms:** If the lease terms are entered incorrectly into the system, it can lead to incorrect rent amounts, due dates, and late fees.
*   **Tenant Disputes:** Tenants may dispute charges on their account, requiring a manual review and resolution process.

### 2.5 Trust/Escrow/Security Deposit Handling

**Procedure:**
1.  **Account Setup:** The platform allows for the creation of dedicated trust, escrow, or security deposit accounts that are separate from operating accounts. These accounts can be set up to comply with state-specific regulations.
2.  **Deposit Collection:** When a new lease is signed, the security deposit is collected from the tenant and deposited into the designated security deposit account.
3.  **Interest Tracking:** For states that require it, the system tracks the interest earned on security deposits and allocates it to the appropriate tenant.
4.  **Funds Disbursement:** At the end of the lease, the property manager can disburse the security deposit back to the tenant, or deduct for damages, from the security deposit account. The system provides a clear audit trail of all security deposit transactions.

**Inputs:**
*   Lease agreement (security deposit amount)
*   Tenant information
*   Bank account details for security deposit account

**Outputs:**
*   Security deposit statement
*   Disbursement of security deposit funds

**Roles/Permissions:**
*   **Property Manager:** Can set up security deposit accounts, collect and disburse security deposits.
*   **Tenant:** Can view their security deposit balance.

**Edge Cases & Exception Handling:**
*   **Disputes over Deductions:** If a tenant disputes deductions from their security deposit, the property manager must provide documentation to justify the deductions. The platform should allow for the storage of move-in and move-out inspection reports to support these claims.

**Common Failure Modes:**
*   **Commingling of Funds:** Failure to keep security deposits in a separate account from operating funds can lead to legal and financial penalties.
*   **Incorrect Interest Calculation:** Forgetting to calculate or incorrectly calculating interest on security deposits can lead to disputes with tenants.

### 2.6 Reserves (HOA/Condo): operating vs reserves management
**Procedure:**
1.  **Fund Segregation:** The platform allows for the creation of separate bank accounts for operating funds and reserve funds, ensuring clear segregation as required by law for HOAs and Condos.
2.  **Budgeting and Funding:** The system facilitates the creation of annual budgets, including contributions to the reserve fund for future capital expenditures. Reserve contributions are collected from homeowners as part of their regular assessments.
3.  **Reserve Study Integration:** While not explicitly mentioned in the PRD, a complete solution would integrate with reserve study providers or allow for the manual input of a reserve study to track the funding status of key components (roofs, elevators, etc.).
4.  **Expense Allocation:** Expenses are carefully allocated to either the operating fund or the reserve fund. Operating expenses are for the day-to-day management of the property, while reserve expenses are for major repairs and replacements.
5.  **Reporting:** The platform provides clear reporting on the financial health of both the operating and reserve funds, including the current balance, contributions, and expenditures.

**Inputs:**
*   Annual budget
*   Reserve study
*   Homeowner assessment payments
*   Vendor invoices for operating and reserve expenses

**Outputs:**
*   Balance sheet showing segregated operating and reserve funds
*   Income and expense statement for both operating and reserve funds
*   Reserve fund status report

**Roles/Permissions:**
*   **Property Manager/HOA Board Member:** Can set up budgets, allocate expenses, and view reports.

**Edge Cases & Exception Handling:**
*   **Underfunded Reserves:** If the reserve fund is underfunded, the system should highlight this and provide tools to model catch-up contributions.
*   **Special Assessments:** The system should be able to handle special assessments for unexpected major expenses.

**Common Failure Modes:**
*   **Improper Use of Reserve Funds:** Using reserve funds for operating expenses is a common failure mode that can lead to legal issues. The platform should have controls in place to prevent this.
*   **Inadequate Reserve Funding:** Failure to adequately fund the reserve account can lead to financial distress when major repairs are needed.

### 2.7 Month-End Close Checklist + Reporting Pack

**Procedure:**
1.  **Bank Reconciliation:** The first step in the month-end close process is to reconcile all bank accounts to ensure that all transactions have been recorded and categorized correctly.
2.  **Review Income and Expenses:** Review the income and expense statement for the month to identify any anomalies or miscategorized transactions.
3.  **Accruals:** Make any necessary accrual entries for income that has been earned but not yet received, or expenses that have been incurred but not yet paid.
4.  **Generate Reporting Pack:** Once the books are closed for the month, the system generates a comprehensive reporting pack, which may include:
    *   Income Statement
    *   Balance Sheet
    *   Cash Flow Statement
    *   Rent Roll
    *   Owner Statements
    *   Budget vs. Actuals Report
5.  **Distribute Reports:** The reporting pack is distributed to stakeholders, such as property owners and investors.

**Inputs:**
*   All transactional data for the month
*   Bank statements

**Outputs:**
*   A comprehensive month-end reporting pack

**Roles/Permissions:**
*   **Bookkeeper/Property Manager:** Can perform the month-end close process and generate reports.
*   **Owner/Investor:** Can view the month-end reports.

**Edge Cases & Exception Handling:**
*   **Late Invoices:** A process should be in place to handle invoices that are received after the month has been closed.

**Common Failure Modes:**
*   **Incomplete Bank Reconciliation:** Failure to fully reconcile all bank accounts can lead to inaccurate financial statements.
*   **Errors in Data Entry:** Manual data entry errors can lead to inaccuracies in the financial reports.

### 3.1 Data Model Entities

*   **Property:** Represents a single rental property.
*   **Unit:** Represents a single rentable unit within a property.
*   **Owner:** Represents the owner of a property.
*   **Tenant:** Represents the tenant leasing a unit.
*   **Vendor:** Represents a supplier of goods or services.
*   **GL Account:** Represents an account in the general ledger.
*   **Fund:** Represents a pool of money, such as an operating fund or a reserve fund.
*   **Bank Account:** Represents a bank account held by the landlord.

### 3.2 Artifacts

*   **Owner Statement:** A report for property owners detailing income and expenses for their properties.
*   **Rent Roll:** A report showing the rent status for all tenants in a property.
*   **Reconciliation Report:** A report showing the reconciliation status of bank accounts.
*   **Month-End Reporting Pack:** A collection of financial reports generated at the end of each month.
*   **Invoices:** Bills from vendors for goods or services.
*   **Leases:** Legal contracts between landlords and tenants.

### 4.1 Skill Candidates


*   **CP-001: Owner Statement Generation:** The platform's ability to generate detailed owner statements maps directly to this skill.
(Content truncated due to size limit. Use page ranges or line ranges to read remaining content)