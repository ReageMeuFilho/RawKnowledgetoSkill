# Final Skill Specification: AI Maintenance Coordinator

> **Gap ID**: GAP-AF-002
> **Skills Specified**: SKILL-254
> **Priority**: P0 (MVP Critical)
> **Stage 4 Completed**: January 2026
> **Engineering Spec**: `knowledge/operations/ES-AF-002-ai-maintenance-coordinator.md` (8,577 lines)

---

## 📋 EXECUTIVE SUMMARY

The **AI Maintenance Coordinator** is a transformative agentic AI system designed to revolutionize property maintenance operations through end-to-end automation. This system handles work orders from start to finish: triage, troubleshooting, vendor selection, coordination, scheduling and job completion verification, functioning as a 24/7 digital maintenance dispatcher.

### Business Impact

| Metric | Target | Source |
|--------|--------|--------|
| Cost Reduction | **$12/door** maintenance cost savings | Vendoroo benchmark |
| Time Savings | **10 hours/week** per coordinator | Industry research |
| AI Automation Rate | **80%** tasks without human intervention | Target |
| Remote Resolution | **20-35%** issues resolved without dispatch | Troubleshooting engine |
| Response Time | **Instant** - every call answered immediately | 24/7 coverage |

---

## 🎯 SKILL SPECIFIED

### SKILL-254: AI Maintenance Coordinator

| Attribute | Value |
|-----------|-------|
| **Skill Name** | ai-maintenance-coordinator |
| **Category** | operations |
| **Priority** | P0 (Critical) |
| **Status** | ✅ **SPECIFIED** |

---

## 🔧 CORE FEATURES

### F-001: Multi-Channel Request Intake

| Requirement ID | Description | Priority |
|----------------|-------------|----------|
| F-001-RQ-001 | Voice call handling via Twilio with real-time transcription | Must-Have |
| F-001-RQ-002 | SMS processing with 24-hour conversation context | Must-Have |
| F-001-RQ-003 | Email parsing with attachment handling (up to 5MB) | Must-Have |
| F-001-RQ-004 | Portal API for PMS integration | Must-Have |

**Supported Channels:**
- Phone/Voice (Twilio)
- SMS/Text
- Email (SendGrid)
- Web Portal API

---

### F-002: AI-Powered Triage and Classification

| Requirement ID | Description | Priority |
|----------------|-------------|----------|
| F-002-RQ-001 | Issue classification across 6 categories with >90% accuracy | Must-Have |
| F-002-RQ-002 | Emergency keyword detection with 100% recall | Must-Have |
| F-002-RQ-003 | Property context loading within 2 seconds | Must-Have |

**Issue Categories:**
1. Plumbing
2. HVAC
3. Electrical
4. Appliance
5. Structural
6. Pest

**Urgency Levels:**
- `ROUTINE` - Standard priority
- `URGENT` - Same-day response needed
- `EMERGENCY` - Immediate response (fire, flood, gas leak)

---

### F-003: Remote Troubleshooting Engine

| Requirement ID | Description | Priority |
|----------------|-------------|----------|
| F-003-RQ-001 | Troubleshooting knowledge base covering top 50 scenarios | Must-Have |
| F-003-RQ-002 | Interactive troubleshooting sessions with state management | Must-Have |
| F-003-RQ-003 | Resolution tracking with success rate monitoring | Should-Have |

**Target Resolution Rate**: 25% average (avoiding unnecessary truck rolls)

---

### F-004: Intelligent Vendor Management

| Requirement ID | Description | Priority |
|----------------|-------------|----------|
| F-004-RQ-001 | Multi-criteria vendor scoring algorithm | Must-Have |
| F-004-RQ-002 | Automated dispatch with confirmation tracking | Must-Have |
| F-004-RQ-003 | Vendor performance monitoring and scorecards | Should-Have |

**Vendor Scoring Weights:**
| Criterion | Weight |
|-----------|--------|
| Performance History | 40% |
| Cost Competitiveness | 25% |
| Property Familiarity | 20% |
| Availability | 15% |

