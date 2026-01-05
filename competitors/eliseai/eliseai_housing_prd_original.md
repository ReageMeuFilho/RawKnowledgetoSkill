# EliseAI – Founder-Facing Product Requirement Document (v2, Extended)
## AI Platform for Housing Operations (Leasing, Residents, Maintenance, Renewals, Delinquency)

Version: 2.0 (Founder-Facing, Extended)
Last Updated: January 2026
Audience: Founders, Product, Engineering, GTM, Operations
Scope: End-to-end product blueprint based on public information about EliseAI's housing platform

---

## 0. Product thesis & framing

EliseAI is a **multi-module, agentic AI platform** for housing that automates leasing, resident communication, maintenance, renewals, and delinquency from a single AI + CRM stack (EliseCRM).

### 0.1 One-sentence thesis

EliseAI turns fragmented property operations into a unified, AI-orchestrated system that answers, acts, and follows up across the full prospect-to-resident journey, while centralizing data and workflows in EliseCRM.

### 0.2 Product pillars

1. **Agentic AI, not a chatbot**  
   - AI that can hold multi-step conversations, schedule tours, create and route work orders, manage renewals, and follow up on delinquencies with policy-aware behavior.

2. **EliseCRM as the nervous system**  
   - A CRM purpose-built for multifamily that centralizes prospect and resident records, communications, reporting, and workflows.

3. **Omnichannel automation**  
   - Voice, SMS, email, and webchat support so Elise can respond instantly on any channel residents/prospects use.

4. **Maintenance AI + Maintenance App**  
   - Resident-facing AI that triages maintenance requests and an AI-powered app that auto-assigns, routes, and tracks work orders for supervisors and techs.

5. **Lifecycle automation (ResidentAI)**  
   - Proactive engagement for renewals, delinquencies, and resident questions, with empathy and guardrails to protect resident relationships.

6. **Centralization & role specialization**  
   - Built for centralized operations across large portfolios, enabling specialized roles and consistent service regardless of property.

---

## 1. Vision, mission, and success conditions

### 1.1 Vision

Be the **default AI operating system for housing**—the primary way large operators run communications and operations across leasing, resident services, maintenance, and payments from one platform.

### 1.2 Mission

Fix housing operations by giving property teams AI teammates that handle repetitive communications and workflows end-to-end, so humans can focus on high-value interactions and asset strategy.

### 1.3 Long-term outcomes (3–5 years)

- EliseAI powers >60% of top operators across housing verticals, with AI handling the majority of inbound communications and operational tasks across the portfolio.
- EliseCRM becomes the primary system-of-engagement for resident and prospect interactions, with PMS as the system-of-record for leases and ledgers.
- Platform extends horizontally into healthcare but shares core capabilities, models, and orchestration patterns.

### 1.4 Non-goals (housing scope)

- Replace PMS core ledgers and accounting.  
- Own tightly regulated financial flows (EliseAI can orchestrate reminders and promises-to-pay but defers to payments partners and PMS for money movement).  
- Deep field service optimization beyond maintenance auto-assignment and routing.

---

## 2. Market, customer segments, and personas

### 2.1 Market positioning

- EliseAI serves **mid-market and enterprise housing operators**, including multifamily, SFR, student, and affordable housing.
- It is trusted by hundreds of leading management companies and serves over 60% of the top 50 real estate operators.

### 2.2 Segments

1. **Enterprise multifamily portfolios**  
   - Thousands to tens of thousands of units; complex org structures; multiple PMS instances.  
   - Prioritize scalability, governance, and role specialization.

2. **Mid-market multifamily & SFR operators**  
   - Hundreds to low thousands of units; strong need to centralize leasing and resident services without massive data/IT teams.

3. **Student & affordable housing operators**  
   - Highly seasonal occupancy cycles and high resident service needs; regulatory and compliance focus for affordable.

### 2.3 Key personas & JTBD

**Centralized Leasing Director**
- JTBD: Maintain high occupancy and fast lease-up while controlling payroll and vendor spend.  
- Needs: AI to capture and nurture every lead, schedule tours, and give unified reporting on conversion funnels.

