# Vendoroo – Founder-Facing Product Requirement Document
## AI-Powered Maintenance Coordination Platform

Version: 2.1 (Founder-Facing Internal Spec, Extended)
Last Updated: January 2026
Audience: Founders, core product, engineering, GTM, ops
Scope: Deep product, technical, and commercial blueprint

---

## 0. Product thesis & framing

### 0.1 One-sentence thesis

Vendoroo converts maintenance coordination from a labor-bound, ad-hoc function into a deterministic, AI-orchestrated system that reliably triages, troubleshoots, dispatches, and justifies every maintenance action across a portfolio at scale.

### 0.2 Product pillars

1. **Agentic AI first**  
   Roos are specialized AI teammates (not just a chatbot) that own well-defined outcomes: answer, triage, troubleshoot, dispatch, coordinate, and reconcile.

2. **PMS-native operations**  
   Vendoroo runs invisibly behind the customer's existing PMS, so ops teams don't have to move systems or change core workflows.

3. **Maintenance brain & memory**  
   Every call, issue, vendor interaction, and invoice trains a persistent "maintenance brain" for that portfolio, enabling better decisions over time.

4. **Financial defensibility**  
   Every maintenance dollar is traceable and explainable to owners, with policy alignment and fraud/waste reduction as first-class objectives.

5. **Scale without burnout**  
   Door count can grow 2–3x without adding proportional maintenance headcount, while reducing burnout risk.

---

## 1. Vision, mission, success conditions

### 1.1 Vision

Become the default AI maintenance brain for professionally managed residential real estate globally – the system of record and execution for everything that touches maintenance.

### 1.2 Mission

Give property managers AI teammates that behave like their best coordinators, never sleep, never forget, and always log every decision, so operators can focus on owners, growth, and strategy.

### 1.3 3–5 year end state

- Vendoroo is integrated with the majority of mid-market PMS platforms in North America and key platforms in UK/EU.  
- Most customers let Roos autonomously handle 80%+ of maintenance work orders end-to-end within configured policy bounds.  
- Vendoroo is the primary data source for maintenance-related analytics (budgets, forecasting, vendor performance) for each portfolio.

### 1.4 Non-goals (current horizon)

- Replace PMS end-to-end (leasing, accounting, marketing, etc.).  
- Deep field-service management for large in-house technician teams (route optimization, truck inventory) – only basic capabilities.  
- Direct B2C product for tenants (tenants interact with Roos, but buyers are operators).

---

## 2. Target customers, segments, and personas

### 2.1 Segmentation

1. Regional PM firms (50–500 doors)  
   - Characteristics: founder/owner-led, thin ops team, manual coordination, rapidly growing door count.  
   - Risks: burnout, inconsistent service, owner churn from perceived chaos.

2. Multi-market / institutional operators (500–5000+ doors)  
   - Characteristics: multiple offices, standardized processes on paper, fragmented vendor networks, strong owner/investor governance.  
   - Risks: inconsistent execution across markets, compliance and SLA risk, maintenance cost variance.

3. SFR portfolio owners (20–200 doors)  
   - Characteristics: financially sophisticated but operationally lean, mix of PMS and spreadsheets, no dedicated coordinator.  
   - Risks: owner time sink, poor tenant experience, overpaying for ad-hoc vendors.

4. Boutique hospitality / STR & serviced apartments  
   - Characteristics: guest expectations close to hotel-level service; maintenance ties directly to reviews and ADR.  
   - Risks: negative reviews, OTAs penalties, revenue leakage.

### 2.2 Primary personas

- PM Owner / Director of Operations  
  - Goals: protect margins, reduce chaos, scale, keep owners happy.  
  - Fears: loss of control, AI damaging relationships, costly implementation.

- Maintenance Manager / Coordinator  
  - Goals: make workload manageable, standardize, reduce interruptions.  
  - Fears: being replaced vs being augmented, AI making wrong emergency calls.

- Asset Manager / Owner Representative  
  - Goals: maintain asset value, avoid overspend, understand where money goes.  
  - Fears: opaque expenses, hidden inefficiencies, lack of documentation.

- Tenant / Resident / Guest (indirect)  
  - Goals: swift response, clear communication, fair handling.  
  - Fears: being ignored, unclear timelines, unsafe living conditions.

---

## 3. Problem analysis and requirements

### 3.1 Core problems

1. High coordination load  
   - Requirement: AI must handle repeatable tasks (triage, status updates, basic troubleshooting, vendor chasing) with minimal human intervention.

