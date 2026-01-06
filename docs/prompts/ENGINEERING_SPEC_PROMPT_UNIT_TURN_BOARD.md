# Engineering Specification Prompt: Unit Turn Board

**Gap ID**: GAP-AF-005  
**Skill ID**: SKILL-257 (unit-turn-board)  
**Stage**: 2 → Engineering Specification  
**Input Document**: `knowledge/operations/KD-AF-005-unit-turn-board.md`

---

## 🎯 Your Mission

Create a comprehensive Engineering Specification document that enables a development team to build a **production-grade Unit Turn Board** for property management. The Turn Board is a visual Kanban-style dashboard that tracks and coordinates the make-ready process between tenant move-out and new tenant move-in.

---

## 📋 Knowledge Document Summary

The Research Agent has provided:
- ✅ Turn process workflow (10 sections)
- ✅ Kanban board visualization patterns
- ✅ Task assignment logic with auto-dispatch
- ✅ Move-in coordination with leasing
- ✅ Data model (UnitTurn, TurnTask, TurnTemplate)
- ✅ Metrics & analytics (turn time, cost, vendor scores)
- ✅ Notification & escalation system
- ✅ Integration requirements
- ✅ Competitive analysis (AppFolio, Yardi, RentManager, Buildium, Property Meld)
- ✅ Industry benchmarks (3-day target, $2,500-$4,000/unit)

---

## 📄 Specification Requirements

### Section 1: Executive Summary
- System purpose and business value
- Scope (in-scope vs out-of-scope)
- Key success metrics
- Target users (Property Managers, Maintenance Supervisors, Leasing Agents, Vendors)

---

### Section 2: Turn Lifecycle State Machine

Define the complete state machine for unit turns:

```
STATES:
- NOTICE_RECEIVED: Tenant gave move-out notice
- SCHEDULED: Turn scheduled, awaiting move-out
- MOVE_OUT_INSPECTION: Conducting scope inspection
- IN_PROGRESS: Make-ready tasks underway
- FINAL_INSPECTION: All tasks complete, pending QC
- READY: Unit cleared for marketing/move-in
- COMPLETED: New tenant moved in

TRANSITIONS:
- Define all valid state transitions
- Trigger conditions (automatic vs manual)
- Guard conditions (prerequisites)
- Actions on transition (notifications, task creation)
```

Include:
- State diagram (Mermaid or ASCII)
- Transition rules table
- Rollback/exception handling

---

### Section 3: Task State Machine

Define the state machine for individual turn tasks:

```
STATES:
- PENDING: Created but not yet actionable
- BLOCKED: Waiting on dependencies
- READY: Available for assignment
- ASSIGNED: Assigned to vendor/tech
- IN_PROGRESS: Work started
- COMPLETED: Work finished
- VERIFIED: QC passed
- FAILED: QC failed, needs rework
- CANCELLED: Task no longer needed
```

Include:
- Dependency resolution algorithm
- Parallel vs sequential task handling
- Auto-unblock when dependencies complete

---

### Section 4: Kanban Board UI Specification

#### 4.1 Board Layout Options

**Option A: Columns by Turn Status**
```
| NOTICE | INSPECTION | IN PROGRESS | FINAL CHECK | READY |
|--------|------------|-------------|-------------|-------|
| Unit A |            | Unit B      |             | Unit C|
|        |            | Unit D      |             |       |
```

**Option B: Rows by Unit, Columns by Task Category**
```
| Unit    | Cleaning | Painting | Repairs | HVAC | Inspection |
|---------|----------|----------|---------|------|------------|
| Unit A  | ✅       | 🔄       | ⏳      | ✅   | ⏳         |
| Unit B  | ✅       | ✅       | ✅      | ✅   | 🔄         |
```

Specify:
- Default view and toggle options
- Responsive design (desktop, tablet, mobile)
- Color coding scheme for statuses
- Card content (what info shows on each unit card)

#### 4.2 Unit Card Design

Define card elements:
```
┌─────────────────────────────────┐
│ [Unit #] [Property Name]    🔴  │  ← Status indicator
│ Move-out: Jan 15 | Move-in: Jan 22 │
│ Days remaining: 7               │
│ ━━━━━━━━━━━━━━━━ 60%           │  ← Progress bar
│ Tasks: 3/5 complete             │
│ Blockers: Painting (vendor)     │  ← Blocker alert
│ [Expand] [Assign] [Complete]    │  ← Action buttons
└─────────────────────────────────┘
```

#### 4.3 Interactions

Specify UX for:
- Drag-and-drop cards between columns
- Click to expand task list
- Inline status updates
- Quick-assign vendor dropdown
- Filter/search (by property, status, date range)
- Sort options (urgency, move-in date, % complete)