---

### F-005: Work Order Lifecycle Management

| Requirement ID | Description | Priority |
|----------------|-------------|----------|
| F-005-RQ-001 | Complete state machine with 12 distinct states | Must-Have |
| F-005-RQ-002 | Automated state transitions with timeout handling | Must-Have |
| F-005-RQ-003 | Complete audit trail for compliance | Must-Have |

**Work Order States:**
```
NEW → TRIAGING → TROUBLESHOOTING → AWAITING_DISPATCH → 
AWAITING_APPROVAL → DISPATCHING → SCHEDULED → VENDOR_EN_ROUTE → 
IN_PROGRESS → NEEDS_PARTS → PENDING_VERIFICATION → COMPLETED
```

---

### F-006: Approval Workflow and Cost Management

| Requirement ID | Description | Priority |
|----------------|-------------|----------|
| F-006-RQ-001 | Configurable approval thresholds | Must-Have |
| F-006-RQ-002 | Owner notification preferences | Should-Have |
| F-006-RQ-003 | Emergency override capabilities | Must-Have |

---

## 🏗️ SYSTEM ARCHITECTURE

### 4-Layer Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      INTAKE LAYER                           │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │  Voice   │ │   SMS    │ │  Email   │ │  Portal  │       │
│  │ Handler  │ │ Handler  │ │  Parser  │ │   API    │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
│                      ↓                                      │
│              Channel Unification                            │
└─────────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────────┐
│                       BRAIN LAYER                           │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │ Triage   │ │Trouble-  │ │ Vendor   │ │ Decision │       │
│  │ Engine   │ │ shooting │ │ Selector │ │ Engine   │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
│                                                             │
│  LangGraph Agent Orchestration                              │
└─────────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────────┐
│                      ACTION LAYER                           │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │ Vendor   │ │ Resident │ │   PMS    │ │ Payment  │       │
│  │ Dispatch │ │ Notify   │ │   Sync   │ │ Process  │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
└─────────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────────┐
│                   ORCHESTRATION LAYER                       │
│  ┌─────────────────────────────────────────────────────┐   │
│  │            Temporal Workflow Engine                  │   │
│  │  - Durable execution                                 │   │
│  │  - State persistence                                 │   │
│  │  - Automatic retries                                 │   │
│  │  - Timeout handling                                  │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## 🛠️ TECHNOLOGY STACK

### Core Technologies

| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| AI Orchestration | LangGraph | 1.0+ | Agent workflow orchestration |
| Workflow Engine | Temporal | 1.x | Durable execution, state persistence |
| Backend Framework | FastAPI | Latest | REST APIs |
| Database | MongoDB | 8.x | Primary data store |
| Cache | Redis | 7.x | Session state, rate limiting |
| Vector DB | Pinecone/MongoDB Atlas | Latest | Knowledge base retrieval |
| Telephony | Twilio | Latest | Voice and SMS |
| Email | SendGrid | Latest | Email processing |

### Infrastructure

| Component | Technology | Purpose |
|-----------|------------|---------|
| Container | Docker | Containerization |
| Orchestration | Kubernetes | Container management |
| Message Queue | Redis Streams | Event processing |
| Monitoring | DataDog | APM and metrics |

---

## 📊 DATA MODEL

### Core Entities

```python
class MaintenanceRequest(BaseModel):
    request_id: str
    source_channel: SourceChannel  # phone, sms, email, portal
    property_id: str
    unit_id: str
    resident_id: str
    issue_description: str
    issue_category: Optional[str]
    urgency: UrgencyLevel
    attachments: List[Attachment]
    created_at: datetime
    session_id: str

class WorkOrder(BaseModel):
    work_order_id: str
    request_id: str
    status: WorkOrderStatus  # 12 states
    property_id: str
    unit_id: str
    resident_info: ResidentInfo
    issue_details: IssueDetails
    vendor_assignment: Optional[VendorAssignment]
    timeline: Timeline
    cost_tracking: CostTracking
    communication_log: List[CommunicationEntry]
    audit_trail: List[AuditEntry]

class VendorProfile(BaseModel):
    vendor_id: str
    company_name: str
    specialties: List[str]
    service_area: GeoArea
    performance_metrics: PerformanceMetrics
    contact_info: ContactInfo
    availability: AvailabilitySchedule
    pricing: PricingStructure
```