**Property / Community Manager**
- JTBD: Keep day-to-day operations under control, reduce missed calls, and manage maintenance SLAs.  
- Needs: Single pane of glass for resident communication, work orders, renewals, and delinquencies.

**Maintenance Supervisor / Technician**
- JTBD: Receive clear, structured work orders, minimize travel and rework, and track time effectively.  
- Needs: Mobile app with auto-assignment, routing, offline mode, and full timeline/context per work order.

**VP / Head of Operations / Portfolio Manager**
- JTBD: Standardize operations across regions, prove ROI, and reduce tech stack complexity.  
- Needs: EliseCRM dashboards for leasing, maintenance, renewals, and delinquency KPIs.

**Prospect & Resident**
- JTBD (prospect): Get fast, accurate answers and book tours at any time on any channel.  
- JTBD (resident): Resolve questions, submit maintenance, renew leases, and manage payments without waiting on hold.

---

## 3. Problem analysis and requirements

### 3.1 Core problems EliseAI addresses

1. **Missed and slow responses**  
   - Lost leads and frustrated residents due to missed calls and delayed replies.  
   - Requirement: AI must respond instantly, 24/7, across channels with accurate, PMS-backed information.

2. **Operational fragmentation**  
   - Leasing, maintenance, and resident support spread across phones, inboxes, and partial tools.  
   - Requirement: EliseCRM centralizes communications, workflows, and data.

3. **Maintenance inefficiency**  
   - Poor work order clarity, manual routing, and limited visibility cause slow resolution and high labor cost.  
   - Requirement: MaintenanceAI + Maintenance App must streamline intake, routing, and technician workflows.

4. **Revenue risk in renewals & delinquency**  
   - Inconsistent outreach and manual follow-up lead to lower renewal rates and higher bad debt.  
   - Requirement: ResidentAI flows must proactively manage renewals and delinquencies with empathy and guardrails.

### 3.2 Product-level success metrics (external)

- Occupancy lift (~2% in some case studies).  
- Up to multi-million dollar payroll savings across large portfolios (~$14M in cited analysis).  
- AI handling ~99% of work orders and a substantial share of leasing and resident requests.  
- Measurable reduction in bad debt and improved renewal velocity.

### 3.3 Internal success conditions (founder-facing)

- EliseCRM becomes the daily home screen for leasing/ops teams: high DAU/MAU among users.  
- AI flows require minimal configuration per property while still respecting local policies.  
- Maintenance App achieves high technician adoption and reduces manual scheduling overhead.

---

## 4. Platform architecture and modules

### 4.1 Core modules

1. **EliseCRM** – central data and workflow hub.  
2. **LeasingAI** – AI for lead capture, qualification, and tour scheduling.  
3. **ResidentAI** – AI for resident questions, maintenance, renewals, delinquency.  
4. **VoiceAI** – AI-powered call handling and outbound dialing.  
5. **MaintenanceAI** – AI for maintenance intake & triage.  
6. **Maintenance App** – Technician & supervisor app (mobile + web).

### 4.2 Omnichannel layer

- Channels: phone, SMS/text, email, webchat.  
- Requirements:
  - Single conversation thread per prospect/resident across channels in EliseCRM.  
  - Unified consent and opt-out management for compliance.  
  - Configurable AI personality and brand voice per operator.

### 4.3 Integration layer

- Deep PMS integrations for: availability, pricing, unit status, resident ledger, maintenance work orders.  
- Integrations with calendaring tools (for tours) and possibly payments partners (for reminders and promises-to-pay).  
- Bi-directional sync between EliseCRM and PMS for key entities and statuses.

### 4.4 Data & AI layer

- Models trained on over **30 million conversations** with prospects and residents.  
- Domain-specific NLU to understand leasing, maintenance, payments, and community policies.  
- Guardrails around content safety, fair housing, and regulatory constraints (e.g., equal treatment of prospects).

---

## 5. Domain model (housing scope)

### 5.1 Core entities (conceptual)

