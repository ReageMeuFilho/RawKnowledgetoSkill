# PRD-Driven Skill Manufacturing Workflow

> **Goal**: Systematically identify ALL skills needed for a product, then source knowledge to create them.

## 🎯 Why PRD-First?

| Approach | Pros | Cons |
|----------|------|------|
| **PRD-First** ✅ | Goal-oriented, efficient, traceable | Requires clear PRD |
| Knowledge-First | Discovers unknown capabilities | May create unused skills |

**PRD-First is better because:**
- Every skill maps to a product requirement
- No wasted effort on unused skills
- Clear prioritization based on product roadmap
- Traceability from feature → skill → source

---

## 📊 The 4-Phase Workflow

```
PRD ──► SKILL INVENTORY ──► KNOWLEDGE SOURCING ──► SKILL CREATION
```

### Phase 1: PRD Analysis
**Input**: Product Requirement Document
**Output**: Feature List with User Stories

Extract from PRD:
- All features/capabilities
- User stories for each
- Acceptance criteria
- Edge cases mentioned

### Phase 2: Skill Inventory & Gap Analysis
**Input**: Feature List
**Output**: Skill Map + Gaps

For each feature, identify:
- What skill(s) enable it?
- Do we have this skill already?
- What's the priority (MVP vs Later)?

### Phase 3: Knowledge Sourcing
**Input**: Skill Gaps
**Output**: Source List with URLs/Files

For each missing skill, find:
- Training videos
- Documentation
- Expert interviews
- Industry SOPs
- Competitor analysis

### Phase 4: Skill Creation
**Input**: Raw Knowledge Sources
**Output**: Production-ready SKILL.md files

Use the Knowledge-to-Skills pipeline.

---

## 🏠 Example: Short-Term Rental PMS

### Step 1: PRD Features → Skills Needed

| PRD Feature | Required Skills |
|-------------|-----------------|
| Guest inquiry response | `guest-inquiry-handler`, `availability-checker` |
| Booking management | `booking-creator`, `booking-modifier`, `booking-cancellation` |
| Dynamic pricing | `pricing-optimizer`, `competitor-rate-analyzer`, `demand-forecaster` |
| Check-in coordination | `check-in-orchestrator`, `access-code-manager`, `guest-communication` |
| Cleaning coordination | `turnover-scheduler`, `cleaner-dispatcher`, `quality-inspector` |
| Maintenance triage | `maintenance-classifier`, `vendor-dispatcher`, `emergency-handler` |
| Guest communication | `message-responder`, `review-requester`, `issue-resolver` |
| Revenue reporting | `revenue-calculator`, `payout-reconciler`, `tax-reporter` |
| Multi-property sync | `calendar-syncer`, `channel-manager`, `rate-pusher` |
| Owner reporting | `owner-statement-generator`, `performance-reporter` |

### Step 2: Prioritize by MVP Phase

| Priority | Skills | Phase |
|----------|--------|-------|
| P0 - Critical | `booking-creator`, `availability-checker`, `guest-communication` | MVP |
| P1 - Important | `pricing-optimizer`, `turnover-scheduler`, `maintenance-classifier` | MVP |
| P2 - Enhanced | `demand-forecaster`, `competitor-rate-analyzer`, `review-requester` | Phase 2 |
| P3 - Advanced | `tax-reporter`, `owner-statement-generator`, `channel-manager` | Phase 3 |

### Step 3: Source Knowledge for Each Skill

| Skill | Knowledge Sources |
|-------|-------------------|
| `guest-inquiry-handler` | Airbnb Superhost tutorials, Hospitable training, expert interviews |
| `pricing-optimizer` | PriceLabs docs, Beyond Pricing guides, revenue management courses |
| `turnover-scheduler` | TurnoverBnB training, Breezeway docs, cleaning company SOPs |
| `maintenance-classifier` | Property management training, vendor contracts, emergency protocols |

---

## 📁 Recommended File Structure