2. After-hours and emergency gaps  
   - Requirement: system must classify and route emergencies with extremely low false-negative rate and clear, auditable logic.

3. Inefficient dispatch and vendor selection  
   - Requirement: provider selection must move from "whoever picks up" to policy-driven, performance-informed matching.

4. Fragmented communication and lack of visibility  
   - Requirement: single source of truth for each work order – timeline of events, decisions, communications, and artifacts.

5. Owner distrust / lack of cost defensibility  
   - Requirement: each invoice and work order must be justifiable against policy and historical patterns.

### 3.2 Functional success criteria

- 70–80% of inbound maintenance contacts are fully handled by Roos without human needing to touch every step.  
- Emergency misclassification rate is below agreed threshold (e.g., <0.5% false negatives).  
- Noticeable reduction in average time to first response and average time to resolution.

### 3.3 Non-functional success criteria

- Roos availability: >99.9% (excluding scheduled maintenance).  
- AI responses must meet defined tone/brand guidelines 95%+ of the time.  
- Zero known security incidents attributable to AI or integrations.

---

## 4. Product capabilities overview

1. AI multi-channel intake (voice, SMS, email, portal/chat).  
2. Structured triage, classification, and urgency assessment.  
3. Remote troubleshooting flows per issue category.  
4. Vendor intelligence and automated assignment.  
5. Scheduling and coordination with tenants and vendors.  
6. Work-in-progress tracking and escalation.  
7. Completion verification and tenant satisfaction checks.  
8. Invoice validation and accounting/owner reporting.  
9. Maintenance book and analytics (patterns, forecasting).  
10. Policy and configuration layer (per customer and per property).

---

## 5. Detailed domain model

### 5.1 Core entities

(1) Account  
Represents a customer (PM firm, SFR owner, hospitality operator).

Key fields:
- id, name, type (PM, SFR, hospitality, institutional).  
- contact info, billing info.  
- PMS integration settings, accounting integration settings.  
- global policies (budget thresholds, emergency definitions, escalation contacts).

(2) Property  

Key fields:
- id, account_id, name, type (apartment, SFR, MF, STR, etc.).  
- address, geo, unit_count.  
- maintenance_preferences (preferred vendors, do_not_use_vendors, budget limits per urgency, escalation rules).  
- access_info (keybox/smart lock details, special instructions).  
- maintenance_history metadata (recurring_issue_tags, warranties).

(3) Unit (optional, if PMS exposes)  

Key fields:
- id, property_id, unit_label.  
- occupancy status, tenant_id (if occupied).  
- unit-specific quirks (e.g., water pressure issues, old HVAC).

(4) Tenant / Resident / Guest  

Key fields:
- id, property_id, unit_id.  
- name, phone, email, language_preference, communication_preferences.  
- lease_start, lease_end (if applicable).  
- maintenance_history (requests, patterns, satisfaction scores).

(5) MaintenanceRequest  

Key fields:
- id, property_id, unit_id, tenant_id.  
- request_source (phone, sms, email, portal).  
- raw_text, extracted_summary.  
- created_at, updated_at.  
- linked_work_order_id.

(6) WorkOrder  

Key fields:
- id, maintenance_request_id, account_id, property_id, unit_id.  
- job_type (repair, inspection, replacement, emergency_response, preventive).  
- issue_category, urgency_level, safety_flags.  
- troubleshooting_steps (structured list + free-form notes).  
- assigned_vendor_id, vendor_contact_snapshot.  
- scheduling_info (proposed_slots, confirmed_slot, timezone).  
- completion_info (notes, photos, parts, labor_hours).  
- financials (estimated_cost, approved_budget, actual_cost).  
- status (state machine: received, triaged, awaiting_approval, awaiting_vendor, scheduled, in_progress, completed, rework, cancelled).

(7) Vendor  

Key fields:
- id, account_id.  
- name, contact, business_type (independent, company).  
- specialties (plumbing, HVAC, electrical, etc.).  
- service_areas (postal codes, cities).  
- performance_metrics (jobs_completed, on_time_rate, avg_rating, rework_rate, reliability_score).  
- rates (base_call_fee, hourly_rate, after_hours_multiplier).  
- availability (days, times, emergency_capable).  
- integration (manual, email, sms, portal, API).  
- tier (bronze/silver/gold), status (active/inactive/do_not_use).

(8) Invoice  

