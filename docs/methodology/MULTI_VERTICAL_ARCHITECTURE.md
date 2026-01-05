# Multi-Vertical Capability Architecture

> **Problem**: Skills, tools, and integrations may be shared across verticals (STR, LTR, HOA) or unique to one vertical.
> **Solution**: Three-tier registry with Core → Shared → Vertical-Specific organization.

---

## 🎯 The Challenge

```
STR PRD (Guesty)        LTR PRD (AppFolio)       HOA PRD (BuildingLink)
      │                       │                        │
      ▼                       ▼                        ▼
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│ STR Skills  │         │ LTR Skills  │         │ HOA Skills  │
│             │         │             │         │             │
│ • Turnover  │ ◄─────► │ • Lease     │         │ • Voting    │
│ • Pricing   │ SHARED  │ • Rent      │ ◄─────► │ • Dues      │
│ • Guest Msg │         │ • Maint     │ SHARED  │ • Maint     │
└─────────────┘         └─────────────┘         └─────────────┘
      │                       │                        │
      └───────────────────────┼────────────────────────┘
                              │
                              ▼
                    ┌─────────────────┐
                    │   CORE SKILLS   │
                    │                 │
                    │ • Communication │  ← Used by ALL
                    │ • Payments      │
                    │ • Database      │
                    └─────────────────┘
```

---

## 📊 Three-Tier Architecture

### Tier 1: CORE (Universal)
Skills/tools used by **ALL verticals**

```
Examples:
• send_whatsapp_message     - All verticals message people
• process_payment           - All verticals collect money
• query_database            - All verticals need data
• send_email                - All verticals send emails
• create_calendar_event     - All verticals schedule things
```

### Tier 2: SHARED (Cross-Vertical)
Skills/tools used by **SOME verticals**

```
Examples:
• maintenance_triage        - STR + LTR + HOA (all have maintenance)
• rent_collection           - STR + LTR (both collect rent, HOA collects dues)
• property_inspection       - STR + LTR (both inspect properties)
• vendor_dispatch           - STR + LTR + HOA (all work with vendors)
```

### Tier 3: VERTICAL-SPECIFIC (Unique)
Skills/tools used by **ONE vertical only**

```
STR-Only:
• turnover_scheduler        - Only STR has same-day turnovers
• dynamic_pricing           - Only STR has nightly rate changes
• guest_review_management   - Only STR has OTA reviews

LTR-Only:
• lease_renewal             - Only LTR has annual leases
• tenant_screening          - Only LTR does credit checks
• eviction_process          - Only LTR handles evictions

HOA-Only:
• board_voting              - Only HOA has board votes
• assessment_collection     - Only HOA collects assessments
• architectural_review      - Only HOA reviews modifications
```

---

## 📁 Repository Structure

```
RawKnowledgetoSkill/
│
├── registry/
│   │
│   ├── MASTER_REGISTRY.md           # Index of ALL skills/tools
│   │
│   ├── core/                        # TIER 1: Universal
│   │   ├── SKILLS.md                # Core skills (all verticals)
│   │   ├── TOOLS.md                 # Core tools
│   │   ├── INTEGRATIONS.md          # Core integrations
│   │   └── DATA.md                  # Core data objects
│   │
│   ├── shared/                      # TIER 2: Cross-Vertical
│   │   ├── SKILLS.md                # Shared skills
│   │   ├── TOOLS.md                 # Shared tools
│   │   └── VERTICAL_MAP.md          # Which verticals use what
│   │
│   └── verticals/                   # TIER 3: Vertical-Specific
│       ├── str/                     # STR-only
│       │   ├── SKILLS.md
│       │   ├── TOOLS.md
│       │   └── INTEGRATIONS.md
│       │
│       ├── ltr/                     # LTR-only
│       │   ├── SKILLS.md
│       │   ├── TOOLS.md
│       │   └── INTEGRATIONS.md
│       │
│       └── hoa/                     # HOA-only
│           ├── SKILLS.md
│           ├── TOOLS.md
│           └── INTEGRATIONS.md
│
├── competitors/
│   ├── str/                         # STR competitor PRDs
│   │   ├── guesty/
│   │   ├── hostaway/
│   │   └── hospitable/
│   │
│   ├── ltr/                         # LTR competitor PRDs
│   │   ├── appfolio/
│   │   ├── buildium/
│   │   └── rentmanager/
│   │
│   └── hoa/                         # HOA competitor PRDs
│       ├── buildinglink/
│       ├── appfolio/
│       └── townsq/
│
├── products/                        # YOUR product definitions
│   ├── str-pms/
│   ├── ltr-pms/
│   └── hoa-os/
│
└── skills/                          # Generated skills output
    ├── core/                        # Core skills (shared)
    ├── str/                         # STR-specific skills
    ├── ltr/                         # LTR-specific skills
    └── hoa/                         # HOA-specific skills
```

