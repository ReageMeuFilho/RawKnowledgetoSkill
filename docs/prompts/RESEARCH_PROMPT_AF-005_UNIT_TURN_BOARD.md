# Stage 1 Research Prompt: Unit Turn Board Design

> **Gap ID**: GAP-AF-005
> **Skill ID**: SKILL-257 (unit-turn-board)
> **Priority**: P0 (MVP Critical)
> **Category**: operations
> **Created**: January 2026

---

## 📋 QUICK START

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-AF-005 (Unit Turn Board Design)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology  
3. This prompt - Detailed research questions

SAVE OUTPUT TO:
knowledge/operations/KD-AF-005-unit-turn-board.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-AF-005
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-AF-005 Unit Turn Board Design" && git push
```

---

## 🎯 EXECUTIVE SUMMARY

### What is a Unit Turn Board?

A **Unit Turn Board** is a visual dashboard that manages the **make-ready process** when a resident moves out and a new resident moves in. It coordinates all tasks required to prepare a unit for the next occupant: cleaning, painting, repairs, inspections, and move-in preparation.

In multifamily property management, the **unit turn process** is CRITICAL because:
- **Every day a unit is vacant = lost revenue** (typically $50-150/day depending on market)
- Complex coordination needed between **multiple vendors** (cleaners, painters, maintenance, carpet)
- **Dependency management** - paint can't start until repairs are done
- **Timeline pressure** - new resident often has a move-in date

### Why This Matters

| Without Unit Turn Board | With Unit Turn Board |
|------------------------|---------------------|
| Manual coordination via spreadsheets | Visual drag-drop workflow |
| Vendors call to ask "what's next?" | Automated task assignment |
| Units sit vacant waiting for next step | Parallel task execution |
| No visibility into bottlenecks | Real-time progress tracking |
| Average turn: 7-14 days | Target turn: 3-5 days |

### Primary Research Reference: AppFolio

AppFolio's **Unit Turn Board** is the industry leader. Their visual dashboard allows property managers to:
- See all turns at once by status
- Assign tasks to vendors/staff
- Track turn time metrics
- Identify bottlenecks

---

## 🔬 RESEARCH QUESTIONS

### Section 1: Turn Process Workflow

**CRITICAL**: Understand the end-to-end unit turn process.

#### 1.1 Move-Out Triggers
- When does a unit enter the turn process?
- How is move-out date captured (notice, lease end, eviction)?
- What data is inherited from the vacating resident?
- How early can turn prep begin (pre-move-out inspection)?

#### 1.2 Pre-Move-Out Activities
- What can happen BEFORE the resident leaves?
- Pre-move-out inspection process
- Security deposit assessment
- Key return handling

#### 1.3 Post-Move-Out Stages
- What are the typical turn stages/statuses?
- Common sequence:
  ```
  Move-Out → Inspection → Repairs → Paint → Clean → Final Inspection → Move-In Ready
  ```
- Can stages run in parallel?
- What triggers stage transitions?

---

### Section 2: Board Structure & Visualization

#### 2.1 Kanban Design
- How is the board visually organized?
- Column-based (by status) vs Row-based (by unit)?
- Card design - what info shows on each unit card?
- Color coding (by status, priority, overdue)?

#### 2.2 Task Categories
Research the standard task categories:

| Category | Typical Tasks | Avg Duration |
|----------|--------------|--------------|
| **Inspection** | Walk-through, photo documentation | ? |
| **Repairs** | Drywall, fixtures, appliances | ? |
| **Paint** | Full repaint vs touch-up | ? |
| **Flooring** | Carpet clean/replace, hardwood refinish | ? |
| **Cleaning** | Deep clean, appliance detail | ? |
| **Final** | Quality check, photo staging | ? |

#### 2.3 Dependency Management
- How are task dependencies represented?
- Can paint start before repairs complete?
- What's the critical path logic?
- How are blockers visualized?

#### 2.4 Priority Indicators
- How is urgency shown?
- New move-in date pressure
- Days in current stage
- Total turn time elapsed

---

### Section 3: Task Assignment Logic

#### 3.1 Vendor vs In-House
- How are tasks routed to vendors vs staff?
- Rules for assignment:
  - Task type → Vendor specialization
  - Availability checking
  - Geographic proximity (for multi-property)
  - Cost considerations

#### 3.2 Scheduling Optimization
- How are vendor schedules managed?
- Calendar integration
- Double-booking prevention
- Travel time between properties

#### 3.3 Parallel Execution
- Which tasks can run simultaneously?
- Resource conflict detection (same vendor, same time)
- Optimal task sequencing algorithms

#### 3.4 Automatic Assignment
- Can tasks auto-assign based on rules?
- Vendor performance scores affecting assignment
- Fallback logic if preferred vendor unavailable

---

### Section 4: Move-In Coordination

#### 4.1 New Resident Timeline
- How is move-in date integrated?
- Countdown to move-in displayed?
- Warning when turn is at risk of missing date?

#### 4.2 Move-In Checklist
- What needs completion before move-in?
- Utility transfers
- Key prep/lockbox setup
- Welcome package preparation
- Final walkthrough scheduling

#### 4.3 Handoff to Leasing
- When is unit marked "Ready to Show"?
- How does turn board integrate with leasing?
- Can a unit be shown during turn (with caveats)?

---

### Section 5: Data Model

#### 5.1 Unit Turn Record
```
Research what data is tracked per turn:
- Turn ID
- Unit ID
- Property ID  
- Move-out date
- Move-in date (expected)
- Turn start date
- Turn complete date
- Status
- Total turn days
- Total cost
- Tasks (list)
- Notes/photos
```

#### 5.2 Turn Task Record
```
Research what data is tracked per task:
- Task ID
- Turn ID
- Task type/category
- Description
- Assigned to (vendor/staff)
- Scheduled date/time
- Status
- Dependencies (blocked by tasks)
- Cost estimate
- Actual cost
- Completion date
- Notes/photos
```

#### 5.3 Turn Template
```
Research template structure:
- Template name (Standard Turn, Full Rehab, etc.)
- Default tasks
- Default sequence
- Estimated duration
- Estimated cost
```

---

### Section 6: Metrics & Analytics

#### 6.1 Turn Time Metrics
- **Average Turn Time**: Days from move-out to move-in ready
- **Turn Time by Stage**: Time in each status
- **Turn Time by Property**: Compare properties
- **Turn Time Trend**: Improving or degrading?

#### 6.2 Cost Metrics
- **Cost per Turn**: Total cost to make-ready
- **Cost by Category**: Paint, clean, repairs breakdown
- **Cost vs Estimate**: Variance tracking
- **Cost per Square Foot**: Normalization

#### 6.3 Vacancy Impact
- **Vacancy Days**: Total days unit unoccupied
- **Lost Revenue**: Vacancy days × daily rent
- **Turn as % of Vacancy**: How much of vacancy is "turning"?

#### 6.4 Vendor Metrics
- **Tasks by Vendor**: Workload distribution
- **On-Time Completion**: Vendor reliability
- **Cost per Vendor**: Price comparison
- **Quality Score**: Rework frequency

---

### Section 7: Notifications & Alerts

#### 7.1 Status Change Alerts
- Who is notified when task status changes?
- Notification channels (email, SMS, in-app)?
- Assignee notifications

#### 7.2 Escalation Alerts
- Task overdue triggers
- Turn at risk of missing move-in
- Cost exceeding estimate
- Dependency blocked alerts

#### 7.3 Daily Summaries
- Daily turn board digest
- Units completing today
- Units starting today
- Overdue tasks list

---

### Section 8: Integrations

#### 8.1 PMS Integration
- How does turn board sync with PMS?
- Move-out data pulled automatically?
- Work order creation from turn tasks?
- Vendor billing integration

#### 8.2 Vendor Portal
- Do vendors have portal access?
- Can vendors update task status?
- Photo upload from vendor?
- Time tracking?

#### 8.3 Mobile Access
- Mobile app for turn board?
- Field worker task updates?
- Photo documentation from mobile?
- Offline capability?

#### 8.4 Inspection Integration
- Digital inspection forms
- Photo requirements per task
- Before/after documentation
- Compliance checklist

---

### Section 9: Competitive Analysis

#### 9.1 AppFolio (Primary)
- Unit Turn Board features
- Visual design approach
- Metrics provided
- Limitations

#### 9.2 Yardi
- Turn management approach
- Strengths/weaknesses

#### 9.3 RentManager
- Turn features
- Differentiation

#### 9.4 Buildium
- Turn workflow
- Market positioning

#### 9.5 Property Meld
- Turn integration with maintenance
- Any unique approaches?

---

### Section 10: Best Practices

#### 10.1 Turn Optimization Strategies
- Pre-move-out inspections
- Bulk vendor contracts
- Standard turn packages
- Concurrent task execution

#### 10.2 Common Bottlenecks
- Vendor availability
- Material procurement
- Weather delays (exterior)
- Scope creep

#### 10.3 Industry Benchmarks
- Average turn time by market
- Cost per turn by property type
- Best-in-class targets

---

## 📚 PRIMARY SOURCES

### Must Check
- [ ] **AppFolio Help Center** - Unit Turn Board documentation
- [ ] **AppFolio Blog** - Turn management best practices
- [ ] **YouTube**: "AppFolio unit turn board", "make ready process property management"
- [ ] **YouTube**: "Multifamily unit turn optimization"
- [ ] **NARPM** - National Association of Residential Property Managers resources
- [ ] **Multifamily Executive Magazine** - Turn process articles

### Secondary Sources
- [ ] Yardi turn management docs
- [ ] RentManager resources
- [ ] Property Meld blog (may have turn content)
- [ ] Buildium turn features

### Industry Research
- [ ] Multifamily operations studies
- [ ] Turn time benchmarking reports
- [ ] Vacancy cost analysis

### Community Sources
- [ ] Reddit: r/PropertyManagement "unit turn"
- [ ] BiggerPockets forums "make ready"
- [ ] LinkedIn multifamily groups

---

## ✅ DEFINITION OF DONE

Your knowledge document is complete when you can answer:

1. **Workflow**
   - [ ] What are the standard turn stages?
   - [ ] What triggers each stage transition?
   - [ ] What tasks can run in parallel?

2. **Board Design**
   - [ ] How is the visual board structured?
   - [ ] What information appears on unit cards?
   - [ ] How are dependencies shown?

3. **Assignment**
   - [ ] How are tasks assigned to vendors?
   - [ ] What scheduling logic is used?
   - [ ] Can assignments be automated?

4. **Metrics**
   - [ ] What KPIs are tracked?
   - [ ] What are industry benchmarks?
   - [ ] How is cost tracked?

5. **Data Model**
   - [ ] Turn record schema defined
   - [ ] Task record schema defined
   - [ ] Template structure defined

6. **Integrations**
   - [ ] PMS sync documented
   - [ ] Vendor portal features
   - [ ] Mobile access capabilities

---

## 📝 OUTPUT FORMAT

Save your research to: `knowledge/operations/KD-AF-005-unit-turn-board.md`

Use this structure:

```markdown
# Knowledge Document: Unit Turn Board Design