Key fields:
- id, work_order_id, vendor_id.  
- line_items (description, qty, rate, total).  
- taxes, total_amount, currency.  
- received_date, due_date.  
- validation_status (pending, auto_approved, flagged, rejected).  
- export_status (to accounting), payment_status.

(9) FinancialRecord  

Key fields:
- id, work_order_id, property_id, account_id.  
- transaction_type (vendor_payment, owner_charge, adjustment, refund).  
- amount, currency, date.  
- accounting_category, external_ids.

(10) PolicyRule  

Key fields:
- id, scope (account-wide / property / unit).  
- rule_type (budget, escalation, safety, communication).  
- condition_expression (JSON/YAML representation, e.g., "if urgency='emergency' and category='no_heat' then ...").  
- action (auto_approve, auto_escalate, vendor_preference, notification).  
- enabled, created_by, updated_by.

(11) AuditLog  

Key fields:
- id, actor_type (roo, human), actor_id (if human).  
- work_order_id, request_id, account_id.  
- action_type (triage_decision, vendor_assigned, budget_change, invoice_flagged, message_sent).  
- input_snapshot (sanitized).  
- output_summary.  
- created_at.

(12) MaintenanceBookEntry  

Key fields:
- id, property_id, unit_id, system_type (HVAC, plumbing, electrical, etc.).  
- asset_info (model, age, warranty_expiry).  
- recurring_issues, recommendations, last_service_date.  
- preferred_vendor_id.

---

## 6. AI agents and orchestration requirements

### 6.1 Agent responsibilities & boundaries

For each Roo we define:
- Inputs (data, context, tools).  
- Outputs (decisions, state changes, messages).  
- Hard constraints (what it cannot do).  
- Failure modes and fallbacks.

(1) Receptionist Roo
- Inputs: caller ID, phone transcript, historical interactions, property/tenant mapping.  
- Outputs: new MaintenanceRequest, updated WorkOrder, initial summary.  
- Constraints: cannot promise specific times or costs unless policy allows; must escalate unclear identity.

(2) Triage & Troubleshooting Roo
- Inputs: request summary, property/unit history, MaintenanceBook.  
- Outputs: classified issue_category, urgency_level, safety_flags, troubleshooting_steps.  
- Constraints: cannot downgrade emergencies, must obey safety PolicyRules.

(3) Coordinator Roo
- Inputs: WorkOrder, vendor list, tenant preferences, policy rules.  
- Outputs: assigned_vendor_id, proposed_slots, confirmed_slot, notifications.  
- Constraints: cannot assign do_not_use vendors; cannot exceed budget without approval.

(4) Invoice & Compliance Roo
- Inputs: Invoice, WorkOrder, PolicyRules, vendor rates.  
- Outputs: validation_status, flags, suggested annotations, accounting export record.  
- Constraints: can't auto-approve above threshold; must log all decisions to AuditLog.

(5) Assistant Roo
- Inputs: arbitrary queries from PM team, all domain data.  
- Outputs: natural-language answers with links to underlying records.  
- Constraints: read-only; cannot mutate state.

### 6.2 Orchestration engine

Requirements:
- Central state machine per WorkOrder with defined transitions and invariants.  
- Agent tasks queued and executed with idempotency guarantees.  
- Ability to pause/resume automation per account/property/work_order.  
- AuditLog entry for each agent decision.

---

## 7. End-to-end workflows (expanded)

### 7.1 Call-based maintenance request (canonical path)

1) Tenant calls maintenance number.  
2) IVR/telephony routes call to Receptionist Roo.  
3) Roo: greeting in brand voice; verifies property/unit (DID, caller ID, questions).  
4) Roo: captures issue description and runs quick classification questions.  
5) Triage Roo: assigns category & urgency, checks MaintenanceBook for patterns.  
6) Roo: attempts troubleshooting if safe and appropriate.  
7) If resolved: logs steps, closes WorkOrder or marks "monitor" with callback.  
8) If dispatch needed: passes WorkOrder to Coordinator Roo for vendor assignment.

### 7.2 After-hours emergency flow

1) Call flagged as after-hours by schedule.  
2) PolicyRules: stricter mapping (more cases considered emergency).  
3) Triage Roo uses emergency script: determine immediate dangers, instruct tenant on safety (e.g., shut-off valve).  
4) Coordinator Roo: finds emergency-capable vendor, attempts immediate dispatch.  
5) Notifications: PM on-call receives Slack/SMS with summary and ability to override.  
6) Post-incident: WorkOrder tagged as emergency; additional review and reporting.

