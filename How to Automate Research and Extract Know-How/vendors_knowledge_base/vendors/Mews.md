# Mews Research

## 1. Company Overview

Mews is a cloud-native hospitality management platform designed for a wide range of properties, including hotels, hostels, serviced apartments, and mixed-use spaces. The company's mission is to modernize and simplify hotel operations through automation, a guest-centric approach, and an open, integrable ecosystem. Mews provides a comprehensive suite of tools that cover the entire guest journey, from booking to check-out, as well as back-of-house operations and financial management.

| Vertical | Products | Market Position | Strengths | Limitations |
| :--- | :--- | :--- | :--- | :--- |
| STR/Hospitality | Mews Property Management System (PMS), Mews Booking Engine, Mews Virtual Concierge, Mews Payments, Mews API and Marketplace | Trusted by over 12,500 properties worldwide, with a strong focus on modern, cloud-native technology and an open platform. | Comprehensive, all-in-one platform with a strong focus on automation, guest experience, and a large number of integrations. | As a cloud-native platform, it may not be suitable for properties with unreliable internet access. The extensive feature set may have a learning curve for new users. |

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

The process for generating owner statements and processing payouts in Mews can be inferred from the available documentation on billing and reporting.

**Steps and Procedures:**
1.  **Generate Owner Invoices:** Invoices for owner-related charges and revenues are generated using the **Bills and invoices report**. This report can be filtered by the owner's company or customer profile to create a statement of account.
2.  **Validate Invoices:** The generated invoices are reviewed for accuracy, ensuring all charges and revenues are correctly allocated.
3.  **Process Payouts:** Payouts to owners are processed based on the invoiced amounts. Mews Payments facilitates the transfer of funds.
4.  **Reconcile Payouts:** The **Payout report** is used to reconcile the payouts made to owners with the property's bank account. This report provides a detailed breakdown of each payout batch, including gross amount, commission, and net payout.

**Inputs and Data Fields:**
*   Owner profile (company or customer)
*   Billing information
*   Revenue and expense items

**Outputs/Artifacts:**
*   Owner invoices/statements
*   Payout reports

### Bank Reconciliation

Mews provides a clear process for monthly bank reconciliation, primarily using the **Payment report** and the **Payout report**.

**Steps and Procedures:**
1.  **Generate Charged Payments Report:** At the end of the month, a **Payment report** is generated for all payments charged during that month.
2.  **Generate Settled Payments Report:** A **Payment report** is also generated for payments settled in the first week of the following month to capture any delayed settlements.
3.  **Compare Reports with Bank Statements:** The charged payments report is compared with the property's bank statements. Any discrepancies are investigated using the settled payments report to identify payments that were charged in one month but settled in the next.
4.  **Use Payout Report for Tracking:** The **Payout report** is used to track all initiated payouts and their expected arrival dates in the property's bank account.

**Inputs and Data Fields:**
*   Payment and settlement dates
*   Payment status (charged, settled)
*   Bank transfer information

**Outputs/Artifacts:**
*   Payment reports
*   Payout reports

### AP: Invoice Intake → Coding → Approvals → Payments

While not explicitly detailed, the accounts payable process in Mews can be inferred from the billing and payment functionalities.

**Steps and Procedures:**
1.  **Invoice Intake:** Vendor invoices are received and entered into Mews as bills, assigned to the appropriate vendor (company) profile.
2.  **Coding:** The bill items are coded to the correct accounting categories.
3.  **Approvals:** The system likely has an internal approval process for bills before they are paid.
4.  **Payments:** Bills are paid using Mews Payments or by recording an external payment in the system.

**Inputs and Data Fields:**
*   Vendor profile
*   Invoice details (date, amount, items)
*   Accounting categories

**Outputs/Artifacts:**
*   Bills
*   Payment records

### AR: Rent Roll → Collections → Notices → Adjustments

Mews has features for managing accounts receivable, including receivable tracking and a City Ledger.

