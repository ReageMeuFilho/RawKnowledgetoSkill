# Engineering Specification Prompt: AI Maintenance Coordinator

**Gap ID**: GAP-AF-002  
**Skill ID**: SKILL-254  
**Created**: 2026-01-06  
**Created By**: Cursor AI  
**Stage 1 Quality Score**: 9.5/10 (Exceptional)  
**Research Document**: `knowledge/operations/KD-AF-002-ai-maintenance-coordinator.md`

---

## 📋 YOUR MISSION

You are an **Engineering Agent** tasked with producing a **comprehensive engineering specification document** for the **AI Maintenance Coordinator** system. This specification must be detailed enough for a development team to implement the system without ambiguity.

**Your output file**: `knowledge/operations/ES-AF-002-ai-maintenance-coordinator.md`

**Expected output**: 6,000-10,000+ lines of detailed technical specification covering all 20 sections below.

---

## 📚 REQUIRED READING

Before starting, thoroughly read:

1. **`knowledge/operations/KD-AF-002-ai-maintenance-coordinator.md`** - Stage 1 research (EXCEPTIONAL quality)
   - Vendoroo deep-dive with 8-step workflow
   - Complete data model with 6 entities
   - 7 core business rules + 6 edge cases
   - 5 external system integrations
   - 48+ source citations

2. **`docs/AGENT_GUIDE.md`** - Process guidelines

3. **Reference**: Previous engineering specs:
   - `knowledge/ai-workforce/ES-HOAI-001-ai-workforce-architecture.md` (11,398 lines)
   - `knowledge/communication/ES-AF-001-ai-leasing-assistant.md` (10,773 lines)

---

## 🏗️ SPECIFICATION SECTIONS

You must produce detailed specifications for ALL 20 sections below. Each section should be comprehensive, with schemas, tables, diagrams, pseudocode, and implementation details.

---

### SECTION 1: Executive Summary & System Overview

Produce a comprehensive executive summary covering:

1. **Problem Statement**
   - Current maintenance coordination challenges (chaos, delays, high costs)
   - Impact on property managers, residents, and owners
   - Why manual/call center solutions are insufficient

2. **Solution Overview**
   - AI Maintenance Coordinator as a "24/7 digital dispatcher"
   - End-to-end workflow automation from intake to invoice
   - Hot Path (AI decisions) vs Cold Path (Temporal workflows)

3. **Key Capabilities**
   - Instant multi-channel request intake (phone, text, email, portal)
   - Remote troubleshooting to avoid unnecessary truck rolls
   - Intelligent vendor selection and dispatch
   - Continuous coordination and status updates
   - Post-completion verification and billing

4. **Business Value Metrics**
   - Target: $12/door maintenance cost reduction
   - Target: 50% reduction in average work order completion time
   - Target: 80% AI-handled tasks without human intervention
   - Target: 95% first-try answer rate (no voicemail)

5. **Architecture Summary Diagram**
   ```
   [Resident Channels] → [AI Coordinator] → [Vendor Dispatch]
          ↓                    ↓                   ↓
   [PMS Integration]    [Troubleshooting KB]  [Completion Tracking]
   ```

---

### SECTION 2: Technical Architecture Overview

Provide a detailed technical architecture including:

1. **System Components Diagram**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        AI MAINTENANCE COORDINATOR                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐          │
│  │  INTAKE LAYER    │  │  BRAIN LAYER     │  │  ACTION LAYER    │          │
│  │                  │  │                  │  │                  │          │
│  │ - Voice Agent    │  │ - Issue Triage   │  │ - Vendor Router  │          │
│  │ - SMS Handler    │  │ - Troubleshoot   │  │ - Scheduler      │          │
│  │ - Email Parser   │  │ - Decision       │  │ - Notifier       │          │
│  │ - Portal API     │  │ - Escalation     │  │ - Invoice        │          │
│  └────────┬─────────┘  └────────┬─────────┘  └────────┬─────────┘          │
│           │                     │                     │                     │
│           └─────────────────────┼─────────────────────┘                     │
│                                 │                                           │
│  ┌──────────────────────────────┴────────────────────────────────────────┐ │
│  │                     ORCHESTRATION LAYER (Temporal)                     │ │
│  │  - Work Order Workflow    - Dispatch Workflow    - Billing Workflow   │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                     DATA LAYER (MongoDB + Redis + Vector)              │ │
│  │  - Work Orders    - Properties    - Vendors    - Communications       │ │
│  │  - Troubleshooting KB (Vector)    - Session State (Redis)            │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                     INTEGRATION LAYER (MCP Servers)                    │ │
│  │  - mcp-pms (AppFolio, Yardi)    - mcp-telephony (Twilio)             │ │
│  │  - mcp-vendor-portal            - mcp-payment (Treasury)              │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

2. **Layer Responsibilities**
   - Define clear boundaries between layers
   - Specify communication patterns (sync vs async)
   - Document data flow between layers

3. **Hot Path vs Cold Path Architecture**

| Aspect | Hot Path | Cold Path |
|--------|----------|-----------|
| Purpose | AI reasoning, NLU, troubleshooting | Durable workflows, financial transactions |
| Technology | LangGraph + Claude/GPT | Temporal + TigerBeetle |
| Latency | <500ms | <5s |
| Guarantees | Best effort | Exactly-once, durable |
| Examples | Intent detection, troubleshooting | Work order creation, invoice processing |

4. **Service Architecture**

| Service | Type | Technology | Scaling |
|---------|------|------------|---------|
| intake-service | Stateless | Python/FastAPI | Horizontal |
| brain-service | Stateful | LangGraph | Horizontal with session affinity |
| vendor-service | Stateless | Python/FastAPI | Horizontal |
| notification-service | Stateless | Python/FastAPI | Horizontal |
| workflow-service | Durable | Temporal Worker | Horizontal |

---

### SECTION 3: Request Intake & Channel Management

Detail the multi-channel intake system:

1. **Phone/Voice Channel**

```yaml
voice_intake:
  provider: Twilio
  capabilities:
    - speech_to_text: Deepgram/Whisper
    - text_to_speech: ElevenLabs/Azure Neural
    - real_time_processing: WebSocket streaming
    - call_recording: Optional (compliance)
  
  greeting_script:
    default: "Hello, this is {property_name} maintenance. How can I help you today?"
    after_hours: "Hello, this is {property_name} after-hours maintenance support. What's your emergency?"
  
  call_flow:
    1: verify_caller_identity
    2: understand_issue
    3: log_work_order
    4: troubleshoot_or_dispatch
    5: confirm_next_steps
    6: end_call
  
  fallback_triggers:
    - "speak to a human"
    - "transfer me"
    - 2_failed_understanding_attempts
```

2. **SMS/Text Channel**

```yaml
sms_intake:
  provider: Twilio
  
  message_types:
    - new_request: "My [issue] in [location]"
    - status_check: "What's the status of my repair?"
    - confirmation: "YES" / "NO" / "10am works"
  
  conversation_state:
    storage: Redis
    ttl: 24_hours
    context_window: last_10_messages
  
  response_guidelines:
    max_length: 160_chars (SMS limit)
    tone: friendly, concise
    always_include: next_step_or_question
```

3. **Email Channel**

```yaml
email_intake:
  provider: SendGrid/Microsoft Graph
  
  parsing:
    - extract_subject_as_summary
    - extract_body_for_details
    - detect_urgency_keywords
    - extract_attachments (photos)
  
  auto_response:
    immediate: "We received your maintenance request. Reference: {wo_id}"
    
  threading:
    maintain_conversation_thread: true
    reply_to_chain: true
```

4. **Portal/API Channel**

```yaml
portal_intake:
  endpoint: POST /api/v1/maintenance/requests
  
  request_schema:
    property_id: string (required)
    unit_id: string (required)
    resident_id: string (required)
    issue_category: enum (required)
    description: string (required)
    urgency: enum [routine, urgent, emergency]
    photos: array[string] (optional, max 5)
    preferred_times: array[datetime] (optional)
  
  response:
    work_order_id: string
    status: "received"
    estimated_response_time: string
    next_steps: string
```

5. **Channel Unification**

Specify how all channels feed into a unified processing pipeline:

