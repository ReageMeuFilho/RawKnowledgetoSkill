# AI Property Management Platform - Knowledge Document

## 1. Company Overview

**Products:** The company is developing a comprehensive, AI-powered property management platform designed to compete with and surpass market leaders like Entrata, EliseAI, Roam, and MagicDoor. The platform will serve a wide range of property types, including multifamily, single-family, student housing, affordable housing, commercial, and community associations. The core offerings are built on three pillars: intelligent automation, unified operations, and exceptional user experiences.

**Verticals:** The primary vertical is **AI PMS**, with a focus on providing a next-generation property management solution driven by artificial intelligence.

**Market Position:** The company aims to achieve a top-three market position within three years of launch. The platform is designed to be a market leader, combining the best features of its competitors while introducing innovative capabilities.

**Strengths:**
*   **AI-Native Architecture:** Built from the ground up with AI at its core, enabling high automation rates.
*   **Comprehensive Feature Set:** Combines features that are currently fragmented across competitors, such as Voice AI, a resident portal, and accounting, into a single platform.
*   **Unified Data Layer:** Ensures a single source of truth across all modules and services.
*   **Scalable and Extensible:** Modern, cloud-native architecture allows for scalability and the addition of new features over time.

**Limitations:**
*   **New Market Entrant:** As a new platform, it will need to build brand recognition and trust.
*   **Competition:** The property management software market is competitive, with established players.

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

**Objective:** To generate, validate, and distribute owner statements and payouts in a timely and transparent manner.

**Exact Steps and Procedures:**

1.  **Data Collection:** Gather all financial information for the reporting period. This includes rental income, ancillary income, and all expenses.
2.  **Data Organization:** Categorize all income and expenses and track them for each property separately.
3.  **Statement Generation:** Use a property management software or a template to create a clear and professional owner statement.
4.  **Validation:** Review the statement for accuracy to ensure all financial information is recorded correctly.
5.  **Distribution:** Deliver the owner statement to the property owner in a timely manner and be prepared to answer any questions.

### Bank Reconciliation

**Objective:** To ensure the accuracy of financial records by matching the transactions in the accounting system with the bank statements.

**Exact Steps and Procedures:**

1.  **Gather Documents:** Collect the bank statement and the corresponding accounting records.
2.  **Compare Transactions:** Match the deposits and withdrawals in the accounting system with those on the bank statement.
3.  **Identify Discrepancies:** Look for outstanding checks, deposits in transit, and any transactions on the bank statement that are not in the accounting records.
4.  **Adjust Records:** Make necessary adjustments in the accounting records for any discrepancies found.
5.  **Calculate and Compare Adjusted Balances:** Ensure that the adjusted bank statement balance matches the adjusted accounting records balance.

### AP: Invoice Intake → Coding → Approvals → Payments

**Objective:** To efficiently process and pay vendor invoices while maintaining accurate financial records and strong vendor relationships.

**Exact Steps and Procedures:**

1.  **Invoice Intake/Capture:** Invoices are received and the data is accurately captured.
2.  **Invoice Coding & Review:** The invoice is reviewed for accuracy, matched with purchase orders, and coded to the appropriate GL account and property.
3.  **Approval Workflow:** The coded invoice is routed for approval.
4.  **Payment Authorization:** Once approved, the payment is authorized.
5.  **Payment Execution:** The authorized payment is executed and the accounting system is updated.

### AR: Rent Roll → Collections → Notices → Adjustments

**Objective:** To effectively manage the accounts receivable process, from rent collection to handling delinquencies.

**Exact Steps and Procedures:**

1.  **Rent Roll Generation:** Generate a rent roll that provides a summary of rental income.
2.  **Rent Collection:** Collect rent from tenants.
3.  **Delinquency Management:** Identify and manage delinquent accounts.
4.  **Notices:** Send out late payment notices and other communications to tenants.
5.  **Adjustments:** Make any necessary adjustments to tenant accounts.

### Trust/Escrow/Security Deposit Handling

**Objective:** To properly manage and account for funds held in trust, such as security deposits, in compliance with legal and ethical requirements.

**Exact Steps and Procedures:**

1.  **Establish Trust Accounts:** Set up separate trust or escrow accounts for each property owner.
2.  **Deposit Funds:** Deposit all security deposits and other trust funds into the designated trust account in a timely manner.
3.  **Record Keeping:** Maintain accurate and detailed records of all trust account transactions.
4.  **Reconciliation:** Reconcile trust accounts regularly.
5.  **Disbursement:** Disburse the security deposit according to the terms of the lease agreement and state and local laws.

