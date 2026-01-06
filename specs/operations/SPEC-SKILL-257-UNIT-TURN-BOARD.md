# Skill Specification: Unit Turn Board

**Skill ID**: SKILL-257  
**Gap ID**: GAP-AF-005  
**Status**: ✅ SPECIFIED  
**Date**: January 2026  
**Engineering Spec**: `knowledge/operations/ES-AF-005-unit-turn-board.md` (9,305 lines)

---

## Skill Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Unit Turn Board |
| **Category** | operations |
| **Priority** | P0 (MVP) |
| **Effort** | L (16-20 weeks) |
| **Best Implementation** | AppFolio Unit Turn Board + HappyCo Make Ready |

---

## Description

Comprehensive digital platform for managing the unit turnover process between tenant move-out and new tenant move-in. Features a Kanban-style visual board with 7-state turn lifecycle, intelligent task orchestration with dependency management, auto-assignment engine for vendors, and real-time sync across web and mobile platforms.

---

## Key Features

### 1. Turn Lifecycle Management (7 States)

| State | Description | Auto-Trigger |
|-------|-------------|--------------|
| **SCHEDULED** | Turn created from lease termination | PMS event |
| **MOVE_OUT** | Move-out inspection & assessment | Date reached |
| **IN_PROGRESS** | Active work being performed | Inspection complete |
| **INSPECTION** | Final quality inspection | All tasks done |
| **READY** | Available for new tenant | QA passed |
| **LEASED** | New lease started | Lease signed |
| **ARCHIVED** | Historical record | 30 days after move-in |

### 2. Kanban Board Interface

| Feature | Specification |
|---------|---------------|
| Layout | Columns by status, rows by unit |
| Interaction | Drag-and-drop between columns |
| Real-time | <1 second sync latency |
| Mobile | Fully responsive design |
| Critical Path | Blocking tasks highlighted |

### 3. Task Dependency System

- Task dependency graph with blocking/non-blocking types
- Parallel execution optimization
- Critical path calculation
- Auto-resequencing on changes

### 4. Auto-Assignment Engine

**Vendor Scoring Algorithm:**
| Factor | Weight | Calculation |
|--------|--------|-------------|
| Rating | 40% | Historical performance score |
| Availability | 25% | Calendar availability |
| Cost Efficiency | 20% | Cost vs market rate |
| Proximity | 15% | Distance to property |

### 5. Vendor Portal

- Task acceptance/decline workflow
- Progress update submission
- Photo documentation upload
- Completion reporting

### 6. Mobile Applications

- React Native (iOS + Android)
- Offline capability with SQLite
- Camera integration for photos
- GPS check-in/out

---

## Performance Targets

| Metric | Target |
|--------|--------|
| Board Load Time | <2 seconds (P95) |
| Real-time Sync | <1 second |
| API Availability | 99.9% uptime |
| Concurrent Users | 1000+ per property |
| Task Assignment | <100ms P95 |

---

## Business Impact

| Metric | Target |
|--------|--------|
| Turn Time Reduction | 2-3 days |
| Revenue Protection | $200-400/unit |
| Cost Savings | 15-25% per unit |
| Management Time Saved | 720 hours (portfolio) |

---

## Technology Stack

| Layer | Technology |
|-------|------------|
| Backend | Node.js 22, TypeScript, Hono |
| Frontend | React 19, TailwindCSS, shadcn/ui |
| Mobile | React Native 0.75+ |
| Database | PostgreSQL 16 |
| Cache | Redis 8 |
| Real-time | Socket.IO |
| API Gateway | Kong |
| Infrastructure | AWS ECS |

---

## Data Model

### Turn Entity
```json
{
  "turn_id": "UUID",
  "property_id": "UUID",
  "unit_id": "UUID",
  "status": "SCHEDULED|MOVE_OUT|IN_PROGRESS|INSPECTION|READY|LEASED|ARCHIVED",
  "move_out_date": "date",
  "target_ready_date": "date",
  "actual_ready_date": "date (nullable)",
  "template_id": "UUID (nullable)",
  "tasks": [
    {
      "task_id": "UUID",
      "task_type": "string",
      "description": "string",
      "status": "PENDING|ASSIGNED|IN_PROGRESS|BLOCKED|COMPLETED|CANCELLED",
      "assignee_type": "INTERNAL|VENDOR",
      "assignee_id": "UUID",
      "estimated_cost": "decimal",
      "actual_cost": "decimal",
      "dependency_task_ids": ["UUID"]
    }
  ],
  "costs": {
    "estimated_total": "decimal",
    "actual_total": "decimal",
    "labor": "decimal",
    "materials": "decimal",
    "vacancy_cost": "decimal"
  }
}
```

