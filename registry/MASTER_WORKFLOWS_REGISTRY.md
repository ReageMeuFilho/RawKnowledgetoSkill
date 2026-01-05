# Master Workflows Registry: Conversation Flows & State Machines

> **How conversations progress** - Multi-turn flows, branching logic, handoffs
> **Purpose**: Define structured conversation patterns and state transitions
> **Last Updated**: January 2026

---

## 🔄 Why Workflows Matter

Some conversations aren't simple Q&A - they're multi-step processes:

```
❌ SIMPLE (doesn't need workflow)        ✅ COMPLEX (needs workflow)

User: "What's the WiFi password?"        User: "I want to report a leak"
Agent: "GuestWifi2024"                   Agent: "Where is the leak?"
                                         User: "Kitchen sink"
                                         Agent: "How severe? Dripping or flowing?"
                                         User: "Flowing"
                                         Agent: "This is urgent. I'm dispatching..."
                                         [Creates ticket, notifies vendor, follows up]
```

---

## 📊 Workflow Types

| Type | Purpose | Example |
|------|---------|---------|
| **Linear** | Step-by-step process | Check-in flow |
| **Branching** | Different paths based on input | Maintenance triage |
| **Loop** | Repeat until condition met | Collect missing info |
| **Parallel** | Multiple things at once | Notify + Create ticket |
| **Handoff** | Transfer to human/other agent | Escalation |

---

## 🏠 Property Management Workflows

### WORKFLOW-001: Maintenance Request (Branching)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    MAINTENANCE REQUEST WORKFLOW                                  │
└─────────────────────────────────────────────────────────────────────────────────┘

                         [User reports issue]
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │ 1. CLASSIFY ISSUE      │
                    │    - Category          │
                    │    - Location          │
                    │    - Description       │
                    └───────────┬────────────┘
                                │
                    ┌───────────┴───────────┐
                    │ 2. ASSESS URGENCY     │
                    └───────────┬───────────┘
                                │
            ┌───────────────────┼───────────────────┐
            │                   │                   │
            ▼                   ▼                   ▼
     ┌────────────┐      ┌────────────┐      ┌────────────┐
     │ 🔴 EMERGENCY│      │ 🟡 URGENT  │      │ 🟢 NORMAL  │
     │            │      │            │      │            │
     │ - Water    │      │ - No hot   │      │ - Squeaky  │
     │   flooding │      │   water    │      │   door     │
     │ - Gas leak │      │ - A/C out  │      │ - Light    │
     │ - Fire     │      │   in heat  │      │   out      │
     └─────┬──────┘      └─────┬──────┘      └─────┬──────┘
           │                   │                   │
           ▼                   ▼                   ▼
     ┌────────────┐      ┌────────────┐      ┌────────────┐
     │ Immediate  │      │ Same-day   │      │ Schedule   │
     │ dispatch   │      │ dispatch   │      │ within 48h │
     │ + Notify   │      │            │      │            │
     │ owner      │      │            │      │            │
     └─────┬──────┘      └─────┬──────┘      └─────┬──────┘
           │                   │                   │
           └───────────────────┼───────────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │ 3. CREATE TICKET       │
                    │    - Log details       │
                    │    - Assign priority   │
                    │    - Link to history   │
                    └───────────┬────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │ 4. DISPATCH VENDOR     │
                    │    - Select vendor     │
                    │    - Send details      │
                    │    - Confirm ETA       │
                    └───────────┬────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │ 5. CONFIRM WITH USER   │
                    │    - Provide ETA       │
                    │    - Give ticket #     │
                    │    - Set expectations  │
                    └───────────┬────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │ 6. FOLLOW UP           │
                    │    - Check resolution  │
                    │    - Request feedback  │
                    │    - Close ticket      │
                    └────────────────────────┘