- **Account / Operator**: organization using EliseAI.  
- **Portfolio / Community / Property**: hierarchical structure for groupings.  
- **Unit / Floorplan**: rentable units with availability, pricing, and attributes.  
- **Prospect**: lead record with interest, tour history, qualification data.  
- **Resident**: occupant record with lease data, contact info, balances, preferences.  
- **Conversation**: thread across channels, with AI and human messages.  
- **Task / Ticket**: internal action items (follow-up, manual review, callbacks).  
- **Work Order**: maintenance job with full lifecycle and technician assignments.  
- **Invoice / Charge**: monetary records for payments and fees.  
- **Policy / Rule**: configuration objects driving AI flows and escalation.

### 5.2 Maintenance-specific entities

- **MaintenanceRequest**: resident-submitted issue (raw + structured).  
- **MaintenanceWorkOrder**: actionable job created/routed from MaintenanceRequest or preventive campaign.  
- **Technician**: user with skills, levels, base location, and schedule.  
- **MaintenanceTimeline**: ordered events (assignment, travel, start, completion, notes).

---

## 6. Module: EliseCRM

### 6.1 Purpose and scope

EliseCRM is the central hub where AI and humans operate together: all communications, tasks, and workflows across leasing, resident services, maintenance, renewals, and delinquency are surfaced here.

### 6.2 Key capabilities

- Unified inbox: view and respond to conversations across phone, SMS, email, chat.  
- Resident & prospect profiles: full history of interactions, leases, work orders, payments, and tasks.  
- Workflows: automated sequences for lead nurturing, renewals, delinquency outreach, and maintenance follow-ups.  
- Reporting: cross-portfolio dashboards for leasing KPIs, maintenance SLAs, renewals, delinquencies.

### 6.3 Requirements (founder-facing)

- Multi-portfolio support with role-based access (central teams vs on-site).  
- Real-time AI + human collaboration: humans can jump into conversations or override AI decisions.  
- Auditability: every AI decision, message, and state change logged with context.

---

## 7. Module: LeasingAI

### 7.1 Scope

Automate lead response, qualification, tour scheduling, and follow-up to maximize occupancy and reduce manual leasing work.

### 7.2 Capabilities

- 24/7 response to prospect inquiries via chat, SMS, phone, email.  
- Access PMS and EliseCRM to provide real-time availability and pricing.  
- Capture preferences and recommend units/floorplans.  
- Schedule and reschedule tours, including AI-guided self-tours.  
- Lead nurturing campaigns using email/SMS to increase lead-to-lease conversion.

### 7.3 Requirements

- Channel-agnostic logic: same core flows across voice/text/email/chat.  
- Fair housing compliance checks and phrasing templates.  
- Configurable qualification criteria and pre-screening questions per operator.

---

## 8. Module: ResidentAI

### 8.1 Scope

Provide an AI layer for resident communications: maintenance, general questions, renewals, and payments/delinquency.

### 8.2 Capabilities

- Answer resident questions about rent, policies, amenities, portals, and services.  
- Collect maintenance requests and guide residents through structured intake and troubleshooting.  
- Proactively reach out on renewals with options and handle inbound questions.  
- Manage delinquency flows: reminders, explanations of fees, and promises-to-pay sequences.

### 8.3 Requirements

- Empathetic tone, especially in financial conversations.  
- Guardrails around legal/financial advice; escalate complex cases to humans.  
- Policy-driven scripts for renewal offers and delinquency scenarios.

---

## 9. Module: MaintenanceAI

### 9.1 Scope

Resident-facing AI that collects, categorizes, and routes maintenance requests, and communicates status updates, while coordinating with the Maintenance App and PMS.

### 9.2 Capabilities

- Intake via SMS, email, chat, or voice: understand free-form complaints and convert to structured work orders (category, severity, symptoms, location in unit).  
- Emergency triage: classify emergencies and route to on-call or fire/flood/gas protocols, especially after hours.  
- Self-service troubleshooting: offer steps residents can take for non-urgent issues to avoid unnecessary trips.  
- Automated status updates: notify residents when a work order is created, assigned, scheduled, in-progress, and completed.