### Reserves (HOA/Condo): operating vs reserves management

**Objective:** To properly manage and differentiate between operating funds and reserve funds to ensure the financial stability of an HOA or condo association.

**Exact Steps and Procedures:**

1.  **Establish Separate Accounts:** Maintain two separate bank accounts: one for operating funds and one for reserve funds.
2.  **Fund Allocation:** Allocate a portion of homeowner association fees to each fund.
3.  **Operating Fund Management:** Use the operating fund for predictable, recurring expenses.
4.  **Reserve Fund Management:** Use the reserve fund for major projects and unexpected emergencies.
5.  **Reserve Study:** Conduct a reserve study every 3-5 years to determine the appropriate level of reserve funding.

### Month-end close checklist + reporting pack

**Objective:** To ensure a timely and accurate month-end close and to provide comprehensive financial reports to stakeholders.

**Exact Steps and Procedures:**

1.  **Pre-Close Preparation:** Confirm opening balances, clean up payables and expenses, reconcile cash and cards, update the rent roll, and track pending journals and accruals.
2.  **Core Month-End Closing:** Reconcile the general ledger, finalize payroll, book all accruals, handle CAM allocations, apply rent payments, and review any capital expense or budget reclasses.
3.  **Compliance, Controls & Review:** Run a 2-step review for all GL entries, verify role-based access, audit trail spot checks, check documentation completeness, and validate investor reporting readiness.
4.  **Reporting:** Generate a comprehensive reporting pack that includes a P&L statement, balance sheet, cash flow statement, and other relevant reports.

## 3. Data Model and Artifacts

**Data Model Entities:**

*   **Property:** PropertyID, Name, Address, City, State, PostalCode, MainPhone, FaxNumber, pUnitCount
*   **Building:** BuildingID, Name, BuildingTypeID, PropertyID, ManagerID
*   **Unit:** UnitID, BuildingID, UnitNumber, RoomCount, BathroomCount, SquareFootage, FloorPlan, Notes, Vehicle, Floor
*   **Guest/Tenant:** GuestID, FirstName, LastName, CompanyName, DateOfBirth, PhoneNumber, EmailAddress
*   **Vendor:** (Not explicitly defined in the provided data model, but a standard entity in property management)
*   **GL Account:** (Not explicitly defined, but a standard entity for accounting)
*   **Fund:** (Not explicitly defined, but relevant for HOA/Condo management)
*   **Bank Account:** (Not explicitly defined, but essential for financial management)

**Artifacts:**

*   Owner Statements
*   Bank Reconciliation Reports
*   AP Aging Reports
*   Rent Rolls
*   Lease Agreements
*   Financial Statements (P&L, Balance Sheet, Cash Flow)

## 4. Skill Candidates

*   **CP-001 - CP-009:** Core property management tasks such as tenant and lease management, maintenance, and inspections.
*   **INT-001 - INT-005:** Integration with other systems, such as accounting software, CRMs, and marketing platforms.
*   **FIN-001 - FIN-005:** Financial management tasks, including budgeting, forecasting, and financial reporting.
*   **AP-001 - AP-004:** Accounts payable workflows, from invoice processing to payment.
*   **AR-001 - AR-002:** Accounts receivable workflows, including rent collection and delinquency management.
*   **TR-001 - TR-004:** Treasury management tasks, such as cash management and bank reconciliation.
*   **REP-001 - REP-003:** Reporting and analytics, including generating standard and custom reports.
*   **TRE-001 - TRE-006:** Treasury and risk management, including fraud detection and compliance.
*   **RA-001 - RA-002:** Regulatory and compliance tasks, such as tax and audit support.

## 5. Treasury Capture Opportunities

*   **Invoice Approval and Payment:** An AI agent could be used to automate the approval of invoices and the execution of payments, reducing manual effort and the risk of errors.
*   **Owner Payouts:** The calculation and distribution of owner payouts could be automated, ensuring accuracy and timeliness.
*   **Fund Segregation:** An AI agent could be used to manage the segregation of funds, such as security deposits and reserve funds, to ensure compliance with legal and regulatory requirements.

## 6. Training Data Candidates

*   **Example Artifacts:** Sample owner statements, invoices, leases, and financial reports can be used to train an AI model to understand and process these documents.
*   **Edge Cases:** Examples of disputed invoices, delinquent tenant accounts, and other exception scenarios can be used to train an AI model to handle these situations.
*   **Evaluation Scenarios:** A set of test cases can be developed to evaluate the performance of an AI model in various scenarios.
