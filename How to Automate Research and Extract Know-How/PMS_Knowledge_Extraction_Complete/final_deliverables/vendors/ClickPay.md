# ClickPay Research



## Company Overview

ClickPay is a comprehensive payment platform designed for the real estate industry. It enables property managers and landlords to bill and collect payments from residents. The platform supports various payment methods, including credit cards, e-checks (ACH), and paper checks. ClickPay aims to automate the entire receivables process, from billing to reconciliation, and integrates with various accounting systems.

### Products and Services:

*   **Online Payments:** Custom-branded online and mobile payment portals for residents to pay rent, HOA fees, and other charges.
*   **Lockbox & Check Scanning:** A service designed to handle paper check processing and reduce manual data entry.
*   **Online Bill Pay:** Electronically sweeps payments initiated from a resident's bank, accelerating cash flow.
*   **e-Bill & Print Solutions:** Manages electronic and paper bill printing to reduce costs.
*   **Walk-in Payments:** Allows residents to pay with cash at over 35,000 locations.

### Verticals:

*   Property Managers
*   Association Managers (HOA/Condo)

### Market Position:

ClickPay positions itself as an all-in-one real estate receivable solution that consolidates paper-based and electronic payments. It emphasizes its real-time integration capabilities with accounting software, business rule automation, and premier customer service.

### Strengths:

*   **Comprehensive Payment Options:** Accepts a wide range of payment types.
*   **Accounting System Integration:** Offers real-time data syncing with property management accounting software.
*   **Automation:** Automates payment acceptance rules and business configurations.
*   **Security:** SSAE 16, PCI-DSS compliant, and uses SSL encryption.

### Limitations:

*   The website does not provide detailed information about specific workflows and procedures, requiring further investigation into their help center and other resources.


## Workflow Deep Dives

### 1. Owner Statements / Owner Payouts

**Procedure for generating owner statements:**

1.  Navigate to the **Financial Reports** tab.
2.  Select **Detailed Transactions Report**.
3.  Choose the desired **Management** and **LLC/Association** from the drop-down menus.
4.  Apply filters such as **Payment Type**, **Status**, and **Transaction Date** range.
5.  (Optional) Use the **Advanced** options for more specific filtering.
6.  Click **Search** to generate the report.
7.  Export the report in **Excel** or **PDF** format.

**Inputs and Data Fields:**

*   Management company
*   LLC/Association
*   Payment Type
*   Status
*   Transaction Date range

**Outputs/Artifacts:**

*   Detailed Transactions Report (Excel or PDF)

**Roles/Permissions:**

*   The user must have access to the **Financial Reports** tab.

**Edge Cases and Exception Handling:**

*   The chatbot suggests that if a pre-formatted statement per owner/lot is needed, the user should specify the required format and distribution method.

**Common Failure Modes:**

*   The standard report may not be in the desired format for all users.


### 2. Bank Reconciliation

**Procedure for bank reconciliation:**

1.  Go to the **Financial Reports** tab.
2.  Select **Bank Deposit Reports**.
3.  Enter the date range that you are reconciling.
4.  Click **Search**.
5.  Match each **LLC Deposit** amount and date to the deposits on the bank statement.
6.  Expand each deposit to view the individual payments.
7.  Repeat for each payment method.

**Inputs and Data Fields:**

*   Date range

**Outputs/Artifacts:**

*   Bank Deposit Report (Excel or PDF)

**Roles/Permissions:**

*   The user must have access to the **Financial Reports** tab.

**Edge Cases and Exception Handling:**

*   Each payment method (ACH, credit card, etc.) posts as a separate batch and must be reconciled individually.

**Common Failure Modes:**

*   Discrepancies between the ClickPay report and the bank statement require manual investigation.


### 3. AP: Invoice Intake → Coding → Approvals → Payments

ClickPay does not offer an Accounts Payable module. The platform is focused on receivables (resident/owner payments). Any AP-related functionalities, such as vendor payments or owner distributions, are handled outside of ClickPay, likely within the user's accounting system.


### 4. AR: Rent Roll → Collections → Notices → Adjustments