> **Gap ID**: GAP-AF-005
> **Skill ID**: SKILL-257
> **Priority**: P0 (MVP)
> **Stage**: 1 - Research
> **Researcher**: [Your Name/ID]
> **Date**: [Date]
> **Quality Target**: 9.0/10

---

## Executive Summary
[2-3 paragraphs summarizing key findings]

## 1. Turn Process Workflow
### 1.1 Move-Out Triggers
[Research findings with citations]

### 1.2 Pre-Move-Out Activities
[Research findings]

### 1.3 Post-Move-Out Stages
[Research findings]

## 2. Board Structure & Visualization
[Detailed findings]

## 3. Task Assignment Logic
[Detailed findings]

## 4. Move-In Coordination
[Detailed findings]

## 5. Data Model
[Schema definitions with JSON examples]

## 6. Metrics & Analytics
[KPIs and benchmarks]

## 7. Notifications & Alerts
[Alert types and triggers]

## 8. Integrations
[Integration requirements]

## 9. Competitive Analysis
[AppFolio vs others]

## 10. Best Practices
[Optimization strategies]

## References
[All sources with URLs]
```

---

## 🎯 SUCCESS CRITERIA

| Criteria | Target |
|----------|--------|
| **Citations** | 25+ authoritative sources |
| **Completeness** | All 10 sections addressed |
| **Technical Depth** | Data models, workflows, metrics |
| **Practical** | Actionable for engineering |
| **Quality** | 9.0/10 minimum rating |

---

## 📊 CONTEXT: How This Fits the Pipeline

```
GAP-AF-002 (AI Maintenance Coordinator) ✅ COMPLETE
    └── SKILL-254: Handles reactive maintenance
    └── Work order lifecycle

GAP-VEN-001 (Maintenance Brain) 🔄 IN PROGRESS
    └── SKILL-270-272: Intelligent learning for maintenance
    └── Vendor optimization

GAP-AF-005 (Unit Turn Board) ⏳ YOU ARE HERE
    └── SKILL-257: Proactive make-ready coordination
    └── Visual workflow management

Together: Complete Maintenance & Turn Operations
```

---

## 💡 RESEARCH TIPS

### Key Terms to Search
- "Unit turn" / "Unit turnover"
- "Make-ready process"
- "Apartment turn board"
- "Multifamily turn time"
- "Vacancy turn"
- "Turn cost"

### Video Resources Often Rich
- AppFolio webinars
- Multifamily operations conferences
- Property management training videos

### Industry Context
- **Typical turn time**: 5-10 days (varies by market)
- **Cost per turn**: $500-2,000+ depending on scope
- **Critical KPI**: Every day matters ($50-150/day lost revenue)

---

**Good luck! This is a P0 skill critical for MVP operations. 🏠**

