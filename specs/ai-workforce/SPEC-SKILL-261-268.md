# Skill Specification: AI Workforce Architecture

> **Skill IDs**: SKILL-261 through SKILL-268
> **Gap ID**: GAP-HOAI-001
> **Source**: HOAi / Vantaca
> **Created**: January 5, 2026
> **Status**: ✅ Specified
> **Engineering Spec**: ES-HOAI-001 (11,398 lines, 9.2/10 quality)

---

## 📊 SPECIFICATION SUMMARY

| Metric | Value |
|--------|-------|
| Total Skills | 8 |
| MVP Priority | P0 (All) |
| Category | `ai-workforce` |
| Tools Required | 12 |
| User Stories | 32 |
| Estimated Effort | XL (16-20 weeks) |

---

## 🎯 SKILLS OVERVIEW

| Skill ID | Name | Category | Priority | Effort |
|----------|------|----------|----------|--------|
| SKILL-261 | Multi-Channel Voice Agent | `ai-workforce` | P0 | L |
| SKILL-262 | AI AP Agent | `ai-workforce` | P0 | L |
| SKILL-263 | AI Budget Agent | `ai-workforce` | P0 | M |
| SKILL-264 | AI Research Agent | `ai-workforce` | P0 | M |
| SKILL-265 | Managerial Hub (HITL) | `ai-workflow` | P0 | XL |
| SKILL-266 | AI Scenario Modeling | `ai-workflow` | P0 | M |
| SKILL-267 | AI Outbound Calling | `ai-workforce` | P0 | M |
| SKILL-268 | Configurable AI Coverage | `ai-workflow` | P0 | L |

---

# SKILL-261: Multi-Channel Voice Agent

## Definition

```yaml
skill_id: SKILL-261
name: Multi-Channel Voice Agent
category: ai-workforce
priority: P0
source: HOAi
competitors: [HOAi, Boom AI]
```

## Description

An AI-powered voice agent capable of handling inbound calls across phone, SMS, chat, and email channels. The agent can authenticate residents, understand intent, retrieve data, execute actions, and escalate to humans when needed. Designed for 24/7 availability with <3 second response times.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 261-RQ-001 | Answer inbound calls within 3 seconds | Must-Have | Call answered < 3s measured |
| 261-RQ-002 | Authenticate callers via phone lookup, security questions, or account number | Must-Have | 3 auth methods available |
| 261-RQ-003 | Detect caller intent through natural language | Must-Have | Intent classified with >80% confidence |
| 261-RQ-004 | Process payment inquiries and payment requests | Must-Have | Integration with payment system |
| 261-RQ-005 | Create maintenance requests from voice | Must-Have | Task created in system |
| 261-RQ-006 | Generate and deliver documents on request | Should-Have | PDF generation + delivery |
| 261-RQ-007 | Search knowledge base for general questions | Must-Have | RAG retrieval functional |
| 261-RQ-008 | Escalate to human when confidence < threshold | Must-Have | Warm transfer capability |
| 261-RQ-009 | Support multi-language (English primary) | Should-Have | English fluent, Spanish basic |
| 261-RQ-010 | Log all calls with transcripts | Must-Have | Full audit trail |

## Data Model

```typescript
interface VoiceCall {
  call_id: string;
  channel: 'phone' | 'sms' | 'chat' | 'email';
  caller_phone: string;
  caller_id?: string;  // Resolved resident ID
  started_at: Date;
  ended_at?: Date;
  duration_seconds?: number;
  
  authentication: {
    method: 'phone_lookup' | 'security_questions' | 'account_number';
    status: 'pending' | 'authenticated' | 'failed';
    attempts: number;
  };
  
  intent: {
    detected: string;
    confidence: number;
    classification: 'payment_inquiry' | 'make_payment' | 'maintenance' | 
                   'document_request' | 'general_question' | 'speak_to_human' | 'unknown';
  };
  
  actions_taken: Array<{
    action: string;
    timestamp: Date;
    result: 'success' | 'failure';
    details: object;
  }>;
  
  escalation?: {
    reason: string;
    transferred_to: string;
    transfer_time: Date;
  };
  
  transcript: Array<{
    speaker: 'agent' | 'caller';
    text: string;
    timestamp: Date;
  }>;
  
  metadata: {
    agent_id: string;
    recording_url?: string;
    sentiment_score?: number;
  };
}
```

## API Specification

### Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/voice/calls` | Initiate call handling |
| GET | `/api/v1/voice/calls/{id}` | Get call details |
| POST | `/api/v1/voice/calls/{id}/authenticate` | Authenticate caller |
| POST | `/api/v1/voice/calls/{id}/action` | Execute action |
| POST | `/api/v1/voice/calls/{id}/escalate` | Escalate to human |
| GET | `/api/v1/voice/calls/{id}/transcript` | Get transcript |

### Webhook Events

```yaml
events:
  - voice.call.started
  - voice.call.authenticated
  - voice.call.intent_detected
  - voice.call.action_executed
  - voice.call.escalated
  - voice.call.ended
```

## Integration Points

| System | Integration Type | Purpose |
|--------|-----------------|---------|
| Twilio | WebSocket + REST | Call handling, voice streaming |
| OpenAI | REST | Speech-to-text, intent detection |
| Payment System | REST | Payment processing |
| Maintenance System | REST | Request creation |
| Knowledge Base | Vector Search | Question answering |

## User Stories

```gherkin
US-261-01: As a resident, I want to call and get my balance so that I know what I owe
  Given I call the management company
  When the AI agent answers
  And I authenticate successfully
  And I ask "What's my balance?"
  Then I hear my current balance amount

US-261-02: As a resident, I want to report a maintenance issue by phone so that I don't need to use an app
  Given I am authenticated on a call
  When I say "My kitchen sink is leaking"
  Then a maintenance request is created
  And I receive a confirmation number

US-261-03: As a resident, I want to speak to a human when the AI can't help
  Given I am on a call with the AI agent
  When my request requires human judgment
  Then I am transferred to a human agent
  And my call context is preserved
```

## Dependencies

| Dependency | Type | Notes |
|------------|------|-------|
| SKILL-265 | Internal | HITL Dashboard for escalation |
| SKILL-268 | Internal | Policy engine for coverage rules |
| Twilio Account | External | Voice platform |
| OpenAI API | External | GPT-4 for conversation |

## Effort Estimate

| Component | Estimate | Notes |
|-----------|----------|-------|
| Twilio Integration | 2 weeks | WebSocket setup, call handling |
| Speech Processing | 2 weeks | STT/TTS pipeline |
| Intent Detection | 1 week | LLM integration |
| Action Handlers | 2 weeks | Payment, maintenance, docs |
| Escalation Flow | 1 week | Transfer to human |
| **Total** | **8 weeks** | **Size: L** |

---

# SKILL-262: AI AP Agent

## Definition

```yaml
skill_id: SKILL-262
name: AI AP Agent
category: ai-workforce
priority: P0
source: HOAi
competitors: [HOAi, AppFolio]
```

## Description

An AI agent specialized in Accounts Payable processing. Handles invoice ingestion, OCR extraction, validation, GL coding, approval routing, and payment scheduling. Designed to process 15,000+ invoices/month with >90% straight-through processing.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 262-RQ-001 | Ingest invoices from email attachments | Must-Have | PDF/image extraction |
| 262-RQ-002 | Extract invoice data via OCR | Must-Have | >95% field accuracy |
| 262-RQ-003 | Validate vendor against approved vendor list | Must-Have | Vendor matching |
| 262-RQ-004 | Detect duplicate invoices | Must-Have | Duplicate prevention |
| 262-RQ-005 | Auto-assign GL codes based on vendor/description | Must-Have | >85% auto-coding |
| 262-RQ-006 | Route for approval based on amount thresholds | Must-Have | Policy-driven routing |
| 262-RQ-007 | Detect potential fraud indicators | Should-Have | Anomaly detection |
| 262-RQ-008 | Schedule payments based on terms | Must-Have | Payment scheduling |
| 262-RQ-009 | Handle exceptions via HITL queue | Must-Have | Escalation path |
| 262-RQ-010 | Provide audit trail for all actions | Must-Have | Complete logging |

## Data Model

