# Buildium Knowledge Document

## 1. Company Overview

Buildium, a subsidiary of RealPage, offers a comprehensive, cloud-based property management software solution. The platform is primarily designed for residential property management, catering to single-family homes, multi-family units, and community associations. However, it is also flexible enough to manage mixed portfolios that include student housing and commercial properties. Buildium's core functionalities encompass accounting, online payments, leasing, and maintenance management. The company highlights its integration of artificial intelligence and automation to enhance the efficiency of property management operations. Key strengths of the platform include its extensive feature set, dedicated customer support, and a marketplace for third-party integrations.

## 2. Workflow Deep Dives

### Owner Statements and Payouts

Buildium facilitates the generation and distribution of detailed "Rental Owner Statements," which provide a comprehensive summary of financial activities for each rental owner. These statements include a breakdown of income, expenses, assets, liabilities, and equity transactions. They can be generated for individual properties, property groups, or entire owner portfolios.

| Step | Description |
| :--- | :--- |
| **Generation** | Statements are generated on-demand from the "Reports" section. Users can customize the statement period and select which details to include, such as an income statement, transaction details, and account numbers. A chronological view of transactions is available to provide a clearer understanding of cash flow. |
| **Validation** | While the system provides the data, validation is a manual process for the property manager to ensure accuracy before distribution. |
| **Distribution** | Statements can be distributed in several ways: through a dedicated owner portal, via email or physical mail in bulk using the "Mailings" feature, or by printing or downloading the report in PDF, XLSX, or CSV format. |

### Bank Reconciliation

Buildium supports both manual and automatic bank reconciliation. The automatic reconciliation feature streamlines the process by downloading bank transactions and matching them with entries in the Buildium system.

| Step | Description |
| :--- | :--- |
| **Matching** | The system automatically clears transactions that have a clear match between the bank feed and system entries. For transactions without a clear match, users can manually match them. |
| **Exception Handling** | If a match is not found, the system prompts the user to add a new transaction or search for a matching one. Users also have the option to ignore a transaction. |
| **Posting** | Once reconciled, the transactions are posted to the appropriate accounts, ensuring the accuracy of financial records. |

### AP: Invoice Intake → Coding → Approvals → Payments

Buildium's accounts payable workflow is significantly enhanced through its integration with AvidXchange, which automates the entire process from invoice receipt to payment.

| Step | Description |
| :--- | :--- |
| **Invoice Intake & Coding** | AvidXchange's AvidInvoice feature enables paperless invoice management. It leverages AI and machine learning to automatically extract data from invoices, which minimizes manual data entry and reduces the risk of errors. |
| **Approvals** | The integration provides customizable approval workflows, allowing for multi-level review and authorization of invoices. It also offers real-time visibility into the status of each invoice. |
| **Payments** | The automated payment process enhances security, accuracy, and speed. |

### AR: Rent Roll → Collections → Notices → Adjustments

The accounts receivable workflow is managed through the "Rentals" and "Accounting" tabs, providing a clear overview of rent collection and outstanding balances.

| Step | Description |
| :--- | :--- |
| **Rent Roll & Collections** | The "Rent Roll" provides a comprehensive list of all active leases, including their status, rent amount, and remaining term. The "Outstanding Balances" page tracks overdue rent, categorized by the number of days past due. |
| **Notices & Adjustments** | While not explicitly detailed as a separate feature, the platform's task management system can be used to create and track notices to tenants with outstanding balances. Adjustments to rent and other charges can be made when adding or editing a lease. |

### Month-End Close Checklist + Reporting Pack

Buildium's extensive reporting capabilities are crucial for an efficient month-end close process. The "Reports" tab provides a wide array of financial reports that can be compiled into a comprehensive reporting pack.

**Reporting Pack Components:**

*   Accounts Receivable Summary
*   Balance Sheet
*   Budget vs. Actual
*   Cash Flow Statement
*   Income Statement

These reports can be generated for individual properties or the entire portfolio, providing the necessary documentation for a thorough month-end review.

## 3. Data Model and Artifacts

Based on the reviewed documentation and tutorials, the following data model entities and artifacts have been identified:

*   **Data Model Entities:** Property, Unit, Owner, Tenant, Vendor, GL Account, Fund, Bank Account.
*   **Artifacts:** Rental Owner Statement, Bank Reconciliation Report, various financial reports (Balance Sheet, Income Statement, etc.), Invoices, Leases, Work Orders.

## 4. Skill Candidates

The following skill candidates have been identified based on the analyzed workflows:

*   **CP-001:** Generate and distribute owner statements.
*   **CP-002:** Reconcile bank accounts.
*   **CP-003:** Process and pay bills.
*   **CP-004:** Manage accounts receivable and collections.
*   **FIN-001:** Generate financial reports.
*   **AP-001:** Automate invoice intake and coding.
*   **AP-002:** Manage invoice approval workflows.
*   **AR-001:** Track and manage rent roll and lease information.
*   **REP-001:** Generate and customize month-end reporting packs.

## 5. Treasury Capture Opportunities

The following treasury capture opportunities have been identified:

*   **AP-003:** AI-powered approval of invoices within predefined parameters.
*   **TR-001:** Automated owner payouts based on approved owner statements.
*   **TRE-001:** Automated fund segregation for security deposits and other liabilities.

## 6. Training Data Candidates

The following artifacts and scenarios can be used as training data for the identified skill candidates:

*   Sample Rental Owner Statements with various transaction types.
*   Bank statements with a mix of matched and unmatched transactions.
*   Invoices with different formats and from various vendors.
*   Lease agreements with diverse terms and conditions.
*   Reddit threads discussing common issues and edge cases.
