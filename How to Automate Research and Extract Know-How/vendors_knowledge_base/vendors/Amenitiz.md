# Amenitiz Research

## 1. Company Overview

Amenitiz is a comprehensive, all-in-one property management system (PMS) designed for independent hoteliers, B&Bs, and short-term rental (STR) property managers. The platform aims to streamline operations, maximize occupancy, and provide centralized control over property management tasks. Amenitiz is positioned as a user-friendly, cloud-based solution that empowers independent hoteliers with technology to simplify their work and enhance their online presence.

**Products and Services:**

*   **Property Management System (PMS):** Centralized reservation management, guest communication, and housekeeping management.
*   **Channel Manager:** Synchronizes bookings and availability across multiple online travel agencies (OTAs) like Booking.com, Airbnb, and Expedia.
*   **Website Builder and Booking Engine:** Enables properties to create their own direct booking websites with an integrated booking engine to drive commission-free reservations.
*   **PriceAdvisor:** A dynamic pricing tool that provides rate recommendations based on market data and demand.
*   **AmenitizPay:** An integrated payment processing solution to automate payment collection.
*   **The Hotel Club:** A network for hoteliers to access exclusive benefits and marketing opportunities.

**Verticals:**

*   Primary: STR/Hospitality (Hotels, B&Bs)

**Market Position:**

Amenitiz targets the independent hotelier segment, which is often underserved by more complex and expensive enterprise-level PMS solutions. Their all-in-one offering, which includes a website builder and channel manager, is a key differentiator, providing a complete solution for properties looking to establish and grow their online presence.

**Strengths:**

*   **All-in-one solution:** Combines PMS, channel manager, website builder, and booking engine in a single platform.
*   **User-friendly interface:** Designed for ease of use, catering to non-technical users.
*   **Focus on direct bookings:** Empowers hoteliers to increase direct, commission-free bookings through their own websites.
*   **Integrated payment processing:** Simplifies payment collection and automation.

**Limitations:**

*   **Limited to STR/Hospitality:** The platform is not designed for long-term rentals (LTR) or HOA/Condo management.
*   **Fewer advanced features:** May lack some of the advanced features and customizations found in more enterprise-focused PMS solutions.
*   **Reliance on marketplace apps:** Some functionalities require integration with third-party apps from the Amenitiz Marketplace.


## 2. Workflow Deep Dives

### AP: Invoice Intake → Coding → Approvals → Payments

Amenitiz's invoicing functionality is primarily focused on generating invoices for guests, rather than processing incoming invoices from vendors (AP). However, the platform does have a feature for handling passive invoices in Italy, which suggests some level of AP functionality may be available in specific regions.

**Invoice Generation (AR):**

*   **Invoice Creation:** Invoices can be generated in two ways:
    1.  **From a reservation:** This links the invoice directly to a booking and its associated charges.
    2.  **Independently:** For services or charges not tied to a specific reservation.
*   **Invoice Types:** Amenitiz supports two invoice formats:
    1.  **Detailed:** Shows a breakdown of charges per night.
    2.  **Simplified:** Groups charges by category (e.g., accommodation, extras).
*   **Invoice and Payment Statuses:** The system tracks the status of invoices (Draft, Issued, Cancelled) and payments (Paid, Unpaid, Partial, Overpaid).
*   **Payment Recording:** Payments can be recorded against invoices, and once an invoice is fully paid, it becomes non-editable.
*   **Delivery:** Invoices can be downloaded as PDFs or sent to clients via email directly from the platform.

**Passive Invoices (Italy):**

*   For Italian properties, Amenitiz has a feature to handle "passive invoices," which are invoices received from suppliers. This feature allows users to download these invoices in XML format. This is the only explicit mention of AP-related functionality.

**Approvals:**

The documentation does not mention any formal approval workflows for invoices. The process seems to be managed directly by the user with the appropriate permissions.


### Owner Statements / Owner Payouts

Amenitiz allows property managers to give property owners limited access to the platform. This access can be configured to allow owners to see and edit inventory, view the calendar, and see reservations for their specific properties.

**Owner Access:**

*   Property managers can create a "limited access" user profile for property owners.
*   This allows owners to view information related to their properties only.
*   Permissions can be set to allow access to specific tabs, such as inventory, calendar, and reservations.

**Payouts:**

*   The platform supports splitting AmenitizPay payments between different bank accounts. This is useful for property managers who manage accommodations for multiple owners and need to direct funds to the correct owner accounts.
*   This is achieved by creating multiple AmenitizPay accounts, one for each bank account.

**Limitations:**

The documentation does not explicitly mention the generation of formal "owner statements." While owners can be given access to view their property's performance, there is no clear workflow for generating a consolidated statement for a specific period. Payouts seem to be handled through the splitting of payments at the time of transaction, rather than through a separate owner payout process.


### Bank Reconciliation

The Amenitiz documentation does not provide a specific workflow for bank reconciliation. However, it does mention that the platform aims to provide "simplified daily accounting and joyous reconciliation" through its AmenitizPay feature. The platform also allows for splitting payments between different bank accounts, which is a key feature for property managers handling multiple owners.

**Inferred Process:**

1.  **Payment Processing:** Payments are processed through AmenitizPay, which centralizes transaction data.
2.  **Payouts:** Payouts are made to the property owner's or manager's bank account. The system can be configured to split payouts between multiple bank accounts.
3.  **Reporting:** The platform provides payment reports that can be used to track transactions and reconcile with bank statements.

**Limitations:**

The platform does not appear to have an automated bank reconciliation feature that matches transactions with bank statements. The reconciliation process would likely be a manual one, using the reports generated by Amenitiz.

