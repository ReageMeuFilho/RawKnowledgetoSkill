# AppFolio Research

## 1. Company Overview


AppFolio is a cloud-based property management software provider that offers a comprehensive platform, the AppFolio Performance Platform, designed to streamline operations for property management companies. Their platform is built with a focus on delivering value to residents, owners, and property management teams. AppFolio's solutions cater to a wide range of property types, including multifamily, single-family, student housing, affordable housing, community associations, and commercial properties. They also offer solutions for investment management. The company emphasizes its AI-powered features, unified data, and the ability to generate new revenue streams for its clients. AppFolio's platform includes features for leasing, maintenance, accounting, and communication, all accessible from a single interface.

**Products:**
* AppFolio Property Manager
* AppFolio Investment Management
* Realm-X AI

**Target Markets:**
* Multifamily
* Single-Family
* Student Housing
* Affordable Housing
* Community Associations
* Commercial
* Investment Management


## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

The Owner Statement is a document that summarizes the status of the operating cash account for an owner's properties for a selected time period. It is not a formal financial report, but rather a simple summary to give the owner an overview of their properties cash related transactions. The Owner Statement is typically the lead item in the owner packet that is sent out each month, it may also be generated as an individual document at any time desired.

**How to Run an Owner Statement:**

1.  Login with a user account that has permissions to perform this function.
2.  Find the owner you wish to view by:
    *   Using the AppFolio Search: Near the top right of the AppFolio screen, in the Search box, enter the name of the desired owner, when presented with search results, click the name of the owner.
3.  The owner page will load in the right-side Task pane in the Letters section, click the link for Owner Statement.
4.  The Owner Statement will load in a new tab/window.
5.  To change statement settings like properties and date range, at the top-right of the statement click the Customize tab.
6.  On the Report Options page, make your selections and click Run Report, the report will regenerate displaying according to your selections.

**Owner Statement Sections:**