---

### Section 5: Task Dependency System

#### 5.1 Dependency Types
- **BLOCKS**: Task A must complete before Task B can start
- **SOFT_DEPENDS**: Task B can start, but Task A should ideally finish first
- **PARALLEL**: Tasks can run simultaneously

#### 5.2 Dependency Graph Algorithm
```
Input: List of tasks with dependencyIds
Output: Ordered execution plan with parallelization

Algorithm:
1. Build directed acyclic graph (DAG)
2. Topological sort
3. Identify parallel execution groups
4. Handle circular dependency detection
```

#### 5.3 Visualization
- Show dependency arrows/lines on board
- Lock icon on blocked tasks
- Tooltip showing what task is blocking

---

### Section 6: Auto-Assignment Engine

#### 6.1 Assignment Rules DSL

Define a rule language for auto-assignment:
```yaml
rule: "carpet-cleaning-urgent"
  condition:
    task_type: "carpet_cleaning"
    days_until_move_in: "< 5"
  action:
    assign_to: "Vendor-Express-Clean"
    priority: "high"
    
rule: "default-cleaning"
  condition:
    task_type: "cleaning"
  action:
    assign_to: "round_robin"
    vendor_pool: ["Vendor-A", "Vendor-B", "Vendor-C"]
```

#### 6.2 Vendor Selection Algorithm

Factors to consider:
- Vendor availability (calendar integration)
- Vendor rating/score
- Cost (hourly rate, flat rate)
- Distance/location (for routing)
- Skill match (task type to vendor specialization)
- Workload balance

Scoring formula:
```
score = (w1 * rating) + (w2 * availability) + (w3 * cost_efficiency) + (w4 * proximity)
```

#### 6.3 Scheduling Calendar

- Tech/vendor calendar view
- Drag-drop task scheduling
- Conflict detection
- Route optimization (optional)

---

### Section 7: Template System

#### 7.1 Turn Template Schema

```json
{
  "templateId": "string",
  "name": "string",
  "description": "string",
  "unitType": "enum (studio, 1br, 2br, 3br, sfr)",
  "propertyType": "enum (multifamily, sfr, commercial)",
  "estimatedDuration": "number (days)",
  "estimatedCost": "number",
  "tasks": [
    {
      "templateTaskId": "string",
      "name": "string",
      "category": "enum (cleaning, painting, repairs, hvac, inspection, other)",
      "defaultDurationHours": "number",
      "defaultCost": "number",
      "dependsOn": ["templateTaskId"],
      "isRequired": "boolean",
      "vendorType": "string",
      "checklistItems": ["string"]
    }
  ]
}
```

#### 7.2 Template Management UI

- Create/edit/delete templates
- Clone and customize
- Set as default per unit type
- Version history

#### 7.3 Template Application

When a turn is created:
1. Match unit to appropriate template
2. Copy template tasks to turn tasks
3. Adjust dates based on move-out/move-in
4. Apply property-specific overrides

---

### Section 8: Complete Data Model

#### 8.1 Entity Definitions

**UnitTurn**
```typescript
interface UnitTurn {
  id: string;
  unitId: string;
  propertyId: string;
  previousLeaseId: string;
  nextLeaseId?: string;
  status: TurnStatus;
  moveOutDate: Date;
  moveInDate?: Date;
  templateId?: string;
  priority: 'low' | 'medium' | 'high' | 'critical';
  estimatedCost: number;
  actualCost: number;
  estimatedDuration: number; // days
  actualDuration?: number;
  inspectionNotes?: string;
  createdAt: Date;
  updatedAt: Date;
  completedAt?: Date;
}
```

**TurnTask**
```typescript
interface TurnTask {
  id: string;
  unitTurnId: string;
  templateTaskId?: string;
  name: string;
  description?: string;
  category: TaskCategory;
  status: TaskStatus;
  assigneeType: 'vendor' | 'staff' | 'unassigned';
  assigneeId?: string;
  scheduledStart?: Date;
  scheduledEnd?: Date;
  actualStart?: Date;
  actualEnd?: Date;
  estimatedCost: number;
  actualCost?: number;
  estimatedHours: number;
  actualHours?: number;
  dependencyIds: string[];
  priority: number;
  checklistItems: ChecklistItem[];
  photos: Photo[];
  notes: string[];
  createdAt: Date;
  updatedAt: Date;
}
```