```
RawKnowledgetoSkill/
│
├── products/                           # PRD Analysis
│   ├── str-pms/                        # Short-Term Rental PMS
│   │   ├── PRD.md                      # Full PRD
│   │   ├── SKILL_INVENTORY.md          # Skills needed
│   │   ├── SKILL_GAPS.md               # What's missing
│   │   └── SOURCE_PLAN.md              # Where to get knowledge
│   │
│   ├── ltr-pms/                        # Long-Term Rental PMS
│   │   └── ...
│   │
│   └── hoa-os/                         # HOA/Condo OS
│       └── ...
│
├── raw-knowledge/                      # Sourced Knowledge
│   ├── str/                            # STR domain
│   │   ├── guest-communication/
│   │   │   ├── airbnb-superhost-guide.md
│   │   │   ├── hospitable-training.md
│   │   │   └── expert-interview-john.md
│   │   ├── pricing/
│   │   │   ├── pricelabs-docs.md
│   │   │   └── revenue-management-course.md
│   │   └── operations/
│   │       ├── turnoverbnb-training.md
│   │       └── cleaning-sop.md
│   │
│   └── ltr/                            # LTR domain
│       └── ...
│
├── skills/                             # Generated Skills
│   ├── str-pms/
│   │   ├── guest-inquiry-handler/
│   │   │   ├── SKILL.md
│   │   │   └── scripts/
│   │   ├── booking-creator/
│   │   └── ...
│   │
│   └── ltr-pms/
│       └── ...
│
└── out/                                # Processing artifacts
    └── ...
```

---

## 🔄 Continuous Process

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   PRD Update ──► New Feature ──► Skill Gap ──► Source ──► Skill │
│       ▲                                                    │    │
│       │                                                    │    │
│       └──────────── Product Feedback ◄─────────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

When product evolves:
1. PRD gets updated with new features
2. Run skill gap analysis
3. Source knowledge for new skills
4. Create skills
5. Deploy to production
6. Gather feedback → inform PRD

---

## 🎯 Quick Start Checklist

### For Your STR PMS:

- [ ] Review existing PRDs (Host OS, NEXUS Core, etc.)
- [ ] Create `products/str-pms/SKILL_INVENTORY.md`
- [ ] Identify skill gaps
- [ ] Create sourcing plan for each gap
- [ ] Source knowledge (videos, docs, interviews)
- [ ] Run Knowledge-to-Skills pipeline
- [ ] Deploy skills to runtime

### Knowledge Sourcing Tips:

| Source Type | Where to Find | Quality |
|-------------|---------------|---------|
| **Training Videos** | YouTube, Udemy, vendor sites | High (visual + audio) |
| **Documentation** | Airbnb Help, vendor docs | High (authoritative) |
| **Expert Interviews** | Property managers, consultants | Very High (real-world) |
| **SOPs** | Cleaning companies, maintenance vendors | High (operational) |
| **Competitor Analysis** | Guesty, Hostaway, Hospitable demos | Medium (reverse-engineered) |
| **Community Forums** | BiggerPockets, STR FB groups | Medium (varied quality) |

---

## 📝 Templates

### SKILL_INVENTORY.md Template

```markdown
# Skill Inventory: [Product Name]

## Overview
- **Product**: [Name]
- **PRD Version**: [Date]
- **Skills Identified**: [Count]
- **Skills Existing**: [Count]
- **Skills Needed**: [Count]

## Skill Map

| ID | Skill Name | PRD Feature | Priority | Status | Sources |
|----|------------|-------------|----------|--------|---------|
| S001 | guest-inquiry-handler | Guest Communication | P0 | NEEDED | TBD |
| S002 | booking-creator | Booking Management | P0 | NEEDED | TBD |
| ... | ... | ... | ... | ... | ... |

## MVP Skills (P0-P1)
[List skills required for MVP]

## Phase 2 Skills (P2)
[List skills for Phase 2]

## Phase 3 Skills (P3)
[List skills for Phase 3]
```

### SOURCE_PLAN.md Template

```markdown
# Knowledge Sourcing Plan: [Product Name]

## Skill: [skill-name]

### Required Knowledge
- [What expertise is needed]

### Source Options
| Source | Type | URL/Location | Quality | Status |
|--------|------|--------------|---------|--------|
| Airbnb Superhost Guide | Doc | [URL] | High | Sourced |
| Property Manager Interview | Interview | John Smith | Very High | Scheduled |

### Sourcing Priority
1. [First source to get]
2. [Second source]
3. [Third source]

### Timeline
- [ ] Source by: [Date]
- [ ] Process by: [Date]
- [ ] Deploy by: [Date]
```