### 7.3 Email/SMS request flow

1) Tenant sends email/SMS describing issue.  
2) Ingestion: parse content, map to tenant/property, create MaintenanceRequest.  
3) Triage Roo: same classification & troubleshooting logic via asynchronous Q&A.  
4) Confirmation sent via same channel; WorkOrder created.

### 7.4 Preventive maintenance campaign

1) PM sets up rule: "HVAC inspection every 6 months for all properties in region X".  
2) System generates WorkOrders with job_type=preventive on schedule.  
3) Coordinator Roo batches vendor assignments and routes jobs.  
4) Completion and reporting aggregated by campaign.

### 7.5 Invoice review and export

1) Vendor submits invoice via portal/email attachment/API.  
2) Parsing: extract line items and totals.  
3) Invoice & Compliance Roo compares to WorkOrder scope, PolicyRules, and standard rates.  
4) If clean: auto_approved, ready for export.  
5) If issues: flagged with explanation; PM can adjust or reject.  
6) Approved invoices -> FinancialRecord -> export to accounting (file/API).

---

## 8. UI/UX requirements

### 8.1 PM console views

1) Global maintenance dashboard  
   - Metrics: open WOs by status/urgency, average response time, remote resolution rate, vendor performance snapshots.  
   - Filters: account, property, vendor, issue_category, timeframe.

2) WorkOrder detail view  
   - Timeline of events (calls, messages, agent decisions).  
   - Current status and next action.  
   - Vendor, schedule, tenant info, photos, invoices.  
   - Controls: pause automation, reassign vendor, override decisions.

3) Policy configuration  
   - UI for budget thresholds, emergency definitions, vendor preferences.  
   - Simulation mode: "show me how this rule would change decisions".

4) Maintenance book view  
   - Per property/unit: historical issues, patterns, recommendations.  
   - Export option for owner reports.

### 8.2 Vendor experience

- Mobile-friendly web interface with:
  - Job list and filters.  
  - Job detail (description, photos, access, budgets).  
  - Accept/decline, ETA, status updates.  
  - Invoice submission.

### 8.3 Owner reporting outputs

- Configurable templates for monthly/quarterly reports:  
  - Executive summary (issues, spend, trends).  
  - Detailed breakdown per property and category.  
  - Commentary on major repairs and recommendations.

---

## 9. Technical architecture & performance

### 9.1 High-level components

- API gateway & auth.  
- Orchestration service (state machine, queues).  
- Agent services (Roo workers).  
- Integration services (PMS, accounting, telephony).  
- Web app (PM console, vendor portal).  
- Data & analytics (OLTP + analytics store).

### 9.2 Performance requirements

- Voice latency: <1.5–2 seconds for most responses.  
- WorkOrder state changes: eventual consistency within seconds.  
- Reporting: dashboard queries under a few seconds for typical portfolio sizes.

### 9.3 Scalability

- Initial target: thousands of concurrent conversations and tens of thousands of WorkOrders/month per cluster.  
- Scale horizontally on stateless services; shard data by account or region as needed.

---

## 10. Security, compliance, and risk

### 10.1 Security

- Encrypted in transit and at rest.  
- RBAC for PM staff, vendors, and owners.  
- Strict audit logging of sensitive operations.

### 10.2 Privacy & compliance

- GDPR-ready data subject rights flows.  
- Data minimization on PII and payment details.  
- Clear data retention policies per region.

### 10.3 Risk mitigation

- Emergency misclassification: conservative policies, manual review hooks.  
- Integration failures: retry logic, monitoring, manual fallback.

---

## 11. Commercial model and unit economics

### 11.1 Pricing

- Per-door subscription with tiers; optional add-ons for payments and advanced analytics.  
- Implementation/onboarding fee for larger accounts.

### 11.2 Unit economics targets

- Gross margin 70–80% at scale.  
- Low CS hours per 1000 doors via robust productization.

### 11.3 Sales & GTM

- Land-and-expand motion, starting with maintenance chaos and after-hours coverage.  
- Partnerships with PMS vendors and industry influencers.

---

## 12. Implementation roadmap (high-level)

- Phase 0: solidify orchestrator and core flows for 1–2 PMSs.  
- Phase 1: productionize console, vendor portal, and invoice validation.  
- Phase 2: maintenance book, predictive analytics, preventive maintenance.  
- Phase 3: deeper ecosystem integrations, marketplace elements, and regional expansions.