**Vendor**
```typescript
interface Vendor {
  id: string;
  name: string;
  email: string;
  phone: string;
  specializations: TaskCategory[];
  serviceArea: GeoArea;
  rating: number; // 1-10
  totalJobs: number;
  avgCompletionTime: number; // hours
  avgCostVariance: number; // % over/under estimate
  status: 'active' | 'inactive' | 'suspended';
  hourlyRate?: number;
  flatRates: { [taskType: string]: number };
}
```

#### 8.2 Relationships

```
Unit (1) ←→ (many) UnitTurn
UnitTurn (1) ←→ (many) TurnTask
TurnTask (many) ←→ (1) Vendor
TurnTemplate (1) ←→ (many) TemplateTask
Property (1) ←→ (many) Unit
```

#### 8.3 Indexes

Specify indexes for performance:
- UnitTurn: (propertyId, status), (moveInDate), (status, priority)
- TurnTask: (unitTurnId, status), (assigneeId, status), (scheduledStart)

---

### Section 9: Metrics & Analytics Dashboard

#### 9.1 Key Performance Indicators

| KPI | Calculation | Target |
|-----|-------------|--------|
| Avg Turn Time | avg(completedAt - moveOutDate) | < 3 days (MF), < 10 days (SFR) |
| Turn Cost | sum(task.actualCost) + vacancy_loss | < $3,000/unit |
| Vacancy Days | moveInDate - moveOutDate | Minimize |
| On-Time Completion | turns completed by moveInDate / total | > 95% |
| Task Completion Rate | tasks on-time / total tasks | > 90% |
| Vendor SLA Compliance | tasks meeting SLA / total | > 90% |

#### 9.2 Dashboard Visualizations

- **Turn Pipeline**: Funnel showing units at each stage
- **Timeline**: Gantt chart of active turns
- **Cost Analysis**: Actual vs estimated by category
- **Vendor Leaderboard**: Ranked by score
- **Trend Charts**: Turn time, cost over months
- **Heat Map**: Properties with most turns

#### 9.3 Report Types

- Daily Turn Status Summary
- Weekly Performance Report
- Monthly Cost Analysis
- Vendor Performance Scorecard
- Property-level Turn Analytics

---

### Section 10: Notification & Escalation System

#### 10.1 Notification Events

| Event | Recipients | Channels | Timing |
|-------|------------|----------|--------|
| Turn Created | PM, Maintenance Lead | Email, Push | Immediate |
| Task Assigned | Vendor/Tech | Email, SMS, Push | Immediate |
| Task Started | PM | Push | Immediate |
| Task Completed | PM, Next Assignee | Push | Immediate |
| Task Overdue | PM, Supervisor, Vendor | Email, SMS | At due + 1hr |
| Inspection Failed | PM, Maintenance | Push, SMS | Immediate |
| Unit Ready | Leasing | Email, Push | Immediate |
| 3 Days to Move-In | All stakeholders | Email | Daily |
| Turn Complete | PM, Leasing, Owner | Email | Immediate |

#### 10.2 Escalation Rules

```yaml
escalation_policy:
  - trigger: "task_overdue"
    delay: "1 hour"
    action: "notify_assignee"
    
  - trigger: "task_overdue"
    delay: "4 hours"
    action: "notify_supervisor"
    
  - trigger: "task_overdue"
    delay: "24 hours"
    action: "reassign_and_alert_manager"
    
  - trigger: "turn_at_risk"
    condition: "days_until_move_in < 3 AND completion_pct < 80"
    action: "critical_alert_all"
```

#### 10.3 Notification Templates

Provide templates for:
- Task assignment (vendor)
- Overdue reminder
- Escalation alert
- Daily summary
- Unit ready notification

---

### Section 11: Integration Specifications

#### 11.1 PMS Integration

**Inbound (from PMS)**
- Lease termination notices → Create turn
- Move-out dates → Update turn schedule
- Unit data → Turn context

**Outbound (to PMS)**
- Turn status updates
- Unit availability flag
- Cost reconciliation

#### 11.2 Work Order System

- Create work orders from turn tasks
- Sync status bidirectionally
- Link photos/notes

#### 11.3 Vendor Portal API

```
POST /api/vendor/tasks/{taskId}/accept
POST /api/vendor/tasks/{taskId}/start
POST /api/vendor/tasks/{taskId}/complete
POST /api/vendor/tasks/{taskId}/photos
GET  /api/vendor/tasks?status=assigned
```

#### 11.4 Inspection App

- Offline-capable mobile inspection
- Photo capture with annotations
- Checklist completion
- Sync on reconnect

#### 11.5 Accounting Integration

- Vendor invoice creation
- Cost coding by category
- Budget tracking

---

### Section 12: Mobile App Requirements

#### 12.1 Field Tech App

- View assigned tasks
- Update task status
- Capture photos
- Add notes
- Offline mode with sync
- Push notifications
- GPS check-in/out (optional)