*   **The Management Company Name:** The management company name, address & statement period.
*   **Owner Information:** The owner name, address & properties reflected on the statement (if more than one will show consolidated #).
*   **Cash Flow Summary:** Cash flow summary listing all income and expense transactions for the period and properties selected, only reflects the cash operating account, ending balance is income minus expenses.
*   **Bills Due:** Lists all outstanding bills due for payment.
*   **Property Cash Summary:** Lists reserve and prepaid items on the property balance.


### Bank Reconciliation

AppFolio offers a three-way reconciliation process to ensure that your accounting records accurately match your bank statements. This process involves reconciling three checkpoints on the same date to reflect identical totals.

**The Three Way Reconciliation Process:**

*   **Check Point #1: Bank Reconciliation Report**
    *   Statement Balance
    *   Plus: Deposits and Other Debits
    *   Less: Outstanding Checks and Other Credits
    *   Available Balance as of
    *   Total
*   **Check Point #2: Bank Account Activity Report**
    *   Ending Bank Book Balance as of
    *   Plus: Undeposited Receipts
    *   Available Balance as of
    *   Total
*   **Check Point #3: Bank Balance Detail**
    *   Available Balance as of
    *   Total

All three checkpoints must be reconciled on the same date and reflect identical totals.


### AP: Invoice Intake → Coding → Approvals → Payments

AppFolio offers AP automation solutions to increase efficiency, visibility, and control in the AP process. They have a seamless integration with AvidXchange, which is connected to a large supplier network, enabling users to process invoices and make payments without paper.

**Key features of AppFolio's AP workflow:**

*   **Go Paperless:** Receive, track, and approve invoices digitally, reducing the cost of managing paper invoices and minimizing errors.
*   **Design Processes and Workflows:** Create custom approval processes and workflows to suit your needs. Invoices can be automatically coded, assigned to the proper workflow, and routed electronically for approval.
*   **Scale for Growth:** Streamline payment processes with payment automation, allowing your AP team to handle a growing workload and focus on value-added projects.
*   **Pay Suppliers Faster:** Pay suppliers on time and with their preferred payment method, fostering better vendor relationships.


### AR: Rent Roll → Collections → Notices → Adjustments

AppFolio provides a process for managing delinquencies and sending notices to tenants.

**Delinquency Reporting and Notices:**

1.  **Creating a Delinquency Report:** On the 5th of each month, a 'Delinquency (As Of)' report is generated from the reports section of AppFolio. This report shows all tenants with outstanding balances.
2.  **Sending Notice of Late Rent:** If a tenant has not paid their rent, a 'Notice of Late Rent Breach of Lease' is generated in Zipform, filled out, and sent to the Property Manager (PM) for signature via DocuSign. Once signed, the notice is sent to the tenant via AppFolio with an email template.
3.  **Notice to Vacate:** If the tenant has still not paid by the 10th of the month, a 'Notice to Vacate' is generated in Zipforms, signed by the PM via DocuSign, and sent to the tenant with an email template.

**Email Templates:**

*   **Late Rent Notice:** A formal notice sent to the tenant informing them of their overdue rent and the amount owed. It warns of potential late fees and eviction proceedings if the matter is not addressed promptly.
*   **Notice to Vacate:** An official notice to vacate the property due to nonpayment of rent. It specifies the amount owed, the deadline to vacate, and the potential for legal action.


## 3. Data Model and Artifacts

Based on the integration with LeadSimple, the following data entities are synced from AppFolio:

*   **Owners**
*   **Tenants**
*   **Applicants**
*   **Vendors**
*   **Properties**
*   **Units**

This suggests that AppFolio's data model is centered around these core entities. The integration also syncs delinquent rent and amount receivable, which indicates that these are key data points within the system.


## 4. Skill Candidates

Based on the research, the following skill candidates have been identified:

*   **CP-001:** Onboard new property
*   **CP-002:** Onboard new owner
*   **CP-003:** Onboard new tenant
*   **INT-001:** Integrate with bank feeds
*   **FIN-001:** Reconcile bank accounts
*   **FIN-002:** Process owner payouts
*   **FIN-003:** Match transactions
*   **FIN-004:** Handle reconciliation exceptions
*   **FIN-005:** Record rent payments and adjustments
*   **AP-001:** Process invoices
*   **AP-002:** Code invoices
*   **AP-003:** Manage invoice approvals
*   **AP-004:** Process vendor payments
*   **AR-001:** Manage rent roll
*   **AR-002:** Process collections and notices
*   **TR-001:** Manage trust accounts
*   **TR-002:** Handle security deposits
*   **REP-001:** Generate owner statements
*   **TRE-001:** Own approval workflows
*   **TRE-002:** Calculate owner distributions

## 5. Treasury Capture Opportunities

*   **AP Workflow:** An AI agent could own the approval of invoices and the processing of vendor payments. This would involve setting up rules for automatic approvals based on certain criteria (e.g., amount, vendor) and flagging exceptions for manual review.
*   **Owner Payouts:** An AI agent could automatically calculate and process owner payouts based on collected rent and expenses.
*   **Fund Segregation:** An AI agent could manage the segregation of funds, ensuring that security deposits and other trust funds are held in separate accounts.


### Trust/Escrow/Security Deposit Handling

AppFolio recommends establishing two separate trust accounts for handling funds:

*   **Security Deposit Trust Account:** Used exclusively for holding tenant security deposits.
*   **Operating Trust Account:** Used for collecting rents and paying bills.

This separation of funds helps to ensure compliance with state laws and provides a clear audit trail. Key practices for managing trust accounts include:

*   **Avoiding Commingling:** Never mix personal or business funds with trust funds.
*   **Accurate Record-Keeping:** Maintain a chronological record of all transactions, a separate record for each beneficiary or transaction, and a record of all bank deposits.
*   **Regular Reconciliation:** Reconcile trust accounts on a regular basis to ensure that your records match the bank's records.
