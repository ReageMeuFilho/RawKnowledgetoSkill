# Complete Capability Stack: Skills + Tools + Integrations + Data

> **From PRD to Reality**: Everything needed to make a feature actually work

---

## 🎯 The Complete Picture

A feature in a PRD requires **4 layers** to become reality:

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         COMPLETE CAPABILITY STACK                                │
└─────────────────────────────────────────────────────────────────────────────────┘

                              PRD FEATURE
                          "Schedule Cleaning"
                                  │
           ┌──────────────────────┼──────────────────────┐
           │                      │                      │
           ▼                      ▼                      ▼
    ┌─────────────┐        ┌─────────────┐        ┌─────────────┐
    │   SKILL     │        │   TOOLS     │        │    DATA     │
    │ (Knowledge) │        │ (Functions) │        │  (Context)  │
    │             │        │             │        │             │
    │ WHEN to     │        │ HOW to      │        │ WHAT info   │
    │ schedule    │        │ send msg    │        │ is needed   │
    │ WHO to      │        │ HOW to      │        │             │
    │ contact     │        │ check cal   │        │ • Cleaner   │
    │ WHAT to     │        │ HOW to      │        │   contacts  │
    │ say         │        │ update DB   │        │ • Property  │
    │ DECISIONS   │        │             │        │   details   │
    └─────────────┘        └─────────────┘        └─────────────┘
           │                      │                      │
           │                      ▼                      │
           │               ┌─────────────┐               │
           │               │INTEGRATIONS │               │
           │               │             │               │
           │               │ • WhatsApp  │               │
           │               │ • Calendar  │               │
           │               │ • Database  │               │
           └───────────────┴─────────────┴───────────────┘
                                  │
                                  ▼
                         FEATURE WORKS! ✅