---

## Integration Points

| System | Integration | Data Flow |
|--------|-------------|-----------|
| PMS (AppFolio, Yardi) | REST API | Bidirectional |
| Accounting | Webhook | Cost sync |
| Leasing/Marketing | REST API | Availability updates |
| Email (SendGrid) | REST API | Notifications |
| SMS (Twilio) | REST API | Alerts |
| Push (Firebase) | HTTP v1 | Mobile notifications |
| Storage (S3) | AWS SDK | Photos |

---

## Template System

### Pre-built Templates
| Template | Unit Type | Tasks | Est. Duration |
|----------|-----------|-------|---------------|
| Standard | Apartment | 15-20 | 3-5 days |
| Deep Clean | Any | 25-30 | 5-7 days |
| Full Renovation | Any | 40-50 | 14-21 days |
| Quick Turn | Studio | 8-10 | 1-2 days |

### Template Features
- Inheritance support (base → custom)
- Task dependency preservation
- Version control
- Property-type specific defaults

---

## Analytics Dashboard

### Key Metrics
| Metric | Description |
|--------|-------------|
| Avg Turn Time | Days from move-out to ready |
| Turn Cost | Total cost per turn |
| Task Completion Rate | On-time completion % |
| Vendor Performance | Score by vendor |
| Vacancy Cost | Lost revenue per turn |

### Visualizations
- Turn funnel by status
- Cost trends over time
- Vendor performance comparison
- Property benchmarking

---

## Implementation Timeline

| Phase | Weeks | Deliverables |
|-------|-------|--------------|
| Phase 1 | 1-4 | Turn lifecycle, state machine, basic UI |
| Phase 2 | 5-8 | Kanban board, task dependencies |
| Phase 3 | 9-12 | Auto-assignment, vendor portal |
| Phase 4 | 13-16 | PMS integrations, notifications |
| Phase 5 | 17-20 | Mobile apps, analytics |

---

## Use Cases

### 1. Standard Unit Turn
**Trigger**: Lease termination notice received  
**Flow**: SCHEDULED → MOVE_OUT → IN_PROGRESS → INSPECTION → READY  
**Duration**: 5-7 days target

### 2. Emergency Turn
**Trigger**: Unexpected vacancy (eviction, abandonment)  
**Flow**: MOVE_OUT → IN_PROGRESS → READY (expedited)  
**Duration**: 2-3 days target

### 3. Renovation Turn
**Trigger**: Major upgrade planned  
**Flow**: Extended IN_PROGRESS with multiple inspections  
**Duration**: 14-21 days

---

## Competitive Advantage

| Feature | AppFolio | Yardi | RentManager | **CitadelOS** |
|---------|:--------:|:-----:|:-----------:|:-------------:|
| Visual Kanban | ✅ | ⚠️ | ⚠️ | ✅ |
| Auto-Assignment | ⚠️ | ❌ | ❌ | ✅ |
| Vendor Portal | ✅ | ⚠️ | ❌ | ✅ |
| Mobile Offline | ✅ | ❌ | ❌ | ✅ |
| Real-time Sync | ✅ | ⚠️ | ❌ | ✅ |
| AI Optimization | ❌ | ❌ | ❌ | ✅ |

**Differentiator**: AI-powered auto-assignment with learning vendor scoring + full real-time sync

---

## References

- Full Engineering Spec: `knowledge/operations/ES-AF-005-unit-turn-board.md`
- Knowledge Document: `knowledge/operations/KD-AF-005-unit-turn-board.md`
- Stage 2 Prompt: `docs/prompts/ENGINEERING_SPEC_PROMPT_UNIT_TURN_BOARD.md`

