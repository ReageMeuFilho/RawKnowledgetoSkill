# BoomAI Knowledge Document

## 1. Company Overview

Boom is the world's first AI-powered Property Management System (AiPMS) designed for the short-term rental (STR), aparthotel, and boutique hotel markets. It is built as an AI-native platform to automate guest communications, streamline operations, and optimize revenue. 

- **Products:** The core of Boom's offering is its AI-native platform, which includes a Property Management System (PMS), Channel Manager, AI Guest Messaging (BAM - Business Agentic Manager), and Dynamic Pricing & Revenue Intelligence. 
- **Verticals:** The primary vertical is Short-Term Rentals (STR), with expansion into boutique hotels and aparthotels. The PRD also mentions future plans for long-term rentals.
- **Market Position:** Boom positions itself as a market leader in the AI-powered PMS space for STRs, with a strong emphasis on its agentic AI capabilities. It is operating in over 20 countries with a high Net Promoter Score (NPS) of 86.
- **Strengths:**
    - AI-native architecture, not a legacy system with AI bolted on.
    - Agentic AI (BAM) that can make autonomous decisions.
    - Unified platform for all core property management functions.
    - Strong focus on automation, with claims of 75%+ automation of guest communications.
    - Proven ROI for its customers.
- **Limitations:**
    - The PRD is a forward-looking document, and some features like the Voice AI Concierge are marked as "Coming Soon."
    - The document is based on "Boom Reverse Engineering & Public Information," which might not be fully accurate.
    - The focus is heavily on the STR market, so its suitability for other verticals like LTR or HOA/Condo is not yet proven.

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

Boom's platform is designed to provide transparent and automated financial reporting to property owners. This is a critical workflow for maintaining trust and ensuring owners have a clear understanding of their investment's performance.

**Steps and Procedures:**

1.  **Data Aggregation:** The system automatically collects revenue data from all connected booking channels (e.g., Airbnb, VRBO, direct bookings) and expenses entered into the system.
2.  **P&L Statement Generation:** Boom generates a detailed Profit and Loss (P&L) statement for each property. This statement includes a breakdown of:
    *   **Revenue:** Nightly rental income, cleaning fees, pet fees, and other additional charges.
    *   **Expenses:** Platform fees, cleaning and maintenance costs, utilities, marketing costs, and technology subscriptions.
3.  **Owner Portal Access:** Property owners are given access to a dedicated portal where they can view their P&L statements, occupancy rates, and other performance metrics in real-time.
4.  **Payout Calculation:** The system calculates the net profit due to the owner after deducting all expenses and management fees.
5.  **Payout Distribution:** While the PRD and guides don't explicitly detail the payout distribution method, a system with this level of automation would likely support direct deposit or other electronic payment methods.

**Inputs and Data Fields:**

*   Booking data from all channels
*   Expense records
*   Management fee structure
*   Owner bank account information

**Outputs/Artifacts Produced:**

*   Profit & Loss (P&L) Statement
*   Occupancy reports
*   Guest feedback summaries

**Roles/Permissions Involved:**

*   **Property Manager:** Has access to all data and can configure reporting settings.
*   **Property Owner:** Has access to their own property's data through the owner portal.

**Edge Cases and Exception Handling:**

*   **Disputes:** The system should have a mechanism for owners to flag and dispute any charges or revenue discrepancies.
*   **Refunds and Cancellations:** The system needs to accurately account for refunds and cancellations and reflect them in the P&L statement.

**Common Failure Modes and How to Resolve Them:**

*   **Data Sync Errors:** If data from a booking channel fails to sync, it could lead to inaccurate P&L statements. The system should have robust error handling and notification mechanisms to alert the property manager of any sync issues.
*   **Incorrect Expense Categorization:** If expenses are not categorized correctly, it can distort the P&L statement. The system should provide clear guidance on expense categorization and allow for easy correction of any errors.

### AP: Invoice Intake -> Coding -> Approvals -> Payments

Information about a specific accounts payable workflow is not available in the PRD or on the website. However, the "Automated Accounting Tasks" feature suggests that some level of AP automation is likely a part of the platform. The process would likely involve:

1.  **Invoice Intake:** Digital invoices are received, likely via email or a dedicated portal.
2.  **Coding:** The system would use AI to extract key information from the invoice, such as vendor name, invoice number, date, amount, and line items. It would then code this information to the appropriate GL account.
3.  **Approvals:** The system would route the invoice to the appropriate person for approval based on pre-defined workflows.
4.  **Payments:** Once approved, the system would facilitate payment to the vendor, likely via ACH or other electronic payment methods.

**Inputs and Data Fields:**

*   Invoice file (PDF, image, etc.)
*   Vendor information
*   GL account codes
*   Approval workflows

**Outputs/Artifacts Produced:**

*   Coded invoice record
*   Payment transaction record
*   Audit trail of approvals

**Roles/Permissions Involved:**

*   **Property Manager:** Can configure approval workflows and approve invoices.
*   **Accountant:** Can review and reconcile payments.

**Edge Cases and Exception Handling:**

