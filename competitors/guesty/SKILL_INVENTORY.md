# Guesty STR PMS - Skill Inventory

> **Source**: `guesty_str_pms_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: STR (Short-Term Rental)

---

## 📊 Extraction Summary

| Category | Count |
|----------|-------|
| Skills | 67 |
| Tools | 45 |
| Memory Types | 18 |
| Integrations | 32 |
| Workflows | 12 |
| Triggers | 28 |

---

## 🎯 Skills Extracted

### Module 1: Guests & Reservations

| ID | Skill Name | Description | Priority |
|----|------------|-------------|----------|
| SKILL-STR-001 | Unified Inbox Management | Aggregate and manage guest messages across all OTA channels | HIGH |
| SKILL-STR-002 | Message Triage & Routing | Categorize inbound messages and route to appropriate handler | HIGH |
| SKILL-STR-003 | AI Response Suggestion | Generate contextually appropriate guest responses | HIGH |
| SKILL-STR-004 | Message Translation | Detect language and translate messages bidirectionally | MEDIUM |
| SKILL-STR-005 | Sentiment Analysis | Analyze guest sentiment and flag negative/urgent messages | MEDIUM |
| SKILL-STR-006 | Calendar Sync Management | Maintain unified calendar across all OTA channels | HIGH |
| SKILL-STR-007 | Double-Booking Prevention | Detect and prevent calendar conflicts in real-time | HIGH |
| SKILL-STR-008 | Date Blocking | Block dates for owner stays, maintenance, cleaning buffers | HIGH |
| SKILL-STR-009 | Guest App Content Management | Manage white-label guest portal content | MEDIUM |
| SKILL-STR-010 | Upsell Management | Present and track upsell offers to guests | MEDIUM |
| SKILL-STR-011 | Pre-Arrival Questionnaire | Collect guest preferences before arrival | LOW |
| SKILL-STR-012 | Guest Profile Management | Maintain unified guest profiles across channels | HIGH |
| SKILL-STR-013 | Guest Segmentation | Categorize guests by value, frequency, preferences | MEDIUM |
| SKILL-STR-014 | Duplicate Profile Merging | Identify and merge duplicate guest records | LOW |
| SKILL-STR-015 | Direct Reservation Creation | Create manual bookings outside OTA channels | HIGH |
| SKILL-STR-016 | Payment Collection | Collect and process guest payments | HIGH |
| SKILL-STR-017 | Refund Processing | Process partial or full refunds | MEDIUM |
| SKILL-STR-018 | Guest Verification | Verify guest identity before check-in | MEDIUM |
| SKILL-STR-019 | Risk Scoring | Calculate risk score for bookings | MEDIUM |
| SKILL-STR-020 | Damage Claim Processing | Handle damage claims and documentation | MEDIUM |

### Module 2: Distribution & Operations

| ID | Skill Name | Description | Priority |
|----|------------|-------------|----------|
| SKILL-STR-021 | Channel Connection | Connect and authenticate OTA accounts | HIGH |
| SKILL-STR-022 | Listing Content Sync | Sync title, description, photos to channels | HIGH |
| SKILL-STR-023 | Rate Distribution | Distribute rates across all connected channels | HIGH |
| SKILL-STR-024 | Availability Sync | Sync availability in real-time across channels | HIGH |
| SKILL-STR-025 | Sync Status Monitoring | Track and alert on sync failures | HIGH |
| SKILL-STR-026 | Direct Booking Website | Manage branded direct booking website | MEDIUM |
| SKILL-STR-027 | Website SEO Optimization | Optimize website for search engines | LOW |
| SKILL-STR-028 | Task Auto-Generation | Create cleaning/maintenance tasks from events | HIGH |
| SKILL-STR-029 | Task Assignment | Assign tasks to staff/vendors | HIGH |
| SKILL-STR-030 | Task Progress Tracking | Track task completion with photos | HIGH |
| SKILL-STR-031 | Task Escalation | Escalate overdue or failed tasks | MEDIUM |
| SKILL-STR-032 | Automation Rule Builder | Create if-then automation rules | HIGH |
| SKILL-STR-033 | Automated Messaging | Send automated messages on triggers | HIGH |
| SKILL-STR-034 | Automated Pricing Adjustment | Apply pricing rules automatically | HIGH |
| SKILL-STR-035 | Multi-Unit Management | Manage buildings with multiple units | MEDIUM |
| SKILL-STR-036 | Analytics Dashboard | Display KPIs and performance metrics | HIGH |
| SKILL-STR-037 | Report Generation | Generate exportable reports | MEDIUM |
| SKILL-STR-038 | Smart Lock Integration | Manage access codes for smart locks | HIGH |
| SKILL-STR-039 | Access Code Generation | Generate unique codes per reservation | HIGH |
| SKILL-STR-040 | Access Code Delivery | Deliver codes via SMS/email/app | HIGH |
| SKILL-STR-041 | Access Revocation | Revoke codes at checkout | HIGH |

### Module 3: Business & Financials

| ID | Skill Name | Description | Priority |
|----|------------|-------------|----------|
| SKILL-STR-042 | Dynamic Pricing | Optimize rates based on demand signals | HIGH |
| SKILL-STR-043 | Competitor Price Monitoring | Track competitor rates in market | MEDIUM |
| SKILL-STR-044 | Seasonal Pricing Rules | Apply seasonal rate modifiers | HIGH |
| SKILL-STR-045 | Event-Based Pricing | Adjust prices for local events | MEDIUM |
| SKILL-STR-046 | Occupancy-Based Pricing | Adjust rates based on occupancy levels | HIGH |
| SKILL-STR-047 | Payment Processing | Process credit card and bank payments | HIGH |
| SKILL-STR-048 | Security Deposit Handling | Hold and release security deposits | HIGH |
| SKILL-STR-049 | Payment Reconciliation | Match payments to bank deposits | HIGH |
| SKILL-STR-050 | Owner Ledger Management | Track owner account balances | HIGH |
| SKILL-STR-051 | Escrow Management | Hold funds in escrow for disputes | MEDIUM |
| SKILL-STR-052 | Tax Collection & Tracking | Collect and track guest taxes | HIGH |
| SKILL-STR-053 | Payout Processing | Process payouts to owners | HIGH |
| SKILL-STR-054 | Owner Statement Generation | Generate monthly owner statements | HIGH |
| SKILL-STR-055 | Owner Portal Access | Provide owners view-only access | MEDIUM |
| SKILL-STR-056 | Owner Stay Management | Allow owners to block personal stays | MEDIUM |
| SKILL-STR-057 | API Key Management | Manage API access credentials | LOW |
| SKILL-STR-058 | Webhook Management | Configure event webhooks | LOW |

### Cross-Cutting Skills

| ID | Skill Name | Description | Priority |
|----|------------|-------------|----------|
| SKILL-STR-059 | Notification Management | Send push/email/SMS notifications | HIGH |
| SKILL-STR-060 | Permission Management | Manage user roles and access | HIGH |
| SKILL-STR-061 | Multi-Brand Management | Support multiple brands in one account | MEDIUM |
| SKILL-STR-062 | Regional Access Control | Limit access by region | MEDIUM |
| SKILL-STR-063 | Audit Logging | Track all user actions | HIGH |
| SKILL-STR-064 | Data Export | Export data in various formats | MEDIUM |
| SKILL-STR-065 | Bulk Operations | Perform batch updates | MEDIUM |
| SKILL-STR-066 | Search & Filter | Search across all data types | HIGH |
| SKILL-STR-067 | Mobile App Support | Core features on mobile | HIGH |

---

## 🔧 Tools Required

### Communication Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-001 | send_whatsapp_message | Send WhatsApp messages | BUY (Twilio) |
| TOOL-STR-002 | send_sms | Send SMS messages | BUY (Twilio) |
| TOOL-STR-003 | send_email | Send email messages | BUY (SendGrid) |
| TOOL-STR-004 | send_push_notification | Send mobile push | BUY (Firebase) |
| TOOL-STR-005 | translate_message | Translate text between languages | BUY (Google Translate) |

### Calendar/Booking Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-006 | sync_airbnb_calendar | Sync with Airbnb API | BUILD |
| TOOL-STR-007 | sync_booking_calendar | Sync with Booking.com API | BUILD |
| TOOL-STR-008 | sync_vrbo_calendar | Sync with Vrbo API | BUILD |
| TOOL-STR-009 | import_ical_feed | Import iCal calendar feeds | BUILD |
| TOOL-STR-010 | export_ical_feed | Export iCal calendar feeds | BUILD |
| TOOL-STR-011 | check_availability | Check date availability | BUILD |
| TOOL-STR-012 | block_dates | Block calendar dates | BUILD |
| TOOL-STR-013 | create_reservation | Create new reservation | BUILD |
| TOOL-STR-014 | update_reservation | Update existing reservation | BUILD |
| TOOL-STR-015 | cancel_reservation | Cancel reservation | BUILD |

### Payment Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-016 | charge_card | Charge credit/debit card | BUY (Stripe) |
| TOOL-STR-017 | process_refund | Process payment refund | BUY (Stripe) |
| TOOL-STR-018 | create_payment_link | Generate payment link | BUY (Stripe) |
| TOOL-STR-019 | verify_payment_status | Check payment status | BUY (Stripe) |
| TOOL-STR-020 | hold_deposit | Hold security deposit | BUY (Stripe) |
| TOOL-STR-021 | release_deposit | Release security deposit | BUY (Stripe) |
| TOOL-STR-022 | process_payout | Send payout to owner | BUY (Stripe Connect) |

### Task Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-023 | create_task | Create new task | BUILD |
| TOOL-STR-024 | assign_task | Assign task to staff | BUILD |
| TOOL-STR-025 | update_task_status | Update task status | BUILD |
| TOOL-STR-026 | upload_task_photo | Upload completion photo | BUILD |
| TOOL-STR-027 | send_task_notification | Notify staff of task | BUILD |

### Smart Lock Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-028 | generate_access_code | Generate unique door code | BUILD |
| TOOL-STR-029 | set_code_validity | Set code time window | BUILD |
| TOOL-STR-030 | revoke_access_code | Revoke door code | BUILD |
| TOOL-STR-031 | get_lock_activity | Get lock access log | BUILD |

### Pricing Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-032 | calculate_dynamic_price | Calculate optimized rate | BUILD |
| TOOL-STR-033 | get_competitor_rates | Fetch competitor pricing | BUY (AirDNA) |
| TOOL-STR-034 | apply_price_rule | Apply pricing modifier | BUILD |
| TOOL-STR-035 | sync_rates_to_channels | Push rates to OTAs | BUILD |

### Analytics Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-036 | calculate_occupancy | Calculate occupancy rate | BUILD |
| TOOL-STR-037 | calculate_adr | Calculate average daily rate | BUILD |
| TOOL-STR-038 | calculate_revpar | Calculate RevPAR | BUILD |
| TOOL-STR-039 | generate_revenue_report | Generate revenue report | BUILD |
| TOOL-STR-040 | generate_owner_statement | Generate owner statement | BUILD |

### Database Tools

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-STR-041 | search_reservations | Search reservations | BUILD |
| TOOL-STR-042 | search_guests | Search guest profiles | BUILD |
| TOOL-STR-043 | search_messages | Search message history | BUILD |
| TOOL-STR-044 | get_property_context | Load property details | BUILD |
| TOOL-STR-045 | get_guest_history | Load guest history | BUILD |

---

## 💾 Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-STR-001 | Conversation History | All guest messages per thread | 2 years |
| MEM-STR-002 | Reservation History | All bookings per property | Forever |
| MEM-STR-003 | Guest Profile | Unified guest data | Forever |
| MEM-STR-004 | Guest Preferences | Dietary, accessibility, special requests | Forever |
| MEM-STR-005 | Payment History | All transactions | 7 years |
| MEM-STR-006 | Task History | All tasks per property | 1 year |
| MEM-STR-007 | Price History | Historical rates per date | 2 years |
| MEM-STR-008 | Sync Status | Channel sync state | 30 days |
| MEM-STR-009 | Access Code Log | Lock access history | 1 year |
| MEM-STR-010 | Owner Ledger | Owner account transactions | 7 years |
| MEM-STR-011 | Audit Trail | All user actions | 3 years |
| MEM-STR-012 | Analytics Snapshots | Daily metrics | 2 years |
| MEM-STR-013 | Automation Executions | Rule execution log | 90 days |
| MEM-STR-014 | Webhook Events | Webhook delivery log | 30 days |
| MEM-STR-015 | Guest Verification | ID verification records | 1 year |
| MEM-STR-016 | Damage Claims | Claim history | 5 years |
| MEM-STR-017 | Tax Records | Tax collection data | 7 years |
| MEM-STR-018 | Property Context | Property details, amenities | Forever |

---

## 🔌 Integrations Required

### OTA Channels

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-001 | Airbnb API | Calendar, messaging, bookings | API |
| INT-STR-002 | Booking.com API | Calendar, messaging, bookings | API |
| INT-STR-003 | Vrbo API | Calendar, messaging, bookings | API |
| INT-STR-004 | Expedia API | Calendar, bookings | API |
| INT-STR-005 | iCal | Calendar import/export | Standard |

### Communication

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-006 | Twilio | SMS, WhatsApp | API |
| INT-STR-007 | SendGrid | Email delivery | API |
| INT-STR-008 | Firebase FCM | Push notifications | API |
| INT-STR-009 | APNs | iOS push notifications | API |

### Payments

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-010 | Stripe | Payment processing | API |
| INT-STR-011 | Stripe Connect | Payouts | API |
| INT-STR-012 | PayPal | Alternative payments | API |
| INT-STR-013 | Wise | Multi-currency payouts | API |

### Smart Locks

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-014 | August API | Smart lock control | API |
| INT-STR-015 | Level Lock API | Smart lock control | API |
| INT-STR-016 | Nuki API | Smart lock control | API |
| INT-STR-017 | Yale Connect API | Smart lock control | API |

### Pricing & Data

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-018 | AirDNA | Competitor pricing data | API |
| INT-STR-019 | Google Translate | Message translation | API |
| INT-STR-020 | OpenAI | AI response generation | API |

### Accounting

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-021 | QuickBooks | Accounting sync | API |
| INT-STR-022 | Xero | Accounting sync | API |

### Marketing

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-023 | Mailchimp | Email campaigns | API |
| INT-STR-024 | HubSpot | CRM sync | API |
| INT-STR-025 | Klaviyo | Email marketing | API |

### Verification

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-026 | Onfido | ID verification | API |
| INT-STR-027 | Jumio | ID verification | API |

### Analytics

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-028 | Google Analytics | Website tracking | API |
| INT-STR-029 | Mixpanel | Product analytics | API |

### Calendar

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-030 | Google Calendar | Calendar export | API |

### Automation

| ID | Integration | Purpose | Type |
|----|-------------|---------|------|
| INT-STR-031 | Zapier | External automations | Webhook |
| INT-STR-032 | Slack | Notifications | API |

---

## 🔄 Workflows Identified

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-STR-001 | Guest Inquiry Response | New message received | Categorize → Generate response → Translate if needed → Send |
| WF-STR-002 | Booking Confirmation | Reservation created | Sync calendar → Send confirmation → Create tasks → Generate codes |
| WF-STR-003 | Pre-Arrival Sequence | 7 days before check-in | Send guest app link → Request questionnaire → Verify guest |
| WF-STR-004 | Check-In Flow | Check-in time | Send access code → Welcome message → House rules |
| WF-STR-005 | Checkout & Turnover | Check-out time | Create cleaning task → Notify cleaner → Track completion |
| WF-STR-006 | Payment Collection | Booking confirmed | Send payment link → Retry on failure → Reconcile |
| WF-STR-007 | Dynamic Pricing | Nightly | Calculate demand → Check competitors → Apply rules → Sync |
| WF-STR-008 | Owner Payout | Monthly | Calculate balance → Generate statement → Process payout |
| WF-STR-009 | Damage Claim | Claim filed | Review photos → Assess damage → Approve/deny → Payout |
| WF-STR-010 | Guest Verification | Pre-check-in | Request ID → Verify → Calculate risk → Gate check-in |
| WF-STR-011 | Review Request | Post-checkout | Wait 24h → Send review request → Track response |
| WF-STR-012 | Escalation | SLA breach | Detect breach → Notify manager → Log incident |

---

## ⚡ Triggers Identified

| ID | Trigger | Event | Actions |
|----|---------|-------|---------|
| TRIG-STR-001 | Inbound Message | Guest sends message | Route to inbox, trigger AI response |
| TRIG-STR-002 | Reservation Created | New booking | Sync calendar, send confirmation |
| TRIG-STR-003 | Reservation Confirmed | Booking confirmed | Start pre-arrival sequence |
| TRIG-STR-004 | Reservation Cancelled | Booking cancelled | Update calendar, process refund |
| TRIG-STR-005 | Payment Received | Payment successful | Update status, send receipt |
| TRIG-STR-006 | Payment Failed | Payment declined | Retry, alert host |
| TRIG-STR-007 | Check-In Time | Scheduled arrival | Send access code, welcome message |
| TRIG-STR-008 | Check-Out Time | Scheduled departure | Create cleaning task, revoke codes |
| TRIG-STR-009 | Pre-Arrival 7 Days | 7 days before check-in | Send guest app link |
| TRIG-STR-010 | Pre-Arrival 24 Hours | 24 hours before check-in | Send reminder, verify guest |
| TRIG-STR-011 | Post-Checkout 24 Hours | 24 hours after checkout | Request review |
| TRIG-STR-012 | Task Overdue | Task past due date | Escalate to manager |
| TRIG-STR-013 | Sync Failed | Channel sync error | Alert host, retry |
| TRIG-STR-014 | Low Occupancy | Occupancy below threshold | Trigger pricing adjustment |
| TRIG-STR-015 | High Demand | Demand spike detected | Increase rates |
| TRIG-STR-016 | Review Posted | Guest leaves review | Notify host |
| TRIG-STR-017 | Negative Sentiment | AI detects negative message | Flag for urgent response |
| TRIG-STR-018 | Message SLA Breach | Response > 2 hours | Alert host |
| TRIG-STR-019 | Owner Stay Request | Owner blocks dates | Update calendar |
| TRIG-STR-020 | Payout Schedule | Weekly/monthly | Process owner payouts |
| TRIG-STR-021 | Tax Remittance Due | Tax deadline approaching | Alert finance |
| TRIG-STR-022 | Deposit Release | 14 days post-checkout | Release escrow |
| TRIG-STR-023 | Damage Reported | Guest/host reports damage | Create claim |
| TRIG-STR-024 | API Rate Limit | API quota exceeded | Throttle requests |
| TRIG-STR-025 | Webhook Delivery Failed | Webhook error | Retry with backoff |
| TRIG-STR-026 | Guest Verification Failed | ID check failed | Alert host, gate check-in |
| TRIG-STR-027 | High Risk Booking | Risk score > 70 | Flag for review |
| TRIG-STR-028 | Scheduled Report | Report schedule time | Generate and send report |

---

## 📊 Vertical Classification

| Category | Core | Shared | STR-Specific |
|----------|------|--------|--------------|
| Skills | 12 | 18 | 37 |
| Tools | 8 | 15 | 22 |
| Memory | 5 | 8 | 5 |
| Integrations | 6 | 12 | 14 |

### Core (All Verticals)
- Communication tools (SMS, Email, WhatsApp)
- Payment processing
- Task management basics
- User authentication
- Notification system
- Audit logging

### Shared (STR + LTR)
- Calendar management
- Guest/Tenant profiles
- Maintenance tasks
- Owner portal
- Financial reporting
- Access code management

### STR-Specific
- OTA channel management
- Dynamic pricing
- Turnover automation
- Guest verification
- Direct booking website
- Revenue optimization



