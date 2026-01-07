## 3. Data Model and Artifacts

*   **Data Model Entities:** Property, Unit, Owner, Tenant (Guest), Vendor (inferred), GL Account (inferred via QuickBooks integration), Fund (inferred via trust accounting), Bank Account.
*   **API Endpoints and Integration Patterns:** No formal, publicly documented REST or GraphQL API was found. Integration appears to be primarily through partnerships and specific integrations like the one with QuickBooks.
*   **User Roles and Permissions Model:** OwnerRez has a tiered access system that allows for different levels of permissions for various users. This includes roles for property managers, owners, cleaners, and maintenance staff. Permissions can be customized to control access to calendar information, guest details, financial data, and more.
*   **Approval Workflow Patterns:** While there isn't a formalized, system-wide approval workflow for things like expenses, the platform does have an "Awaiting Approval" status for bookings, which suggests a simple approval step in the booking process.
*   **Audit Logging Capabilities:** The system has audit logs to track changes, as evidenced by references to the need to retain user data for audit log purposes.

## 4. Skill Candidates

*   **CP-001:** Create and manage owner statements.
*   **CP-002:** Process owner payouts.
*   **INT-001:** Integrate with QuickBooks for bank reconciliation.
*   **FIN-001:** Track and categorize expenses.
*   **AP-001:** Record invoices as expenses.
*   **AR-001:** Generate and send invoices to guests.
*   **AR-002:** Automate payment collection from guests.
*   **TR-001:** Manage security deposit holds.
*   **TR-002:** Process refundable security deposits.
*   **REP-001:** Generate financial reports.
*   **TRE-001:** Manage trust/escrow accounts.

## 5. Treasury Capture Opportunities

*   **Expense Approvals:** An AI agent could be implemented to approve or flag expenses based on predefined rules, adding a layer of control to the AP process.
*   **Owner Payouts:** An AI agent could automate the owner payout process, ensuring accuracy and timeliness.
*   **Fund Segregation:** An AI agent could monitor the trust account to ensure proper segregation of funds and compliance with regulations.

## 6. Training Data Candidates

*   **Example Artifacts:** Sample owner statements, expense reports, and booking invoices.
*   **Edge Cases:** Scenarios involving prorated statements, hidden expenses, failed security deposits, and refunds.
*   **Evaluation Scenarios:** Testing the AI's ability to correctly calculate owner payouts, identify and flag suspicious expenses, and accurately reconcile bank statements.

## 7. Missing Workflows

*   **Reserves (HOA/Condo):** No specific features for managing HOA/Condo reserves were found. The platform is primarily focused on short-term vacation rentals.
*   **Month-end close checklist + reporting pack:** While OwnerRez offers various reports, it does not appear to have a dedicated month-end close checklist or a pre-packaged reporting pack for this purpose.