```typescript
interface Invoice {
  invoice_id: string;
  status: 'received' | 'processing' | 'pending_approval' | 'approved' | 'rejected' | 'paid';
  
  source: {
    channel: 'email' | 'upload' | 'api';
    received_at: Date;
    original_file_url: string;
  };
  
  extracted_data: {
    vendor_name: string;
    vendor_id?: string;  // Matched vendor
    invoice_number: string;
    invoice_date: Date;
    due_date: Date;
    amount: number;
    currency: string;
    line_items: Array<{
      description: string;
      quantity: number;
      unit_price: number;
      total: number;
      gl_code?: string;
    }>;
    confidence_score: number;
  };
  
  validation: {
    vendor_matched: boolean;
    duplicate_check: 'passed' | 'potential_duplicate' | 'duplicate';
    amount_reasonable: boolean;
    fraud_indicators: string[];
  };
  
  coding: {
    gl_account: string;
    cost_center: string;
    property_id?: string;
    auto_coded: boolean;
    coding_confidence: number;
  };
  
  approval: {
    required: boolean;
    approver_id?: string;
    approved_at?: Date;
    approval_notes?: string;
  };
  
  payment: {
    scheduled_date?: Date;
    payment_method: 'ach' | 'check' | 'wire';
    payment_reference?: string;
    paid_at?: Date;
  };
  
  audit_trail: Array<{
    action: string;
    actor: string;  // agent_id or user_id
    timestamp: Date;
    details: object;
  }>;
}
```

## API Specification

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/ap/invoices` | Submit invoice |
| GET | `/api/v1/ap/invoices/{id}` | Get invoice details |
| PUT | `/api/v1/ap/invoices/{id}/approve` | Approve invoice |
| PUT | `/api/v1/ap/invoices/{id}/reject` | Reject invoice |
| PUT | `/api/v1/ap/invoices/{id}/code` | Update GL coding |
| POST | `/api/v1/ap/invoices/{id}/schedule-payment` | Schedule payment |
| GET | `/api/v1/ap/vendors` | List approved vendors |

## User Stories

```gherkin
US-262-01: As an AP clerk, I want invoices auto-extracted so I don't manually enter data
  Given an invoice email arrives
  When the AP Agent processes it
  Then all invoice fields are extracted
  And I only review exceptions

US-262-02: As a controller, I want invoices over $5000 routed for my approval
  Given an invoice for $7500 is processed
  When it passes validation
  Then it appears in my approval queue
  And I can approve with one click

US-262-03: As an auditor, I want full audit trail of invoice processing
  Given an invoice was paid
  When I review the invoice
  Then I see every step from receipt to payment
  And I see who/what approved each step
```

## Effort Estimate

| Component | Estimate |
|-----------|----------|
| Email Ingestion | 1 week |
| OCR Pipeline | 2 weeks |
| Validation Engine | 1 week |
| GL Coding | 2 weeks |
| Approval Workflow | 1 week |
| Payment Integration | 1 week |
| **Total** | **8 weeks (L)** |

---

# SKILL-263: AI Budget Agent

## Definition

```yaml
skill_id: SKILL-263
name: AI Budget Agent
category: ai-workforce
priority: P0
source: HOAi
competitors: [HOAi]
```

## Description

An AI agent specialized in budget creation, analysis, and forecasting. Analyzes historical spending patterns, predicts future expenses, identifies variances, and helps create annual budgets with AI-powered recommendations.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 263-RQ-001 | Analyze historical spending by category | Must-Have | 3-year trend analysis |
| 263-RQ-002 | Predict future expenses based on patterns | Must-Have | Forecast accuracy >85% |
| 263-RQ-003 | Identify budget variances and anomalies | Must-Have | Real-time variance alerts |
| 263-RQ-004 | Generate budget recommendations | Must-Have | Category-level suggestions |
| 263-RQ-005 | Create what-if scenarios | Should-Have | Scenario comparison |
| 263-RQ-006 | Track budget vs actual in real-time | Must-Have | Live dashboard |
| 263-RQ-007 | Generate budget reports | Must-Have | PDF/Excel export |
| 263-RQ-008 | Support reserve fund planning | Should-Have | Reserve calculations |

## Data Model

```typescript
interface Budget {
  budget_id: string;
  property_id: string;
  fiscal_year: number;
  status: 'draft' | 'pending_approval' | 'approved' | 'active';
  
  categories: Array<{
    category_id: string;
    name: string;
    budgeted_amount: number;
    actual_amount: number;
    variance: number;
    variance_percentage: number;
    ai_recommendation?: {
      suggested_amount: number;
      confidence: number;
      reasoning: string;
    };
  }>;
  
  totals: {
    budgeted: number;
    actual: number;
    variance: number;
    remaining: number;
  };
  
  forecasts: Array<{
    month: string;
    predicted_spend: number;
    confidence_interval: [number, number];
  }>;
  
