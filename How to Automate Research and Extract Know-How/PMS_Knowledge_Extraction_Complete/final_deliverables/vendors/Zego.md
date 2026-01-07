# Zego Knowledge Document

## 1. Company Overview

Zego is a property management automation company that provides a platform for payments, utility management, and resident engagement. The company aims to simplify workflows for property managers and associations, serving a wide range of residential real estate verticals, including multifamily, single-family, HOA, student housing, and manufactured housing. Zego's primary focus is on providing a comprehensive payment platform, as indicated by its original name, PayLease. The company has been in operation for over 20 years and serves over 7,000 management companies.

### Products and Services

*   **Zego Pay:** A comprehensive payment platform that automates rent and HOA dues collection. It supports various payment methods, including ACH, credit/debit cards, and digital wallets. It also offers features like CashPay for in-person cash payments, Lockbox for check processing, and Check Scanning.
*   **Zego Utility:** A utility management solution that automates the entire utility lifecycle, from invoice processing and accounts payable to resident billing and cost recovery. It aims to help properties maximize utility expense recoupment and improve NOI.
*   **Zego Mobile Doorman:** A resident experience and engagement application that provides a centralized platform for communication, work order management, package notifications, and lease renewals.
*   **Resident Payouts:** A service for automating security deposit refunds and other resident payouts.
*   **Revenue Protection Suite:** A set of tools designed to mitigate risks associated with digital payments, such as chargebacks, NSF returns, and fraud.

### Verticals

Zego primarily serves the following verticals:

*   **LTR (Long-Term Rentals):** Multifamily and Single-Family rentals.
*   **HOA/Condo:** Homeowner and Community Associations.
*   **Student Housing**
*   **Manufactured Housing**
*   **Build to Rent Communities**

### Market Position, Strengths, and Limitations

**Strengths:**

*   **Comprehensive Payment Platform:** Zego offers a wide array of payment options, catering to diverse resident preferences and aiming for 100% digital payment adoption.
*   **Strong Integration Capabilities:** The company emphasizes its seamless integrations with major property management accounting software, which is a significant value proposition for property managers.
*   **Established Market Presence:** With over 20 years in the industry and a large customer base, Zego has a strong foothold in the property management market.
*   **Focus on Resident Experience:** The Zego Mobile Doorman app indicates a strategic focus on improving resident satisfaction and retention.

**Limitations:**

*   **Lack of Detailed Workflow Documentation:** Publicly available information does not provide granular, step-by-step details of its internal workflows, making it difficult to assess the full extent of its automation capabilities.
*   **Mixed Customer Feedback:** While the company website showcases positive testimonials, Reddit discussions reveal some negative customer experiences, particularly concerning customer service and payment processing issues.
*   **Primarily a Payments Platform:** While expanding into utility management and resident engagement, Zego's core strength and identity remain rooted in payment processing.

## 2. Workflow Deep Dives

Detailed, step-by-step procedures for the requested workflows are not publicly available. The following descriptions are based on high-level information from Zego's website and marketing materials.

### 1. Owner Statements / Owner Payouts

Zego's platform facilitates the collection of rent and other dues from residents, which are then reconciled and disbursed to property owners. The exact process for generating owner statements and executing payouts is not detailed, but it is likely integrated with the property management accounting software that Zego partners with.

### 2. Bank Reconciliation

Zego's payment platform automates the reconciliation of digital payments, integrating with property management accounting systems to reduce manual data entry and potential for errors. The platform likely provides reporting features to assist with bank reconciliation, but the specific matching rules and exception handling processes are not documented.

### 3. AP: Invoice Intake → Coding → Approvals → Payments

Zego Utility includes an expense management component that automates utility accounts payable. This service likely involves receiving utility invoices, capturing the data, and processing the payments. The level of automation for invoice coding and approval workflows is not specified.

### 4. AR: Rent Roll → Collections → Notices → Adjustments

Zego Pay is central to the accounts receivable process, providing multiple channels for residents to pay rent and dues. The platform automates payment collection and reconciliation. While Zego likely provides data to the accounting system for managing the rent roll and adjustments, the platform itself does not appear to manage the entire AR workflow, such as sending notices for late payments.

