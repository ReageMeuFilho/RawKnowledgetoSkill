> # BILT Rewards Research

## 1. Company Overview

Bilt Rewards is a fintech company that has created a loyalty program centered around rent payments. Their primary product is the Bilt Mastercard, a credit card that allows users to pay their rent without incurring transaction fees, while earning points on rent and other purchases. The company has also established the Bilt Rewards Alliance, a network of partner properties that offer integrated rent payment and rewards experiences for their residents. Bilt's business model is a three-sided marketplace connecting renters, property managers, and merchants. [1]

Bilt is primarily focused on the residential rental market (LTR), with some expansion into the condo and co-op space, and plans to enter the mortgage market. The company has achieved a significant market position as a first-mover in the rent rewards space, with a network of over 4 million members and 4.5 million rental homes. [1] Their key strengths lie in their strong brand recognition, large and growing user base, valuable rewards program, and a profitable business model. However, their public-facing information is heavily skewed towards the renter experience, with limited details available about the operational workflows and benefits for property managers.

## 2. Workflow Deep Dives

Due to Bilt's renter-centric focus, there is a lack of publicly available, detailed information regarding the operational workflows for property managers. The information below is based on inferences from the available documentation.

### Rent Payment and Collections (AR)

The rent payment process is the most well-documented workflow, although primarily from the renter's perspective.

*   **Exact Steps and Procedures:**
    1.  Residents can initiate rent payments through the Bilt Rewards mobile app or website.
    2.  For properties within the Bilt Alliance, payments are processed directly through the resident portal, which is integrated with the property's existing management system (e.g., RealPage, Yardi). [1]
    3.  For properties outside of the Bilt Alliance, Bilt provides a "BillPay" service. This service gives each renter a unique bank account and routing number, which they can then use to set up Bilt as a payment method in their landlord's online payment portal. [2]
    4.  Bilt also offers the option to mail a physical check to the landlord on the renter's behalf. [3]
*   **Required Inputs and Data Fields:** Renter's name, property address, rent amount, and payment method (Bilt Mastercard or a linked bank account).
*   **Outputs/Artifacts Produced:** Payment confirmations and reward points for the renter.
*   **Roles/Permissions Involved:** The primary roles are the renter and, for Alliance properties, the property manager.
*   **Edge Cases and Exception Handling:** The Product Requirement Document (PRD) mentions automated retry logic for failed payments, but no further details are provided. [1]

### Other Workflows

There is no publicly available information regarding the following workflows for property managers:

*   Owner statements and payouts
*   Bank reconciliation
*   AP: invoice intake, coding, approvals, and payments
*   Trust, escrow, and security deposit handling
*   Reserves management for HOA/Condo
*   Month-end close checklists and reporting packages

## 3. Data Model and Artifacts

*   **Data Model Entities:** The PRD outlines the following core data entities: User, Property, Payment, Points, Merchant, and Card/Payment Method. [1]
*   **API Endpoints and Integration Patterns:** The PRD indicates that Bilt integrates with major property management systems, banking and payment providers (such as Column N.A., Mastercard, and Plaid), credit bureaus, and travel partners. It also lists some API endpoints related to wallet management. [1]
*   **User Roles and Permissions Model:** The primary user role is the renter. While a property manager portal exists for Bilt Alliance partners, the specific roles and permissions within that portal are not detailed in the available documentation.
*   **Approval Workflow Patterns:** No specific information was found.
*   **Audit Logging Capabilities:** No specific information was found.

## 4. Skill Candidates

Based on the available information, the following skill candidates have been identified:

*   **FIN-001: Rent Payment Processing:** The core of Bilt's service is processing rent payments. An AI agent could be trained to automate the process of paying rent through the Bilt platform, accommodating both Bilt Alliance and BillPay methods.
*   **INT-001: Property Management System Integration:** An AI agent could potentially integrate with property management systems to retrieve rent payment information and automate payments through Bilt.
*   **REP-001: Payment Confirmation and Receipt Generation:** An AI agent could be developed to generate payment confirmations and receipts for rent payments made through the Bilt platform.

## 5. Treasury Capture Opportunities

*   **Payouts:** Given the large volume of rent payments processed by Bilt, there is a significant opportunity for an AI agent to manage and optimize these payout flows.

## 6. Training Data Candidates

*   **Example Artifacts:** The user interface designs for the Bilt app, as shown in the PRD, could serve as valuable training data for an AI agent designed to interact with the application. [1]
*   **Edge Cases:** The PRD's mention of automated retry logic for failed payments suggests that this would be a valuable area for creating training scenarios for an AI agent that needs to handle payment exceptions. [1]

## References

[1] BILT Rewards Product Requirement Document
[2] Bilt Rewards Support Center
[3] Reddit - r/biltrewards