  scenarios: Array<{
    scenario_id: string;
    name: string;
    adjustments: object;
    projected_outcome: number;
  }>;
}
```

## User Stories

```gherkin
US-263-01: As a property manager, I want AI budget recommendations so I can create accurate budgets faster
  Given I'm creating next year's budget
  When I ask the AI for recommendations
  Then I receive category-by-category suggestions
  And I see the reasoning behind each

US-263-02: As a board member, I want to see budget scenarios
  Given a proposed budget
  When I ask "What if utilities increase 15%?"
  Then I see the impact on the overall budget
  And I can compare multiple scenarios
```

## Effort Estimate

**Total: 5 weeks (M)**

---

# SKILL-264: AI Research Agent

## Definition

```yaml
skill_id: SKILL-264
name: AI Research Agent
category: ai-workforce
priority: P0
source: HOAi
competitors: [HOAi]
```

## Description

An AI agent that performs research tasks by searching internal knowledge bases, external sources, and synthesizing information. Used for policy lookups, vendor research, regulation compliance checks, and answering complex questions.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 264-RQ-001 | Search internal knowledge base via RAG | Must-Have | Vector search functional |
| 264-RQ-002 | Synthesize information from multiple sources | Must-Have | Multi-source answers |
| 264-RQ-003 | Cite sources in responses | Must-Have | Source attribution |
| 264-RQ-004 | Research vendor options and pricing | Should-Have | Vendor comparison |
| 264-RQ-005 | Check regulatory compliance requirements | Should-Have | Regulation lookup |
| 264-RQ-006 | Answer policy questions | Must-Have | Policy retrieval |
| 264-RQ-007 | Generate research summaries | Must-Have | Summary generation |

## Data Model

```typescript
interface ResearchQuery {
  query_id: string;
  question: string;
  context?: object;
  
  sources_searched: Array<{
    source_type: 'knowledge_base' | 'documents' | 'policies' | 'external';
    source_id: string;
    relevance_score: number;
  }>;
  
  answer: {
    text: string;
    confidence: number;
    citations: Array<{
      source: string;
      excerpt: string;
      relevance: number;
    }>;
  };
  
  metadata: {
    processing_time_ms: number;
    tokens_used: number;
    model: string;
  };
}
```

## Effort Estimate

**Total: 5 weeks (M)**

---

# SKILL-265: Managerial Hub (HITL Dashboard)

## Definition

```yaml
skill_id: SKILL-265
name: Managerial Hub (HITL Dashboard)
category: ai-workflow
priority: P0
source: HOAi
competitors: [HOAi, AppFolio]
```

## Description

A centralized Human-in-the-Loop dashboard where human supervisors review, approve, modify, and reject AI agent decisions. Provides complete task context, one-click approval, bulk operations, and performance analytics. The critical control layer for AI governance.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 265-RQ-001 | Display pending tasks requiring human review | Must-Have | Task queue visible |
| 265-RQ-002 | One-click approval for confident decisions | Must-Have | <500ms approval |
| 265-RQ-003 | Edit agent outputs before approval | Must-Have | Inline editing |
| 265-RQ-004 | Bulk approve/reject multiple tasks | Must-Have | Multi-select operations |
| 265-RQ-005 | Filter by agent, type, priority, age | Must-Have | Advanced filtering |
| 265-RQ-006 | Show complete task context and history | Must-Have | Full context display |
| 265-RQ-007 | Capture rejection reasons | Must-Have | Required on reject |
| 265-RQ-008 | Real-time updates via WebSocket | Must-Have | Live queue updates |
| 265-RQ-009 | SLA warnings and escalation alerts | Must-Have | Visual SLA indicators |
| 265-RQ-010 | Performance analytics per agent | Must-Have | Approval rates, times |
| 265-RQ-011 | Mobile-responsive design | Should-Have | Tablet/phone support |
| 265-RQ-012 | Keyboard shortcuts for power users | Should-Have | Hot keys defined |

## Data Model

```typescript
interface HITLTask {
  task_id: string;
  agent_id: string;
  agent_type: 'voice' | 'ap' | 'budget' | 'research';
  
  status: 'pending_review' | 'approved' | 'rejected' | 'modified';
  priority: 'critical' | 'high' | 'normal' | 'low';
  
  context: {
    source: string;
    original_input: object;
    agent_reasoning: string;
    confidence_score: number;
  };
  