```

---

## 📋 The 4 Layers Explained

### Layer 1: SKILL (Procedural Knowledge)
**What it is**: The AI's knowledge of HOW to handle situations
**Format**: `SKILL.md` files
**Contains**:
- When to activate (triggers)
- Decision logic (if X then Y)
- Conversation flows
- Business rules
- Edge case handling

### Layer 2: TOOLS (Deterministic Functions)
**What it is**: Python scripts that execute real actions
**Format**: `scripts/*.py` files
**Contains**:
- API calls
- Database operations
- Calculations
- Validations
- External system interactions

### Layer 3: INTEGRATIONS (External Systems)
**What it is**: The services/APIs the tools connect to
**Format**: MCP servers, API configurations
**Contains**:
- WhatsApp (via Twilio/Meta)
- Calendar systems
- Payment processors
- IoT devices (locks, thermostats)
- Third-party platforms

### Layer 4: DATA (Context & Information)
**What it is**: The information needed to execute
**Format**: Database schemas, context objects
**Contains**:
- Contact information
- Property details
- Schedules
- Preferences
- History

---

## 🔧 Example: "Schedule Cleaning" Feature

### The PRD Says:
> "When a guest checks out, automatically schedule cleaning and notify the cleaner"

### Complete Capability Stack:

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ FEATURE: Schedule Cleaning After Checkout                                        │
└─────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│ SKILL: turnover-scheduler                                                        │
│ File: skills/str-pms/turnover-scheduler/SKILL.md                                │
├─────────────────────────────────────────────────────────────────────────────────┤
│ KNOWLEDGE:                                                                       │
│ • Trigger: Checkout detected (booking ends)                                      │
│ • Check: Is there a same-day check-in? (urgency calculation)                    │
│ • Decide: Which cleaner to assign (based on availability, property, rating)     │
│ • Compose: Message to cleaner with property address, access code, checklist     │
│ • Handle: Cleaner accepts/declines/doesn't respond                              │
│ • Escalate: If no cleaner available, alert property manager                     │
│ • Confirm: Cleaning completed, update calendar                                   │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      │ USES
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│ TOOLS (Deterministic Functions)                                                  │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│ send_whatsapp_message.py          check_cleaner_availability.py                 │
│ ┌─────────────────────────┐       ┌─────────────────────────┐                   │
│ │ def send_message(       │       │ def check_availability( │                   │
│ │   phone: str,           │       │   cleaner_id: str,      │                   │
│ │   message: str,         │       │   date: datetime,       │                   │
│ │   media_url: str = None │       │   duration_hours: int   │                   │
│ │ ) -> MessageResult      │       │ ) -> AvailabilityResult │                   │
│ └─────────────────────────┘       └─────────────────────────┘                   │
│                                                                                  │
│ create_cleaning_task.py           get_property_details.py                       │
│ ┌─────────────────────────┐       ┌─────────────────────────┐                   │
│ │ def create_task(        │       │ def get_property(       │                   │
│ │   property_id: str,     │       │   property_id: str      │                   │
│ │   cleaner_id: str,      │       │ ) -> PropertyDetails    │                   │
│ │   scheduled_time: datetime,│    │   # Returns address,    │                   │
│ │   checklist_id: str     │       │   # access_code, etc.   │                   │
│ │ ) -> TaskResult         │       │                         │                   │
│ └─────────────────────────┘       └─────────────────────────┘                   │
│                                                                                  │
│ update_calendar.py                wait_for_response.py                          │
│ ┌─────────────────────────┐       ┌─────────────────────────┐                   │
│ │ def block_calendar(     │       │ def wait_for_reply(     │                   │
│ │   property_id: str,     │       │   conversation_id: str, │                   │
│ │   start: datetime,      │       │   timeout_minutes: int  │                   │
│ │   end: datetime,        │       │ ) -> ResponseResult     │                   │
│ │   reason: str           │       │                         │                   │
│ │ ) -> CalendarResult     │       │                         │                   │
│ └─────────────────────────┘       └─────────────────────────┘                   │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      │ CONNECTS TO
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│ INTEGRATIONS (External Systems)                                                  │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│ ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│ │  WhatsApp    │  │   Calendar   │  │   Database   │  │  Smart Lock  │          │
│ │  (Twilio)    │  │   (Google)   │  │ (PostgreSQL) │  │   (Seam)     │          │
│ │              │  │              │  │              │  │              │          │
│ │ • Send msg   │  │ • Read events│  │ • Store task │  │ • Get code   │          │
│ │ • Receive    │  │ • Create     │  │ • Get cleaner│  │ • Create     │          │
│ │ • Media      │  │ • Update     │  │ • Log history│  │   temp code  │          │
│ └──────────────┘  └──────────────┘  └──────────────┘  └──────────────┘          │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      │ REQUIRES
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│ DATA (Context & Information)                                                     │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│ Property Context          Cleaner Context           Booking Context             │
│ ┌──────────────────┐     ┌──────────────────┐      ┌──────────────────┐         │
│ │ • property_id    │     │ • cleaner_id     │      │ • booking_id     │         │
│ │ • address        │     │ • name           │      │ • checkout_time  │         │
│ │ • access_code    │     │ • phone          │      │ • next_checkin   │         │
│ │ • cleaning_time  │     │ • properties     │      │ • guest_count    │         │
│ │ • checklist_id   │     │ • availability   │      │ • special_notes  │         │
│ │ • owner_id       │     │ • rating         │      │                  │         │
│ └──────────────────┘     └──────────────────┘      └──────────────────┘         │
│                                                                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 Complete Inventory Template

For EACH skill in the registry, we need:

```markdown
# Capability Inventory: [SKILL-ID] [skill-name]

## Skill Definition
- **SKILL.md Location**: `skills/[vertical]/[skill-name]/SKILL.md`
- **Triggers**: [What activates this skill]
- **Decisions**: [What choices the AI makes]
- **Outputs**: [What the skill produces]

## Tools Required

| Tool | Purpose | Input | Output | Script |
|------|---------|-------|--------|--------|
| [tool-name] | [What it does] | [Parameters] | [Return] | `scripts/[name].py` |

## Integrations Required

| Integration | Purpose | API/Service | MCP Server |
|-------------|---------|-------------|------------|
| [name] | [What for] | [API] | [mcp-server-name] |

## Data Required

| Data Object | Fields | Source |
|-------------|--------|--------|
| [object] | [fields] | [where it comes from] |

## Dependencies
- **Other Skills**: [skills this depends on]
- **Shared Tools**: [tools shared with other skills]
```

---

## 🔄 Updated Pipeline: PRD → Full Capability Stack

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    PRD → FULL CAPABILITY STACK PIPELINE                          │
└─────────────────────────────────────────────────────────────────────────────────┘

  PHASE 1              PHASE 2              PHASE 3              PHASE 4
  FEATURE              SKILL                TOOL                 INTEGRATION
  EXTRACTION           MAPPING              MAPPING              MAPPING
  
  ┌─────────┐         ┌─────────┐         ┌─────────┐         ┌─────────┐
  │   PRD   │         │  SKILL  │         │  TOOL   │         │ INTEG   │
  │         │────────►│INVENTORY│────────►│INVENTORY│────────►│INVENTORY│
  │Features │         │         │         │         │         │         │
  │extracted│         │What AI  │         │What     │         │What     │
  │         │         │knows    │         │executes │         │connects │
  └─────────┘         └─────────┘         └─────────┘         └─────────┘
                            │                   │                   │
                            ▼                   ▼                   ▼
                      ┌─────────┐         ┌─────────┐         ┌─────────┐
                      │SKILL.md │         │scripts/ │         │MCP      │
                      │files    │         │*.py     │         │servers  │
                      └─────────┘         └─────────┘         └─────────┘

  PHASE 5              PHASE 6
  DATA                 KNOWLEDGE
  MAPPING              SOURCING
  
  ┌─────────┐         ┌─────────┐
  │  DATA   │         │ SOURCE  │
  │INVENTORY│────────►│  PLAN   │
  │         │         │         │
  │What info│         │Where to │
  │needed   │         │learn    │
  └─────────┘         └─────────┘
       │                   │
       ▼                   ▼
  ┌─────────┐         ┌─────────┐
  │Database │         │Training │
  │schemas  │         │docs,etc │
  └─────────┘         └─────────┘
```

---

## 📋 Master Inventory Structure

```
registry/
├── MASTER_SKILL_REGISTRY.md      # All skills
├── MASTER_TOOL_REGISTRY.md       # All tools (deterministic functions)
├── MASTER_INTEGRATION_REGISTRY.md # All integrations needed
├── MASTER_DATA_REGISTRY.md       # All data objects needed
└── COMPETITIVE_MATRIX.md         # Who has what
```

---

## 🔧 Tool Categories

### Communication Tools
```
send_whatsapp_message.py      # Send WhatsApp message
send_sms.py                   # Send SMS
send_email.py                 # Send email
make_phone_call.py            # Initiate call
wait_for_response.py          # Monitor for reply
```

### Calendar Tools
```
check_availability.py         # Check calendar slots
create_event.py               # Create calendar event
update_event.py               # Modify event
delete_event.py               # Remove event
sync_calendars.py             # Sync across platforms
```

### Database Tools
```
query_database.py             # General query
create_record.py              # Insert record
update_record.py              # Update record
search_records.py             # Search with filters
```

### Payment Tools
```
process_payment.py            # Charge card
create_invoice.py             # Generate invoice
issue_refund.py               # Process refund
check_balance.py              # Check account
```

### IoT Tools
```
get_lock_code.py              # Get current code
create_temp_code.py           # Create temporary code
set_thermostat.py             # Adjust temperature
check_device_status.py        # Device health
```

### Calculation Tools
```
calculate_price.py            # Pricing calculation
calculate_payout.py           # Owner payout
calculate_tax.py              # Tax calculation
calculate_availability.py     # Date math
```

---

## 🎯 What Gets Created From PRD

When you give me a PRD, I extract:

| Output | Description | File Location |
|--------|-------------|---------------|
| **Skills** | What the AI needs to know | `MASTER_SKILL_REGISTRY.md` |
| **Tools** | Functions needed to execute | `MASTER_TOOL_REGISTRY.md` |
| **Integrations** | External systems to connect | `MASTER_INTEGRATION_REGISTRY.md` |
| **Data** | Information required | `MASTER_DATA_REGISTRY.md` |
| **Knowledge Gaps** | What to source/learn | `SOURCE_PLAN.md` |

---

## ✅ Complete Extraction Checklist

For each PRD feature:

- [ ] **Skill identified** - What knowledge does AI need?
- [ ] **Tools identified** - What functions execute actions?
- [ ] **Integrations identified** - What systems connect?
- [ ] **Data identified** - What information is needed?
- [ ] **Triggers identified** - What starts this workflow?
- [ ] **Edge cases identified** - What could go wrong?