ClickPay's primary function is to process resident and owner payments, which is a key part of the Accounts Receivable process. The platform provides several reports to help property managers track and reconcile these payments.

**Procedure for managing AR:**

1.  **View Payment Activity:** Use the **Financial Reports** tab to access reports like the **Bank Deposit Report**, **Payment History**, **Detailed Transaction Report**, and **Returned Transaction Report**.
2.  **Take Payments:** Use the **In-Office Payment** tab to process payments received by phone or in person.

**Inputs and Data Fields:**

*   Building and Account/Address
*   Payer information
*   Payment amount
*   Payment method (ECheck or Credit Card)

**Outputs/Artifacts:**

*   Various financial reports (Excel or PDF)
*   Payment receipts

**Roles/Permissions:**

*   Access to the **Financial Reports** and **In-Office Payment** tabs.

**Edge Cases and Exception Handling:**

*   Returned/NSF payments can be viewed and researched using the **Returned Transaction Report**.

**Common Failure Modes:**

*   ClickPay does not handle the entire AR workflow (e.g., generating rent rolls, sending notices, or processing adjustments). These tasks are managed in the user's primary accounting system.


### 5. Trust/Escrow/Security Deposit Handling

ClickPay does not have a specific feature for managing trust, escrow, or security deposit accounts. All funds are routed to the LLC/association bank accounts that are set up in the system. To handle trust accounts, a new bank account must be added by submitting a bank account change request.


## Data Model and Artifacts

### Data Model Entities:

*   **Property/Building:** A physical property or building.
*   **Unit:** An individual unit within a property.
*   **Owner/Resident/Tenant:** The individual or entity responsible for making payments.
*   **LLC/Association:** The legal entity that owns and manages the property.
*   **Bank Account:** The financial account where payments are deposited.

### Artifacts:

*   **Detailed Transactions Report:** An exportable report (Excel or PDF) that provides a granular view of all transactions.
*   **Bank Deposit Report:** An exportable report (Excel or PDF) that shows all deposits made to the bank account.
*   **Payment History:** A report that allows users to locate individual payments and payer information.
*   **Returned Transaction Report:** A report for viewing and researching returned or NSF payments.
*   **Payment Receipt:** A printable receipt for in-office payments.


## Skill Candidates

### Core Payments (CP)

*   **CP-001: Process Online Payments:** ClickPay's core functionality is processing online payments from residents and owners.
*   **CP-002: Process E-Check (ACH) Payments:** ClickPay supports ACH payments.
*   **CP-003: Process Credit Card Payments:** ClickPay supports credit card payments.
*   **CP-004: Process Paper Check Payments:** ClickPay's Lockbox & Check Scanning service handles paper checks.
*   **CP-009: Handle Returned Payments:** The Returned Transaction Report allows users to manage returned/NSF payments.

### Integrations (INT)

*   **INT-001: Sync with Accounting Systems:** ClickPay integrates with various accounting systems to sync payment data.

### Financial Operations (FIN)

*   **FIN-001: Perform Bank Reconciliation:** The Bank Deposit Report is used to reconcile bank accounts.

### Accounts Receivable (AR)

*   **AR-001: Manage Receivables:** ClickPay is an accounts receivable platform that helps manage resident and owner payments.
*   **AR-002: Generate Invoices/Bills:** ClickPay's e-Bill & Print Solutions service manages the creation and distribution of bills.

### Reporting (REP)

*   **REP-001: Generate Financial Reports:** ClickPay provides various financial reports, including the Detailed Transactions Report and Bank Deposit Report.

## Treasury Capture Opportunities

*   **TRE-001: Own Payment Approvals:** While ClickPay does not have a built-in approval workflow, an AI agent could be implemented to review and approve payments before they are processed, adding a layer of control.
*   **TRE-002: Own Payout Execution:** An AI agent could be responsible for initiating and managing payouts to property owners based on predefined rules and schedules.
*   **TRE-005: Own Fund Segregation:** An AI agent could manage the allocation of funds to different bank accounts (e.g., operating vs. reserve funds) by leveraging ClickPay's ability to support multiple bank accounts.