```python
class MaintenanceRequest:
    request_id: str
    source_channel: Literal["phone", "sms", "email", "portal"]
    property_id: str
    unit_id: str
    resident_id: str
    resident_contact: ContactInfo
    issue_description: str
    issue_category: Optional[str]  # May be determined by AI
    urgency: UrgencyLevel
    attachments: List[Attachment]
    raw_transcript: Optional[str]  # For voice
    created_at: datetime
    session_id: str  # Links multi-turn conversation
```

---

### SECTION 4: Issue Triage & Classification System

Define the AI-powered triage system:

1. **Issue Category Taxonomy**

```yaml
categories:
  plumbing:
    subcategories: [leak, clog, no_water, water_heater, toilet, faucet, garbage_disposal]
    default_vendor_type: plumber
    emergency_keywords: [flood, burst_pipe, sewage, gas_smell]
    
  electrical:
    subcategories: [no_power, outlet, lighting, breaker, smoke_detector]
    default_vendor_type: electrician
    emergency_keywords: [sparking, burning_smell, no_power_whole_unit]
    
  hvac:
    subcategories: [ac_not_cooling, heat_not_working, thermostat, strange_noise, filter]
    default_vendor_type: hvac_tech
    emergency_keywords: [no_heat_winter, gas_smell]
    
  appliance:
    subcategories: [refrigerator, stove, dishwasher, washer, dryer, microwave]
    default_vendor_type: appliance_tech
    emergency_keywords: [gas_smell, fire]
    
  structural:
    subcategories: [door, window, lock, ceiling, floor, wall, roof_leak]
    default_vendor_type: handyman
    emergency_keywords: [roof_collapse, flood_from_above]
    
  pest:
    subcategories: [rodent, insect, bed_bugs, birds]
    default_vendor_type: pest_control
    emergency_keywords: [snake, aggressive_animal]
```

2. **Intent Recognition Model**

```yaml
intent_recognition:
  model: fine-tuned-classifier
  
  intents:
    - new_maintenance_request
    - status_inquiry
    - schedule_change
    - emergency_report
    - complaint
    - general_question
    - speak_to_human
  
  confidence_thresholds:
    high: 0.85  # Proceed automatically
    medium: 0.65  # Proceed with confirmation
    low: 0.65  # Ask clarifying question
```

3. **Urgency Determination Algorithm**

```python
def determine_urgency(request: MaintenanceRequest) -> UrgencyLevel:
    """
    Returns: EMERGENCY (P0), URGENT (P1), ROUTINE (P2)
    """
    
    # Emergency keywords always trigger P0
    EMERGENCY_KEYWORDS = ["flood", "fire", "gas", "no heat", "sewage", "sparking"]
    if any(kw in request.issue_description.lower() for kw in EMERGENCY_KEYWORDS):
        return UrgencyLevel.EMERGENCY
    
    # Time-sensitive conditions
    if is_after_hours() and request.issue_category in ["hvac", "plumbing"]:
        if "no_heat" in request.issue_description and is_winter():
            return UrgencyLevel.EMERGENCY
        if "no_ac" in request.issue_description and is_extreme_heat():
            return UrgencyLevel.URGENT
    
    # Resident-indicated urgency
    if request.urgency == "emergency":
        # Validate with follow-up question
        return UrgencyLevel.URGENT  # Escalate to emergency if confirmed
    
    # Default routing
    return UrgencyLevel.ROUTINE
```

4. **Property Context Loading**

Define what context to load for each request:

```yaml
property_context:
  always_load:
    - property_profile
    - unit_details
    - resident_lease_status
    - owner_preferences
  
  conditional_load:
    if_repeat_issue:
      - past_work_orders (same category, last 90 days)
      - related_vendor_history
    
    if_appliance_issue:
      - appliance_inventory
      - warranty_information
    
    if_hvac:
      - hvac_system_type
      - last_service_date
      - filter_change_schedule
```

---

### SECTION 5: Troubleshooting Engine

Design the remote troubleshooting system that can resolve issues without vendor dispatch:

1. **Troubleshooting Knowledge Base Schema**

```yaml
TroubleshootingEntry:
  entry_id: string
  issue_category: string
  issue_subcategory: string
  keywords: array[string]
  
  steps:
    - step_number: 1
      question: "Is the outlet a GFCI (has reset button)?"
      expected_responses:
        - response: "yes"
          next_step: 2
        - response: "no"
          next_step: 3
        - response: "don't know"
          clarification: "A GFCI outlet has a small 'reset' button..."
      
    - step_number: 2
      instruction: "Please press the reset button firmly."
      verification: "Did the power come back on?"
      outcomes:
        - response: "yes"
          result: RESOLVED
          close_message: "Great! The GFCI was tripped. If this happens again frequently, we should have an electrician check it."
        - response: "no"
          next_step: 4
  
  resolution_rate: 0.35  # Historical % resolved via troubleshooting
  avg_time_to_resolve: 3_minutes
  last_updated: datetime
```

2. **Troubleshooting Flow Engine**

```python
class TroubleshootingSession:
    session_id: str
    work_order_id: str
    entry_id: str
    current_step: int
    responses: List[StepResponse]
    outcome: Optional[TroubleshootingOutcome]
    
    async def execute_step(self, step: TroubleshootingStep) -> StepResult:
        """Execute a troubleshooting step and process response."""
        
        # Present question/instruction to resident
        await self.send_to_resident(step.question or step.instruction)
        
        # Wait for response
        response = await self.await_response(timeout=300)  # 5 min timeout
        
        # Match response to expected outcomes
        matched = self.match_response(response, step.expected_responses)
        
        if matched.result == "RESOLVED":
            return StepResult(outcome=TroubleshootingOutcome.RESOLVED)
        elif matched.next_step:
            return StepResult(next_step=matched.next_step)
        else:
            return StepResult(outcome=TroubleshootingOutcome.DISPATCH_NEEDED)
```

3. **Troubleshooting Content by Category**

Provide detailed troubleshooting trees for top 10 issue types:

**Example: Garbage Disposal Not Working**

```
START
  ├─ Q1: "Is the disposal making any sound when you flip the switch?"
  │   ├─ YES → Q2
  │   └─ NO → Q3
  │
  ├─ Q2: "Is it humming but not spinning?"
  │   ├─ YES → "Turn OFF disposal. Look underneath for a hex key slot. 
  │   │         Insert 1/4" Allen wrench and rotate back and forth. 
  │   │         Then press reset button. Try again."
  │   │   └─ RESOLVED?
  │   │       ├─ YES → CLOSE (resolved)
  │   │       └─ NO → DISPATCH (jammed/broken)
  │   └─ NO → Q4 (grinding but not draining)
  │
  ├─ Q3: "Can you find a reset button on the bottom of the disposal?"
  │   ├─ YES → "Press the reset button firmly. Try the switch again."
  │   │   └─ RESOLVED?
  │   │       ├─ YES → CLOSE (resolved)
  │   │       └─ NO → CHECK BREAKER
  │   └─ NO → DISPATCH (electrical issue)
  │
  └─ CHECK BREAKER: "Check if the kitchen circuit breaker has tripped."
      ├─ TRIPPED → "Flip it fully OFF then ON. Try disposal."
      │   └─ RESOLVED? → YES=CLOSE / NO=DISPATCH
      └─ NOT TRIPPED → DISPATCH (internal failure)
```

4. **Resolution Tracking**

```yaml
resolution_metrics:
  track_per_issue_category:
    - total_attempts
    - successful_resolutions
    - resolution_rate
    - avg_steps_to_resolution
    - avg_time_to_resolution
  
  feedback_loop:
    if_vendor_visit_finds_simple_fix:
      - flag_for_kb_update
      - add_troubleshooting_step
    
    if_troubleshooting_often_fails:
      - review_step_clarity
      - consider_removing_or_reordering
```

---

### SECTION 6: Vendor Management System

Design the vendor roster, selection, and communication system:

1. **Vendor Data Model**

