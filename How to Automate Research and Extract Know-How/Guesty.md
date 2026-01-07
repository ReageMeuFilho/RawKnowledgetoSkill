# Guesty Knowledge Document

## 1. Company Overview

Guesty is a cloud-based Property Management System (PMS) for short-term rentals (STR). It unifies operations across multiple booking channels like Airbnb, Booking.com, and Vrbo. The platform provides a single control plane for inventory management, dynamic pricing, guest communications, task automation, financial operations, and owner reporting. Guesty targets a wide range of users, from individual hosts with a few listings to large enterprise operators with hundreds of properties. Their core value proposition is to eliminate channel fragmentation, reduce manual operational overhead, enable data-driven revenue optimization, automate guest and operational workflows, and provide a compliant financial infrastructure.


## 2. Workflow Deep Dives

### 2.1 Owner Statements & Payouts

Guesty's Owner Portal is the primary interface for managing owner statements and payouts. The process can be broken down as follows:

**1. Setup:**
- Owner statements are part of the Accounting feature, which is a premium add-on.
- Business models must be set up to define how revenue and expenses are shared between the property management company (PMC) and the owner.
- The owner statement template can be customized (Default or Credit/Debit) to control how financial data is presented.
- Brands can be applied to statements for white-labeling.
- The language of the statement can be set in the owner's profile.

**2. Generation:**
- Owner statements are generated automatically on the 1st of the month (or a custom date) for the previous calendar month.
- Statements can also be generated manually.

**3. Review and Approval:**
- PMCs can preview, approve, or flag statements for review.
- If changes are made that affect a generated statement (e.g., business model update), the statement can be regenerated.

**4. Distribution:**
- Statements can be sent to owners individually or in bulk.
- Owners access their statements through the secure Owner Portal, which requires a password.

**5. Payouts:**
- The Owner Portal facilitates automated owner payments, though the exact mechanism for this is not detailed in the publicly available documentation. It is likely integrated with a payment processor like GuestyPay.

### 2.2 Bank Reconciliation

Guesty's bank reconciliation feature is designed to help PMCs maintain trust account integrity and meet regulatory requirements. The process is as follows:

**1. Setup:**
- It is recommended to have two separate bank accounts: a trust account and an operational account.
- A pre-reconciliation process is required to clear past transactions when using the feature for the first time.

**2. Ongoing Maintenance:**
- Regularly group transactions.
- Move transactions from the default cash account to the correct account.
- Record payment processor fees, reserves, channel commission payments, bank fees, and interest.

**3. Reconciliation Process:**
- Create a new reconciliation and set the end date.
- Enter the bank ending balance and optionally upload a bank statement.
- Review each transaction and clear it if it matches the bank statement.
- If a transaction is not to be cleared, it can be moved to the next period.
- Once the difference between cleared transactions and the bank ending balance is zero, the reconciliation can be submitted.
- A reconciliation statement (report) is generated, showing the correlation between the bank balance and the cash balance in Guesty, as well as any uncleared transactions.
- If a journal entry with a past date is added to a reconciled period, the reconciliation needs to be resubmitted.

### 2.3 Accounts Payable (AP)

Guesty's AP workflow appears to be centered around the ability to upload and attach invoices to transactions and journal entries. This suggests the following process:

**1. Invoice Intake:**
- Invoices from vendors are received by the PMC.
- These invoices can be uploaded into Guesty as attachments to transactions or journal entries.

**2. Coding and Approvals:**
- The documentation does not provide explicit details on invoice coding and approval workflows. However, it can be inferred that when a transaction or journal entry is created for a vendor payment, the appropriate expense account would be selected (coding).
- Approval workflows are not explicitly mentioned, but it is likely that they are handled through user roles and permissions within the Guesty platform.

**3. Payments:**
- The documentation does not provide specific details on how vendor payments are processed. It is possible that payments are made outside of the Guesty platform and then recorded as transactions in Guesty.


### 2.4 Accounts Receivable (AR)

Guesty's AR workflow is primarily focused on collecting payments from guests for reservations. The process can be summarized as follows:

**1. Rent Roll/Collections:**
- Guesty automatically collects payments from guests based on the payment schedule of the booking channel (e.g., Airbnb, Booking.com) or the payment rules set up for direct bookings.
- The platform supports automated payment rules and auto-payments.

**2. Notices and Adjustments:**
- The documentation does not provide specific details on sending notices for late payments or making adjustments to guest invoices. However, it is likely that these actions can be managed through the Guesty platform.


### 2.5 Trust, Escrow, and Security Deposit Handling
Guesty's Accounting feature is built on the principles of trust accounting. This is crucial for property managers who hold funds on behalf of guests and owners.