```

**States**:
| State | Description | Next States |
|-------|-------------|-------------|
| `awaiting_classification` | Collecting issue details | `assessing_urgency` |
| `assessing_urgency` | Determining priority | `dispatching` |
| `dispatching` | Sending to vendor | `awaiting_vendor_response` |
| `awaiting_vendor_response` | Waiting for vendor ETA | `confirmed`, `escalate` |
| `confirmed` | User informed of ETA | `in_progress` |
| `in_progress` | Vendor working on issue | `resolved`, `escalate` |
| `resolved` | Issue fixed | `closed` |
| `closed` | Ticket complete | END |
| `escalate` | Human needed | HANDOFF |

---

### WORKFLOW-002: Guest Check-In (Linear)

```
[24h before] ──► [Send pre-arrival info] ──► [Day of: Send access code]
                                                        │
                                                        ▼
                                              [Confirm arrival]
                                                        │
                                                        ▼
                                              [First night check-in]
```

**States**:
| State | Trigger | Action | Next |
|-------|---------|--------|------|
| `scheduled` | 24h before check-in | Send pre-arrival message | `pre_arrival_sent` |
| `pre_arrival_sent` | Check-in day | Send access code | `access_sent` |
| `access_sent` | User confirms arrival | Log check-in | `arrived` |
| `arrived` | 8 PM same day | Send "how's everything?" | `first_night_check` |
| `first_night_check` | Response or 24h | Resolve issues or close | `active_stay` |

---

### WORKFLOW-003: Lease Renewal (Complex)

```
[90 days before expiry]
        │
        ▼
[Check tenant eligibility]
        │
   ┌────┴────┐
   │         │
Eligible  Not Eligible
   │         │
   ▼         ▼
[Send offer] [Send non-renewal notice]
   │
   ▼
[Await response]
   │
   ┌────┬────┐
   │    │    │
Accept Negotiate Decline
   │    │    │
   ▼    ▼    ▼
[Generate] [Counter] [Move-out]
[new lease] [offer]  [process]
```

---

## 📋 Workflow Specification Template

```markdown
### WORKFLOW-XXX: [workflow-name]

**Vertical**: [STR / LTR / HOA]
**Type**: [Linear / Branching / Loop / Parallel]
**Trigger**: [What starts this workflow]

## Flow Diagram
[ASCII diagram]

## States

| State | Description | Entry Condition | Exit Conditions |
|-------|-------------|-----------------|-----------------|
| state_1 | Description | How to enter | How to exit |

## Transitions

| From | To | Condition | Action |
|------|-----|-----------|--------|
| state_1 | state_2 | condition | action |

## Data Collected

| Step | Data | Required | Validation |
|------|------|----------|------------|
| Step 1 | field_name | Yes/No | Rules |

## Tools Used

| Step | Tool | Purpose |
|------|------|---------|
| Step 1 | TOOL-XXX | Purpose |

## Timeout Handling

| State | Timeout | Action |
|-------|---------|--------|
| awaiting_response | 24h | Send reminder |
| awaiting_response | 48h | Escalate |

## Error Handling

| Error | Recovery |
|-------|----------|
| Vendor unavailable | Try next vendor |
| User unresponsive | Schedule callback |
```

---

## 🔧 Implementing Workflows in Kortix

Workflows translate to LangGraph state machines:

```python
from langgraph.graph import StateGraph

# Define the workflow
maintenance_workflow = StateGraph(MaintenanceState)

# Add nodes (states)
maintenance_workflow.add_node("classify", classify_issue)
maintenance_workflow.add_node("assess_urgency", assess_urgency)
maintenance_workflow.add_node("dispatch", dispatch_vendor)
maintenance_workflow.add_node("confirm", confirm_with_user)
maintenance_workflow.add_node("follow_up", follow_up)

# Add edges (transitions)
maintenance_workflow.add_edge("classify", "assess_urgency")
maintenance_workflow.add_conditional_edges(
    "assess_urgency",
    route_by_urgency,
    {
        "emergency": "dispatch",
        "urgent": "dispatch",
        "normal": "schedule"
    }
)
```



