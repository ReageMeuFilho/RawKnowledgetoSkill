# Knowledge Document: Unit Turn Board Design

**Gap ID**: GAP-AF-005  
**Skill ID**: SKILL-257  
**Status**: Stage 1 COMPLETE  
**Quality Score**: 8.5/10  
**Date**: January 2026  
**Sources**: 26 authoritative citations

---

## 1. Turn Process Workflow

When a tenant gives notice (often 30–90 days before lease-end), the PMS automatically creates a **unit turn** record and adds the unit to the Turn Board[1][2]. The workflow then follows key stages: **Move-Out Inspection (scope)**, parallel **Make-Ready Tasks** (cleaning, painting, repairs), **Final Inspection**, and **Unit Ready** for marketing. For example, Buildium outlines a standard turnover as: Receive keys, evaluate scope of work, dispatch vendors/in‑house staff, perform the work, and conduct a final walkthrough before marking the unit market-ready[3]. Tasks that can run in parallel are flagged accordingly; e.g. after a move-out inspection automatically triggers cleaning and painting tasks[4]. Each stage transitions when its prerequisite tasks are completed. (For instance, a "Final Inspection" stage won't start until all repair/cleaning orders are done.) In practice, task completion or approval events (or manual updates by staff) move units from one stage to the next. Software may also auto-generate follow-up work orders: AppFolio, for instance, lets you schedule recurring work orders (like a move-out inspection) that *automatically trigger* related tasks such as carpet cleaning or painting[4]. By automating and standardizing these steps, managers shorten vacancy and prevent oversight.

## 2. Board Structure & Visualization

Turn Boards are usually shown as **Kanban-style dashboards**. A common layout is columns by status (e.g. "Scheduled," "In Progress," "Completed") with each card representing a unit or task; another option is one row per unit with columns for each task category. For example, **RentManager's Make Ready Board** displays each unit as a card on the board, with color-coded indicators showing each task's status (scheduled, in progress, or completed)[5]. AppFolio's Unit Turn Board similarly consolidates all tasks for a unit into one view[6]. Each *unit card* typically shows the unit number, current turn status (e.g. "Inspection", "Needs Cleaning"), and urgency cues (often days until next lease start). It may also highlight blockers or delays (for example, a red flag if an inspection failed or a work order is overdue). Dependencies between tasks can be visualized by links or locks on cards, so teams immediately see that "Final Inspection" is blocked until all repairs are done. The board view is interactive: managers can click into a unit's card to expand its task list, update statuses, or reassign tasks. This single-pane view gives everyone—from maintenance to leasing—shared visibility into each unit's progress[6][5].

## 3. Task Assignment Logic

Tasks on the turn board can be assigned to in-house technicians or external vendors based on rules and availability. Systems allow managers to set **auto-assignment rules**: e.g. always assign standard cleaning to a particular vendor or the nearest available tech. AppFolio's Smart Maintenance uses AI to **auto-dispatch** pre-approved vendors for work orders[7]. If a resident submits a request after hours, Smart Maintenance instantly assigns it to an on-call vendor to avoid delay. For in-house crews, managers get a scheduling calendar (AppFolio's "Smart Maintenance Scheduling") where they can drag-and-drop work orders onto tech schedules[8]. This ensures no double-booking and optimal routing. Teams often build **vendor profiles** (rates, skills, ratings) to guide assignments: for instance, Buildium recommends rating vendors on price, timeliness and quality, then using those profiles to quickly pick the best vendor for each task[9]. RentManager's system even lets you define task "Actions" with priority and availability – tasks are automatically sorted so urgent items get a tech assigned first[10]. In practice, the board's assignment logic can include rules like: "assign carpet cleaning to Vendor A if vacancy < 10 days, otherwise vendor B," or round-robin among qualified vendors. Scheduling can also be optimized: the board can display each vendor/tech's planned assignments (Gantt/calendar view) so managers avoid gaps or overlaps, and it can alert if a high-priority task has no available crew.

## 4. Move-In Coordination

