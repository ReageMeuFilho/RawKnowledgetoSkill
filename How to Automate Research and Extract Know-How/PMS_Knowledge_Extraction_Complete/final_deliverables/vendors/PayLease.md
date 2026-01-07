# PayLease/Zego Research Document

## 1. Company Overview

Zego (formerly PayLease) is a property technology company that provides a comprehensive platform for property managers and associations. Their offerings are designed to automate and streamline various operational workflows, with a strong emphasis on payments and utility management. Zego serves a wide range of clients in the property management industry, including multifamily, single-family, HOA/condo, and student housing. The company's market position is strong, with a large number of integrations with leading property management software. Zego's primary strength lies in its ability to digitize and automate the entire payment lifecycle, from rent collection to vendor payments and owner distributions. However, a limitation is that their platform is heavily reliant on integrations with other software for core accounting and property management functions. Zego's focus is on being a payment and workflow automation layer on top of existing systems of record.

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

Zego Pay offers an "Owner payments" feature that allows property managers to digitally deposit payments into property owners' bank accounts, eliminating the need for paper checks. This suggests a workflow for owner payouts, but the specifics of how statements are generated and distributed are not detailed on the website. It is likely that this functionality is integrated with the property management software that Zego partners with, which would be responsible for generating the owner statements. Zego's role appears to be focused on the payment execution.

Zego also offers "Resident Payouts" for security deposits, which suggests a similar workflow could be used for owner payouts. The process for resident payouts involves the property manager creating a new payout, selecting the resident, entering their contact information and the payment amount. The resident then receives a notification and can choose their preferred payment method (e.g., ACH, PayPal, Venmo). This workflow could be adapted for owner payouts, where the property manager initiates the payout and the owner chooses how to receive the funds.

### Bank Reconciliation

Zego emphasizes its seamless integration with various property management accounting software. This integration is key to their bank reconciliation workflow. Zego's platform automates the reconciliation of payments by directly feeding payment data into the accounting system. This eliminates manual data entry and reduces the risk of errors. The platform offers features like Check Scanning and Lockbox services, which further streamline the process by digitizing paper-based payments and automating their reconciliation.

While the website doesn't provide a step-by-step guide to the bank reconciliation process itself, it highlights the benefits of their automated system, which include:

*   **Automated Reconciliation:** Payments made through Zego are automatically reconciled with the accounting software.
*   **Reduced Manual Entry:** The need for manual data entry is significantly reduced, saving time and minimizing errors.
*   **Improved Accuracy:** Automation leads to more accurate and reliable financial data.
*   **Faster Closing:** With a more efficient reconciliation process, property managers can close their books faster.

The Zego help center does not provide specific details on the bank reconciliation process. The search results are focused on resident-facing issues related to payments and bank accounts, not on the back-end accounting workflows for property managers. This suggests that the bank reconciliation process is either handled entirely by the integrated accounting software or is a feature that is not publicly documented in detail. The emphasis on seamless integration with property management software implies that Zego's role is to provide the payment data in a format that is easily consumed by the accounting system, which then handles the reconciliation.

### AP: Invoice Intake → Coding → Approvals → Payments

Zego's primary offering in the accounts payable space is their Utility Expense Management solution. This service automates the entire utility invoice lifecycle, from intake to payment. The workflow is as follows:

1.  **Invoice Intake:** Zego automatically receives utility invoices on behalf of the property manager.
2.  **Invoice Auditing:** The invoices are audited for errors and anomalies.
3.  **Exception Handling:** Any exceptions or discrepancies are flagged and resolved.
4.  **Payment:** Once approved, the invoices are paid automatically.

This workflow is designed to offload the time-consuming task of managing utility bills, reduce late fees, and provide better visibility into utility expenses. Zego's AP automation capabilities appear to be focused on utility invoices, and it is not clear if they offer a similar service for other types of vendor invoices.

### AR: Rent Roll → Collections → Notices → Adjustments

Zego's accounts receivable workflow is centered around their Zego Pay platform, which automates rent collection and homeowner dues. The process is as follows:

1.  **Rent Roll Integration:** Zego integrates with the property management software's rent roll to get a real-time view of who owes what.
2.  **Digital Payments:** Residents can pay their rent online via a variety of methods, including credit card, debit card, and e-check. Zego also offers a CashPay option, which allows residents to pay with cash at participating retail locations.
3.  **Automated Collections:** Zego's platform automates the collections process with features like digital rent reminders and AutoPay.
4.  **Reconciliation:** All payments are automatically reconciled with the accounting software, providing a real-time view of cash flow.

Zego's AR workflow is designed to maximize on-time payments, reduce delinquencies, and streamline the collections process. The platform also offers features like rental payment credit reporting, which can help residents build their credit history.

## 3. Data Model and Artifacts

Based on the research, Zego's data model appears to be centered around the following entities:

*   **Property:** The physical property being managed.
*   **Unit:** An individual unit within a property.
*   **Resident/Tenant:** The individual or family occupying a unit.
*   **Owner:** The owner of the property.
*   **Vendor:** A company that provides services to the property (e.g., a utility company).
*   **Bank Account:** The bank accounts of the property management company, residents, and owners.
*   **Payment:** A financial transaction, such as a rent payment or a vendor payment.

Zego's platform produces a variety of artifacts, including:

*   **Reports:** Zego provides detailed reporting on payments, delinquencies, and other key metrics.
*   **Exports:** Payment data can be exported to various formats for use in other systems.
*   **Statements:** Zego can generate statements for residents, including rent and utility charges.

## 4. Skill Candidates

Based on the research, the following skill candidates have been identified:

*   **CP-001: Owner Statement Generation:** While Zego does not appear to generate owner statements directly, an AI agent could be trained to do so by pulling data from the property management software and Zego's payment platform.
*   **CP-002: Owner Payouts:** An AI agent could be trained to initiate owner payouts through Zego's platform, following a predefined approval workflow.
*   **FIN-001: Bank Reconciliation:** An AI agent could be trained to perform bank reconciliation by comparing data from Zego's platform with bank statements.
*   **AP-001: Invoice Intake:** An AI agent could be trained to ingest invoices from various sources, including email and a vendor portal.
*   **AP-002: Invoice Coding:** An AI agent could be trained to code invoices with the correct GL account and other relevant information.
*   **AP-003: Invoice Approvals:** An AI agent could be trained to manage the invoice approval process, routing invoices to the appropriate approvers and tracking their status.
*   **AP-004: Invoice Payments:** An AI agent could be trained to initiate invoice payments through Zego's platform.
*   **AR-001: Rent Roll Processing:** An AI agent could be trained to process the rent roll, identifying who owes what and when.
*   **AR-002: Collections:** An AI agent could be trained to manage the collections process, sending reminders, and escalating delinquent accounts.

## 5. Treasury Capture Opportunities

Zego's platform presents several opportunities for an AI agent to own treasury functions:

*   **Approvals:** An AI agent could be trained to approve payments, such as vendor invoices and owner payouts, based on a set of predefined rules.
*   **Payouts:** An AI agent could be trained to initiate payouts to owners and vendors, ensuring that they are paid on time and in the correct amount.
*   **Fund Segregation:** An AI agent could be trained to manage the segregation of funds, ensuring that operating funds, reserves, and security deposits are all held in separate accounts.

## 6. Training Data Candidates

To train an AI agent to perform these tasks, the following training data would be required:

*   **Example Artifacts:** Sample owner statements, vendor invoices, and bank statements.
*   **Edge Cases:** Examples of unusual or complex transactions, such as partial payments, refunds, and chargebacks.
*   **Evaluation Scenarios:** A set of test cases that can be used to evaluate the performance of the AI agent.

## 7. References

[1] [Zego: Property Management Software](https://www.gozego.com/)
[2] [Zego Pay: Rent Payment Software](https://www.gozego.com/platform/zego-pay/)
[3] [Automate the security deposit payout process | Zego](https://www.gozego.com/platform/zego-pay/resident-payouts/)
[4] [Utility Expense Management Services for Multifamily](https://www.gozego.com/platform/zego-utility/expense-management/)
[5] [Zego Integrations | Property Management Automation ...](https://www.gozego.com/company/integrations/)