  proposed_action: {
    action_type: string;
    action_data: object;
    impact_assessment?: string;
  };
  
  review: {
    reviewer_id?: string;
    reviewed_at?: Date;
    decision: 'approved' | 'rejected' | 'modified';
    modifications?: object;
    rejection_reason?: string;
    review_duration_ms?: number;
  };
  
  sla: {
    deadline: Date;
    warning_at: Date;
    is_breached: boolean;
  };
  
  created_at: Date;
  updated_at: Date;
}
```

## UI Components

### Component Hierarchy

```
HITLDashboard
├── Header
│   ├── Logo
│   ├── UserMenu
│   └── NotificationBell
├── Sidebar
│   ├── QueueStats
│   ├── AgentFilters
│   └── QuickActions
├── MainContent
│   ├── TaskQueue
│   │   ├── TaskCard[]
│   │   │   ├── TaskHeader (ID, Priority, Age)
│   │   │   ├── TaskSummary
│   │   │   ├── ConfidenceIndicator
│   │   │   └── QuickActions (Approve, Reject, View)
│   │   └── BulkActionBar
│   └── TaskDetail (expanded view)
│       ├── ContextPanel
│       ├── AgentReasoningPanel
│       ├── ProposedActionPanel
│       ├── EditableOutputPanel
│       └── ActionButtons
└── AnalyticsPanel
    ├── ApprovalRateChart
    ├── ProcessingTimeChart
    └── AgentPerformanceTable
```

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `a` | Approve selected |
| `r` | Reject selected |
| `e` | Edit selected |
| `↑/↓` | Navigate tasks |
| `Space` | Toggle selection |
| `Shift+A` | Approve all selected |
| `?` | Show help |

## API Specification

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/hitl/tasks` | List pending tasks (paginated, filtered) |
| GET | `/api/v1/hitl/tasks/{id}` | Get task details |
| PUT | `/api/v1/hitl/tasks/{id}/approve` | Approve task |
| PUT | `/api/v1/hitl/tasks/{id}/reject` | Reject task |
| PUT | `/api/v1/hitl/tasks/{id}/modify` | Modify and approve |
| POST | `/api/v1/hitl/tasks/bulk-approve` | Bulk approve |
| POST | `/api/v1/hitl/tasks/bulk-reject` | Bulk reject |
| GET | `/api/v1/hitl/analytics` | Get performance metrics |
| WS | `/ws/hitl/updates` | Real-time task updates |

## Technology Stack

```yaml
frontend:
  framework: React 19
  language: TypeScript 5.0+
  styling: TailwindCSS 4.1+
  build: Vite 6.0+
  state: React Context + useReducer
  realtime: WebSocket (native)

backend:
  framework: FastAPI
  language: Python 3.10+
  websocket: Starlette WebSockets
  cache: Redis
```

## User Stories

```gherkin
US-265-01: As a manager, I want to approve AI decisions with one click
  Given a task is in my review queue
  And the AI confidence is >95%
  When I click "Approve"
  Then the task is approved in <500ms
  And it's removed from my queue

US-265-02: As a reviewer, I want to see why the AI made its decision
  Given a task requires my review
  When I view the task details
  Then I see the AI's reasoning chain
  And I see the confidence score
  And I see the original input

US-265-03: As a manager, I want to bulk approve low-risk tasks
  Given 10 tasks are pending with >90% confidence
  When I select all and click "Bulk Approve"
  Then all 10 are approved
  And I see confirmation

US-265-04: As a compliance officer, I want full audit trail
  Given a task was approved
  When I review the audit log
  Then I see who approved it
  And when it was approved
  And any modifications made
```

## Effort Estimate

| Component | Estimate |
|-----------|----------|
| Task Queue UI | 2 weeks |
| Task Detail View | 2 weeks |
| Bulk Operations | 1 week |
| WebSocket Updates | 1 week |
| Analytics Dashboard | 2 weeks |
| API Endpoints | 2 weeks |
| **Total** | **10 weeks (XL)** |

---

# SKILL-266: AI Scenario Modeling

## Definition

```yaml
skill_id: SKILL-266
name: AI Scenario Modeling
category: ai-workflow
priority: P0
source: HOAi
competitors: [HOAi]
```

## Description