### AR: Rent Roll → Collections → Notices → Adjustments

Amenitiz's AR functionality is centered around the booking and invoicing process.

*   **Rent Roll:** The "Reservations" module serves as the equivalent of a rent roll, showing all current and upcoming bookings.
*   **Collections:** Payments are collected through the integrated AmenitizPay solution, which automates the process. The platform can be configured to automatically charge guests at the time of booking or on a specific schedule.
*   **Notices:** The "Messaging" module allows for the creation of automated email templates for various guest communications, including booking confirmations, pre-arrival messages, and payment reminders.
*   **Adjustments:** Invoices can be adjusted before they are issued. Once issued, they cannot be edited and must be cancelled and re-created.

### Trust/Escrow/Security Deposit Handling

The documentation does not provide specific details on how trust, escrow, or security deposits are handled. However, the platform does support pre-authorizations, which can be used to hold a security deposit on a guest's credit card.

### Reserves (HOA/Condo): Operating vs. Reserves Management

Amenitiz is not designed for HOA/Condo management and therefore does not have features for managing operating vs. reserve funds.

### Month-End Close Checklist + Reporting Pack

Amenitiz provides a comprehensive "Reports" module that can be used for month-end closing.

**Reporting Pack:**

The platform offers a variety of pre-built report templates, including:

*   **General Report:** Key performance indicators such as occupancy, ADR, and RevPAR.
*   **Revenue Report:** Breakdown of revenue by source.
*   **Payments Report:** Tracking of all payments and their statuses.
*   **VAT Report:** Tax reporting for compliance.

**Month-End Close Process (Inferred):**

1.  **Reconcile Payments:** Use the Payments Report to reconcile all transactions for the month.
2.  **Generate Financial Reports:** Generate the General Report and Revenue Report to get an overview of the property's financial performance.
3.  **Review Occupancy:** Use the Occupancy Report to analyze room performance.
4.  **Finalize Invoices:** Ensure all invoices for the month have been issued and sent to guests.
5.  **Export Data:** Export reports to Excel, PDF, or CSV for further analysis or for use in external accounting software.


## 3. Data Model and Artifacts

### Data Model Entities

Based on the PRD and help center documentation, the key data model entities in Amenitiz include:

*   **Booking/Reservation:** Contains all information related to a booking, including guest details, dates, room type, and payment status.
*   **Guest/Client:** Stores guest information, including contact details, booking history, and communication preferences.
*   **Room:** Defines the properties of a room, such as type, capacity, amenities, and pricing.
*   **Rate Plan:** Manages different pricing structures, including seasonal rates and promotions.
*   **Invoice:** Represents a bill for a guest, including line items, taxes, and payment status.

### Artifacts (Reports, Exports, Statements)

Amenitiz provides a range of reports that can be exported in various formats (Excel, PDF, CSV).

**Reports:**

*   **General Report:** KPIs like occupancy, ADR, RevPAR.
*   **Revenue Report:** Breakdown of revenue by source.
*   **Payments Report:** Tracks all payments and their statuses.
*   **VAT Report:** Tax reporting.
*   **Occupancy Report:** Room category performance.
*   **Bookings Report:** Complete list of bookings with sources.

**Exports:**

*   Reports can be exported to Excel, PDF, and CSV.
*   Passive invoices (for Italy) can be downloaded in XML format.

### API and Integration Patterns

The documentation mentions API rate limiting and integrations with various third-party services, but it does not provide detailed API endpoint documentation. The primary integration pattern appears to be through the Amenitiz Marketplace, which allows for the installation of third-party apps.

### User Roles and Permissions Model

Amenitiz has a role-based access control system with the following default roles:

*   **Property Owner:** Full system access.
*   **Manager:** Operational access with limited access to billing.
*   **Staff:** Limited to assigned tasks.
*   **View-only:** Access to reporting and analytics only.

Property managers can also create custom roles with limited access for property owners, allowing them to view information related to their specific properties.

### Approval Workflow Patterns

The documentation does not describe any formal approval workflow patterns within the system. Actions such as issuing invoices or processing refunds appear to be based on user permissions rather than a multi-step approval process.

### Audit Logging Capabilities

The PRD mentions audit logging as a security feature, indicating that the system tracks user activity.


## 4. Skill Candidates

Based on the analysis of Amenitiz's platform, the following skill candidates have been identified:

*   **FIN-001: Invoice Generation:** The platform's ability to generate detailed and simplified invoices from reservations or independently maps directly to this skill.
*   **FIN-002: Payment Processing:** The integrated AmenitizPay solution for automated payment collection aligns with this skill.
*   **AR-001: Collections Management:** The automated payment collection and reminder functionalities are relevant to this skill.
*   **REP-001: Financial Reporting:** The comprehensive reporting module with various financial reports maps to this skill.
*   **REP-002: Occupancy Reporting:** The Occupancy Report and other performance metrics are relevant to this skill.

## 5. Treasury Capture Opportunities

*   **Payment Processing:** As AmenitizPay processes all payments, this is a primary hook for capturing treasury data.
*   **Payouts:** The ability to split payouts between different bank accounts provides an opportunity to manage and track the flow of funds to property owners.
*   **Refunds:** The platform's refund processing functionality is another point where treasury operations can be monitored.

## 6. Training Data Candidates

*   **Sample Invoices:** The different types of invoices (detailed, simplified) can be used as training data for invoice processing and understanding.
*   **Payment Reports:** The data from payment reports can be used to train models for payment reconciliation and analysis.
*   **Booking Data:** The rich data associated with each booking can be used to train models for demand forecasting and dynamic pricing.