---

## 📈 PERFORMANCE REQUIREMENTS

| Metric | Target | SLA |
|--------|--------|-----|
| System Uptime | 99.9% | Monthly |
| Voice Answer Time | <3 seconds | Per call |
| Request Processing | <5 seconds | From intake to triage |
| Vendor Dispatch | <30 minutes | Emergency response |
| AI Automation Rate | >80% | Tasks without human intervention |
| Issue Classification Accuracy | >90% | Per request |
| Emergency Detection | 100% recall | Life safety |

---

## 🔄 8-STEP MAINTENANCE WORKFLOW

Based on Vendoroo best practices:

```
1. REQUEST INTAKE
   └── Multi-channel capture (voice, SMS, email, portal)

2. TRIAGE & CLASSIFICATION
   └── AI categorization, urgency determination, context loading

3. REMOTE TROUBLESHOOTING
   └── Guided diagnostics, potential self-resolution

4. VENDOR SELECTION
   └── Scoring algorithm, availability check, dispatch

5. SCHEDULING & COORDINATION
   └── Appointment booking, resident confirmation

6. JOB EXECUTION
   └── Vendor en route, in progress, parts needed

7. COMPLETION VERIFICATION
   └── Resident confirmation, quality check

8. BILLING & CLOSEOUT
   └── Invoice processing, PMS sync, analytics
```

---

## 🚀 IMPLEMENTATION ROADMAP

### Phase 1: Core Engine (Weeks 1-8)
- [ ] Multi-channel intake (voice, SMS, email)
- [ ] AI triage and classification
- [ ] Work order state machine
- [ ] Basic vendor management
- [ ] Temporal workflow integration

### Phase 2: Intelligence (Weeks 9-14)
- [ ] Remote troubleshooting engine
- [ ] Knowledge base with 50+ scenarios
- [ ] Vendor scoring algorithm
- [ ] Automated dispatch with retry logic

### Phase 3: Integration (Weeks 15-18)
- [ ] PMS integrations (AppFolio, Yardi, RentManager)
- [ ] Payment processing
- [ ] Approval workflows
- [ ] Owner/manager notifications

### Phase 4: Polish & Scale (Weeks 19-22)
- [ ] Dashboard UI
- [ ] Reporting and analytics
- [ ] Performance optimization
- [ ] Documentation

**Total Estimated Effort**: 22 weeks

---

## ✅ STAGE 4 COMPLETION CHECKLIST

- [x] Engineering Specification reviewed (8,577 lines)
- [x] SKILL-254 (AI Maintenance Coordinator) fully specified
- [x] Technology stack documented (LangGraph, Temporal, FastAPI)
- [x] 4-layer architecture defined
- [x] 8-step workflow documented
- [x] Performance requirements defined
- [x] Data model specified
- [x] Implementation roadmap created
- [ ] MASTER_SKILL_REGISTRY.md updated (next step)

---

## 📚 REFERENCES

- **Stage 1 Research**: `knowledge/operations/KD-AF-002-ai-maintenance-coordinator.md` (9.5/10)
- **Stage 2 Prompt**: `docs/prompts/ENGINEERING_SPEC_PROMPT_AI_MAINTENANCE.md`
- **Stage 3 Spec**: `knowledge/operations/ES-AF-002-ai-maintenance-coordinator.md` (8,577 lines)
- **Primary Source**: Vendoroo AI Maintenance Platform
- **Secondary Sources**: AppFolio Realm-X, Property Meld, Latchel

---

**Status**: ✅ **GAP-AF-002 COMPLETE** - SKILL-254 Fully Specified