---

## 🔄 Processing Workflow

When you give me a PRD:

### Step 1: Identify Vertical
```
"This is a [STR/LTR/HOA] PRD for [Competitor Name]"
```

### Step 2: Extract Capabilities
Extract skills, tools, integrations, data.

### Step 3: Classify Each Capability

For each extracted capability, determine:

| Classification | Criteria | Where It Goes |
|----------------|----------|---------------|
| **CORE** | Used by ALL verticals | `registry/core/` |
| **SHARED** | Used by 2+ verticals | `registry/shared/` |
| **VERTICAL** | Used by 1 vertical only | `registry/verticals/[vertical]/` |

### Step 4: Check for Existing
- Search core registry first
- Then shared registry
- Then vertical-specific registry
- UPDATE existing or CREATE new

---

## 📋 Master Registry Index

The `MASTER_REGISTRY.md` serves as the index:

```markdown
# Master Capability Registry

## Quick Stats
| Vertical | Core | Shared | Specific | Total |
|----------|------|--------|----------|-------|
| STR | 15 | 12 | 23 | 50 |
| LTR | 15 | 14 | 18 | 47 |
| HOA | 15 | 8 | 21 | 44 |

## Skills Index

### Core Skills (All Verticals)
| ID | Skill | Description |
|----|-------|-------------|
| CORE-001 | message-sender | Send messages via any channel |
| CORE-002 | payment-processor | Process payments |
| CORE-003 | calendar-manager | Manage calendars |

### Shared Skills (Multiple Verticals)
| ID | Skill | Verticals | Description |
|----|-------|-----------|-------------|
| SHARED-001 | maintenance-triage | STR, LTR, HOA | Classify maintenance issues |
| SHARED-002 | vendor-dispatcher | STR, LTR, HOA | Dispatch vendors |
| SHARED-003 | rent-collector | STR, LTR | Collect rent payments |

### STR-Specific Skills
| ID | Skill | Description |
|----|-------|-------------|
| STR-001 | turnover-scheduler | Schedule cleanings |
| STR-002 | dynamic-pricer | Adjust nightly rates |

### LTR-Specific Skills
| ID | Skill | Description |
|----|-------|-------------|
| LTR-001 | lease-manager | Handle lease lifecycle |
| LTR-002 | tenant-screener | Screen applicants |

### HOA-Specific Skills
| ID | Skill | Description |
|----|-------|-------------|
| HOA-001 | board-vote-manager | Manage board voting |
| HOA-002 | assessment-collector | Collect HOA dues |
```

---

## 🎯 Classification Rules

### When is something CORE?

✅ **CORE** if:
- Sending messages (WhatsApp, SMS, Email) - everyone messages
- Processing payments - everyone collects money
- Database operations - everyone stores data
- Calendar operations - everyone schedules
- File generation - everyone creates documents

### When is something SHARED?

✅ **SHARED** if:
- Maintenance handling - STR, LTR, HOA all have maintenance
- Vendor management - STR, LTR, HOA all use vendors
- Property inspections - STR, LTR both inspect
- Rent/dues collection - STR, LTR collect rent; HOA collects dues (similar)
- Compliance/taxes - STR, LTR both have rental taxes