```yaml
Vendor:
  vendor_id: string (PK)
  company_name: string
  contact_name: string
  phone: string
  email: string
  
  service_types: array[VendorType]  # plumber, electrician, etc.
  
  coverage:
    zip_codes: array[string]
    max_radius_miles: number
  
  availability:
    business_hours: TimeRange
    after_hours_available: boolean
    emergency_available: boolean
    blackout_dates: array[DateRange]
  
  preferences:
    preferred_contact_method: enum [phone, sms, email]
    max_concurrent_jobs: number
    preferred_job_types: array[string]
  
  performance:
    avg_response_time_minutes: number
    avg_completion_time_hours: number
    first_time_fix_rate: number
    resident_satisfaction_avg: number
    total_jobs_completed: number
    last_job_date: datetime
  
  financials:
    hourly_rate: number
    emergency_rate_multiplier: number
    typical_job_cost_range: { min: number, max: number }
    payment_terms: string
  
  compliance:
    insurance_expiry: date
    license_number: string
    license_expiry: date
    background_check_date: date
  
  status: enum [active, suspended, inactive]
  notes: string
  created_at: datetime
  updated_at: datetime
```

2. **Vendor Selection Algorithm**

```python
def select_vendor(
    request: MaintenanceRequest,
    property: Property,
    vendors: List[Vendor]
) -> RankedVendorList:
    """
    Select and rank vendors for a maintenance request.
    Returns top 3 vendors in priority order.
    """
    
    # Step 1: Filter eligible vendors
    eligible = []
    for vendor in vendors:
        if not vendor_matches_requirements(vendor, request):
            continue
        if not vendor_in_coverage_area(vendor, property):
            continue
        if not vendor_is_available(vendor, request.urgency):
            continue
        if not vendor_is_compliant(vendor):
            continue
        eligible.append(vendor)
    
    # Step 2: Check property-specific preferences
    owner_preferred = get_owner_preferred_vendors(property, request.issue_category)
    if owner_preferred:
        # Boost owner-preferred vendors
        for vendor in eligible:
            if vendor.vendor_id in owner_preferred:
                vendor.score_boost = 50
    
    # Step 3: Score vendors
    scored = []
    for vendor in eligible:
        score = calculate_vendor_score(vendor, request, property)
        scored.append((vendor, score))
    
    # Step 4: Sort by score descending
    scored.sort(key=lambda x: x[1], reverse=True)
    
    return [v for v, s in scored[:3]]


def calculate_vendor_score(vendor: Vendor, request: MaintenanceRequest, property: Property) -> float:
    """
    Score a vendor based on multiple factors.
    Higher score = better fit.
    """
    score = 0.0
    
    # Performance weight: 40%
    score += vendor.performance.resident_satisfaction_avg * 10  # 0-50
    score += (1 - vendor.performance.avg_response_time_minutes / 120) * 20  # 0-20 (faster = better)
    score += vendor.performance.first_time_fix_rate * 20  # 0-20
    
    # Cost weight: 25%
    avg_cost = (vendor.financials.typical_job_cost_range.min + 
                vendor.financials.typical_job_cost_range.max) / 2
    market_avg = get_market_average_cost(request.issue_category)
    cost_ratio = avg_cost / market_avg
    score += max(0, (2 - cost_ratio)) * 12.5  # 0-25 (cheaper = better)
    
    # Familiarity weight: 20%
    jobs_at_property = count_jobs_at_property(vendor, property)
    score += min(jobs_at_property / 5, 1) * 20  # 0-20 (more familiar = better)
    
    # Availability weight: 15%
    if request.urgency == UrgencyLevel.EMERGENCY:
        if vendor.availability.emergency_available:
            score += 15
    else:
        response_likelihood = estimate_response_likelihood(vendor)
        score += response_likelihood * 15  # 0-15
    
    # Owner preference boost
    score += getattr(vendor, 'score_boost', 0)
    
    return score
```

3. **Vendor Communication Protocol**

```yaml
vendor_dispatch:
  initial_contact:
    method_priority: [sms, phone, email]
    
    sms_template: |
      [Maintenance Request]
      Property: {address}
      Unit: {unit}
      Issue: {category} - {description}
      Urgency: {urgency}
      Contact: {resident_name} {resident_phone}
      
      Reply YES to accept. Expected arrival: {requested_time}
    
    timeout_per_method:
      emergency: 5_minutes
      urgent: 15_minutes
      routine: 2_hours
  
  confirmation_parsing:
    accept_patterns: ["yes", "confirmed", "on my way", "accepted"]
    decline_patterns: ["no", "can't", "unavailable", "busy"]
    reschedule_patterns: ["can do X instead", "available at"]
  
  if_no_response:
    action: try_next_vendor
    max_attempts: 3
    escalate_after: all_vendors_exhausted
  
  if_declined:
    action: try_next_vendor
    record: vendor_decline_reason
```

4. **Vendor Portal Integration**

```yaml
vendor_portal_api:
  base_url: /api/v1/vendor-portal
  
  endpoints:
    GET /jobs:
      description: List assigned jobs
      filters: [status, date_range]
    
    GET /jobs/{job_id}:
      description: Get job details
      includes: [property_info, resident_contact, access_instructions]
    
    POST /jobs/{job_id}/accept:
      body: { eta: datetime }
    
    POST /jobs/{job_id}/decline:
      body: { reason: string }
    
    POST /jobs/{job_id}/en-route:
      body: { eta: datetime }
    
    POST /jobs/{job_id}/arrived:
      body: { timestamp: datetime }
    
    POST /jobs/{job_id}/complete:
      body:
        summary: string
        resolution: string
        photos: array[string]
        parts_used: array[{ name, cost }]
        labor_hours: number
        total_cost: number
        requires_follow_up: boolean
    
    POST /jobs/{job_id}/invoice:
      body:
        invoice_number: string
        line_items: array[{ description, amount }]
        total: number
        attachments: array[string]
```

---

### SECTION 7: Work Order Lifecycle & State Machine

Define the complete work order state machine:

1. **Work Order States**

```yaml
WorkOrderState:
  NEW:
    description: Request received, not yet processed
    allowed_transitions: [TRIAGING, CANCELLED]
    auto_transition_after: 30_seconds → TRIAGING
  
  TRIAGING:
    description: AI analyzing issue, checking history
    allowed_transitions: [TROUBLESHOOTING, AWAITING_DISPATCH, ESCALATED]
    timeout: 2_minutes → ESCALATED
  
  TROUBLESHOOTING:
    description: AI guiding resident through troubleshooting
    allowed_transitions: [RESOLVED, AWAITING_DISPATCH, ESCALATED]
    timeout: 10_minutes → AWAITING_DISPATCH
  
  AWAITING_DISPATCH:
    description: Ready to assign vendor
    allowed_transitions: [DISPATCHING, AWAITING_APPROVAL, ESCALATED]
  
  AWAITING_APPROVAL:
    description: Cost exceeds threshold, waiting for owner/manager approval
    allowed_transitions: [DISPATCHING, CANCELLED, ESCALATED]
    timeout: 24_hours → ESCALATED
  
  DISPATCHING:
    description: Contacting vendors for assignment
    allowed_transitions: [SCHEDULED, ESCALATED]
    timeout: 30_minutes → ESCALATED
  
  SCHEDULED:
    description: Vendor confirmed, appointment set
    allowed_transitions: [VENDOR_EN_ROUTE, RESCHEDULED, CANCELLED]
  
  VENDOR_EN_ROUTE:
    description: Vendor heading to property
    allowed_transitions: [IN_PROGRESS, NO_SHOW]
  
  IN_PROGRESS:
    description: Vendor on-site working
    allowed_transitions: [PENDING_VERIFICATION, NEEDS_PARTS, ESCALATED]
  
  NEEDS_PARTS:
    description: Vendor needs to return with parts
    allowed_transitions: [SCHEDULED]
  
  PENDING_VERIFICATION:
    description: Work done, awaiting confirmation
    allowed_transitions: [COMPLETED, REOPENED]
    timeout: 24_hours → COMPLETED (auto-close)
  
  COMPLETED:
    description: Issue resolved, work order closed
    allowed_transitions: [REOPENED]
  
  RESOLVED:
    description: Resolved via troubleshooting (no vendor)
    allowed_transitions: [REOPENED]
  
  REOPENED:
    description: Issue recurred or wasn't fixed
    allowed_transitions: [TRIAGING]
  
  ESCALATED:
    description: Requires human intervention
    allowed_transitions: [any_state]
  
  CANCELLED:
    description: Work order cancelled
    allowed_transitions: []  # Terminal
```

