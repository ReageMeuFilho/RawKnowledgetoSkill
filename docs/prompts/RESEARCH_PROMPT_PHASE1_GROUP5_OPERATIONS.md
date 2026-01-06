# Research Prompt: Phase 1 Group 5 - Operations Basics

## 🎯 RESEARCH OBJECTIVE

Research and document the **5 core operations skills**. These enable day-to-day property management - cleaning schedules, task management, maintenance intake, and smart lock integration.

---

## ⚠️ IMPORTANT CONTEXT

**We already have AI-powered operations specified (MVP):**
- AI Maintenance Coordinator (SKILL-254)
- Maintenance Brain (SKILL-270-272)
- Unit Turn Board (SKILL-257)

This research focuses on the **foundational operations** that support those AI capabilities - the basic task management and device integrations.

---

## 📋 SKILLS TO RESEARCH

| Skill ID | Name | Priority | Category |
|----------|------|----------|----------|
| SKILL-017 | task-auto-generation | P0 | operations |
| SKILL-018 | task-assignment | P0 | operations |
| SKILL-019 | task-progress-tracking | P0 | operations |
| SKILL-021 | maintenance-request-handling | P0 | operations |
| SKILL-022 | smart-lock-integration | P0 | operations |

---

## 🏢 PLATFORMS TO ANALYZE

### Primary (Best-in-Class)
| Platform | Why | Focus Areas |
|----------|-----|-------------|
| **Breezeway** | Operations specialist | Task automation, quality control |
| **Properly** | Cleaning operations | Checklists, photo verification |
| **Guesty** | Enterprise operations | Team management, scheduling |

### Secondary
| Platform | Focus |
|----------|-------|
| Hostaway | Task automation |
| TurnoverBnB | Cleaning marketplace |
| RemoteLock | Smart lock specialist |

### Smart Lock Providers (Technical Sources)
| Provider | Focus |
|----------|-------|
| August | Consumer + Pro locks |
| Yale | Residential smart locks |
| Schlage | Enterprise locks |
| RemoteLock | Multi-brand management |

---

## 📚 RESEARCH QUESTIONS BY SKILL

### SKILL-017: Task Auto-Generation

**Core Questions:**
1. What events trigger automatic task creation?
2. What task types are auto-generated (cleaning, inspection, checkout)?
3. How is task timing calculated (relative to check-in/out)?
4. What customization options exist per property/task type?
5. How are recurring tasks handled?

**Technical Questions:**
- Event-driven task generation architecture?
- Task template data model?
- Timing calculation with buffer periods?
- Timezone handling for task schedules?

**Trigger Types:**
| Trigger | Task Generated | Timing |
|---------|---------------|--------|
| Checkout | Cleaning | X hours after checkout |
| Check-in | Inspection | X hours before |
| Booking confirmed | Welcome prep | Day before |
| Monthly schedule | Deep clean | Recurring |

**Sources to Check:**
- [ ] Breezeway task automation
- [ ] Guesty auto-task documentation
- [ ] Properly cleaning schedules
- [ ] YouTube: "vacation rental cleaning automation"
- [ ] Reddit: r/airbnb_hosts "task management"

---

### SKILL-018: Task Assignment

**Core Questions:**
1. How are tasks assigned to team members/vendors?
2. What assignment algorithms exist (round-robin, proximity, skill)?
3. How is availability/capacity considered?
4. Can tasks be reassigned?
5. How are assignment notifications sent?

**Technical Questions:**
- Assignment algorithm options?
- Team member availability calendar?
- Workload balancing logic?
- Auto-assignment vs manual override?

**Assignment Strategies:**
- **Round-robin**: Distribute evenly
- **Proximity-based**: Closest cleaner to property
- **Skill-based**: Match task type to specialist
- **Preferred vendor**: Property-specific assignments

**Sources to Check:**
- [ ] Breezeway assignment features
- [ ] TurnoverBnB cleaner matching
- [ ] Field service management best practices
- [ ] YouTube: "cleaning team management"
- [ ] Jobber/ServiceTitan patterns

---

### SKILL-019: Task Progress Tracking

**Core Questions:**
1. What task states/statuses exist?
2. How is progress updated (app, web, SMS)?
3. What completion verification is required?
4. How are delays/issues flagged?
5. What reporting/analytics are available?

**Technical Questions:**
- Task state machine?
- Real-time status updates (WebSocket)?
- Photo/checklist completion tracking?
- Time tracking per task?

**Task States:**
```
PENDING → ASSIGNED → ACCEPTED → IN_PROGRESS → COMPLETED → VERIFIED
                  → DECLINED → REASSIGNED
                            → BLOCKED → ESCALATED
```

**Verification Methods:**
- Checklist completion
- Photo documentation (before/after)
- GPS confirmation (at property)
- QR code scan
- Manager sign-off

**Sources to Check:**
- [ ] Breezeway task tracking
- [ ] Properly photo verification
- [ ] Guesty task status workflow
- [ ] YouTube: "property cleaning checklist app"
- [ ] Operations management best practices

---

### SKILL-021: Maintenance Request Handling

