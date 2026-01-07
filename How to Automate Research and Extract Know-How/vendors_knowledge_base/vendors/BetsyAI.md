# BetsyAI Knowledge Document

## 1. Company Overview

**Products:** BetsyAI is an AI-powered platform that provides guest messaging automation, guest journey orchestration, and revenue optimization for the hospitality industry. It functions as an AI copilot that integrates with existing Property Management Systems (PMS) rather than a full replacement. The core features include a unified inbox for multi-channel communication, an AI-powered message generation engine for automated responses, and a revenue optimization engine for upselling opportunities like early check-ins, late check-outs, and gap night fillings.

**Verticals:** The primary focus of BetsyAI is on the short-term rental (STR), vacation rental, and boutique hospitality sectors.

**Market Position:** BetsyAI positions itself as a specialized AI layer that enhances existing PMS functionalities. This integration-first approach differentiates it from monolithic PMS platforms like Boom and Cloudbeds. By focusing on communication and revenue optimization, BetsyAI aims to provide a lightweight and rapidly deployable solution for hospitality operators.

**Strengths:**
- **AI-driven Automation:** 24/7 automated guest communication and upsell management.
- **Integration-First:** Seamless integration with a wide range of existing PMS solutions.
- **Revenue-Aligned Model:** A commission-based model where BetsyAI only earns when it generates additional revenue for the client.
- **Unified Intelligence:** Provides a centralized view of guest interactions and sentiment analysis.

**Limitations:**
- **Dependency on PMS:** As a supplementary layer, its functionality is dependent on the features and data available in the connected PMS.
- **Mixed User Feedback:** Some user reviews suggest that the effectiveness of the upsell features can be inconsistent and that the value proposition may not be universally realized.

## 2. Workflow Deep Dives

BetsyAI is not a full Property Management System (PMS) and does not directly handle financial workflows such as owner statements, bank reconciliation, AP/AR, trust accounting, reserves management, or month-end closing. These functions are typically managed by the underlying PMS that BetsyAI integrates with. BetsyAI's workflows are centered around guest communication and revenue generation.

### Guest Communication and Journey Orchestration

**Exact Steps and Procedures:**
1.  **Integration:** BetsyAI connects to the user's PMS and ingests property data, booking information, and guest contact details.
2.  **Unified Inbox:** All guest communications from various channels (Airbnb, VRBO, email, SMS, etc.) are centralized into a single inbox.
3.  **AI-Powered Responses:** The AI engine analyzes incoming messages and provides automated responses to common inquiries based on pre-configured templates and information from the PMS.
4.  **Guest Journey Automation:** Multi-step communication sequences are triggered at different stages of the guest journey (pre-arrival, during-stay, post-checkout).
5.  **Escalation:** If the AI cannot handle a request or if it's an emergency, the message is escalated to a human agent.

**Inputs and Data Fields:**
- Guest name, contact information, booking details, and communication history.
- Property information, amenities, and house rules from the PMS.

**Outputs/Artifacts:**
- Automated guest messages, pre-arrival information packages, and post-stay follow-ups.

**Roles/Permissions:**
- Property managers and support staff can view and manage guest communications.

**Edge Cases and Exception Handling:**
- The system is designed to escalate complex or sensitive issues to human agents.

### Revenue Optimization and Upselling

**Exact Steps and Procedures:**
1.  **Opportunity Identification:** The AI continuously scans for revenue opportunities such as gap nights, early check-ins, and late checkouts.
2.  **Dynamic Pricing:** BetsyAI dynamically prices upsell offers based on demand and availability.
3.  **Automated Offers:** Personalized offers are automatically sent to guests via their preferred communication channel.
4.  **Confirmation and Scheduling:** Once a guest accepts an offer, the system confirms the booking and coordinates with housekeeping and other operational teams.

**Inputs and Data Fields:**
- Booking calendar, pricing information, and guest data from the PMS.

**Outputs/Artifacts:**
- Upsell offers, booking confirmations, and revenue reports.

**Roles/Permissions:**
- Property managers can configure upselling rules and monitor performance.

**Common Failure Modes and How to Resolve Them:**
- **Low Conversion Rates:** This can be due to unattractive offers or targeting the wrong guests. The solution is to refine the upselling strategy and pricing.
- **Operational Conflicts:** Upselling can create conflicts with cleaning schedules and other operational tasks. This can be mitigated by improving coordination and communication between teams.

## 3. Data Model and Artifacts

Since BetsyAI is an AI layer on top of a PMS, it doesn’t have its own comprehensive data model for property management. Instead, it interfaces with the PMS data model. The key entities it interacts with are:

-   **Property:** Information about the rental unit, including amenities, location, and policies.
-   **Booking:** Details of each reservation, including dates, guest information, and pricing.
-   **Guest:** Contact information and communication history of guests.

**Artifacts:**
-   **Reports:** Revenue reports, performance dashboards, and communication logs.
-   **Exports:** Data exports for analysis and reporting.

## 4. Skill Candidates

Based on the analysis of BetsyAI's capabilities, the following skill candidates are identified:

-   **CP-001: Guest Messaging & Communication:** Automated responses to guest inquiries.
-   **CP-002: Inquiry Management:** Handling pre-booking questions and converting leads.
-   **CP-003: Booking Confirmation & Pre-Arrival:** Sending booking confirmations and pre-arrival information.
-   **CP-004: In-Stay Support & Issue Resolution:** Assisting guests during their stay and handling service requests.
-   **CP-005: Post-Stay & Review Management:** Post-checkout communication and automated review responses.
-   **INT-001: PMS Integration:** Connecting to and synchronizing with various PMS platforms.
-   **REP-001: Reporting & Analytics:** Generating reports on revenue, and communication metrics.
-   **TRE-001: Upsell & Ancillary Revenue:** Identifying and capturing upsell opportunities.

## 5. Treasury Capture Opportunities

BetsyAI's business model is centered around capturing a percentage of the upsell revenue it generates. This presents a direct treasury capture opportunity:

-   **Commission on Upsells:** The 9% commission on all successful upsells (early check-ins, late check-outs, gap nights) is a primary treasury hook.
-   **Payment Processing for Upsells:** If BetsyAI were to handle the payment processing for these upsells, it would provide another treasury capture point.

## 6. Training Data Candidates

-   **Guest Communication Logs:** The extensive logs of guest inquiries and AI responses are a rich source of training data for natural language understanding and generation models.
-   **Upsell Offer Performance:** Data on the performance of different upsell offers can be used to train models for dynamic pricing and offer personalization.
-   **Edge Cases and Escalations:** The instances where the AI has to escalate to a human agent are valuable for training the model to handle a wider range of scenarios.