### 5. Trust/Escrow/Security Deposit Handling

Zego offers a "Resident Payouts" service for automating security deposit refunds. This suggests that the platform can handle the disbursement of funds held in trust or escrow. The specific procedures for managing these accounts are not detailed.

### 6. Reserves (HOA/Condo): Operating vs. Reserves Management

While Zego serves the HOA/Condo vertical, there is no specific information available on how its platform facilitates the management of operating versus reserve funds.

### 7. Month-End Close Checklist + Reporting Pack

Zego's platform provides reporting and analytics capabilities, which would be valuable for the month-end close process. However, there is no mention of a specific month-end close checklist or a pre-packaged reporting pack.

## 3. Data Model and Artifacts

Detailed information about Zego's data model is not publicly available. Based on the services offered, the following entities are likely part of their data model:

*   **Property:** Represents a managed property (e.g., apartment building, HOA).
*   **Unit:** A specific unit within a property.
*   **Owner:** The owner of a property.
*   **Tenant/Resident:** The individual residing in a unit.
*   **Vendor:** Utility companies and other service providers.
*   **GL Account:** General ledger accounts for financial tracking.
*   **Bank Account:** Bank accounts for processing payments and payouts.

**Artifacts:**

*   **Reports:** Payment transaction reports, reconciliation reports, utility usage and cost reports.
*   **Exports:** Data exports to integrated accounting systems.
*   **Statements:** Resident utility bills, owner statements (inferred).

## 4. Skill Candidates

Based on the research, the following skill candidates can be mapped to the provided skill IDs:

*   **CP-001 - CP-009 (Core Payments):** Zego's entire payment platform is relevant here. Specific skills could include processing ACH payments, credit card payments, and cash payments through their CashPay network.
*   **INT-001 - INT-005 (Integrations):** Zego's emphasis on seamless integrations with property management accounting software is a key area for skill development.
*   **FIN-001 - FIN-005 (Financial Operations):** Skills related to bank reconciliation and financial reporting can be developed based on Zego's platform.
*   **AP-001 - AP-004 (Accounts Payable):** Zego Utility's expense management features provide a basis for developing skills in utility invoice processing and payment.
*   **AR-001 - AR-002 (Accounts Receivable):** Zego Pay's payment collection capabilities are directly applicable to AR skills.
*   **TR-001 - TR-004 (Treasury):** The Resident Payouts feature for security deposits is a relevant area for treasury-related skills.
*   **REP-001 - REP-003 (Reporting):** Zego's reporting and analytics features can inform the development of reporting skills.
*   **TRE-001 - TRE-006 (Treasury Operations):** The management of payments and payouts provides opportunities for treasury operations skills.
*   **RA-001 - RA-002 (Reconciliation):** Zego's automated reconciliation features are a key area for skill development.

## 5. Treasury Capture Opportunities

*   **Payment Approvals:** An AI agent could potentially be used to review and approve certain types of payments, especially if Zego's platform allows for configurable approval workflows.
*   **Payout Calculations:** An AI agent could assist in calculating resident payouts, such as security deposit refunds, by applying predefined rules and logic.
*   **Fund Segregation:** While not explicitly mentioned, an AI agent could help ensure proper fund segregation by monitoring transactions and flagging any potential compliance issues.

## 6. Training Data Candidates

*   **Example Artifacts:** Sample utility bills, anonymized payment transaction data, and sample reconciliation reports could be used as training data.
*   **Edge Cases:** Reddit discussions mentioning payment processing errors, incorrect charges, and customer service issues can provide valuable edge cases for training and testing.
*   **Evaluation Scenarios:** Scenarios involving disputed charges, partial payments, and complex utility billing calculations would be useful for evaluating the performance of AI skills.

## 7. References

[1] [Zego Official Website](https://www.gozego.com/)
[2] [Zego YouTube Channel](https://www.youtube.com/@go_zego)
[3] [Reddit - r/PropertyManagement](https://www.reddit.com/r/PropertyManagement/)