The Turn Board keeps leasing teams informed so they can **count down to the next move-in**. Each unit on the board shows its scheduled lease start date, so staff see "days until move-in" and know how urgently to wrap up tasks. Many systems automatically flag units that are approaching their lease start (e.g. within 3 days) in a different color. Once all turn tasks for a unit are complete and it passes final inspection, the board will mark the unit **"Turn-Ready"** or "Available." For example, AppFolio's board sends automatic updates to leasing agents as tasks finish[6]. At that point, the unit can be handed off: leasing gets a digital move-in checklist (lockbox codes, keys, condition report) and the property is opened on marketing portals. In some setups, the system may auto-generate a "Turn Complete" work order or checklist that reminds leasing to schedule showings. Alerts or dashboard summaries can also notify leasing when units become ready. In short, the turn board ties directly to move-in planning: it shows how many days until the new resident arrives, highlights readiness status, and automatically informs leasing when the unit is cleared and ready for occupancy[6].

## 5. Data Model

In a PMS, a **UnitTurn** record tracks the overall turnover, with fields like unitId, leaseEndDate, leaseStartDate, status, and a list of associated tasks. A **TurnTask** represents an individual work item within a turn (e.g. "Paint living room") and includes fields like taskId, unitTurnId, description, status, assignedTo (vendor or staff ID), scheduledDate, completedDate, estimatedCost, actualCost, and optional dependencyIds (to enforce sequence). A **TurnTemplate** defines a reusable set of tasks for a type of unit. For example, a template might be "Standard 2BR Turn" with tasks: deep-clean, HVAC service, repaint (each with default durations and costs). When a UnitTurn is created, the system can copy the relevant TurnTemplate's tasks into actual TurnTasks for that unit. (This follows RentManager's model of *Make Ready Templates* bundling prioritized *Actions* into workflows[11].)

### Example JSON Schemas

**UnitTurn Record:**
```json
{
  "unitTurnId": "UT123",
  "unitId": "Unit-1001",
  "leaseEndDate": "2025-12-31",
  "leaseStartDate": "2026-01-15",
  "status": "In Progress",
  "tasks": ["T-501","T-502","T-503"],
  "createdAt": "2025-11-01T09:00Z",
  "updatedAt": "2025-11-05T15:30Z"
}
```

**TurnTask Record:**
```json
{
  "taskId": "T-501",
  "unitTurnId": "UT123",
  "templateTaskId": "Temp-10",
  "name": "Deep Clean Carpets",
  "status": "Completed",
  "assignedTo": "Vendor-CleanCo",
  "scheduledDate": "2026-01-01",
  "completedDate": "2026-01-02",
  "estimatedCost": 150,
  "actualCost": 145,
  "dependencyIds": []
}
```

**TurnTemplate Record:**
```json
{
  "templateId": "MakeReady-Standard-2BR",
  "name": "Standard 2BR Turn",
  "description": "Standard tasks for turning a 2BR unit",
  "tasks": [
    {"templateTaskId":"Temp-10","name":"General Cleaning","defaultDurationDays":1,"defaultCost":100},
    {"templateTaskId":"Temp-11","name":"Paint Walls","defaultDurationDays":1,"defaultCost":120},
    {"templateTaskId":"Temp-12","name":"HVAC Service","defaultDurationDays":0.5,"defaultCost":80}
  ]
}
```

## 6. Metrics & Analytics

Key KPIs focus on **speed and cost of turns**. "Unit Turn Time" measures the days from move-out to new lease start[12]. Every day a unit sits vacant is lost rent, so teams aim for as few days as possible. For example, industry sources note typical targets of ~3 days in multifamily complexes and 1–2 weeks for single-family homes[13]. Turn cost (labor, materials, vendor invoices, plus vacancy loss) is another major KPI – some firms report average turnover costs around $2,500–$4,000 per unit[14][15]. Dashboards often show **vacancy days** (time from lease end to new lease start) and **cost per turn**, as these directly hit the bottom line.

Turnover analytics drill into sub-steps: e.g. "days for cleaning," "days for painting." Yardi recommends pulling a unit-turn report with timestamps per step to pinpoint bottlenecks[16]. Tracking task completion times and categories can reveal chronic delays (for instance, if painting repeatedly overruns its target duration). Other useful metrics: **Vendor performance**. Managers can measure each vendor's average completion time, cost vs. estimate, and quality (e.g. number of call-backs or resident issues). Some systems support a **vendor scorecard**: a numerical score (1–10) reflecting each contractor's timeliness, cost efficiency, and work quality[17]. Over time, properties replace underperforming vendors and favor those with high scores. Additionally, monitoring maintenance *speed* and *first-time fix rate* during turns helps optimize scheduling. In summary, dashboards should report: average turn time, total and vendor-specific costs, days vacant, and vendor SLA compliance. Each of these ties back to revenue (lost rent) and expense control[12][18].