*   **Invoice Errors:** The system should be able to flag invoices with missing or conflicting information.
*   **Approval Escalations:** The system should have a mechanism for escalating invoices that are not approved in a timely manner.

**Common Failure Modes and How to Resolve Them:**

*   **OCR Errors:** The AI may not be able to accurately extract all information from the invoice. The system should allow for manual correction of any errors.
*   **Workflow Misconfigurations:** If approval workflows are not configured correctly, it could lead to delays in payment. The system should provide clear guidance on workflow configuration and allow for easy modification.

### AR: Rent Roll -> Collections -> Notices -> Adjustments

While the PRD and website focus on short-term rentals, the concepts can be adapted to a long-term rental accounts receivable workflow.

**Steps and Procedures:**

1.  **Rent Roll Generation:** The system would generate a rent roll for all tenants, showing the amount due and the due date.
2.  **Automated Collections:** The system would automatically send rent reminders to tenants before the due date.
3.  **Late Fee Calculation:** If rent is not paid on time, the system would automatically calculate and apply late fees.
4.  **Notices:** The system would generate and send late rent notices to tenants who have not paid.
5.  **Adjustments:** The system would allow for manual adjustments to be made to a tenant's account, such as for concessions or other credits.

**Inputs and Data Fields:**

*   Tenant lease information
*   Rent roll data
*   Payment records

**Outputs/Artifacts Produced:**

*   Rent roll report
*   Tenant statements
*   Late rent notices

**Roles/Permissions Involved:**

*   **Property Manager:** Can view and manage all aspects of the AR workflow.
*   **Tenant:** Can view their account statement and make payments through a tenant portal.

**Edge Cases and Exception Handling:**

*   **Partial Payments:** The system should be able to handle partial payments and accurately reflect the remaining balance.
*   **Disputed Charges:** The system should have a mechanism for tenants to dispute charges on their account.

**Common Failure Modes and How to Resolve Them:**

*   **Incorrect Lease Information:** If the lease information in the system is incorrect, it could lead to inaccurate rent charges. The system should allow for easy correction of any errors.
*   **Payment Processing Errors:** If there is an error in processing a tenant's payment, it could lead to a late fee being charged incorrectly. The system should have robust error handling and notification mechanisms to alert the property manager of any payment processing issues.

### Trust/Escrow/Security Deposit Handling

Boom offers a feature called **BoomGuard** which appears to be their solution for damage protection. This suggests a workflow for handling security deposits and damage claims.

**Steps and Procedures:**

1.  **Security Deposit Collection:** At the time of booking, a security deposit is collected from the guest.
2.  **Damage Reporting:** If damage occurs, the property manager can report it through the Boom platform, likely with photo documentation.
3.  **Claim Processing:** BoomGuard would then process the claim, which may involve assessing the damage and determining the amount to be withheld from the security deposit.
4.  **Payout to Owner/Vendor:** The funds from the security deposit are then used to cover the cost of repairs, with any remaining balance returned to the guest.

**Inputs and Data Fields:**

*   Guest booking information
*   Security deposit amount
*   Damage report with photos
*   Repair invoices

**Outputs/Artifacts Produced:**

*   Damage claim record
*   Payout records

**Roles/Permissions Involved:**

*   **Property Manager:** Can report damage and initiate a claim.
*   **Guest:** Is notified of the claim and has the opportunity to dispute it.

**Edge Cases and Exception Handling:**

*   **Disputed Claims:** The system should have a clear process for handling disputed claims, which may involve mediation or arbitration.
*   **Insufficient Security Deposit:** If the cost of the damage exceeds the security deposit, the system should have a process for collecting the additional funds from the guest.

**Common Failure Modes and How to Resolve Them:**

*   **Lack of Documentation:** If the damage is not well-documented, it may be difficult to win a disputed claim. The system should encourage property managers to provide thorough documentation.
*   **Delayed Claim Processing:** If claims are not processed in a timely manner, it can lead to frustration for both the property manager and the guest. The system should have clear SLAs for claim processing.

## 3. Data Model and Artifacts

Based on the PRD and website, the following data model entities can be inferred:

*   **Property:** Represents a single rental unit.
*   **Unit:** A sub-unit of a property, if applicable (e.g., a room in a hotel).
*   **Owner:** The owner of a property.
*   **Tenant/Guest:** The person renting the property.
*   **Vendor:** A company or individual that provides services to the property (e.g., cleaning, maintenance).
*   **GL Account:** A general ledger account for tracking income and expenses.
*   **Fund:** Not explicitly mentioned, but implied by the trust accounting features.
*   **Bank Account:** Bank accounts for owners, vendors, and the property management company.

**Artifacts:**

*   **Owner Statement:** A report showing the financial performance of a property.
*   **P&L Statement:** A detailed breakdown of income and expenses.
*   **Rent Roll:** A report showing all tenants and their rent status.
*   **Invoice:** A bill from a vendor for services rendered.
*   **Lease Agreement:** A contract between a tenant and a property owner.

## 4. Skill Candidates

Based on the research, the following skill candidates have been identified:

**Core Platform (CP):**

