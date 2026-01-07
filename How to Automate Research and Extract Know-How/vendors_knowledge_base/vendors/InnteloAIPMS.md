# InnteloAIPMS Research

## 1. Company Overview

InnteloAIPMS is a technology company providing an AI-native operating platform for the hospitality and real estate sectors. Their target market includes independent hotels, boutique properties, branded residences, mixed-use developments, and smart cities. The company's core value proposition is to unify guest experience, team operations, personalization, and customer data into a single intelligent ecosystem. Inntelo's platform is built around four core pillars:

*   **AI Guest Experience:** An intelligent concierge that handles guest interactions across various channels (WhatsApp, phone, voice, chat) in over 40 languages.
*   **AI Operations & Planning:** Predictive and intelligent task automation for housekeeping, maintenance, and service workflows with real-time prioritization and resource optimization.
*   **AI Personalisation & Upselling:** Real-time revenue generation through contextual, personalized offers based on guest behavior, intent, and hotel context.
*   **AI Customer Data Platform:** Unified guest profiles, first-party data consolidation, loyalty insights, and predictive customer intelligence.

Inntelo's key differentiator is its agentic and conversational AI working in tandem. The conversational AI handles natural guest interactions, while the agentic AI executes tasks and coordinates across departments. The company aims to capture and resolve 97% of guest interactions through AI agents, reduce front desk administrative burden by over 60%, and generate new revenue streams through upselling and personalization.

## 2. Workflow Deep Dives

Detailed information on financial workflows such as owner statements, bank reconciliation, AP, AR, trust/escrow accounting, reserves management, and month-end close was not available in the provided documentation or through public web searches. The primary focus of the available information is on guest-facing and operational workflows.

### 2.1. AI-Native Housekeeping

*   **Procedures:**
    1.  **Predictive Task Planning:** The system anticipates room needs based on guest profiles and length of stay, schedules deep cleans, predicts linen needs, and optimizes cleaning sequences.
    2.  **Intelligent Task Management:** The AI creates daily housekeeping tasks automatically from various triggers like room checkout schedules, guest requests, and maintenance issues.
    3.  **Dynamic Prioritization:** Tasks are dynamically prioritized based on factors like VIP guest status, guest arrivals, and staff capacity.
    4.  **Mobile Housekeeping App:** Staff receive a prioritized task list on a mobile app with room details, special requests, and multimedia instructions.
    5.  **Quality Control & Compliance:** The system includes room inspection checklists, photo verification of cleaning quality, and a guest feedback loop.
*   **Inputs:** Guest profiles, reservation data, room status, guest requests, maintenance schedules, linen inventory levels.
*   **Outputs:** Prioritized task lists, housekeeping dashboard with live occupancy maps, staff utilization metrics, and issue tracking.
*   **Roles:** Housekeeping staff, housekeeping management.
*   **Edge Cases:** Staff absence, early guest check-in, urgent maintenance requests.

### 2.2. AI-Native Maintenance

*   **Procedures:**
    1.  **Predictive Maintenance Planning:** The system maintains an asset inventory with service history, creates preventative maintenance schedules, and predicts equipment failures.
    2.  **Unified Work Order System:** A single system for both reactive and planned maintenance. Guest requests automatically create work orders.
    3.  **Intelligent Task Management:** The AI sequences tasks intelligently, optimizes resource allocation based on technician skills and availability, and estimates task duration.
    4.  **Technician Mobile App:** Technicians receive live task assignments with details, can document work with photos, and track parts and time.
    5.  **Maintenance Analytics:** The system provides metrics like Mean Time Between Failures (MTBF), Mean Time To Repair (MTTR), and cost per room.
*   **Inputs:** Asset inventory, service history, guest requests, sensor data (for predictive failures).
*   **Outputs:** Maintenance work orders, daily work queues for technicians, maintenance analytics dashboard.
*   **Roles:** Maintenance technicians, maintenance supervisors.
*   **Edge Cases:** Critical issues like water leaks or electrical problems are escalated immediately.

## 3. Data Model and Artifacts

Based on the PRD, the data model includes the following entities:

*   Property
*   Unit
*   Owner
*   Tenant
*   Vendor
*   GL Account
*   Fund
*   Bank Account

The platform produces various artifacts, including:

*   **Reports:** Housekeeping dashboard, maintenance analytics, revenue reports.
*   **Exports:** Data from dashboards and reports can likely be exported, although specific formats are not mentioned.
*   **Statements:** While not explicitly detailed, the system would likely generate guest folios and bills.

## 4. Skill Candidates

Based on the analysis, the following skill candidates have been identified:

*   **CP-001:** Guest Communication Management
*   **CP-002:** Service Request Fulfillment
*   **CP-003:** Concierge Services
*   **CP-004:** Proactive Guest Communication
*   **INT-001:** PMS Integration
*   **INT-002:** Housekeeping System Integration
*   **INT-003:** Maintenance System Integration
*   **INT-004:** F&B System Integration
*   **INT-005:** Payment System Integration
*   **FIN-001:** Upselling and Revenue Generation
*   **AP-001:** (Partial) Invoice intake from F&B orders
*   **REP-001:** Housekeeping and Maintenance Reporting
*   **TRE-001:** (Partial) Payment processing for upsells

## 5. Treasury Capture Opportunities

*   **Approvals:** The agentic AI could potentially own approval workflows for guest-related charges and service requests that have a cost associated with them.
*   **Payouts:** While no direct information on owner payouts was found, if the system were expanded to manage rental income, the AI could calculate and trigger owner payouts.
*   **Fund Segregation:** In a scenario with security deposits or pre-payments, the AI could manage the segregation of these funds into appropriate accounts.

## 6. Training Data Candidates

*   **Example Artifacts:** Guest messages (requests, complaints, questions), housekeeping and maintenance work orders, room inspection checklists, guest folios.
*   **Edge Cases:** Ambiguous guest requests requiring clarification, conflicting priorities between departments, handling of VIP guest escalations.
*   **Evaluation Scenarios:** Measuring the accuracy of intent recognition from guest messages, the efficiency of task routing and completion, and the revenue generated from upselling offers.