AI-powered scenario modeling that allows users to simulate different business scenarios and see predicted outcomes. Used for budget planning, staffing decisions, and strategic planning.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 266-RQ-001 | Create what-if scenarios with variable adjustments | Must-Have | Multiple variables |
| 266-RQ-002 | Compare multiple scenarios side-by-side | Must-Have | Comparison view |
| 266-RQ-003 | Predict outcomes based on historical data | Must-Have | ML predictions |
| 266-RQ-004 | Show confidence intervals | Must-Have | Uncertainty ranges |
| 266-RQ-005 | Save and share scenarios | Should-Have | Collaboration |

## Effort Estimate

**Total: 5 weeks (M)**

---

# SKILL-267: AI Outbound Calling

## Definition

```yaml
skill_id: SKILL-267
name: AI Outbound Calling
category: ai-workforce
priority: P0
source: HOAi
competitors: [HOAi, EliseAI]
```

## Description

AI agent capability to make outbound calls for tasks like payment reminders, appointment confirmations, survey collection, and proactive notifications.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 267-RQ-001 | Make outbound calls via Twilio | Must-Have | Call initiation |
| 267-RQ-002 | Support call campaigns (batch calling) | Must-Have | Campaign management |
| 267-RQ-003 | Respect do-not-call lists | Must-Have | DNC compliance |
| 267-RQ-004 | Handle voicemail detection and recording | Must-Have | VM handling |
| 267-RQ-005 | Track call outcomes and follow-ups | Must-Have | Outcome tracking |
| 267-RQ-006 | Schedule calls based on contact preferences | Should-Have | Time zone aware |

## Data Model

```typescript
interface OutboundCall {
  call_id: string;
  campaign_id?: string;
  
  target: {
    phone_number: string;
    contact_id: string;
    contact_name: string;
    preferred_times?: string[];
    dnc_status: boolean;
  };
  
  purpose: {
    type: 'payment_reminder' | 'appointment_confirmation' | 'survey' | 'notification';
    script_id: string;
    context: object;
  };
  
  execution: {
    scheduled_for: Date;
    attempted_at?: Date;
    status: 'scheduled' | 'in_progress' | 'completed' | 'failed' | 'voicemail';
    duration_seconds?: number;
  };
  
  outcome: {
    result: 'answered' | 'voicemail' | 'no_answer' | 'busy' | 'dnc_blocked';
    goal_achieved: boolean;
    notes?: string;
    follow_up_required: boolean;
    follow_up_date?: Date;
  };
}
```

## Effort Estimate

**Total: 5 weeks (M)**

---

# SKILL-268: Configurable AI Coverage

## Definition

```yaml
skill_id: SKILL-268
name: Configurable AI Coverage
category: ai-workflow
priority: P0
source: HOAi
competitors: [HOAi]
```

## Description

A policy engine that allows administrators to configure when AI agents operate autonomously vs. when they require human approval. Supports time-based rules, amount thresholds, risk levels, and custom conditions.

## Functional Requirements

| Req ID | Requirement | Priority | Acceptance Criteria |
|--------|-------------|----------|---------------------|
| 268-RQ-001 | Define policies with conditions and actions | Must-Have | Policy CRUD |
| 268-RQ-002 | Support AND/OR/NOT logical operators | Must-Have | Complex conditions |
| 268-RQ-003 | Time-based conditions (business hours, dates) | Must-Have | Temporal rules |
| 268-RQ-004 | Amount threshold conditions | Must-Have | Numeric comparisons |
| 268-RQ-005 | Risk-level based routing | Must-Have | Risk assessment |
| 268-RQ-006 | Priority-based policy resolution | Must-Have | Conflict handling |
| 268-RQ-007 | Policy versioning and rollback | Must-Have | Version control |
| 268-RQ-008 | Policy simulation/testing | Should-Have | Test before deploy |
| 268-RQ-009 | Audit trail for policy changes | Must-Have | Change logging |

## Data Model

```yaml
policy:
  id: string
  name: string
  version: semver
  priority: integer (1-100)
  status: active|inactive|deprecated
  
  conditions:
    - field: string          # e.g., "task.amount"
      operator: equals|not_equals|greater_than|less_than|contains|in|not_in
      value: any
      logical_operator: AND|OR|NOT
  
  actions:
    allow: boolean
    deny: boolean
    escalate: boolean
    require_approval: boolean
    custom_actions: array
  
  fallback:
    action: allow|deny|escalate
    reason: string
  
  metadata:
    created_at: timestamp
    updated_at: timestamp
    created_by: string
    tags: array
```