2. **State Machine Diagram**

```
                              ┌──────────────┐
                              │     NEW      │
                              └──────┬───────┘
                                     │
                              ┌──────▼───────┐
                              │   TRIAGING   │
                              └──────┬───────┘
                       ┌─────────────┼─────────────┐
                       │             │             │
               ┌───────▼───────┐     │     ┌───────▼───────┐
               │TROUBLESHOOTING│     │     │AWAITING_DISPATCH│
               └───────┬───────┘     │     └───────┬───────┘
                       │             │             │
               ┌───────▼───────┐     │     ┌───────▼───────┐
               │   RESOLVED    │     │     │AWAITING_APPROVAL│
               └───────────────┘     │     └───────┬───────┘
                                     │             │
                              ┌──────▼───────┐     │
                              │  ESCALATED   │◄────┘
                              └──────────────┘
                                     │
                                     │ (Human resolves)
                                     │
                              ┌──────▼───────┐
                              │ DISPATCHING  │
                              └──────┬───────┘
                                     │
                              ┌──────▼───────┐
                              │  SCHEDULED   │
                              └──────┬───────┘
                                     │
                              ┌──────▼───────┐
                              │VENDOR_EN_ROUTE│
                              └──────┬───────┘
                                     │
                              ┌──────▼───────┐
                              │ IN_PROGRESS  │
                              └──────┬───────┘
                       ┌─────────────┼─────────────┐
                       │             │             │
               ┌───────▼───────┐     │     ┌───────▼───────┐
               │  NEEDS_PARTS  │     │     │PEND_VERIFICATION│
               └───────────────┘     │     └───────┬───────┘
                                     │             │
                              ┌──────▼───────┐     │
                              │  COMPLETED   │◄────┘
                              └──────────────┘
```

3. **State Transition Events**

```yaml
state_events:
  on_enter:
    NEW:
      - log_request_received
      - send_acknowledgment_to_resident
      
    TRIAGING:
      - load_property_context
      - classify_issue
      - check_history
      
    TROUBLESHOOTING:
      - load_troubleshooting_entry
      - start_troubleshooting_session
      
    DISPATCHING:
      - select_vendors
      - start_dispatch_workflow
      
    SCHEDULED:
      - notify_resident_of_appointment
      - send_reminder_to_vendor
      - schedule_reminder_notifications
      
    COMPLETED:
      - send_completion_notification
      - request_feedback
      - trigger_invoice_workflow
      - update_vendor_metrics
      
    ESCALATED:
      - notify_on_call_staff
      - create_escalation_ticket
  
  on_exit:
    TROUBLESHOOTING:
      - save_troubleshooting_transcript
      - update_kb_metrics
```

---

### SECTION 8: Notification & Communication System

Design the comprehensive notification system:

1. **Notification Types & Templates**

```yaml
notifications:
  resident:
    request_received:
      channels: [sms, email, push]
      template: |
        Your maintenance request has been received.
        Reference: {wo_number}
        Issue: {issue_summary}
        We're working on it and will update you shortly.
    
    vendor_scheduled:
      channels: [sms, email, push]
      template: |
        Good news! A technician has been scheduled.
        Date: {date}
        Time Window: {time_window}
        Technician: {vendor_name}
        
        They will contact you before arrival.
    
    vendor_en_route:
      channels: [sms, push]
      template: |
        Heads up! {vendor_name} is on the way.
        ETA: {eta}
        Please ensure access to {unit}.
    
    work_completed:
      channels: [sms, email]
      template: |
        Your maintenance has been completed!
        Work Order: {wo_number}
        Resolution: {resolution_summary}
        
        Please confirm everything looks good by replying YES, 
        or let us know if you have concerns.
    
    feedback_request:
      channels: [email]
      template: |
        How did we do?
        Rate your recent maintenance experience: [link]
  
  staff:
    escalation_alert:
      channels: [slack, sms, email]
      priority: high
      template: |
        ⚠️ ESCALATION: {escalation_reason}
        Work Order: {wo_number}
        Property: {property_address}
        Resident: {resident_name} ({resident_phone})
        Issue: {issue_summary}
        
        Action Required: [link to dashboard]
    
    daily_summary:
      channels: [email, slack]
      schedule: 8am
      template: |
        📊 Daily Maintenance Summary
        
        New Requests: {new_count}
        Completed: {completed_count}
        In Progress: {in_progress_count}
        Escalations: {escalation_count}
        
        Avg Resolution Time: {avg_resolution}
  
  vendor:
    job_assignment:
      channels: [sms, email, portal_push]
      template: |
        [New Job Assignment]
        Property: {address}
        Issue: {issue_category} - {description}
        Urgency: {urgency}
        Resident: {resident_name}
        
        Reply YES to accept by {deadline}.
    
    reminder:
      channels: [sms]
      template: |
        Reminder: You have a job today.
        {address}, Unit {unit}
        Time: {scheduled_time}
        Issue: {issue_summary}
  
  owner:
    approval_request:
      channels: [email, portal_push]
      template: |
        Maintenance Approval Required
        
        Property: {property_address}
        Issue: {issue_summary}
        Estimated Cost: ${estimated_cost}
        Threshold: ${approval_threshold}
        
        Approve: [YES link]
        Deny: [NO link]
        More Info: [link]
    
    completion_report:
      channels: [email]
      template: |
        Maintenance Completed - {property_address}
        
        Issue: {issue_summary}
        Resolution: {resolution}
        Cost: ${total_cost}
        Vendor: {vendor_name}
        
        Photos: [attached or link]
        Invoice: [attached]
```

2. **Notification Delivery Engine**

```python
class NotificationEngine:
    async def send_notification(
        self,
        notification_type: str,
        recipient: Recipient,
        context: Dict,
        priority: Priority = Priority.NORMAL
    ) -> NotificationResult:
        """Send notification across configured channels."""
        
        template = self.get_template(notification_type)
        channels = self.get_channels_for_recipient(recipient, notification_type)
        
        results = []
        for channel in channels:
            # Respect quiet hours for non-emergency
            if not priority == Priority.EMERGENCY:
                if self.is_quiet_hours(recipient, channel):
                    continue
            
            # Render template for channel
            content = self.render_template(template, context, channel)
            
            # Send via appropriate provider
            result = await self.send_via_channel(channel, recipient, content)
            results.append(result)
        
        return NotificationResult(results)
```

3. **Communication Preferences Schema**

```yaml
CommunicationPreferences:
  resident_id: string
  
  channels:
    sms:
      enabled: boolean
      phone: string
    email:
      enabled: boolean
      address: string
    push:
      enabled: boolean
      device_tokens: array[string]
  
  quiet_hours:
    enabled: boolean
    start: time  # e.g., "22:00"
    end: time    # e.g., "08:00"
    timezone: string
    allow_emergency: boolean  # Ignore quiet hours for emergencies
  
  language: string  # e.g., "en", "es"
  
  notification_preferences:
    status_updates: boolean
    reminders: boolean
    marketing: boolean
```

---

### SECTION 9: Scheduling & Calendar Integration

Detail the scheduling system:

1. **Appointment Scheduling Model**

```yaml
Appointment:
  appointment_id: string
  work_order_id: string
  vendor_id: string
  property_id: string
  unit_id: string
  
  scheduled_window:
    date: date
    start_time: time
    end_time: time
    duration_estimate: minutes
  
  actual:
    arrived_at: datetime
    completed_at: datetime
    duration: minutes
  
  access_instructions:
    entry_method: enum [meet_resident, lockbox, key_on_file, smart_lock]
    lockbox_code: string (if applicable)
    special_instructions: string
  
  reminders:
    - type: vendor_1_day_before
      sent_at: datetime
    - type: resident_1_day_before
      sent_at: datetime
    - type: vendor_1_hour_before
      sent_at: datetime
  
  status: enum [confirmed, rescheduled, cancelled, completed, no_show]
```

2. **Scheduling Algorithm**