*   **CP-001: Reservation Creation:** Create a new reservation in the PMS.
*   **CP-002: Reservation Modification:** Modify an existing reservation (e.g., change dates, number of guests).
*   **CP-003: Reservation Cancellation:** Cancel a reservation and process any applicable refunds.
*   **CP-004: Guest Profile Management:** Create and update guest profiles with contact information, preferences, and communication history.
*   **CP-005: Calendar & Inventory Blocking:** Block off dates on the calendar for maintenance or other reasons.

**Integrations (INT):**

*   **INT-001: Channel Management (OTA Sync):** Synchronize availability and rates across all connected OTAs.
*   **INT-002: Dynamic Pricing Integration:** Integrate with a dynamic pricing engine to automatically adjust rates.
*   **INT-003: Smart Lock Integration:** Integrate with smart lock systems to automate keyless entry for guests.

**Finance (FIN):**

*   **FIN-001: P&L Statement Generation:** Generate a P&L statement for a property for a specified period.
*   **FIN-002: Owner Statement Generation:** Generate an owner statement showing a summary of income, expenses, and net profit.

**Accounts Payable (AP):**

*   **AP-001: Invoice Processing (OCR):** Use OCR to extract data from invoices.
*   **AP-002: Invoice Coding:** Code invoices to the correct GL account.
*   **AP-003: Invoice Approval Routing:** Route invoices for approval based on pre-defined workflows.

**Accounts Receivable (AR):**

*   **AR-001: Automated Rent Collection:** Automatically collect rent from tenants on the due date.
*   **AR-002: Late Fee Application:** Automatically apply late fees to overdue rent payments.

**Trust Accounting (TR):**

*   **TR-001: Security Deposit Collection:** Collect a security deposit from a guest at the time of booking.
*   **TR-002: Security Deposit Refund:** Refund a security deposit to a guest after check-out.

**Reporting (REP):**

*   **REP-001: Occupancy Report Generation:** Generate a report showing occupancy rates for a property or group of properties.
*   **REP-002: Revenue Report Generation:** Generate a report showing revenue for a property or group of properties.

**Treasury (TRE):**

*   **TRE-001: Automated Owner Payouts:** Automatically pay out net profits to property owners on a regular schedule.

**Robotic Automation (RA):**

*   **RA-001: AI Guest Messaging:** Use AI to automatically respond to guest inquiries.
*   **RA-002: Automated Task Creation:** Automatically create tasks for cleaning, maintenance, and other operational activities.

## 5. Treasury Capture Opportunities

Based on the research, the following treasury capture opportunities have been identified:

*   **Owner Payouts:** By owning the owner payout process, an AI agent can ensure that owners are paid accurately and on time, while also capturing a fee for the service.
*   **Vendor Payments:** By owning the vendor payment process, an AI agent can ensure that vendors are paid on time, while also capturing a fee for the service.
*   **Security Deposit Handling:** By owning the security deposit handling process, an AI agent can ensure that security deposits are collected, held, and refunded in accordance with all applicable laws and regulations, while also capturing a fee for the service.

## 6. Training Data Candidates

Based on the research, the following training data candidates have been identified:

*   **Guest Communications:** A dataset of guest communications, including inquiries, requests, and complaints, can be used to train an AI agent to handle guest communications more effectively.
*   **Invoices:** A dataset of invoices can be used to train an AI agent to extract key information from invoices and code them to the correct GL account.
*   **Lease Agreements:** A dataset of lease agreements can be used to train an AI agent to extract key information from lease agreements, such as rent amount, due date, and lease term.


### AP: Invoice Intake -> Coding -> Approvals -> Payments

Information about a specific accounts payable workflow is not available in the PRD or on the website. However, the "Automated Accounting Tasks" feature suggests that some level of AP automation is likely a part of the platform. The process would likely involve:

1.  **Invoice Intake:** Digital invoices are received, likely via email or a dedicated portal.
2.  **Coding:** The system would use AI to extract key information from the invoice, such as vendor name, invoice number, date, amount, and line items. It would then code this information to the appropriate GL account.
3.  **Approvals:** The system would route the invoice to the appropriate person for approval based on pre-defined workflows.
4.  **Payments:** Once approved, the system would facilitate payment to the vendor, likely via ACH or other electronic payment methods.

**Inputs and Data Fields:**

*   Invoice file (PDF, image, etc.)
*   Vendor information
*   GL account codes
*   Approval workflows

**Outputs/Artifacts Produced:**

*   Coded invoice record
*   Payment transaction record
*   Audit trail of approvals

**Roles/Permissions Involved:**

*   **Property Manager:** Can configure approval workflows and approve invoices.
*   **Accountant:** Can review and reconcile payments.

**Edge Cases and Exception Handling:**

*   **Invoice Errors:** The system should be able to flag invoices with missing or conflicting information.
*   **Approval Escalations:** The system should have a mechanism for escalating invoices that are not approved in a timely manner.

**Common Failure Modes and How to Resolve Them:**

*   **OCR Errors:** The AI may not be able to accurately extract all information from the invoice. The system should allow for manual correction of any errors.
*   **Workflow Misconfigurations:** If approval workflows are not configured correctly, it could lead to delays in payment. The system should provide clear guidance on workflow configuration and allow for easy modification.