## Policy Examples

### Invoice Approval Policy
```yaml
policy:
  id: "invoice_approval_001"
  name: "Invoice Approval Threshold"
  priority: 80
  
  conditions:
    - field: "task.type"
      operator: "equals"
      value: "invoice_processing"
    - field: "invoice.amount"
      operator: "greater_than"
      value: 5000
      logical_operator: "AND"
  
  actions:
    require_approval: true
    escalate: false
  
  fallback:
    action: "allow"
    reason: "Invoice under threshold"
```

### After-Hours Policy
```yaml
policy:
  id: "after_hours_001"
  name: "After Hours Task Handling"
  priority: 90
  
  conditions:
    - field: "current_time"
      operator: "not_in"
      value: ["09:00-17:00"]
    - field: "task.priority"
      operator: "less_than"
      value: "high"
      logical_operator: "AND"
  
  actions:
    escalate: true
  
  fallback:
    action: "allow"
    reason: "Within business hours or high priority"
```

## User Stories

```gherkin
US-268-01: As an admin, I want to set approval thresholds so routine tasks are auto-approved
  Given I'm configuring the AP agent
  When I set "auto-approve invoices under $1000"
  Then invoices under $1000 are processed without HITL
  And invoices over $1000 go to the approval queue

US-268-02: As an admin, I want to test policies before deploying
  Given I've created a new policy
  When I run a simulation with test data
  Then I see which tasks would be affected
  And I can adjust before going live
```

## Effort Estimate

| Component | Estimate |
|-----------|----------|
| Policy Schema | 1 week |
| Evaluation Engine | 2 weeks |
| Admin UI | 2 weeks |
| Simulation Mode | 1 week |
| Versioning | 1 week |
| **Total** | **7 weeks (L)** |

---

# TOOL SPECIFICATIONS

## Tools Required

| Tool ID | Name | Used By Skills | Description |
|---------|------|----------------|-------------|
| TOOL-001 | Agent Orchestrator | All | LangGraph-based multi-agent orchestration |
| TOOL-002 | Policy Engine | SKILL-268 | OPA-based policy evaluation |
| TOOL-003 | Task State Machine | All | Finite state machine for task lifecycle |
| TOOL-004 | HITL Queue Manager | SKILL-265 | Redis-based task queue |
| TOOL-005 | Voice Pipeline | SKILL-261, 267 | Twilio + STT/TTS integration |
| TOOL-006 | OCR Pipeline | SKILL-262 | Invoice data extraction |
| TOOL-007 | Vector Search | SKILL-264 | MongoDB Atlas Vector Search |
| TOOL-008 | Audit Logger | All | Immutable audit trail |
| TOOL-009 | Trust Score Calculator | All | Agent performance scoring |
| TOOL-010 | Notification Service | All | Multi-channel notifications |
| TOOL-011 | Report Generator | SKILL-263 | PDF/Excel generation |
| TOOL-012 | Campaign Manager | SKILL-267 | Outbound call campaigns |

---

# DEPENDENCY MAP

```
SKILL-268 (Policy Engine)
    │
    ├──▶ SKILL-261 (Voice Agent)
    ├──▶ SKILL-262 (AP Agent)
    ├──▶ SKILL-263 (Budget Agent)
    ├──▶ SKILL-264 (Research Agent)
    └──▶ SKILL-267 (Outbound Calling)
              │
              └──▶ SKILL-265 (HITL Dashboard) ◀── All Agents
                        │
                        └──▶ SKILL-266 (Scenario Modeling)
```

**Build Order**:
1. SKILL-268 (Policy Engine) - Foundation
2. SKILL-265 (HITL Dashboard) - Control Layer
3. SKILL-261 (Voice Agent) - First agent
4. SKILL-262 (AP Agent) - Second agent
5. SKILL-264 (Research Agent) - Supporting agent
6. SKILL-263 (Budget Agent) - Financial agent
7. SKILL-267 (Outbound Calling) - Extends voice
8. SKILL-266 (Scenario Modeling) - Analytics layer

---

# TOTAL EFFORT SUMMARY