```python
async def schedule_appointment(
    work_order: WorkOrder,
    vendor: Vendor,
    resident_preferences: List[TimeSlot]
) -> Appointment:
    """
    Find optimal appointment time considering:
    - Vendor availability
    - Resident preferences
    - Property access constraints
    - Existing vendor schedule
    - Travel time between jobs
    """
    
    # Get vendor's available slots for next 7 days
    vendor_slots = await get_vendor_availability(vendor, days=7)
    
    # Filter by property access hours
    property_hours = get_property_access_hours(work_order.property_id)
    available_slots = filter_by_access_hours(vendor_slots, property_hours)
    
    # Consider travel time from previous jobs
    optimized_slots = optimize_for_routing(available_slots, vendor)
    
    # Match against resident preferences
    if resident_preferences:
        matched_slots = match_preferences(optimized_slots, resident_preferences)
        if matched_slots:
            selected = matched_slots[0]
        else:
            # Propose alternatives
            selected = await negotiate_time(optimized_slots[:3], resident)
    else:
        # Pick first available
        selected = optimized_slots[0]
    
    # Create appointment
    appointment = Appointment(
        work_order_id=work_order.id,
        vendor_id=vendor.id,
        scheduled_window=selected,
        access_instructions=get_access_instructions(work_order.property_id)
    )
    
    # Schedule reminders
    schedule_reminders(appointment)
    
    return appointment
```

3. **Rescheduling Protocol**

```yaml
rescheduling:
  resident_initiated:
    allowed_until: 2_hours_before
    max_reschedules: 2
    process:
      1: present_alternative_slots
      2: confirm_new_time
      3: notify_vendor
      4: update_appointment
  
  vendor_initiated:
    allowed: always (with reason)
    must_provide: alternative_times
    process:
      1: record_reason
      2: if_urgent: find_backup_vendor
      3: else: present_alternatives_to_resident
      4: notify_all_parties
  
  ai_initiated:
    triggers:
      - vendor_double_booked
      - emergency_preemption
    process:
      1: assess_priority
      2: find_optimal_resolution
      3: communicate_changes
```

---

### SECTION 10: Approval Workflow & Cost Management

Design the approval system for cost controls:

1. **Approval Configuration Schema**

```yaml
ApprovalPolicy:
  policy_id: string
  property_id: string (or "global")
  
  thresholds:
    auto_approve_below: 250.00
    require_manager_approval: 250.00 - 1000.00
    require_owner_approval: 1000.00+
  
  emergency_override:
    enabled: true
    max_amount: 500.00
    notification: immediate_to_owner
  
  category_exceptions:
    hvac:
      auto_approve_below: 500.00  # Higher threshold for HVAC
    appliance_replacement:
      always_require_approval: true
  
  approval_hierarchy:
    level_1: property_manager
    level_2: regional_manager
    level_3: owner
  
  timeout:
    initial_request: 4_hours
    escalation_interval: 2_hours
    auto_approve_after: 24_hours (if under emergency threshold)
```

2. **Approval Workflow State Machine**

```yaml
ApprovalStates:
  PENDING:
    description: Awaiting approver action
    actions: [approve, deny, request_more_info]
    timeout: 4_hours → ESCALATED
  
  APPROVED:
    description: Approved to proceed
    next: resume_dispatch
  
  DENIED:
    description: Repair not approved
    next: notify_resident_and_close
  
  ESCALATED:
    description: Escalated to higher authority
    actions: [approve, deny, override_approve]
  
  MORE_INFO_REQUESTED:
    description: Approver needs more details
    next: vendor_provides_info → PENDING
```

3. **Cost Estimation Engine**

```python
def estimate_repair_cost(
    issue_category: str,
    issue_details: str,
    property: Property,
    vendor: Vendor
) -> CostEstimate:
    """
    Estimate repair cost based on historical data and vendor rates.
    """
    
    # Get historical costs for similar issues
    historical = get_historical_costs(
        property_id=property.id,
        category=issue_category,
        lookback_days=365
    )
    
    # Get vendor's typical rates
    vendor_avg = vendor.financials.typical_job_cost_range
    
    # Get market average for issue type
    market_avg = get_market_average(issue_category, property.zip_code)
    
    # Calculate estimate
    estimate = CostEstimate(
        low=max(historical.p25, vendor_avg.min, market_avg * 0.7),
        mid=median(historical.p50, (vendor_avg.min + vendor_avg.max) / 2, market_avg),
        high=min(historical.p75, vendor_avg.max, market_avg * 1.5),
        confidence=calculate_confidence(len(historical.samples))
    )
    
    return estimate
```

4. **Invoice Processing Flow**

```yaml
invoice_processing:
  receipt:
    from: [vendor_portal, email_attachment, manual_upload]
    required_fields:
      - vendor_name
      - invoice_number
      - work_order_reference
      - line_items
      - total_amount
  
  validation:
    checks:
      - invoice_matches_work_order
      - amount_within_estimate (tolerance: 20%)
      - vendor_matches_assigned
      - work_date_matches_completion
    
    if_discrepancy:
      minor: flag_for_review
      major: hold_payment_and_escalate
  
  approval:
    auto_approve_if:
      - within_estimate
      - all_validations_pass
      - under_auto_approve_threshold
    
    require_review_if:
      - over_estimate_by_20%
      - validation_warnings
      - vendor_requested_change_order
  
  posting:
    ledger_entry:
      debit: maintenance_expense (category-specific GL code)
      credit: accounts_payable
    
    owner_billing:
      if: expense_passed_to_owner
      include_in: monthly_owner_statement
```

---

### SECTION 11: Property & Unit Context System

Define the property context that informs AI decisions:

1. **Property Profile Schema**

```yaml
PropertyProfile:
  property_id: string
  
  address:
    street: string
    city: string
    state: string
    zip: string
    coordinates: { lat, lng }
  
  type: enum [single_family, multi_family, condo, townhouse]
  units: array[UnitProfile]
  
  access:
    office_hours: TimeRange
    after_hours_contact: ContactInfo
    gate_code: string
    key_storage: enum [lockbox, office, smart_lock]
    lockbox_code: string
  
  systems:
    hvac_type: string
    water_heater_type: string
    electrical_panel_location: string
    shutoff_locations:
      water_main: string
      gas_main: string
      electrical_main: string
  
  vendors:
    preferred:
      plumbing: [vendor_ids]
      electrical: [vendor_ids]
      hvac: [vendor_ids]
    blacklisted: [vendor_ids]
  
  owner:
    owner_id: string
    preferences:
      notification_frequency: enum [immediate, daily_summary, weekly]
      approval_threshold: number
      require_photos: boolean
      require_estimates_over: number
  
  maintenance_history:
    avg_requests_per_month: number
    common_issues: array[{ category, frequency }]
    total_spend_ytd: number
    recent_major_repairs: array[WorkOrderSummary]
```

2. **Unit Profile Schema**

```yaml
UnitProfile:
  unit_id: string
  property_id: string
  unit_number: string
  
  details:
    bedrooms: number
    bathrooms: number
    square_feet: number
    floor: number
  
  resident:
    resident_id: string
    lease_start: date
    lease_end: date
    move_in_date: date
    contact: ContactInfo
    communication_preference: enum [text, email, phone, portal]
    language: string
  
  appliances:
    - type: "refrigerator"
      brand: "Samsung"
      model: "RF28R7551SR"
      serial: "XXX"
      install_date: date
      warranty_expiry: date
    - type: "dishwasher"
      ...
  
  systems:
    hvac_filter_size: string
    last_hvac_service: date
    smoke_detector_last_checked: date
  
  access:
    smart_lock_installed: boolean
    lockbox_code: string
    pet_on_premises: { has_pet: boolean, type: string, notes: string }
    alarm_code: string
  
  maintenance_history:
    recent_work_orders: array[WorkOrderSummary]
    recurring_issues: array[RecurringIssue]
    notes: string
```

3. **Context Loading Strategy**