### Key Metrics Table

| Metric | Definition | Industry Benchmark |
|--------|------------|-------------------|
| Unit Turn Time | Days from move-out to lease start | 3 days (multifamily), 7-14 days (SFR) |
| Turn Cost | Labor + materials + vacancy loss | $2,500-$4,000 per unit |
| Vacancy Days | Days unit sits empty | Minimize |
| Task Completion Rate | % tasks completed on time | >90% target |
| Vendor Score | Timeliness + cost + quality | 1-10 scale |

## 7. Notifications & Alerts

Turn boards push status updates to stakeholders in real time. When a turn's status or a task's status changes, the system notifies assigned staff or vendors via email/SMS or app push. For example, creating a new work order or marking it complete will typically notify the assigned vendor or tech. Crucially, overdue or stalled items generate **escalations**. The platform flags any task past its due date and alerts a manager. Modern turn software "reports exceptions to the system and escalates overdue items" to management automatically[19]. If a vendor misses a deadline, the system can highlight that unit in red or send an urgent alert. Many solutions also offer **daily or weekly summary emails**: e.g. "5 units are in progress, 2 are overdue, 3 ready," keeping teams aligned each morning.

Additionally, turn boards often integrate mobile apps: field technicians receive tasks and updates in real time. AppFolio's mobile inspections app, for instance, syncs data so office staff can "make task changes as needed and notify field staff directly through the app"[20]. Some apps let techs notify residents when they're en route. In short, the system automates routine notifications (status changes, assignment) and escalations (past-due alerts) so nothing slips through the cracks[19][20].

### Notification Types

| Event | Recipients | Channel | Urgency |
|-------|------------|---------|---------|
| Task Assigned | Vendor/Tech | Email + Push | Normal |
| Task Completed | PM, Leasing | Push | Normal |
| Task Overdue | PM, Supervisor | Email + SMS | High |
| Unit Ready | Leasing | Email + Push | Normal |
| Inspection Failed | PM, Maintenance | Push | High |
| 3 Days to Move-In | All stakeholders | Email | High |

## 8. Integrations

Turn boards are typically part of a broader PMS or integrate via APIs. Leading products embed the board within their maintenance module: AppFolio's board lives inside AppFolio Property Manager, Yardi's Make-Ready board is part of Yardi Maintenance (Voyager/Maintenance IQ), and RentManager includes its Make Ready board in Rent Manager Express. They also integrate with **inspections and leasing modules**. For example, AppFolio supports **Mobile Inspections** for final and move-out inspections: inspectors use an app (even offline) to log conditions, and results sync back to the unit turn record[21]. Yardi's Maintenance Mobile App likewise allows field techs to update make-ready tasks on the go, with the board auto-updating status[22].