| Skill | Effort | Weeks |
|-------|--------|-------|
| SKILL-261 | L | 8 |
| SKILL-262 | L | 8 |
| SKILL-263 | M | 5 |
| SKILL-264 | M | 5 |
| SKILL-265 | XL | 10 |
| SKILL-266 | M | 5 |
| SKILL-267 | M | 5 |
| SKILL-268 | L | 7 |
| **TOTAL** | **XL** | **53 weeks** |

**With parallelization (3-4 developers)**: 16-20 weeks

---

# ACCEPTANCE CRITERIA SUMMARY

| Skill | Key Acceptance Criteria |
|-------|------------------------|
| SKILL-261 | Call answered <3s, intent detected >80% confidence, escalation working |
| SKILL-262 | >95% OCR accuracy, >85% auto-coding, 15K invoices/month |
| SKILL-263 | >85% forecast accuracy, scenario comparison functional |
| SKILL-264 | RAG search working, sources cited, summaries accurate |
| SKILL-265 | <500ms approval, real-time updates, bulk operations |
| SKILL-266 | What-if scenarios, side-by-side comparison |
| SKILL-267 | Campaign execution, DNC compliance, outcome tracking |
| SKILL-268 | Policy evaluation <100ms, conflict resolution, audit trail |

---

---

## 📐 Architecture Alignment Notes

### Citadel OS Layer Mapping

| Spec Component | Citadel Layer | Technology | Aligned |
|----------------|---------------|------------|---------|
| Voice/AP/Budget/Research Agents | Layer 4 (Skills) | Claude Skills Framework | ✅ |
| Agent Orchestration | Layer 3A (Hot Path) | LangGraph + LangChain | ✅ |
| Policy Engine (SKILL-268) | Layer 3A (Hot Path) | OPA-based evaluation | ✅ |
| HITL Dashboard | Layer 6 (Applications) | React 19 | ✅ |
| Invoice Payments | Layer 3B (Cold Path) | TigerBeetle via Formance | ✅ |
| WebSocket/Real-time | Layer 2 (Infrastructure) | Redis + WebSocket | ✅ |

### Execution Path Classification

| Skill | Path | Rationale |
|-------|------|-----------|
| SKILL-261 (Voice Agent) | **Hot Path** | AI reasoning, conversation handling |
| SKILL-262 (AP Agent) | **Hybrid** | AI processing (Hot) → Payment (Cold) |
| SKILL-263 (Budget Agent) | **Hot Path** | AI forecasting, scenario modeling |
| SKILL-264 (Research Agent) | **Hot Path** | RAG retrieval, synthesis |
| SKILL-265 (HITL Dashboard) | **Hot Path** | UI interactions, real-time updates |
| SKILL-266 (Scenario Modeling) | **Hot Path** | ML predictions, what-if analysis |
| SKILL-267 (Outbound Calling) | **Hot Path** | AI-driven call campaigns |
| SKILL-268 (AI Coverage Policy) | **Hot Path** | Policy evaluation engine |

### MCP Server Requirements

```yaml
# Required MCP servers for AI Workforce skills
mcp_servers:
  - uri: mcp://treasury/create_transfer
    purpose: Invoice payment processing (SKILL-262)
  - uri: mcp://treasury/query_balance
    purpose: Balance inquiries (SKILL-261)
  - uri: mcp://temporal/trigger_workflow
    purpose: Approval workflows (SKILL-265)
  - uri: mcp://vector/semantic_search
    purpose: Knowledge retrieval (SKILL-264)
  - uri: mcp://hitl/submit_task
    purpose: HITL queue management (SKILL-265)
```

### Infrastructure Alignment

| Incoming Spec | Our Decision | Notes |
|---------------|--------------|-------|
| FastAPI backend | FastAPI (internal OK) | Rust/Axum for external gateway |
| React 19 frontend | React 19 | ✅ Aligned |
| Redis cache | Redis | ✅ Aligned |
| WebSocket updates | Redis Pub/Sub | ✅ Aligned |
| Container deployment | **ECS/Fargate** | Not Kubernetes |

### Compliance Verification

- ✅ AI operations on Hot Path (LangGraph orchestration)
- ✅ Financial transactions route to Cold Path (TigerBeetle)
- ✅ Voice via Twilio (PCI compliant for payments)
- ✅ Audit logging via immutable trail
- ✅ Policy engine for AI governance

---

**Specification Complete** ✅

**Next Steps**:
1. Update MASTER_SKILL_REGISTRY.md with these specifications
2. Create implementation tickets
3. Begin with SKILL-268 (Policy Engine) as foundation