### 9.3 Requirements

- Deep integration with PMS and EliseCRM's maintenance objects for real-time status.  
- Clear, simple triage scripts tuned by category and operator rules.  
- Safety-first logic: low tolerance for under-triaging emergencies.

---

## 10. Module: Maintenance App (technicians & supervisors)

### 10.1 Scope

A dedicated mobile and web app that leverages AI and EliseCRM to assign, route, and track technician work efficiently.

### 10.2 Key features (from public app descriptions)

- **Comprehensive Work Order Management:** View and manage work orders with priority, urgency, due date, full timeline, and resident details.  
- **Smart Auto-Assignment & Scheduling:** Automatically assign work orders based on technician skills, skill levels, location, and priority; supports centralized or hybrid maintenance models.  
- **Real-Time Time Tracking:** Track time per work order and building, simplifying payroll and providing analytics.  
- **Geo-fenced Location Tracking:** Monitor technician location for accurate time logs and routing while respecting privacy.  
- **Offline Mode:** Let technicians work offline and sync when connectivity returns.  
- **Supervisor Tools:** Monitor technician workload and progress, reassign work, and view metrics and trends across properties.

### 10.3 Requirements

- Native iOS and Android apps with responsive web fallback.  
- Seamless sync with EliseCRM so office staff see live maintenance status.  
- Configurable auto-assignment rules per operator/portfolio.  
- Privacy-compliant handling of location and time tracking.

---

## 11. Renewals & delinquency automation

### 11.1 Renewals

- EliseAI proactively engages residents ahead of lease expiration with renewal offers and reminders.  
- AI handles common renewal questions and can explain pricing changes and term options.  
- Workflows move from initial outreach to acceptance, escalation to leasing staff if needed.

### 11.2 Delinquency

- EliseAI manages payment reminders, explains late fees, and coordinates follow-up workflows.  
- Empathetic messaging to protect resident relationships while increasing collections.  
- AI can capture promises-to-pay and update notes in EliseCRM for staff review.

---

## 12. Security, privacy, and compliance

### 12.1 Security expectations

- Industry-standard encryption for data at rest and in transit.  
- Role-based access between leasing, maintenance, corporate teams and vendors.  
- Detailed logs for AI and human actions in sensitive areas (payments, fair housing, emergencies).

### 12.2 Privacy & regulatory

- Compliance with data protection laws in markets served; clear data retention policies.  
- Guardrails for fair housing and non-discrimination in leasing interactions.

---

## 13. Commercial model & unit economics

### 13.1 Pricing & packaging (public info)

- Per-unit monthly pricing, typically in the low single digits per unit; exact pricing via demo/quote.  
- Modules (Leasing, Service/Maintenance, Renewals, Delinquency, VoiceAI) packaged together or as add-ons, all integrated with EliseCRM.

### 13.2 Value claims

- ~2% occupancy growth and ~$14M payroll savings across large portfolios in some reported cases.  
- Handling up to 99% of work orders and large shares of leasing/resident inquiries, reducing staffing pressure.  
- Reduction in bad debt and improved renewals through proactive ResidentAI workflows.

---

## 14. KPIs & success metrics

### 14.1 Leasing & occupancy

- Lead-to-lease conversion rate.  
- Time-to-first-response for new leads.  
- Tour-to-lease conversion and overall occupancy lift.

### 14.2 Maintenance & operations

- % of maintenance requests handled primarily by MaintenanceAI.  
- Average time to work order creation, assignment, and completion.  
- Technician utilization, travel time reduction, and rework rate.

### 14.3 Renewals & delinquency

- Renewal rate and time-to-decision.  
- Bad debt as % of revenue.  
- Collection rates on past due accounts with AI involvement.

### 14.4 Platform & AI

- AI share of conversations vs human.  
- Model accuracy on intent classification and routing.  
- Customer satisfaction and NPS.

---

This document captures a version 2, extended PRD for EliseAI's housing platform using public descriptions of EliseAI, EliseCRM, MaintenanceAI, and the Maintenance App.