### When is something VERTICAL-SPECIFIC?

✅ **STR-SPECIFIC** if:
- Related to nightly rates, dynamic pricing
- Related to turnovers, same-day cleaning
- Related to OTA channels (Airbnb, VRBO)
- Related to guest reviews
- Related to short stays (1-30 days)

✅ **LTR-SPECIFIC** if:
- Related to leases (annual contracts)
- Related to tenant screening/credit
- Related to eviction process
- Related to rent increases
- Related to long stays (6+ months)

✅ **HOA-SPECIFIC** if:
- Related to board governance
- Related to community voting
- Related to assessments (not rent)
- Related to architectural review
- Related to common areas

---

## 📊 Vertical Comparison Matrix

```markdown
# Capability Overlap Matrix

| Capability | STR | LTR | HOA | Classification |
|------------|-----|-----|-----|----------------|
| Send WhatsApp | ✅ | ✅ | ✅ | CORE |
| Process Payment | ✅ | ✅ | ✅ | CORE |
| Maintenance Triage | ✅ | ✅ | ✅ | SHARED (all) |
| Vendor Dispatch | ✅ | ✅ | ✅ | SHARED (all) |
| Property Inspection | ✅ | ✅ | ❌ | SHARED (STR+LTR) |
| Rent Collection | ✅ | ✅ | ❌ | SHARED (STR+LTR) |
| Turnover Scheduling | ✅ | ❌ | ❌ | STR-SPECIFIC |
| Dynamic Pricing | ✅ | ❌ | ❌ | STR-SPECIFIC |
| Lease Renewal | ❌ | ✅ | ❌ | LTR-SPECIFIC |
| Tenant Screening | ❌ | ✅ | ❌ | LTR-SPECIFIC |
| Board Voting | ❌ | ❌ | ✅ | HOA-SPECIFIC |
| Assessment Collection | ❌ | ❌ | ✅ | HOA-SPECIFIC |
```

---

## 🔧 Skill Naming Convention

```
CORE-XXX     → Core skill (all verticals)
SHARED-XXX   → Shared skill (specify which verticals)
STR-XXX      → STR-specific skill
LTR-XXX      → LTR-specific skill
HOA-XXX      → HOA-specific skill
```

---

## 🚀 Benefits of This Architecture

1. **No Duplication**
   - Core skills built ONCE, used everywhere
   - Shared skills built ONCE, mapped to verticals

2. **Clear Ownership**
   - Know exactly which vertical owns which skills
   - Know what's shared vs. unique

3. **Efficient Development**
   - Build core first → all verticals benefit
   - Build shared next → multiple verticals benefit
   - Build specific last → single vertical focus

4. **Easy Discovery**
   - When processing LTR PRD, check if skill exists in CORE or SHARED first
   - Only create LTR-specific if truly unique

5. **Reuse Maximized**
   - ~30% of capabilities are CORE (shared by all)
   - ~25% are SHARED (2+ verticals)
   - ~45% are VERTICAL-SPECIFIC

---

## 📋 Processing a New Vertical

When you start a NEW vertical (e.g., LTR):

### Step 1: Start with Core
All core skills already available:
- Communication tools ✅
- Payment tools ✅
- Database tools ✅

### Step 2: Check Shared
Review shared skills from other verticals:
- "maintenance_triage from STR - does LTR need this?" → YES, reuse
- "turnover_scheduler from STR - does LTR need this?" → NO, STR-specific

### Step 3: Extract Vertical-Specific
Process LTR PRDs, create only what's truly unique:
- lease_manager → LTR-SPECIFIC (new)
- tenant_screener → LTR-SPECIFIC (new)

### Step 4: Promote if Shared
If you find LTR needs something STR already has:
- Move from `STR-XXX` to `SHARED-XXX`
- Update both vertical references