```python
async def load_maintenance_context(
    work_order: WorkOrder
) -> MaintenanceContext:
    """
    Load all relevant context for handling a maintenance request.
    Uses progressive disclosure - load more as needed.
    """
    
    # Always load (Tier 1)
    property = await load_property_profile(work_order.property_id)
    unit = await load_unit_profile(work_order.unit_id)
    resident = await load_resident_profile(work_order.resident_id)
    
    context = MaintenanceContext(
        property=property,
        unit=unit,
        resident=resident
    )
    
    # Conditional load (Tier 2)
    
    # If issue matches recent history
    recent_similar = await find_similar_recent_issues(
        unit.unit_id, 
        work_order.issue_category,
        days=90
    )
    if recent_similar:
        context.related_history = recent_similar
        context.is_potential_recurring = len(recent_similar) >= 2
    
    # If appliance-related
    if work_order.issue_category in ["appliance", "hvac"]:
        context.appliance_details = find_relevant_appliance(
            unit.appliances, 
            work_order.issue_description
        )
        if context.appliance_details:
            context.warranty_status = check_warranty(context.appliance_details)
    
    # Owner preferences for approvals
    if might_need_approval(work_order):
        context.owner_preferences = property.owner.preferences
        context.approval_threshold = property.owner.preferences.approval_threshold
    
    return context
```

---

### SECTION 12: Escalation & Human-in-the-Loop

Design the escalation system:

1. **Escalation Triggers**

```yaml
escalation_triggers:
  automatic:
    emergency_detected:
      keywords: [fire, flood, gas_leak, sewage, no_heat_winter, sparking]
      action: immediate_escalation
      notify: [on_call_manager, emergency_services_if_needed]
    
    vendor_unavailable:
      condition: all_preferred_vendors_declined
      timeout: 30_minutes
      action: escalate_to_manager
    
    resident_frustrated:
      detection: sentiment_analysis (anger > 0.7)
      or: explicit_human_request
      action: offer_human_callback
    
    ai_uncertainty:
      condition: confidence < 0.6 on classification
      action: flag_for_human_review
    
    cost_overrun:
      condition: actual_cost > approved_amount * 1.2
      action: pause_and_escalate
    
    sla_breach:
      condition: time_in_state > state_timeout
      action: escalate_to_next_level
  
  manual:
    resident_requests_human: true
    staff_overrides_ai: true
```

2. **Escalation Response Protocols**

```yaml
escalation_protocols:
  level_1_property_manager:
    contact_methods: [slack_dm, sms, email]
    response_sla: 15_minutes
    authority:
      - override_vendor_selection
      - approve_up_to: 500
      - extend_deadlines
      - close_work_orders
    
    if_no_response:
      after: 15_minutes
      escalate_to: level_2
  
  level_2_regional_manager:
    contact_methods: [phone, slack_dm, sms]
    response_sla: 30_minutes
    authority:
      - all_level_1_plus
      - approve_up_to: 2000
      - authorize_emergency_contractors
      - override_owner_preferences
    
    if_no_response:
      after: 30_minutes
      escalate_to: level_3
  
  level_3_on_call_emergency:
    contact_methods: [phone (call until answer)]
    response_sla: 5_minutes
    authority:
      - unlimited_spend_for_safety
      - contact_emergency_services
      - relocate_residents_if_needed
```

3. **Human Handoff Protocol**

```yaml
human_handoff:
  context_transfer:
    include:
      - full_conversation_transcript
      - work_order_details
      - property_and_unit_context
      - troubleshooting_steps_attempted
      - ai_classification_and_confidence
      - recommended_actions
    
    format: structured_summary_plus_full_log
  
  handoff_message_to_resident:
    template: |
      I'm connecting you with {agent_name}, one of our maintenance specialists.
      They'll be with you in just a moment and have all the details 
      about your {issue_summary}.
  
  handoff_briefing_to_human:
    template: |
      INCOMING: {resident_name} from {property_name}
      
      ISSUE: {issue_category} - {issue_summary}
      URGENCY: {urgency}
      
      AI ATTEMPTED:
      - Classification: {classification} (confidence: {confidence})
      - Troubleshooting: {troubleshooting_summary}
      
      RECOMMENDED ACTION: {recommendation}
      
      CONTEXT:
      - Recent similar issues: {related_issues}
      - Resident sentiment: {sentiment}
      
      [View Full Transcript]
```

4. **HITL Dashboard Requirements**

Define the dashboard for human operators:

```yaml
hitl_dashboard:
  views:
    escalation_queue:
      columns:
        - urgency_icon
        - work_order_number
        - property_address
        - issue_summary
        - time_in_queue
        - escalation_reason
        - assigned_to
      
      filters:
        - urgency
        - property
        - escalation_type
        - time_range
      
      actions:
        - claim_work_order
        - reassign
        - resolve
        - add_note
    
    work_order_detail:
      sections:
        - header: work_order_info
        - property_context: address, access, owner
        - resident_info: name, contact, preferences
        - conversation_transcript: full_ai_resident_exchange
        - troubleshooting_log: steps_attempted_and_outcomes
        - vendor_info: assigned, status, eta
        - action_buttons: [approve, override, dispatch, close, escalate]
    
    real_time_feed:
      shows: all_ai_actions_in_progress
      allows: intervention_at_any_point
```

---

### SECTION 13: Metrics, Analytics & Reporting

Define the comprehensive metrics system:

1. **Key Performance Indicators**

```yaml
kpis:
  operational:
    first_response_time:
      description: Time from request to AI acknowledgment
      target: <30_seconds
      measurement: avg, p50, p95
    
    troubleshooting_resolution_rate:
      description: % of issues resolved without vendor dispatch
      target: 20-35%
      breakdown: by_issue_category
    
    time_to_dispatch:
      description: Time from request to vendor confirmation
      target: <30_minutes (urgent), <4_hours (routine)
      measurement: avg, p50, p95
    
    time_to_completion:
      description: Time from request to work order closure
      target: <24_hours (urgent), <3_days (routine)
      measurement: avg, p50, p95
    
    first_time_fix_rate:
      description: % resolved in single vendor visit
      target: >85%
      breakdown: by_vendor, by_category
    
    ai_handling_rate:
      description: % of requests handled without human intervention
      target: >80%
      breakdown: by_stage (intake, triage, dispatch, completion)
  
  quality:
    resident_satisfaction:
      description: Post-completion survey score
      target: >4.5/5
      breakdown: by_property, by_category
    
    vendor_performance:
      description: Composite score (response, quality, cost)
      target: >4.0/5
      breakdown: by_vendor
    
    escalation_rate:
      description: % of requests requiring human intervention
      target: <15%
      breakdown: by_escalation_reason
    
    reopen_rate:
      description: % of work orders reopened within 30 days
      target: <5%
      breakdown: by_vendor, by_category
  
  financial:
    cost_per_work_order:
      description: Average total cost per completed work order
      target: decrease_5%_yoy
      breakdown: by_category, by_property
    
    cost_per_door:
      description: Monthly maintenance cost per managed unit
      target: <$50/door
      breakdown: by_portfolio
    
    invoice_accuracy:
      description: % of invoices matching estimates
      target: >90%_within_20%
```

2. **Analytics Queries**

```sql
-- Work Order Volume by Status
SELECT 
    status,
    COUNT(*) as count,
    AVG(EXTRACT(EPOCH FROM (completed_at - created_at))/3600) as avg_hours
FROM work_orders
WHERE created_at >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY status;

-- Troubleshooting Effectiveness
SELECT 
    issue_category,
    COUNT(*) as total_attempts,
    SUM(CASE WHEN outcome = 'RESOLVED' THEN 1 ELSE 0 END) as resolved,
    ROUND(100.0 * SUM(CASE WHEN outcome = 'RESOLVED' THEN 1 ELSE 0 END) / COUNT(*), 1) as resolution_rate
FROM troubleshooting_sessions
WHERE created_at >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY issue_category
ORDER BY resolution_rate DESC;

-- Vendor Leaderboard
SELECT 
    v.company_name,
    COUNT(wo.id) as jobs_completed,
    AVG(wo.resident_rating) as avg_rating,
    AVG(EXTRACT(EPOCH FROM (wo.vendor_arrived_at - wo.dispatched_at))/60) as avg_response_mins,
    SUM(wo.total_cost) as total_revenue
FROM vendors v
JOIN work_orders wo ON wo.vendor_id = v.id
WHERE wo.status = 'COMPLETED'
    AND wo.completed_at >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY v.id, v.company_name
ORDER BY avg_rating DESC;

-- Cost Analysis by Category
SELECT 
    issue_category,
    COUNT(*) as work_orders,
    AVG(total_cost) as avg_cost,
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY total_cost) as median_cost,
    MAX(total_cost) as max_cost,
    SUM(total_cost) as total_spend
FROM work_orders
WHERE status = 'COMPLETED'
    AND created_at >= CURRENT_DATE - INTERVAL '90 days'
GROUP BY issue_category
ORDER BY total_spend DESC;
```