#### 12.2 Vendor App

- Accept/decline assignments
- View task details and history
- Update progress
- Submit completion with photos
- Invoice submission

#### 12.3 Manager App

- Board overview (simplified)
- Approve/reassign tasks
- View alerts
- Quick status updates

---

### Section 13: Real-Time Updates Architecture

#### 13.1 WebSocket Events

```typescript
// Events to broadcast
type BoardEvent = 
  | { type: 'TURN_CREATED', turn: UnitTurn }
  | { type: 'TURN_STATUS_CHANGED', turnId: string, newStatus: TurnStatus }
  | { type: 'TASK_STATUS_CHANGED', taskId: string, newStatus: TaskStatus }
  | { type: 'TASK_ASSIGNED', taskId: string, assigneeId: string }
  | { type: 'TASK_PROGRESS', taskId: string, progress: number }
```

#### 13.2 Subscription Model

- Subscribe to property-level updates
- Subscribe to specific turn
- Subscribe to vendor's tasks

#### 13.3 Optimistic Updates

- UI updates immediately on user action
- Rollback on server failure

---

### Section 14: API Specification

#### 14.1 Turn Board Endpoints

```
# Turns
GET    /api/turns?propertyId=&status=&dateRange=
POST   /api/turns
GET    /api/turns/{turnId}
PATCH  /api/turns/{turnId}
DELETE /api/turns/{turnId}

# Turn Tasks
GET    /api/turns/{turnId}/tasks
POST   /api/turns/{turnId}/tasks
PATCH  /api/turns/{turnId}/tasks/{taskId}
POST   /api/turns/{turnId}/tasks/{taskId}/assign
POST   /api/turns/{turnId}/tasks/{taskId}/complete

# Templates
GET    /api/templates
POST   /api/templates
GET    /api/templates/{templateId}
PATCH  /api/templates/{templateId}
POST   /api/templates/{templateId}/apply?turnId=

# Analytics
GET    /api/analytics/turns?propertyId=&dateRange=
GET    /api/analytics/vendors/{vendorId}
GET    /api/analytics/kpis
```

#### 14.2 Request/Response Examples

Provide full examples for key endpoints.

---

### Section 15: Security Requirements

- Role-based access (PM, Supervisor, Tech, Vendor, Leasing)
- Property-level data isolation
- Vendor can only see assigned tasks
- Audit log for all status changes
- Photo access controls

---

### Section 16: Performance Requirements

| Metric | Target |
|--------|--------|
| Board Load Time | < 2 seconds |
| Task Update Latency | < 500ms |
| Real-time Sync | < 1 second |
| Concurrent Users | 100+ per property |
| Board with 100 turns | < 3 second render |

---

### Section 17: Testing Requirements

#### 17.1 Unit Tests
- State machine transitions
- Dependency resolution
- Auto-assignment scoring

#### 17.2 Integration Tests
- PMS sync
- Vendor portal flow
- Notification delivery

#### 17.3 E2E Tests
- Full turn lifecycle
- Multi-user collaboration
- Mobile app flows

---

### Section 18: Implementation Roadmap

#### Phase 1: MVP (Weeks 1-4)
- Basic turn board UI
- Manual task creation
- Status tracking
- Simple notifications

#### Phase 2: Automation (Weeks 5-8)
- Template system
- Auto-task generation
- Dependency handling
- Basic analytics

#### Phase 3: Intelligence (Weeks 9-12)
- Auto-assignment engine
- Vendor scoring
- Advanced analytics
- Mobile apps

#### Phase 4: Optimization (Weeks 13-16)
- AI-powered scheduling
- Predictive analytics
- Route optimization
- Advanced integrations

---

## 📁 Output Location

Save your completed specification to:
```
knowledge/operations/ES-AF-005-unit-turn-board.md
```

---

## ✅ Definition of Done

Your specification is complete when it provides:
1. Complete state machines (turn + task)
2. Detailed UI wireframes/specs
3. Full data model with schemas
4. All API endpoints documented
5. Integration contracts defined
6. Performance requirements specified
7. Implementation roadmap with phases

---

## 🔄 After Completing

1. Save to `knowledge/operations/ES-AF-005-unit-turn-board.md`
2. Update `STATUS.md` - Mark Stage 3 complete for GAP-AF-005
3. Update `docs/PIPELINE_TRACKER.md`
4. Commit and push:
```bash
git add -A
git commit -m "Stage 3 COMPLETE: GAP-AF-005 Unit Turn Board Engineering Spec"
git push
```

---

**Reference**: The knowledge document is at `knowledge/operations/KD-AF-005-unit-turn-board.md`

