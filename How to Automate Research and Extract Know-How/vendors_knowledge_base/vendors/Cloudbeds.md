# Cloudbeds Research

## 1. Company Overview

Cloudbeds is a cloud-based hospitality management platform designed for hotels, hostels, inns, and other lodging businesses. It offers a suite of tools to manage reservations, availability, pricing, and guest information. The platform is primarily focused on the short-term rental (STR) and hospitality market, with features tailored to the needs of hoteliers.

**Products:**

*   **Property Management System (PMS):** The core of the platform, used to manage daily operations.
*   **Channel Manager:** Syncs availability and rates across multiple online travel agencies (OTAs).
*   **Booking Engine:** Allows properties to take direct bookings on their own websites.
*   **Cloudbeds Payments:** A built-in payment processing solution.
*   **Cloudbeds POS:** A point-of-sale system for on-site purchases.

**Verticals:**

*   Hotels
*   Hostels
*   B&Bs and Inns
*   Short-term Rentals

**Market Position:**

Cloudbeds is a major player in the hospitality technology space, with a large customer base and a strong brand presence. It is known for its user-friendly interface and all-in-one solution.

**Strengths:**

*   Comprehensive, all-in-one platform.
*   User-friendly interface.
*   Strong focus on the hospitality market.
*   Good integration with OTAs.

**Limitations:**

*   Limited features for long-term rentals (LTR) and homeowner associations (HOA).
*   No built-in accounts payable (AP) workflow.
*   Owner payouts are a manual process.
*   Limited reporting customization.

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

Based on the available documentation, Cloudbeds does not appear to have a dedicated "owner statement" or "owner payout" feature in the same way a traditional property management system for long-term rentals might. Their focus is on hoteliers, and the terminology reflects that. However, there are features that can be used to achieve a similar outcome.

**Process:**

1.  **Revenue and Expense Tracking:** The system tracks all revenue from bookings and other services, as well as expenses. This information is available in various reports.
2.  **Reporting:** Property owners can generate reports to see the financial performance of their property. The 'Invoices Report' and 'Payment Reconciliation Report' would be particularly useful for this.
3.  **Manual Payouts:** The actual payouts to owners would likely be a manual process based on the data from the reports. There is no automated payout system for owners mentioned in the documentation.

**Key Information:**

*   **Inputs:** Reservation data, payment data, expense data.
*   **Outputs:** Invoices Report, Payment Reconciliation Report.
*   **Roles:** Property Owner, General Manager.

### Bank Reconciliation

Cloudbeds provides a 'Payment Reconciliation Report' and a 'Payouts Report' to assist with bank reconciliation.

**Process:**

1.  **Export Reports:** Users can export the Payouts Report, which contains information about deposits, and the Payment Reconciliation Report, which details transactions.
2.  **Match Transactions:** The data from these reports can be matched with the property's bank statements to ensure that all transactions have been correctly recorded and deposited.
3.  **Identify Discrepancies:** Any discrepancies between the Cloudbeds reports and the bank statements can be identified and investigated.

**Key Information:**

*   **Inputs:** Payment transaction data, bank statements.
*   **Outputs:** Payment Reconciliation Report, Payouts Report.
*   **Roles:** General Manager, Accountant.

### AP: Invoice Intake → Coding → Approvals → Payments

Cloudbeds does not have a dedicated Accounts Payable workflow. The documentation for House Accounts explicitly states: "House Accounts are not designed to register accounts payable/supplier payments (e.g., water/electricity bills, staff salary)." This suggests that AP processes are managed outside of the Cloudbeds platform.

### AR: Rent Roll → Collections → Notices → Adjustments

Cloudbeds uses an "Accounts Receivable" feature to manage outstanding balances. This is primarily used for direct bill clients and other non-guest-related revenue.

**Process:**