3. **Reporting Templates**

```yaml
reports:
  daily_operations:
    frequency: daily
    recipients: [property_managers]
    sections:
      - new_requests_summary
      - in_progress_status
      - completed_yesterday
      - escalations
      - vendor_availability
  
  weekly_performance:
    frequency: weekly (Monday)
    recipients: [regional_managers]
    sections:
      - kpi_dashboard
      - trend_analysis
      - vendor_scorecard
      - top_issues_by_property
      - cost_summary
  
  monthly_owner_report:
    frequency: monthly
    recipients: [property_owners]
    sections:
      - maintenance_summary
      - cost_breakdown
      - completed_work_orders_detail
      - upcoming_recommended_maintenance
      - year_to_date_comparison
  
  quarterly_portfolio_review:
    frequency: quarterly
    recipients: [executives]
    sections:
      - portfolio_health_score
      - cost_benchmarking
      - ai_performance_analysis
      - vendor_optimization_opportunities
      - predictive_maintenance_recommendations
```

---

### SECTION 14: Integration Specifications

Detail all external system integrations:

1. **PMS Integration (AppFolio)**

```yaml
appfolio_integration:
  type: REST API + Webhooks
  
  authentication:
    method: OAuth 2.0
    token_refresh: automatic
    scopes: [properties, units, residents, work_orders, vendors]
  
  inbound_webhooks:
    new_maintenance_request:
      trigger: resident_submits_portal_request
      payload:
        property_id: string
        unit_id: string
        resident_id: string
        description: string
        attachments: array[url]
    
    resident_message:
      trigger: resident_sends_message
      payload:
        thread_id: string
        content: string
  
  outbound_api_calls:
    create_work_order:
      method: POST /api/v1/work-orders
      body:
        property_id: string
        unit_id: string
        description: string
        category: string
        priority: string
        assigned_vendor_id: string
    
    update_work_order:
      method: PATCH /api/v1/work-orders/{id}
      body: partial_work_order
    
    get_property:
      method: GET /api/v1/properties/{id}
      returns: property_profile
    
    get_unit:
      method: GET /api/v1/units/{id}
      returns: unit_profile
    
    get_residents:
      method: GET /api/v1/units/{id}/residents
      returns: array[resident]
    
    get_vendors:
      method: GET /api/v1/vendors
      filters: [trade, status]
      returns: array[vendor]
  
  sync_strategy:
    properties: daily_full_sync + webhook_updates
    units: daily_full_sync + webhook_updates
    residents: daily_full_sync + webhook_updates
    work_orders: bidirectional_real_time
```

2. **Telephony Integration (Twilio)**

```yaml
twilio_integration:
  services:
    voice:
      capability: inbound_calls
      features:
        - speech_to_text (real-time streaming)
        - text_to_speech
        - call_recording (optional)
        - conference
        - transfer
      
      webhook_endpoints:
        incoming_call: /webhooks/twilio/voice/incoming
        status_callback: /webhooks/twilio/voice/status
      
      twiml_handlers:
        gather: speech_input
        say: ai_response
        dial: transfer_to_human
    
    messaging:
      capability: sms_inbound_outbound
      features:
        - two_way_sms
        - mms (photos)
      
      webhook_endpoints:
        incoming_sms: /webhooks/twilio/sms/incoming
        status_callback: /webhooks/twilio/sms/status
  
  phone_numbers:
    strategy: dedicated_per_property
    format: local_area_code_preferred
```

3. **Treasury/Payment Integration**

```yaml
treasury_integration:
  via: mcp-treasury-server
  
  operations:
    check_vendor_payment_history:
      description: Check if vendor was paid recently (warranty check)
      input: { vendor_id, property_id, days_lookback }
      output: { last_payment_date, amount, category }
    
    create_payable:
      description: Create accounts payable entry for vendor invoice
      input:
        vendor_id: string
        invoice_id: string
        amount: number
        category: string
        gl_code: string
        property_id: string
        work_order_id: string
      output: { payable_id, status }
    
    post_owner_charge:
      description: Post maintenance charge to owner statement
      input:
        owner_id: string
        property_id: string
        work_order_id: string
        amount: number
        description: string
      output: { transaction_id }
  
  ledger_codes:
    maintenance_expense: "5100"
    hvac_repairs: "5110"
    plumbing_repairs: "5120"
    electrical_repairs: "5130"
    appliance_repairs: "5140"
    general_repairs: "5150"
```

---

### SECTION 15: Security & Compliance

Define security requirements:

1. **Data Classification**

```yaml
data_classification:
  pii_fields:
    high_sensitivity:
      - resident_ssn (never stored)
      - resident_full_dob
      - financial_account_numbers
    
    medium_sensitivity:
      - resident_phone
      - resident_email
      - unit_address
      - access_codes
    
    low_sensitivity:
      - property_name
      - issue_category
      - vendor_company_name
```

2. **Access Control**

```yaml
rbac:
  roles:
    resident:
      can:
        - create_own_maintenance_request
        - view_own_work_orders
        - respond_to_messages
        - provide_feedback
    
    property_manager:
      can:
        - view_all_property_work_orders
        - override_ai_decisions
        - manage_vendors
        - approve_costs_up_to: 500
        - close_work_orders
    
    regional_manager:
      can:
        - all_property_manager_permissions
        - view_multiple_properties
        - approve_costs_up_to: 2000
        - manage_staff
    
    owner:
      can:
        - view_own_property_work_orders
        - approve_costs
        - set_preferences
        - view_reports
    
    vendor:
      can:
        - view_assigned_jobs
        - accept_decline_jobs
        - update_job_status
        - submit_invoices
    
    ai_agent:
      can:
        - create_work_orders
        - update_work_orders
        - dispatch_vendors
        - send_notifications
      cannot:
        - approve_costs_over_threshold
        - delete_records
        - access_financial_data_directly
```

3. **Compliance Requirements**

```yaml
compliance:
  data_retention:
    work_orders: 7_years
    communication_logs: 3_years
    call_recordings: 1_year (or as required)
    access_codes: rotate_on_turnover
  
  audit_logging:
    log_all:
      - ai_decisions
      - human_overrides
      - cost_approvals
      - data_access
      - vendor_dispatches
    
    retention: 7_years
    immutable: true
  
  privacy:
    resident_consent:
      required_for: call_recording
      method: verbal_at_call_start
    
    data_minimization:
      principle: collect_only_needed
      review: quarterly
  
  encryption:
    at_rest: AES-256
    in_transit: TLS_1.3
    access_codes: additional_encryption_layer
```

---

### SECTION 16: Error Handling & Resilience

Define error handling strategies:

1. **Error Taxonomy**

```yaml
error_types:
  transient:
    - network_timeout
    - service_temporarily_unavailable
    - rate_limited
    retry_strategy: exponential_backoff (max 3 attempts)
  
  recoverable:
    - vendor_api_error
    - pms_sync_failed
    - notification_failed
    strategy: queue_for_retry + alert_if_persistent
  
  unrecoverable:
    - invalid_data
    - permission_denied
    - resource_not_found
    strategy: log + alert + graceful_degradation
  
  critical:
    - database_unavailable
    - core_service_down
    strategy: circuit_breaker + failover + immediate_alert
```

2. **Circuit Breaker Configuration**

```yaml
circuit_breakers:
  pms_integration:
    failure_threshold: 5
    reset_timeout: 60_seconds
    half_open_requests: 3
    fallback: queue_requests_locally
  
  telephony:
    failure_threshold: 3
    reset_timeout: 30_seconds
    fallback: route_to_backup_number
  
  vendor_portal:
    failure_threshold: 5
    reset_timeout: 120_seconds
    fallback: email_notifications_only
```

3. **Graceful Degradation**

