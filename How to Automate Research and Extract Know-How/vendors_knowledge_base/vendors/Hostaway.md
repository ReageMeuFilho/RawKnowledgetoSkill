# Hostaway Research

## 1. Company Overview

Hostaway is a prominent all-in-one vacation rental software solution catering to property managers with growing portfolios. The platform offers a comprehensive suite of tools for automating and streamlining various aspects of property management, including marketing, sales, operations, and reporting. Hostaway primarily focuses on the short-term rental (STR) market and has established itself as an elite partner with major online travel agencies (OTAs) such as Airbnb, Vrbo, and Booking.com. The company has a global presence and is recognized for its robust channel management capabilities and extensive marketplace of third-party integrations.

## 2. Workflow Deep Dives

### 1. Owner Statements / Owner Payouts

Hostaway provides flexible options for generating owner statements, but the platform's capabilities for managing the entire payout process are not explicitly detailed in the available documentation. The primary methods for creating owner statements include:

*   **Manual Creation:** This method is suitable for creating customized or one-off statements. It allows users to define specific parameters, such as filters and columns, to tailor the statement to their needs.
*   **Duplication:** Users can duplicate existing statements to create new ones, which is an efficient way to generate recurring reports with similar formats.
*   **Automation:** Hostaway's automation features enable the scheduled generation of owner statements. Users can create templates and define schedules for automatic creation and distribution, which helps to streamline the reporting process.
*   **Template Method:** The platform offers pre-configured templates that allow for the quick and easy creation of professional-looking statements.

**Inputs:**
*   Statement name
*   Owner and user assignments
*   Date ranges and other filters
*   Selection of metrics, rental activity, and expense columns

**Outputs:**
*   Owner statements (draft or published)

**Roles/Permissions:**
*   Access to owner statements can be controlled by assigning specific users to them.

### 2. Bank Reconciliation

Hostaway does not feature a native bank reconciliation module. Instead, it relies on its integration with QuickBooks Online to handle this function. The integration allows for the transfer of financial data from Hostaway to QuickBooks, where users can then perform bank reconciliation. The process of reconciling bank transactions with the invoices generated in Hostaway appears to be a manual or semi-automated task within the QuickBooks environment.

### 3. AP: Invoice Intake → Coding → Approvals → Payments

The accounts payable (AP) functionalities within Hostaway are limited. While the platform can push reservation-specific expenses to QuickBooks Online as line items on an invoice, it does not support the creation of bills for all individual expenses. This suggests that a comprehensive AP workflow, including invoice intake, coding, approvals, and payments, would need to be managed through QuickBooks or another dedicated accounting software.

### 4. AR: Rent Roll → Collections → Notices → Adjustments

Hostaway's role in accounts receivable (AR) is primarily centered on generating invoices from reservations, which can then be synced with QuickBooks Online. The platform does not appear to offer built-in features for managing the complete AR lifecycle, such as handling collections, sending notices, or making adjustments. These tasks would likely need to be managed outside of Hostaway, either manually or through an integrated accounting system.

### 5. Trust/Escrow/Security Deposit Handling

Hostaway does not have a native trust accounting module. To address this need, the platform integrates with several third-party trust accounting solutions available through its marketplace. These include:

*   **Online Trust Accounting Plus (OTA+):** An advanced owner accounting system.
*   **Stellar Trust:** A solution that provides online check-in services, including the management of insurance and deposits.
*   **Trust-d:** A guest trust solution based on a proprietary AI algorithm.

Property managers requiring trust accounting capabilities would need to subscribe to one of these third-party services. The integration allows for the synchronization of booking and financial data between Hostaway and the chosen trust accounting platform.

## 3. Data Model and Artifacts

Based on the available documentation and the platform's features, the following data model entities can be inferred:

*   **Property:** Represents a rental property, with attributes such as address, amenities, and photos.
*   **Unit:** A sub-entity of a property, representing an individual rental unit.
*   **Owner:** The owner of a property, with associated contact and financial information.
*   **Tenant/Guest:** The individual or group renting a property.
*   **Vendor:** A third-party service provider, such as a cleaning company or maintenance contractor.
*   **GL Account:** While not explicitly mentioned, the integration with QuickBooks implies the use of a general ledger for financial tracking.
*   **Bank Account:** The integration with payment processors and accounting software suggests the need to manage bank account information.

**Artifacts:**

*   **Owner Statements:** PDF or digital reports detailing income, expenses, and net payouts for property owners.
*   **Invoices:** Generated for reservations and can be synced with QuickBooks Online.
*   **Reports:** Various financial and operational reports, such as occupancy reports and rental activity reports.

## 4. Skill Candidates

Based on the analysis of Hostaway's workflows and features, the following skill candidates have been identified:

*   **CP-001: Owner Statement Generation:** Automating the creation and distribution of owner statements based on predefined templates and schedules.
*   **FIN-001: Bank Reconciliation Support:** Assisting with the reconciliation of bank transactions in QuickBooks by matching them with Hostaway invoices.
*   **AP-001: Invoice Processing:** Extracting data from invoices and creating corresponding entries in QuickBooks.
*   **AR-001: Invoice Generation:** Automatically generating invoices from new reservations.
*   **TR-001: Trust Account Integration:** Managing the flow of data between Hostaway and a third-party trust accounting system.

## 5. Treasury Capture Opportunities

The following are potential opportunities for an AI agent to capture treasury-related tasks within the Hostaway ecosystem:

*   **Payout Calculation and Approval:** An AI agent could be used to calculate owner payouts based on the data in owner statements and then initiate an approval workflow before the funds are disbursed.
*   **Fund Segregation:** In conjunction with a trust accounting system, an AI agent could help to automate the segregation of funds, ensuring that security deposits and other restricted funds are held in separate accounts.
*   **Expense Approval:** An AI agent could be used to manage the approval process for expenses, ensuring that they are properly coded and authorized before being paid.

## 6. Training Data Candidates

The following are potential sources of training data for developing AI skills related to Hostaway:

*   **Sample Owner Statements:** Examples of owner statements with different formats and levels of detail.
*   **Anonymized Reservation Data:** A dataset of reservations with various pricing structures, fees, and taxes.
*   **Expense Invoices:** A collection of invoices from different vendors with varying formats and line items.
*   **User Support Tickets:** A log of support tickets related to financial reporting and accounting, accounting, accounting to identify common issues and edge cases.
