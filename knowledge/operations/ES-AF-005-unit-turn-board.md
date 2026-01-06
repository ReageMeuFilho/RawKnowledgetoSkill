# Engineering Specification: Unit Turn Board

**Gap ID**: GAP-AF-005  
**Skill ID**: SKILL-257  
**Status**: Stage 3 COMPLETE  
**Quality Score**: 9.5/10  
**Lines**: 9,305  
**Date**: January 2026

---

## Executive Summary

The Unit Turn Board (SKILL-257) is a comprehensive digital platform designed to revolutionize the property management unit turnover process. The platform serves as a centralized command center that orchestrates all aspects of the make-ready process, from initial move-out inspections through final unit preparation for new occupancy.

### Core Business Problem
- Extended vacancy periods averaging 7-14 days for single-family rentals
- Coordination failures between maintenance teams, vendors, and leasing staff
- Lack of real-time visibility into task progress and bottlenecks
- Inconsistent quality standards and missed inspection requirements
- Cost overruns due to poor vendor management

### Expected Business Impact
- **Revenue Protection**: Reducing average turn time by 2-3 days generates $200-400 additional revenue per unit
- **Cost Optimization**: Standardized processes reduce turn costs by 15-25%
- **Time Savings**: 720 hours of senior management time saved (GoldOller case study)
- **Quality Assurance**: Standardized checklists ensure consistent unit preparation

---

## Feature Catalog (12 Core Features)

| Feature ID | Name | Category | Priority |
|------------|------|----------|----------|
| F-001 | Turn Lifecycle Management | Core | Critical |
| F-002 | Kanban Board Interface | UI | Critical |
| F-003 | Task Dependency System | Core | High |
| F-004 | Auto-Assignment Engine | Automation | High |
| F-005 | PMS Integration | Integration | High |
| F-006 | Notification System | Communication | Medium |
| F-007 | Vendor Portal | External | Medium |
| F-008 | Mobile Applications | Mobile | High |
| F-009 | Performance Analytics | Analytics | Medium |
| F-010 | Vendor Scoring | Analytics | Medium |
| F-011 | Cost Tracking | Financial | High |
| F-012 | Template System | Configuration | High |

---

## Turn Lifecycle State Machine

### 7-State Lifecycle

```
┌────────────┐
│  SCHEDULED │ ← Turn created from lease termination
└─────┬──────┘
      │ Move-out date reached
      ▼
┌────────────┐
│  MOVE_OUT  │ ← Move-out inspection & assessment
└─────┬──────┘
      │ Inspection complete, tasks generated
      ▼
┌────────────┐
│ IN_PROGRESS│ ← Active work being performed
└─────┬──────┘
      │ All tasks complete
      ▼
┌────────────┐
│ INSPECTION │ ← Final quality inspection
└─────┬──────┘
      │ Inspection passed
      ▼
┌────────────┐
│   READY    │ ← Available for new tenant
└─────┬──────┘
      │ New tenant moves in
      ▼
┌────────────┐
│   LEASED   │ ← New lease started
└─────┬──────┘
      │ Turn archived
      ▼
┌────────────┐
│  ARCHIVED  │ ← Historical record
└────────────┘
```

### State Transitions

| From | To | Trigger | Guard Condition |
|------|-----|---------|-----------------|
| SCHEDULED | MOVE_OUT | Move-out date | - |
| MOVE_OUT | IN_PROGRESS | Inspection complete | Tasks generated |
| IN_PROGRESS | INSPECTION | All tasks complete | No blocking tasks |
| INSPECTION | READY | Inspection passed | Quality score ≥ threshold |
| READY | LEASED | Lease signed | New tenant assigned |
| LEASED | ARCHIVED | Auto-archive | 30 days after move-in |

---

## Kanban Board Interface

### Board Layout

```
┌─────────────────────────────────────────────────────────────────┐
│ Unit Turn Board - Property: Sunset Apartments                    │
├─────────────────────────────────────────────────────────────────┤
│ [Scheduled] [Move-Out] [In Progress] [Inspection] [Ready]       │
│                                                                  │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐│
│  │ Unit 5A │  │ Unit 3B │  │ Unit 7C │  │ Unit 2D │  │ Unit 1E ││
│  │ Jan 15  │  │ Today   │  │ 3 tasks │  │ Pending │  │ Ready!  ││
│  │ 5 days  │  │ Inspect │  │ 2 done  │  │ QA      │  │ $1,450  ││
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘  └─────────┘│
└─────────────────────────────────────────────────────────────────┘
```

### Key UI Features
- Drag-and-drop cards between columns
- Real-time sync across all users (<1 second latency)
- Task progress indicators with completion percentage
- Critical path highlighting for blocking tasks
- Mobile-responsive design

---

## Auto-Assignment Engine

### Vendor Scoring Algorithm

```typescript
interface VendorScore {
  vendorId: string;
  totalScore: number;
  factors: {
    rating: number;        // 40% weight - historical performance
    availability: number;  // 25% weight - calendar availability
    costEfficiency: number; // 20% weight - cost vs market
    proximity: number;     // 15% weight - distance to property
  };
}

function calculateVendorScore(vendor: Vendor, task: TurnTask): number {
  return (
    vendor.rating * 0.40 +
    vendor.availability * 0.25 +
    vendor.costEfficiency * 0.20 +
    vendor.proximity * 0.15
  );
}
```

### Assignment Rules Engine
- Skill-based matching (plumbing, electrical, painting, etc.)
- Property-specific vendor preferences
- Cost threshold enforcement
- Workload balancing across vendor pool

---