**Steps and Procedures:**
1.  **Rent Roll/Invoicing:** Invoices for rent and other charges are generated and sent to customers.
2.  **Collections:** The **City Ledger** is used to track unpaid invoices and manage collections.
3.  **Notices:** The system can likely send automated reminders and notices for overdue payments.
4.  **Adjustments:** Any necessary adjustments to invoices can be made before they are closed.

**Inputs and Data Fields:**
*   Customer profile
*   Invoice details
*   Payment status

**Outputs/Artifacts:**
*   Invoices
*   City Ledger report

### Trust/Escrow/Security Deposit Handling

Mews has functionality for handling deposits and security deposits.

**Steps and Procedures:**
1.  **Collect Deposit:** A security deposit is collected from the guest at the time of booking or check-in.
2.  **Hold Deposit:** The deposit is held in a designated account.
3.  **Release/Apply Deposit:** At check-out, the deposit is either released back to the guest or applied to any outstanding charges or damages.

**Inputs and Data Fields:**
*   Deposit amount
*   Guest information
*   Payment details

**Outputs/Artifacts:**
*   Deposit records

## 3. Data Model and Artifacts

### Data Model Entities

Based on the Mews Connector API documentation, the following data model entities have been identified:

*   **Accounts:** Represents customers and companies.
*   **Addresses:** Stores address information for accounts.
*   **Bills:** Represents invoices and bills for services.
*   **Companies:** Represents business entities.
*   **Customers:** Represents individual guests.
*   **Reservations:** Represents bookings and stays.
*   **Products:** Represents items that can be sold, such as room nights or additional services.
*   **Rates:** Defines the price of products.
*   **Services:** Represents the services offered by the property.

### API Endpoints and Integration Patterns

The Mews Connector API provides a comprehensive set of endpoints for interacting with the Mews platform. The API is organized by data model entities, with standard CRUD (Create, Read, Update, Delete) operations available for most entities. The API also supports webhooks for real-time notifications of events.

**Key API capabilities include:**

*   **Reservation Management:** Creating, retrieving, updating, and canceling reservations.
*   **Guest Management:** Managing guest profiles and information.
*   **Billing and Invoicing:** Creating and managing bills and invoices.
*   **Rate and Inventory Management:** Managing room rates and availability.
*   **Reporting:** Accessing various reports and financial data.

Integration with Mews is typically done via the Connector API, which allows third-party applications to connect to and interact with the Mews platform.

## 4. Skill Candidates

| Skill ID | Skill Description | Findings from Mews |
| :--- | :--- | :--- |
| CP-001 | Generate Owner Statements | The **Bills and invoices report** can be used to generate statements for property owners. |
| AP-001 | Process Vendor Invoices | Mews allows for the creation of bills, which can represent vendor invoices. |
| AP-002 | Code Invoices to GL | Bills in Mews can be assigned to accounting categories, which correspond to GL codes. |
| AR-001 | Generate Tenant Invoices | Mews can generate invoices for guests, which can be adapted for tenants in a long-term rental scenario. |
| FIN-001 | Reconcile Bank Accounts | Mews provides a detailed process for monthly bank reconciliation using the **Payment report** and **Payout report**. |

## 5. Treasury Capture Opportunities

*   **Automated Payouts:** An AI agent could automate the process of calculating and processing owner payouts based on the generated statements.
*   **Invoice Approvals:** An AI agent could be used to review and approve vendor invoices based on predefined rules.
*   **Collections Management:** An AI agent could manage the collections process by sending automated reminders and escalating overdue accounts.

## 6. Training Data Candidates

*   **Sample Invoices and Bills:** A collection of sample invoices and bills for various scenarios (owner statements, vendor invoices, tenant invoices) would be valuable for training an AI model.
*   **Bank Reconciliation Data:** Real-world bank reconciliation data, including payment reports, payout reports, and bank statements, would be essential for training a reconciliation model.
*   **API Documentation and Examples:** The Mews API documentation and any available code examples would be useful for training a model to interact with the Mews platform.