1.  **Create an Account:** A new Accounts Receivable account is created for the client.
2.  **Add Charges:** Charges are added to the account as they are incurred.
3.  **Collect Payments:** Payments are recorded against the account balance.
4.  **Send Notices:** The system can be used to generate statements and send reminders for outstanding balances.
5.  **Make Adjustments:** Adjustments can be made to the account to correct errors or apply credits.

**Key Information:**

*   **Inputs:** Client information, charge details, payment information.
*   **Outputs:** Accounts Receivable reports, client statements.
*   **Roles:** General Manager, Accountant.

### Trust/Escrow/Security Deposit Handling

Cloudbeds uses a **Deposits Ledger** to manage pre-check-in payments, which can also be used for security deposits. This feature treats these payments as liabilities, keeping them separate from revenue until they are either consumed or refunded.

**Process:**

1.  **Mark as Deposit:** When a payment is received, it can be marked as a deposit. This automatically directs the funds to the Deposits Ledger.
2.  **Deposit Consumption:** Deposits can be consumed (transferred to the guest folio as revenue) either manually or automatically upon check-in.
3.  **Refunds and Voids:** Deposits can be refunded or voided directly from the Deposits Ledger.
4.  **Reconciliation:** The Deposits Ledger provides a clear overview of all outstanding deposit liabilities, simplifying reconciliation.

**Key Information:**

*   **Inputs:** Payment data, reservation status.
*   **Outputs:** Deposits Ledger report.
*   **Roles:** General Manager, Accountant.

### Reserves (HOA/Condo): operating vs reserves management

No information was found regarding specific features for managing operating vs. reserve funds for HOAs or Condos. This is consistent with Cloudbeds' focus on the hotel and short-term rental market.

### Month-end close checklist + reporting pack

Cloudbeds does not provide a formal month-end close checklist or a pre-packaged reporting pack. However, the system offers a variety of reports that can be used to manually perform a month-end close. These reports include:

*   Invoices Report
*   Payment Reconciliation Report
*   Payouts Report
*   Accounts Receivable reports
*   Deposits Ledger report

## 3. Data Model and Artifacts

### Data Model Entities

*   **Property:** The core entity, representing the hotel or lodging business.
*   **Unit:** Represents a room or other bookable unit within the property.
*   **Guest:** Represents a person who has made a reservation.
*   **Reservation:** Represents a booking for a specific unit for a specific period.
*   **Folio:** A collection of charges and payments associated with a reservation or house account.
*   **House Account:** A non-guest account used to track revenue and expenses not associated with a specific reservation.
*   **Payment:** A record of a payment received.
*   **Item:** A product or service that can be sold and added to a folio.

### Artifacts

*   **Invoices:** Can be generated for guests and house accounts.
*   **Reports:** Various reports are available for download, typically in CSV format. Key reports include:
    *   Invoices Report
    *   Payment Reconciliation Report
    *   Payouts Report
    *   Accounts Receivable Report
    *   Deposits Ledger Report

## 4. Skill Candidates

Based on the research, the following skill candidates have been identified:

| Category | Skill ID | Skill Name | Supported | Notes |
| :--- | :--- | :--- | :--- | :--- |
| Core PMS | CP-001 | Reservation Management | Yes | Core feature of the platform. |
| Core PMS | CP-002 | Guest Profile Management | Yes | Core feature of the platform. |
| Core PMS | CP-003 | Room/Unit Management | Yes | Core feature of the platform. |
| Core PMS | CP-004 | Rate & Availability Management | Yes | Core feature of the platform. |
| Core PMS | CP-005 | Housekeeping Management | Yes | Core feature of the platform. |
| Core PMS | CP-006 | Front Desk Operations | Yes | Core feature of the platform. |
| Core PMS | CP-007 | Guest Communications | Yes | Core feature of the platform. |
| Core PMS | CP-008 | Reporting & Analytics | Yes | A variety of reports are available. |
| Core PMS | CP-009 | User & Permissions Management | Yes | Core feature of the platform. |
| Integrations | INT-001 | Channel Manager | Yes | Core feature of the platform. |
| Integrations | INT-002 | Booking Engine | Yes | Core feature of the platform. |
| Integrations | INT-003 | Payment Gateway | Yes | Cloudbeds Payments and third-party integrations. |
| Integrations | INT-004 | POS | Yes | Cloudbeds POS and third-party integrations. |
| Integrations | INT-005 | Accounting | Yes | Via third-party integrations. |
| Financials | FIN-001 | Invoicing | Yes | Invoices can be generated for guests and house accounts. |
| Financials | FIN-002 | Folio Management | Yes | Core feature of the platform. |
| Financials | FIN-003 | Tax Management | Yes | Supported. |
| Financials | FIN-004 | Multi-currency Support | Yes | Supported. |
| Accounts Payable | AP-001 | Vendor Management | No | Not a supported feature. |
| Accounts Payable | AP-002 | Invoice Processing | No | Not a supported feature. |
| Accounts Payable | AP-003 | Bill Payments | No | Not a supported feature. |
| Accounts Payable | AP-004 | AP Reporting | No | Not a supported feature. |
| Accounts Receivable | AR-001 | AR Aging & Collections | Yes | Supported through the Accounts Receivable feature. |
| Accounts Receivable | AR-002 | Customer Statements | Yes | Supported through the Accounts Receivable feature. |
| Trust Accounting | TR-001 | Trust Account Setup | Yes | Supported through the Deposits Ledger feature. |
| Trust Accounting | TR-002 | Deposit Handling | Yes | Supported through the Deposits Ledger feature. |
| Trust Accounting | TR-003 | Disbursement Management | Manual | Payouts are a manual process. |
| Trust Accounting | TR-004 | Trust Account Reporting | Yes | Supported through the Deposits Ledger feature. |
| Reporting | REP-001 | Standard Reports | Yes | A variety of standard reports are available. |
| Reporting | REP-002 | Custom Reports | No | No evidence of custom reporting capabilities. |
| Reporting | REP-003 | Report Scheduling & Delivery | No | No evidence of report scheduling. |
| Treasury | TRE-001 | Bank Reconciliation | Yes | Supported via reports. |
| Treasury | TRE-002 | Cash Flow Forecasting | No | Not a supported feature. |
| Treasury | TRE-003 | FX Management | No | Not a supported feature. |
| Treasury | TRE-004 | Investment Management | No | Not a supported feature. |
| Treasury | TRE-005 | Debt Management | No | Not a supported feature. |
| Treasury | TRE-006 | Treasury Reporting | No | Not a supported feature. |
| Reserves | RA-001 | Reserve Fund Management | No | Not a supported feature. |
| Reserves | RA-002 | Reserve Study Integration | No | Not a supported feature. |

## 5. Treasury Capture Opportunities

*   **Owner Payouts:** The manual process of calculating and distributing owner payouts is a significant opportunity for an AI agent to take ownership. The agent could be trained to extract the necessary data from reports, calculate the payouts based on predefined rules, and execute the payments.
*   **AP Automation:** The lack of a formal AP workflow presents an opportunity to introduce an AI-powered solution for invoice intake, coding, approvals, and payments.
*   **Deposit Management:** While Cloudbeds has a Deposits Ledger, an AI agent could provide an additional layer of oversight and automation, ensuring that deposits are correctly classified, consumed, and refunded in a timely manner.

## 6. Training Data Candidates

*   **Example Artifacts:** Sample Invoices, Payment Reconciliation Reports, Payouts Reports, and screenshots of the Deposits Ledger and Accounts Receivable modules would be valuable for training an AI agent.
*   **Edge Cases:** The Reddit threads discussing user issues and complaints could provide a rich source of edge cases and failure modes to train the AI agent on how to handle exceptions.
*   **Evaluation Scenarios:** The YouTube tutorials demonstrating various workflows could be used to create evaluation scenarios to test the AI agent's ability to perform the tasks correctly.