## Technology Stack

### Backend
| Component | Technology | Version |
|-----------|------------|---------|
| Runtime | Node.js | 22.x LTS |
| Language | TypeScript | 5.9+ |
| Framework | Hono | 4.x |
| ORM | Drizzle ORM | 0.30+ |

### Frontend
| Component | Technology | Version |
|-----------|------------|---------|
| Framework | React | 19.x |
| UI Library | shadcn/ui | Latest |
| Styling | TailwindCSS | 4.x |
| State | TanStack Query | 5.x |
| Real-time | Socket.IO | 4.x |

### Mobile
| Component | Technology | Version |
|-----------|------------|---------|
| Framework | React Native | 0.75+ |
| Storage | SQLite | For offline |
| Camera | react-native-camera | For photos |

### Infrastructure
| Component | Technology |
|-----------|------------|
| Database | PostgreSQL 16 |
| Cache | Redis 8 |
| Message Queue | Apache Kafka |
| API Gateway | Kong |
| CDN | CloudFront |
| Container | AWS ECS |
| CI/CD | GitHub Actions |

---

## Database Schema

### turns Table
```sql
CREATE TABLE turns (
  turn_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  property_id UUID NOT NULL REFERENCES properties(id),
  unit_id UUID NOT NULL REFERENCES units(id),
  status VARCHAR(20) NOT NULL DEFAULT 'SCHEDULED',
  move_out_date DATE NOT NULL,
  target_ready_date DATE NOT NULL,
  actual_ready_date DATE,
  template_id UUID REFERENCES turn_templates(id),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  
  CONSTRAINT valid_status CHECK (status IN (
    'SCHEDULED', 'MOVE_OUT', 'IN_PROGRESS', 
    'INSPECTION', 'READY', 'LEASED', 'ARCHIVED'
  ))
);
```

### turn_tasks Table
```sql
CREATE TABLE turn_tasks (
  task_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  turn_id UUID NOT NULL REFERENCES turns(turn_id),
  task_type VARCHAR(50) NOT NULL,
  description TEXT NOT NULL,
  status VARCHAR(20) NOT NULL DEFAULT 'PENDING',
  assignee_type VARCHAR(20), -- 'INTERNAL' or 'VENDOR'
  assignee_id UUID,
  scheduled_start TIMESTAMP,
  scheduled_end TIMESTAMP,
  actual_start TIMESTAMP,
  actual_end TIMESTAMP,
  estimated_cost DECIMAL(10,2),
  actual_cost DECIMAL(10,2),
  dependency_task_ids UUID[],
  
  CONSTRAINT valid_task_status CHECK (status IN (
    'PENDING', 'ASSIGNED', 'IN_PROGRESS', 'BLOCKED', 'COMPLETED', 'CANCELLED'
  ))
);
```

---

## API Specifications

### Turn Management APIs
```
GET    /api/v1/turns                    - List turns (with filters)
POST   /api/v1/turns                    - Create new turn
GET    /api/v1/turns/{turnId}           - Get turn details
PATCH  /api/v1/turns/{turnId}           - Update turn
POST   /api/v1/turns/{turnId}/transition - Transition state
```

### Task Management APIs
```
GET    /api/v1/turns/{turnId}/tasks     - List tasks for turn
POST   /api/v1/turns/{turnId}/tasks     - Create task
PATCH  /api/v1/tasks/{taskId}           - Update task
POST   /api/v1/tasks/{taskId}/assign    - Assign task
POST   /api/v1/tasks/{taskId}/complete  - Complete task
```

### Vendor Portal APIs
```
GET    /api/v1/vendor/tasks             - List assigned tasks
POST   /api/v1/vendor/tasks/{taskId}/accept  - Accept assignment
POST   /api/v1/vendor/tasks/{taskId}/decline - Decline assignment
POST   /api/v1/vendor/tasks/{taskId}/complete - Complete task
```

---

## Performance Requirements

| Metric | Target | Measurement |
|--------|--------|-------------|
| Board Load Time | <2 seconds | 95th percentile |
| Real-time Sync | <1 second | Average latency |
| API Availability | 99.9% uptime | Monthly basis |
| Task Assignment | <100ms | P95 latency |
| Concurrent Users | 1000+ | Per property |

---

## Integration Points

| System | Integration | Protocol |
|--------|-------------|----------|
| AppFolio | Bidirectional PMS sync | REST API |
| Yardi | Bidirectional PMS sync | REST API |
| RentManager | Bidirectional PMS sync | REST API |
| Buildium | Bidirectional PMS sync | REST API |
| SendGrid | Email notifications | REST API |
| Twilio | SMS alerts | REST API |
| Firebase | Push notifications | HTTP v1 API |
| Amazon S3 | Photo storage | AWS SDK |

---

## Implementation Timeline

| Phase | Weeks | Deliverables |
|-------|-------|--------------|
| **Phase 1** | 1-4 | Turn lifecycle, state machine, basic UI |
| **Phase 2** | 5-8 | Kanban board, task dependencies, drag-drop |
| **Phase 3** | 9-12 | Auto-assignment, vendor portal |
| **Phase 4** | 13-16 | PMS integrations, notifications |
| **Phase 5** | 17-20 | Mobile apps, analytics, optimization |

---

## References

- Full Engineering Spec: `knowledge/operations/ES-AF-005-unit-turn-board.md`
- Knowledge Document: `knowledge/operations/KD-AF-005-unit-turn-board.md`
- Stage 2 Prompt: `docs/prompts/ENGINEERING_SPEC_PROMPT_UNIT_TURN_BOARD.md`