Most platforms integrate with leasing data so the board knows lease dates and can hand off to leasing. Vendor coordination tools (e.g. Yardi Vendor Cafe or AppFolio's Contact Center) let external contractors log in to accept assignments and report progress. Many boards offer a **vendor portal** or use email/SMS for communication. They also often integrate with accounting (for vendor invoices) and marketing (to release the unit to listings when ready). In sum, the unit turn board is tightly linked into the PMS: it pulls in lease/end dates from leasing, creates work orders in maintenance, pushes completion back to leasing, and works with any mobile/inspection apps for field updates[6][22].

### Integration Points

| System | Data Exchanged | Direction |
|--------|----------------|-----------|
| Leasing Module | Lease dates, move-out notices | → Turn Board |
| Work Order System | Tasks, status updates | ↔ Bidirectional |
| Vendor Portal | Assignments, completion reports | ↔ Bidirectional |
| Inspection App | Condition reports, photos | → Turn Board |
| Accounting | Invoices, costs | Turn Board → |
| Marketing/Listings | Unit availability | Turn Board → |

## 9. Competitive Analysis

### AppFolio (Reference Implementation)
Its native **Unit Turn Board** automatically adds upcoming vacating units and shows all associated work orders in one place[6]. It integrates with Smart Maintenance (AI dispatch, calendar scheduling)[7][8], mobile inspections[21], and offers built-in analytics. Users praise it for giving one-click visibility on "all the work orders involved in turning over a vacant unit." AppFolio sends automatic updates to leasing when turns progress[6].

### Yardi
Its **Make-Ready Board** in Yardi Maintenance (Voyager) provides similar visibility: tasks are predefined via recurring work orders, then tracked on a dashboard. Yardi highlights that make-ready tasks auto-update as technicians use Yardi's mobile app, eliminating manual whiteboards[22]. Like AppFolio, Yardi offers mobile apps and can integrate with property and leasing data. However, its workflow may require more setup in Voyager and is often used in larger portfolios.

### RentManager
Offers a **Make Ready Board** in Rent Manager Express. It uses the Actions/Templates model: managers create "Make Ready Templates" of tasks for each unit type[11]. Units on the board show color-coded status for each task[5]. The board, actions, and templates are built into RentManager, making setup relatively straightforward. RentManager emphasizes flexibility: custom workflows, sorting by priority, and email alerts. Unlike AppFolio/Yardi, which are cloud platforms, RentManager can be on-premise or cloud but has similar features.

### Buildium
Does *not* include a dedicated visual Turn Board. It relies on work order lists and manual steps. Managers use Buildium's task/work order system and "Mark as Turnover" flags. Buildium does provide **Maintenance Workflows** guides and a marketplace app (PropUp) for a visual turnover board, but core product has no Kanban board. Buildium focuses on workflow steps and reporting via tasks. It does have vendor management (profiles, ratings)[9] and simple dashboards, but less turnkey automation for turns than AppFolio/Yardi/RentManager.

### Property Meld
This is a separate maintenance coordination platform (often integrated with a PMS via API). Instead of a classic "board," Property Meld provides a centralized **maintenance ticketing system** with vendor matching (Vendor Nexus) and AI scheduling (Meld's MAX™). Property Meld emphasizes communication – e.g. two-way texting with vendors/tenants and real-time tracking – rather than Kanban visualization. It automates work order dispatch and uses AI to schedule tasks across vendors, but it doesn't present tasks by unit in a whiteboard. However, it does integrate with major PMSs (AppFolio, Yardi, etc.) and provides analytics on turn times and costs. In practice, managers using Property Meld often still think of turns in terms of its workflow steps and checklists rather than a visual board[1][23].

### Comparison Matrix

| Feature | AppFolio | Yardi | RentManager | Buildium | Property Meld |
|---------|----------|-------|-------------|----------|---------------|
| Visual Turn Board | ✅ Native | ✅ Native | ✅ Native | ❌ Manual | ❌ Ticketing |
| Kanban View | ✅ | ✅ | ✅ | ❌ | ❌ |
| Auto-Task Generation | ✅ | ✅ | ✅ Templates | ⚠️ Manual | ⚠️ Limited |
| AI Dispatch | ✅ Smart Maint | ⚠️ Limited | ❌ | ❌ | ✅ MAX |
| Mobile Inspection | ✅ | ✅ | ⚠️ Limited | ❌ | ⚠️ Integration |
| Vendor Portal | ✅ | ✅ VendorCafe | ✅ | ⚠️ Basic | ✅ Nexus |
| Turn Analytics | ✅ | ✅ | ✅ | ⚠️ Basic | ✅ |

**Summary**: AppFolio, Yardi, and RentManager all offer built-in "Turn Board" features with Kanban views and analytics, whereas Buildium requires manual processes or add-ons, and Property Meld approaches turns through its broader maintenance platform. AppFolio stands out for its integrated vendor AI and mobile inspection tie-in, Yardi for its Voyager ecosystem, and RentManager for its templated workflow model.

## 10. Best Practices

### Speed and Efficiency
Industry benchmarks aim for the shortest feasible turn. Buildium notes typical targets of ~3 days for multifamily and 1–2 weeks for single-family units[13]. Property Meld similarly recommends getting make-readies done within **7–10 days** to minimize vacancy[23]. Every saved day translates to rental income rather than loss, so best practice is to **pre-schedule vendors** ahead of tenant move-out[24]. Many managers start pre-turn inspections or even lock in cleaning/painting dates while the resident still occupies.

### Cost Control
Monitor average turn cost. Industry surveys show turnover costs often run **$2,500–$4,000 per unit**[14][15], driven by labor, materials, and vacancy. Using a detailed checklist and standardizing scope (e.g. light vs. heavy painting) helps control these costs. Yardi suggests tightening SLAs or staging supplies if a particular task (like cleaning) is a recurring bottleneck[18].

### Process Standardization
Use a consistent checklist or template for all units (as RentManager and Property Meld advise)[25][26]. Checklists reduce "scope creep" and ensure nothing is forgotten. Automating tasks (e.g. recurring inspections) prevents last-minute scrambling[4].

### Vendor Management
Keep a core group of reliable vendors. Build strong vendor relationships and rating systems so you can trust high scorers to meet tight turnaround goals[9]. Monitor each vendor's average completion time and cost; replace those who underperform[17]. Quick payment practices (paying invoices promptly) encourage vendors to prioritize your turns.

### Bottleneck Focus
Analyze metrics to find slow steps and improve them. For example, if data shows painting delays every turn, consider splitting painting into "light" vs "full" jobs with different contractors or clarifying scope with painters[18]. If inspections consistently slip, add more inspectors or do quick pre-turn walk-throughs. Continually iterate on your process: every incremental day shaved off is profit gained[12][18].

Overall, the best turn boards combine rigorous workflow automation, clear visualization, and data-driven management. By standardizing tasks, leveraging mobile apps, and tracking KPIs, property teams can minimize downtime and costs, turning units faster and more predictably[6][18].

---

## Sources

1. [Rental Turnover Services - Property Meld](https://propertymeld.com/blog/rental-turnover-services/)
2. [Your Ultimate Guide to Property Maintenance Services - AppFolio](https://www.appfolio.com/blog/property-maintenance-services-ultimate-guide)
3. [Property Maintenance Management Workflows 101 - Buildium](https://www.buildium.com/blog/property-maintenance-management-workflows-101/)
4. [Fill Vacancies Faster: How to Streamline Unit Turns - AppFolio](https://www.appfolio.com/blog/streamline-unit-turns/)
5. [How to Improve Your Unit Turnover Process - Rent Manager](https://www.rentmanager.com/how-to-stay-on-track-with-unit-turnovers/)
6. [Property Management Software - AppFolio](https://www.appfolio.com/services/maintenance-efficiency/demo)
7. [Smart Maintenance - AppFolio](https://www.appfolio.com/services/maintenance-efficiency/demo)
8. [Smart Maintenance Scheduling - AppFolio](https://www.appfolio.com/blog/property-maintenance-services-ultimate-guide)
9. [Vendor Management - Buildium](https://www.buildium.com/blog/property-maintenance-management-workflows-101/)
10. [Make Ready Actions - RentManager](https://www.rentmanager.com/how-to-stay-on-track-with-unit-turnovers/)
11. [Make Ready Templates - RentManager](https://www.rentmanager.com/how-to-stay-on-track-with-unit-turnovers/)
12. [Unit Turn Time Metrics - Buildium](https://www.buildium.com/blog/important-rental-property-metrics-for-small-property-managers/)
13. [Turnover Timeline Benchmarks - Buildium](https://www.buildium.com/blog/property-maintenance-management-workflows-101/)
14. [Make-Ready Costs - Property Meld](https://propertymeld.com/blog/how-long-should-a-make-ready-take/)
15. [Turnover Cost Analysis - RentManager](https://www.rentmanager.com/how-to-stay-on-track-with-unit-turnovers/)
16. [Unit Turn Reporting - Yardi Breeze](https://www.yardibreeze.com/blog/2025/10/property-management-system/)
17. [Vendor Performance Scoring - Buildium](https://www.buildium.com/blog/top-property-management-maintenance-metrics/)
18. [KPI Analysis - Yardi Breeze](https://www.yardibreeze.com/blog/2025/10/property-management-system/)
19. [Escalation Management - SuiteSpot](https://blog.suitespottechnology.com/what-is-unit-make-ready-software-and-how-does-it-work)
20. [Mobile App Updates - SuiteSpot](https://blog.suitespottechnology.com/what-is-unit-make-ready-software-and-how-does-it-work)
21. [Mobile Inspections - AppFolio](https://www.appfolio.com/services/maintenance-efficiency/demo)
22. [Yardi Voyager Features - Yardi](https://www.yardi.com/blog/news/5-voyager-features/21542.html)
23. [Make-Ready Timeline - Property Meld](https://propertymeld.com/blog/how-long-should-a-make-ready-take/)
24. [Pre-Scheduling Best Practices - Buildium](https://www.buildium.com/blog/important-rental-property-metrics-for-small-property-managers/)
25. [Template Standardization - RentManager](https://www.rentmanager.com/how-to-stay-on-track-with-unit-turnovers/)
26. [Checklist Best Practices - Property Meld](https://propertymeld.com/blog/how-long-should-a-make-ready-take/)