**Key Principles:**
- **Separate Bank Accounts:** Guesty strongly recommends maintaining two separate bank accounts: a trust account for holding client funds (rents, deposits) and an operating account for business expenses.
- **No Commingling of Funds:** The system is designed to prevent the mixing of trust funds with operational funds, which is a legal requirement in many jurisdictions.
- **Clear Audit Trail:** Trust accounting provides a clear audit trail of all transactions, making it easier to track the ownership of funds and ensure compliance.

**Workflow:**
1. All rents and deposits are received into the trust account.
2. Earned management fees and approved owner reimbursements are transferred from the trust account to the operating account.
3. This transfer is recorded as a single cash-moving transaction in the system (a withdrawal from the trust side and a deposit on the operating side).

### 2.6 Reserves Management (HOA/Condo)

Guesty is primarily focused on short-term rentals (STR) and does not appear to have specific features for HOA/Condo reserves management. The search for "reserves management" in the Help Center returned results related to Stripe's rolling reserve, which is a mechanism for managing risk in payment processing, not for managing operating vs. reserves funds for HOAs or condos.


### 2.7 Month-End Close

Guesty's month-end close process is centered around the concept of locking accounting periods. This feature helps to ensure the integrity of financial data and prevent accidental changes to past records.

**1. Locking Accounting Periods:**
- By default, accounting periods lock on the 10th day of the following month. For example, transactions from March will lock on April 10th.
- This setting can be customized to lock periods monthly or annually.

**2. User Roles and Permissions:**
- Once a period is locked, only users with specific roles (Account Admin, Account Manager, Admin, or Accountant) can make changes to transactions within that period.

**3. Month-End Checklist:**
- While Guesty does not provide a specific month-end close checklist, the following steps can be inferred from the documentation:
    - Reconcile all bank accounts.
    - Review and approve all owner statements.
    - Process all owner payouts.
    - Lock the accounting period.


## 3. Data Model and Artifacts

Based on the research, Guesty's data model appears to include the following entities:

- **Property:** The core entity, representing a rental unit.
- **Unit:** A sub-entity of a property, likely used for multi-unit properties.
- **Owner:** The owner of a property.
- **Tenant/Guest:** The individual renting a property.
- **Vendor:** A third-party service provider.
- **GL Account:** A general ledger account for tracking financial transactions.
- **Fund:** Not explicitly mentioned, but implied by the trust accounting features.
- **Bank Account:** Bank accounts for trust and operational funds.

**Artifacts:**

- **Owner Statement:** A monthly summary of revenue, expenses, and payments for a property owner.
- **Bank Reconciliation Statement:** A report that shows the correlation between the bank balance and the cash balance in Guesty.
- **Invoices:** Invoices can be uploaded and attached to transactions and journal entries.
- **Reports:** Guesty provides a variety of reports, including accounting reports, reservation reports, and analytics dashboards.

## 4. Skill Candidates

Based on the research, the following skill candidates have been identified:

- **CP-001: Owner Onboarding:** Capturing owner details, property information, and business model setup.
- **CP-002: Owner Statement Generation:** Automating the creation of monthly owner statements.
- **CP-003: Owner Payouts:** Processing owner payments based on approved statements.
- **FIN-001: Bank Reconciliation:** Matching bank transactions with Guesty records.
- **AP-001: Invoice Intake:** Uploading and attaching vendor invoices to transactions.
- **AR-001: Guest Payment Collection:** Automating the collection of guest payments for reservations.
- **TR-001: Trust Account Management:** Managing funds in the trust account and ensuring compliance with trust accounting principles.
- **REP-001: Report Generation:** Generating owner statements and bank reconciliation reports.
- **TRE-001: Month-End Close:** Locking accounting periods to ensure the integrity of financial data.

## 5. Treasury Capture Opportunities

The following treasury capture opportunities have been identified:

- **Owner Payouts:** An AI agent could own the approval and processing of owner payouts, ensuring that payments are accurate and timely.
- **Vendor Payments:** An AI agent could manage the entire vendor payment process, from invoice intake to payment execution.
- **Fund Segregation:** An AI agent could monitor the trust account to ensure that funds are properly segregated and that there is no commingling of funds.

## 6. Training Data Candidates


The following training data candidates have been identified:

- **Owner Statements:** Sample owner statements can be used to train an AI agent to understand the format and content of these documents.
- **Bank Reconciliation Reports:** Sample reconciliation reports can be used to train an AI agent to identify and resolve discrepancies.
- **Vendor Invoices:** A collection of vendor invoices can be used to train an AI agent to extract key information, such as vendor name, invoice number, and amount due.
- **Edge Cases:** The documentation mentions several edge cases, such as what to do if a journal entry with a past date is added to a reconciled period. These edge cases can be used to create training scenarios for an AI agent.