```yaml
degradation_modes:
  full_ai_unavailable:
    behavior:
      - route_all_calls_to_human
      - email_notification_to_staff
      - portal_requests_queued
    
    recovery:
      - automatic_on_ai_health_check_pass
  
  pms_unavailable:
    behavior:
      - continue_intake_in_local_db
      - sync_when_available
      - notify_staff_of_sync_gap
  
  telephony_unavailable:
    behavior:
      - voicemail_fallback
      - sms_only_mode
      - email_notification_to_resident
```

---

### SECTION 17: Testing Strategy

Define comprehensive testing:

1. **Test Categories**

```yaml
testing:
  unit_tests:
    coverage_target: 85%
    focus_areas:
      - triage_classification
      - urgency_determination
      - vendor_selection_algorithm
      - cost_estimation
      - state_machine_transitions
  
  integration_tests:
    focus_areas:
      - pms_sync
      - telephony_flow
      - vendor_dispatch_flow
      - notification_delivery
      - workflow_orchestration
  
  e2e_tests:
    scenarios:
      - routine_request_happy_path
      - emergency_escalation
      - troubleshooting_resolution
      - vendor_decline_retry
      - approval_workflow
      - rescheduling_flow
  
  ai_evaluation:
    intent_recognition:
      test_set_size: 500_samples
      accuracy_target: 95%
      precision_target: 90%
      recall_target: 92%
    
    triage_classification:
      test_set_size: 300_samples
      accuracy_target: 90%
    
    troubleshooting_effectiveness:
      simulate: 100_scenarios_per_category
      measure: resolution_rate
  
  performance_tests:
    load:
      concurrent_requests: 100
      duration: 30_minutes
      target_p95_latency: 500ms
    
    stress:
      ramp_up_to: 500_concurrent
      find_breaking_point: true
    
    voice_latency:
      target: <200ms_response_start
```

2. **Test Data Generation**

```yaml
test_data:
  synthetic_properties:
    count: 100
    types: [single_family, multi_family, condo]
    
  synthetic_residents:
    count: 500
    distribution: normal_across_properties
    
  synthetic_work_orders:
    count: 10000
    distribution:
      by_category: historical_proportions
      by_urgency: [routine: 80%, urgent: 15%, emergency: 5%]
    
  synthetic_vendors:
    count: 50
    by_type: [plumber: 10, electrician: 10, hvac: 8, handyman: 15, other: 7]
```

---

### SECTION 18: Deployment & Infrastructure

Define infrastructure requirements:

1. **Service Deployment**

```yaml
deployment:
  environment:
    production:
      region: us-east-1 (primary), us-west-2 (dr)
      kubernetes_cluster: eks
    
    staging:
      region: us-east-1
      kubernetes_cluster: eks-staging
  
  services:
    intake-service:
      replicas: 3
      resources:
        cpu: 500m
        memory: 512Mi
      autoscaling:
        min: 2
        max: 10
        metric: cpu_utilization
        target: 70%
    
    brain-service:
      replicas: 3
      resources:
        cpu: 1000m
        memory: 2Gi
      gpu: optional_for_embeddings
      autoscaling:
        min: 2
        max: 8
        metric: custom (queue_depth)
    
    workflow-workers:
      replicas: 5
      resources:
        cpu: 500m
        memory: 1Gi
      autoscaling:
        min: 3
        max: 20
        metric: pending_workflows
```

2. **Database Configuration**

```yaml
databases:
  mongodb:
    cluster_type: Atlas M30 (production)
    replication: 3-node replica set
    collections:
      - work_orders (indexed: property_id, status, created_at)
      - properties (indexed: property_id)
      - units (indexed: property_id, unit_id)
      - vendors (indexed: vendor_id, service_types)
      - communications (indexed: work_order_id, timestamp)
      - troubleshooting_kb (vector index on embeddings)
  
  redis:
    cluster: 3-node (primary + 2 replicas)
    purpose:
      - session_state
      - conversation_cache
      - rate_limiting
      - real_time_metrics
  
  timescaledb:
    purpose: time-series metrics
    retention: 90_days_hot, 2_years_cold
```

3. **Monitoring & Observability**

```yaml
observability:
  metrics:
    provider: Prometheus + Grafana
    custom_metrics:
      - maintenance_requests_total
      - troubleshooting_resolutions_total
      - vendor_dispatch_latency_seconds
      - ai_confidence_scores
      - escalation_count
  
  logging:
    provider: ELK Stack
    log_levels:
      production: INFO
      staging: DEBUG
    structured_logging: true
  
  tracing:
    provider: Jaeger
    sampling: 10%_production, 100%_staging
  
  alerting:
    channels: [pagerduty, slack]
    alerts:
      - name: high_escalation_rate
        condition: escalation_rate > 20%
        severity: warning
      
      - name: service_degradation
        condition: p95_latency > 2s
        severity: critical
      
      - name: ai_accuracy_drop
        condition: intent_accuracy < 90%
        severity: warning
```

---

### SECTION 19: Implementation Roadmap

Define phased implementation:

1. **Phase 1: Foundation (Weeks 1-6)**

```yaml
phase_1:
  duration: 6_weeks
  objectives:
    - Core data models implemented
    - PMS integration (read-only)
    - Basic intake (portal only)
    - Work order state machine
    - Simple triage (rule-based)
  
  deliverables:
    - MongoDB schemas deployed
    - AppFolio webhook integration
    - Work order API
    - Basic dashboard for staff
  
  team: 2_backend, 1_frontend, 0.5_devops
```

2. **Phase 2: AI Brain (Weeks 7-12)**

```yaml
phase_2:
  duration: 6_weeks
  objectives:
    - AI-powered triage
    - Troubleshooting engine
    - Vendor selection algorithm
    - Multi-channel intake (add SMS, email)
  
  deliverables:
    - LangGraph integration
    - Troubleshooting KB populated
    - Intent classification model
    - SMS/email intake handlers
  
  team: 2_backend, 1_ml_engineer, 1_frontend
```

3. **Phase 3: Voice & Dispatch (Weeks 13-18)**

```yaml
phase_3:
  duration: 6_weeks
  objectives:
    - Voice agent integration
    - Automated vendor dispatch
    - Scheduling system
    - Notification engine
  
  deliverables:
    - Twilio voice integration
    - Vendor portal API
    - Calendar integration
    - Multi-channel notifications
  
  team: 2_backend, 1_frontend, 0.5_devops
```

4. **Phase 4: Polish & Scale (Weeks 19-24)**

```yaml
phase_4:
  duration: 6_weeks
  objectives:
    - HITL dashboard
    - Analytics & reporting
    - Performance optimization
    - Security hardening
    - Beta testing
  
  deliverables:
    - Full HITL dashboard
    - Report generation
    - Load tested to 100 concurrent
    - Security audit complete
    - 10 beta properties live
  
  team: 1_backend, 2_frontend, 1_devops, 1_qa
```

---

### SECTION 20: Appendices

Include additional reference material:

1. **API Reference Summary**
2. **Database Schema DDL**
3. **Message Queue Topics**
4. **Environment Variables**
5. **Glossary of Terms**
6. **Troubleshooting KB Sample Entries**
7. **Notification Template Library**
8. **Vendor Communication Scripts**

---

## ✅ OUTPUT REQUIREMENTS

Your engineering specification must:

1. **Be comprehensive** - Cover ALL 20 sections in detail
2. **Be specific** - Include actual schemas, code samples, configurations
3. **Be actionable** - A developer should be able to implement from this spec
4. **Reference the research** - Build on the Stage 1 findings
5. **Include diagrams** - State machines, architecture, flows
6. **Define interfaces** - API contracts, event schemas
7. **Specify non-functionals** - Performance, security, compliance

**Target length**: 6,000-10,000+ lines

---

## 📤 DELIVERY

1. Save your output to: `knowledge/operations/ES-AF-002-ai-maintenance-coordinator.md`
2. Update `STATUS.md` to mark Stage 3 complete for GAP-AF-002
3. Update `docs/PIPELINE_TRACKER.md` with completion details
4. Commit and push:

```bash
git add -A
git commit -m "Stage 3 COMPLETE: GAP-AF-002 AI Maintenance Coordinator Engineering Spec"
git push
```

---

**Good luck, Engineer! This is a critical MVP skill. The research foundation is exceptional (9.5/10) - build on it!**

