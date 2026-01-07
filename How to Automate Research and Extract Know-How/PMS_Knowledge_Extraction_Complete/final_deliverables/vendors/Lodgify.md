# Lodgify Knowledge Document

## 1. Company Overview

Lodgify is a software-as-a-service (SaaS) platform designed for vacation rental owners and property managers. It provides an all-in-one solution to manage reservations, synchronize calendars across multiple channels, and build a direct booking website. The company primarily targets the short-term rental (STR) market. 

**Products and Verticals:**
*   **Primary Vertical:** Short-Term Rentals (STR)
*   **Core Products:** Property Management Software (PMS), Website Builder, Channel Manager, Booking System, and a Unified Inbox.

**Market Position:**
Lodgify positions itself as a comprehensive solution for hosts to increase direct bookings and streamline their operations. It is often compared to other PMS solutions like Hostaway, Guesty, and OwnerRez.

**Strengths:**
*   **Direct Booking Focus:** Strong emphasis on enabling property owners to create their own websites and receive direct bookings, reducing reliance on OTAs.
*   **All-in-One Platform:** Offers a suite of integrated tools, including a website builder, channel manager, and booking engine.

**Limitations:**
*   **Limited Native Accounting Features:** Lodgify lacks robust, built-in accounting features like bank reconciliation and comprehensive financial reporting. It relies on third-party integrations (e.g., VRPlatform, Clearing) for these functionalities.
*   **Customer Support:** A significant number of users have reported negative experiences with customer support, citing slow response times and a lack of in-depth assistance.
*   **Technical Issues:** Some users have reported technical problems, particularly with channel synchronization and API connections.

## 2. Workflow Deep Dives

### Owner Statements / Owner Payouts

This is the most well-documented workflow within Lodgify's native features.

**Procedure:**
1.  **Create Owner Profile:** Before generating statements, property managers must set up a profile for each owner. This includes their personal information and linking them to their respective properties.
2.  **Define Payout Rules:** Payout rules are established to determine how income from reservations, along with fees and taxes, is divided between the owner and the property manager.
3.  **Manage Transactions:** Expenses and credits related to the rentals can be logged. These can be one-time or recurring transactions.
4.  **Generate Statement:** Statements can be generated for specific periods, either as one-time reports or on a recurring basis (e.g., monthly). The statement includes a detailed breakdown of payouts, fees, taxes, and any other charges. OTA commissions are automatically imported.
5.  **Mark as Paid:** Once payouts are processed, the statements can be marked as paid to maintain clear financial records.
6.  **Download and Share:** Statements can be downloaded in PDF or XLS format for easy sharing and record-keeping.

**Inputs:**
*   Owner profile information
*   Rental property details
*   Reservation data (income, fees, taxes)
*   Expense and credit transactions

**Outputs:**
*   Owner statements (PDF, XLS)

**Roles/Permissions:**
*   Property managers can create and manage owner statements.
*   Owners can be linked to a Lodgify user account to view their own statements.

### Bank Reconciliation, AP, AR, Trust/Escrow, Reserves, Month-End Close

Direct, in-depth documentation for these workflows is not available within Lodgify's help center. The platform's approach to these more complex accounting functions is to rely on integrations with specialized third-party software:

*   **VRPlatform:** An integration that provides trust-compliant accounting, bank feed management, reconciliations, and ACH payments.
*   **Clearing:** Another integration that offers trust accounting and automated bookkeeping, including expense management, owner statements, and payments to homeowners and vendors. This integration is currently limited to the USA and Canada.

This indicates that for a comprehensive treasury and accounting solution, Lodgify users would need to subscribe to and integrate with one of these external platforms.

## 3. Data Model and Artifacts

**Data Model Entities:**
*   **Property:** Represents the rental unit.
*   **Owner:** The owner of the property.
*   **Tenant/Guest:** The individual booking the property.
*   **Reservation:** The booking details, including dates, pricing, and guest information.
*   **Transaction:** Financial entries such as expenses and credits.

**Artifacts:**
*   **Owner Statements:** The primary financial report that can be generated, available in PDF and XLS formats.

## 4. Skill Candidates

Based on the research, the following skill candidates can be mapped:

*   **FIN-001 - Owner Statement Generation:** The process of creating and distributing owner statements is a core feature.
*   **FIN-002 - Payout Calculation:** The system calculates payouts based on predefined rules.
*   **REP-001 - Financial Reporting:** While limited, the generation of owner statements falls under this category.
*   **INT-001 - API Integration:** Lodgify relies heavily on API integrations for accounting functionalities.

## 5. Treasury Capture Opportunities

*   **Payout Approvals:** An AI agent could potentially review and approve owner payouts based on the generated statements and predefined rules.
*   **Fund Segregation:** Given the reliance on third-party trust accounting systems, there is an opportunity for an AI-powered treasury OS to manage the segregation of funds (e.g., security deposits, owner funds, operational funds) directly within the platform.
*   **Expense Management:** An AI agent could automate the logging and categorization of expenses related to properties.

## 6. Training Data Candidates

*   **Example Owner Statements:** The PDF and XLS exports of owner statements can serve as valuable training data for understanding the structure and content of these reports.
*   **Help Center Articles:** The text from the help center articles on owner statements and integrations provides a good corpus of information on the intended workflows.
*   **Reddit Threads:** The user discussions on Reddit, while subjective, offer insights into common pain points, edge cases, and failure modes that could be used to develop more robust AI skills.