**Core Questions:**
1. How do guests/residents submit maintenance requests?
2. What information is captured at intake?
3. How are requests categorized and prioritized?
4. What's the triage workflow?
5. How is request status communicated?

**Technical Questions:**
- Request submission channels (app, SMS, email, portal)?
- Request data model?
- Category/priority taxonomy?
- Photo/video attachment handling?

**Request Categories:**
| Category | Priority | Response Time |
|----------|----------|---------------|
| Emergency (flood, fire) | P0 | Immediate |
| Urgent (no hot water) | P1 | 4 hours |
| Standard (broken blinds) | P2 | 24-48 hours |
| Cosmetic (paint touch-up) | P3 | Next turnover |

**Note**: This is the "intake" skill - the AI Maintenance Coordinator (SKILL-254) handles the intelligent processing.

**Sources to Check:**
- [ ] Guesty maintenance requests
- [ ] AppFolio maintenance portal
- [ ] Property Meld request flow
- [ ] YouTube: "tenant maintenance request"
- [ ] Reddit: r/PropertyManagement "maintenance"

---

### SKILL-022: Smart Lock Integration

**Core Questions:**
1. What smart lock brands are supported?
2. How are access codes generated and distributed?
3. What's the code lifecycle (create, share, expire, revoke)?
4. How is lock status monitored?
5. What happens when locks are offline?

**Technical Questions:**
- Lock API integration patterns?
- Code generation algorithm (random, sequential, semantic)?
- Offline lock handling?
- Battery level monitoring?
- Access log retrieval?

**Supported Locks:**
| Brand | API | Features |
|-------|-----|----------|
| August | REST API | Remote unlock, access logs |
| Yale | Assure API | Scheduled codes |
| Schlage | Encode API | Enterprise features |
| RemoteLock | Universal API | Multi-brand management |
| Nuki | REST API | European standard |

**Code Distribution Flow:**
1. Booking confirmed → Generate unique code
2. Day before check-in → Send code to guest
3. Check-in time → Code activates
4. Checkout time → Code expires/revokes
5. Cleaning scheduled → Cleaner code activated

**Sources to Check:**
- [ ] August Pro API documentation
- [ ] Yale Access API
- [ ] RemoteLock integration guide
- [ ] Guesty smart lock integration
- [ ] YouTube: "vacation rental smart lock"
- [ ] Reddit: r/airbnb_hosts "smart locks"

---

## 📄 OUTPUT REQUIREMENTS

### Document Structure

```markdown
# Knowledge Document: Operations Basics
## Phase 1 Group 5 | Skills: SKILL-017, 018, 019, 021, 022

## 1. Executive Summary
   - Key operational workflows
   - Integration with AI Operations (MVP specs)
   - Vendor/cleaner ecosystem

## 2. Operations Architecture Overview
   - Task lifecycle diagram
   - Integration points with calendar/booking
   - Mobile app requirements

## 3. SKILL-017: Task Auto-Generation
   ### 3.1 Trigger Types & Events
   ### 3.2 Task Templates
   ### 3.3 Timing Calculations
   ### 3.4 Customization Options
   ### 3.5 Edge Cases

## 4. SKILL-018: Task Assignment
   ### 4.1 Assignment Algorithms
   ### 4.2 Availability Management
   ### 4.3 Workload Balancing
   ### 4.4 Notification Flow
   ### 4.5 Reassignment Handling

## 5. SKILL-019: Task Progress Tracking
   ### 5.1 State Machine
   ### 5.2 Update Channels
   ### 5.3 Verification Methods
   ### 5.4 Escalation Rules
   ### 5.5 Reporting Metrics

## 6. SKILL-021: Maintenance Request Handling
   ### 6.1 Intake Channels
   ### 6.2 Request Data Model
   ### 6.3 Category Taxonomy
   ### 6.4 Priority Matrix
   ### 6.5 Status Communication

## 7. SKILL-022: Smart Lock Integration
   ### 7.1 Supported Devices
   ### 7.2 Code Generation Logic
   ### 7.3 Distribution Workflow
   ### 7.4 Monitoring & Alerts
   ### 7.5 Offline Handling

## 8. Integration with AI Operations
   - How these skills feed AI Maintenance Coordinator
   - Data flow to Maintenance Brain
   - Unit Turn Board integration

## 9. References
   - 30+ citations
```

### Quality Targets

| Metric | Target |
|--------|--------|
| Document Length | 400-550 lines |
| Citations | 30+ sources |
| State Machines | Task lifecycle diagram |
| Smart Lock Coverage | 4+ brands documented |

---

## 💾 SAVE LOCATION

```
knowledge/operations/KD-PHASE1-G5-operations-basics.md
```

---

## ✅ COMPLETION CHECKLIST

- [ ] All 5 skills researched
- [ ] Task state machine documented
- [ ] Smart lock APIs documented
- [ ] Assignment algorithms defined
- [ ] Integration with AI Operations mapped
- [ ] 30+ sources cited

---

## 🚀 AFTER COMPLETING

```bash
git add -A
git commit -m "Stage 1 COMPLETE: Phase 1 Group 5 - Operations Basics (5 skills)"
git push
```

