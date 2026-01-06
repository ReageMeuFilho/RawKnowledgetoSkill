# Master Memory Registry: State & Context Specification

> **What the agent REMEMBERS** across conversations and time
> **Critical for**: Continuity, personalization, pattern recognition
> **Last Updated**: January 2026

---

## 🧠 Why Memory Matters

Without memory, every conversation starts from zero:

```
❌ WITHOUT MEMORY                        ✅ WITH MEMORY

Tenant: "Toilet overflowed"              Tenant: "Toilet overflowed"
Agent: "I'll send a plumber"             Agent: "I see this is the SECOND time
                                         your toilet has overflowed. The last
[1 week later]                           time was Jan 1st, and the plumber
                                         said he fixed it. I'm escalating
Tenant: "Toilet overflowed again"        this to a different plumber and
Agent: "I'll send a plumber"             flagging as a recurring issue."
       (no context!)                            (full context!)
```

---

## 📊 Memory Types

| Memory Type | What It Stores | Duration | Example |
|-------------|----------------|----------|---------|
| **Conversation** | Current chat context | Session | "You mentioned 2 guests" |
| **Short-Term** | Recent interactions | Days | "You reported a leak yesterday" |
| **Long-Term** | Historical facts | Months/Years | "Toilet has overflowed 3 times" |
| **Semantic** | Searchable knowledge | Permanent | Similar issues across properties |
| **Entity** | Facts about people/things | Permanent | "John prefers text over email" |

---

## 🏗️ Memory Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           MEMORY HIERARCHY                                       │
└─────────────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────────┐
  │ LAYER 1: CONTEXT WINDOW (Immediate)                                         │
  │ • Current conversation messages                                             │
  │ • Loaded at start of each turn                                              │
  │ • Duration: Current session only                                            │
  │ • Storage: LLM context window                                               │
  └─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌─────────────────────────────────────────────────────────────────────────────┐
  │ LAYER 2: SESSION CACHE (Short-Term)                                         │
  │ • Active conversation state                                                 │
  │ • Variables collected in this session                                       │
  │ • Duration: Minutes to hours                                                │
  │ • Storage: Redis                                                            │
  └─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌─────────────────────────────────────────────────────────────────────────────┐
  │ LAYER 3: ENTITY MEMORY (Long-Term Facts)                                    │
  │ • Tenant preferences, history                                               │
  │ • Property details, past issues                                             │
  │ • Duration: Months to years                                                 │
  │ • Storage: PostgreSQL                                                       │
  └─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌─────────────────────────────────────────────────────────────────────────────┐
  │ LAYER 4: SEMANTIC MEMORY (Searchable)                                       │
  │ • Vector embeddings of past issues                                          │
  │ • Similar conversation lookup                                               │
  │ • Pattern detection                                                         │
  │ • Duration: Permanent                                                       │
  │ • Storage: pgvector                                                         │
  └─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📋 Memory Specification Template

For each type of memory the agent needs:

```markdown
### MEM-XXX: [memory-name]

**Type**: [Conversation / Short-Term / Long-Term / Semantic / Entity]
**Duration**: [Session / Hours / Days / Months / Permanent]
**Storage**: [Context / Redis / PostgreSQL / pgvector]

**What Is Remembered**:
- [Fact 1]
- [Fact 2]

**When It's Stored**:
- [Trigger that causes storage]

**When It's Retrieved**:
- [Trigger that causes retrieval]

**How It's Used**:
- [How the agent uses this memory]

**Data Schema**:
```sql
CREATE TABLE [table_name] (
    ...
);
```

**Related Tools**:
- TOOL-XXX [retrieval tool]
- TOOL-XXX [storage tool]
```

---

## 🏠 Property Management Memory Types

### MEM-001: Conversation Context

**Type**: Conversation
**Duration**: Session
**Storage**: LLM Context Window

**What Is Remembered**:
- All messages in current conversation
- Variables extracted (dates, amounts, names)
- Current intent/goal

**When It's Stored**: Every message
**When It's Retrieved**: Every turn

**Example**:
```
User: "The toilet is broken"
[Stored: issue_type=plumbing, item=toilet, status=broken]

User: "It's in the master bathroom"
[Retrieved: issue_type=plumbing, item=toilet]
[Added: location=master_bathroom]

Agent knows: plumbing issue, toilet, master bathroom
```

---

### MEM-002: Tenant History

**Type**: Long-Term Entity
**Duration**: Permanent
**Storage**: PostgreSQL

**What Is Remembered**:
- All past maintenance requests
- Communication preferences
- Payment history
- Lease details
- Past interactions

**When It's Stored**: After each resolved interaction
**When It's Retrieved**: When tenant initiates contact

**Data Schema**:
```sql
CREATE TABLE tenant_memory (
    tenant_id UUID PRIMARY KEY,
    property_id UUID,
    
    -- Communication preferences
    preferred_channel VARCHAR(20),      -- 'whatsapp', 'sms', 'email'
    preferred_language VARCHAR(10),
    best_contact_time VARCHAR(50),
    
    -- History summaries
    total_maintenance_requests INT,
    avg_response_satisfaction DECIMAL,
    payment_reliability_score DECIMAL,
    
    -- Flags
    is_vip BOOLEAN,
    requires_escalation BOOLEAN,
    notes TEXT,
    
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
```

**Related Tools**:
- TOOL-050 `get_tenant_context`
- TOOL-051 `update_tenant_memory`

---

### MEM-003: Issue History (Your Toilet Example!)

**Type**: Long-Term + Semantic
**Duration**: Permanent
**Storage**: PostgreSQL + pgvector

**What Is Remembered**:
- All past issues for this tenant/property
- Issue descriptions (for semantic search)
- Resolution status
- Vendor who handled it
- Recurrence patterns

**When It's Stored**: When issue is created/updated/resolved
**When It's Retrieved**: When new issue is reported

**Data Schema**:
```sql
CREATE TABLE maintenance_issues (
    issue_id UUID PRIMARY KEY,
    tenant_id UUID,
    property_id UUID,
    unit_id UUID,
    
    -- Issue details
    category VARCHAR(50),           -- 'plumbing', 'electrical', 'hvac'
    subcategory VARCHAR(50),        -- 'toilet', 'faucet', 'drain'
    location VARCHAR(100),          -- 'master bathroom'
    description TEXT,
    description_embedding VECTOR(1536),  -- For semantic search
    
    -- Status
    status VARCHAR(20),             -- 'open', 'in_progress', 'resolved'
    urgency VARCHAR(20),            -- 'emergency', 'urgent', 'normal'
    
    -- Resolution
    vendor_id UUID,
    vendor_notes TEXT,
    resolution_notes TEXT,
    resolved_at TIMESTAMP,
    
    -- Pattern detection
    is_recurring BOOLEAN,
    related_issue_ids UUID[],       -- Links to similar past issues
    recurrence_count INT,
    
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

-- Index for semantic search
CREATE INDEX idx_issue_embedding ON maintenance_issues 
USING ivfflat (description_embedding vector_cosine_ops);
```

**Example: Your Toilet Scenario**:
```sql
-- Issue #1 (Jan 1)
INSERT INTO maintenance_issues VALUES (
    'issue-1', 'tenant-123', 'prop-456', 'unit-789',
    'plumbing', 'toilet', 'master bathroom',
    'Toilet overflowed, water on floor',
    [0.1, 0.2, ...],  -- embedding
    'resolved', 'urgent',
    'plumber-abc', 'Cleared blockage, should be fixed',
    'Resolved', '2026-01-02',
    FALSE, NULL, 1,
    '2026-01-01', '2026-01-02'
);

-- Issue #2 (Jan 8) - Agent detects recurrence!
INSERT INTO maintenance_issues VALUES (
    'issue-2', 'tenant-123', 'prop-456', 'unit-789',
    'plumbing', 'toilet', 'master bathroom',
    'Toilet overflowed again',
    [0.1, 0.2, ...],  -- similar embedding!
    'open', 'urgent',
    NULL, NULL, NULL, NULL,
    TRUE,                    -- Marked as recurring!
    ARRAY['issue-1'],        -- Linked to previous issue
    2,                       -- This is occurrence #2
    '2026-01-08', '2026-01-08'
);
```

**Related Tools**:
- TOOL-052 `search_similar_issues` (semantic search)
- TOOL-053 `detect_recurrence`
- TOOL-054 `get_issue_history`

---

### MEM-004: Property Knowledge

**Type**: Long-Term Entity
**Duration**: Permanent
**Storage**: PostgreSQL

**What Is Remembered**:
- Property details, quirks, notes
- Vendor preferences for this property
- Past issue patterns
- Owner preferences

**Data Schema**:
```sql
CREATE TABLE property_memory (
    property_id UUID PRIMARY KEY,
    
    -- Property notes
    access_instructions TEXT,
    quirks_and_notes TEXT,          -- "Water heater is in garage"
    preferred_vendors JSONB,         -- {"plumbing": "vendor-123"}
    
    -- Issue patterns
    common_issues JSONB,             -- {"plumbing": 5, "hvac": 2}
    problem_areas TEXT[],            -- ["master bathroom toilet"]
    
    -- Owner preferences
    owner_id UUID,
    owner_notification_threshold VARCHAR(20),
    
    updated_at TIMESTAMP
);
```

---

### MEM-005: Conversation Summaries

**Type**: Long-Term
**Duration**: Months
**Storage**: PostgreSQL

**What Is Remembered**:
- Summary of past conversations
- Key decisions made
- Commitments/promises

**When It's Stored**: End of each conversation
**When It's Retrieved**: Start of new conversation with same tenant

**Data Schema**:
```sql
CREATE TABLE conversation_summaries (
    summary_id UUID PRIMARY KEY,
    tenant_id UUID,
    property_id UUID,
    conversation_date DATE,
    
    -- Summary
    summary TEXT,                    -- AI-generated summary
    summary_embedding VECTOR(1536),  -- For retrieval
    
    -- Key points
    issues_discussed TEXT[],
    decisions_made TEXT[],
    commitments TEXT[],              -- "Promised plumber by Tuesday"
    follow_up_required BOOLEAN,
    follow_up_date DATE,
    
    created_at TIMESTAMP
);
```

---

## 🔧 Memory Tools

### Tools for Memory Operations

| Tool ID | Tool Name | Purpose |
|---------|-----------|---------|
| TOOL-050 | `get_tenant_context` | Load tenant's full history at conversation start |
| TOOL-051 | `update_tenant_memory` | Update tenant preferences/notes |
| TOOL-052 | `search_similar_issues` | Semantic search for similar past issues |
| TOOL-053 | `detect_recurrence` | Check if current issue matches past issues |
| TOOL-054 | `get_issue_history` | Get all issues for tenant/property |
| TOOL-055 | `summarize_conversation` | Create summary at end of conversation |
| TOOL-056 | `retrieve_relevant_memories` | Get memories relevant to current context |

---

## 🔄 Memory Flow: Your Toilet Example

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    MEMORY FLOW: RECURRING TOILET ISSUE                           │
└─────────────────────────────────────────────────────────────────────────────────┘

  JANUARY 1ST                            JANUARY 8TH
  
  ┌─────────────────────────┐            ┌─────────────────────────┐
  │ Tenant: "Toilet         │            │ Tenant: "Toilet         │
  │ overflowed"             │            │ overflowed again"       │
  └───────────┬─────────────┘            └───────────┬─────────────┘
              │                                      │
              ▼                                      ▼
  ┌─────────────────────────┐            ┌─────────────────────────┐
  │ 1. Load tenant context  │            │ 1. Load tenant context  │
  │    (MEM-002)            │            │    (MEM-002)            │
  │                         │            │                         │
  │ 2. No similar issues    │            │ 2. Search similar issues│
  │    found                │            │    (TOOL-052)           │
  │                         │            │    → FOUND: Issue #1!   │
  │ 3. Create Issue #1      │            │                         │
  │                         │            │ 3. Detect recurrence    │
  │ 4. Dispatch plumber     │            │    (TOOL-053)           │
  └───────────┬─────────────┘            │    → Same toilet, same  │
              │                          │      problem, 7 days ago│
              ▼                          │                         │
  ┌─────────────────────────┐            │ 4. Create Issue #2      │
  │ Plumber: "Fixed it"     │            │    → Link to Issue #1   │
  │                         │            │    → Mark as recurring  │
  │ Update Issue #1:        │            │                         │
  │ - status: resolved      │            │ 5. Agent response:      │
  │ - vendor_notes: "Cleared│            │    "I see this is the   │
  │   blockage"             │            │    SECOND time your     │
  └─────────────────────────┘            │    toilet has           │
                                         │    overflowed..."       │
                                         │                         │
                                         │ 6. Escalate:            │
                                         │    → Different plumber  │
                                         │    → Flag property      │
                                         │    → Notify owner       │
                                         └─────────────────────────┘
```

---

## 📋 Memory Requirements by Skill

When specifying a skill, include memory requirements:

```markdown
### SKILL: maintenance-triage

**Memory Requirements**:

| Memory Type | What To Retrieve | What To Store |
|-------------|------------------|---------------|
| Tenant History | Past issues, preferences | Updated issue count |
| Issue History | Similar past issues | New issue record |
| Property Memory | Common problems, vendors | Updated problem areas |
| Conversation | Current session | Summary at end |

**Memory Tools Used**:
- TOOL-050 get_tenant_context (at start)
- TOOL-052 search_similar_issues (when issue reported)
- TOOL-053 detect_recurrence (check patterns)
- TOOL-055 summarize_conversation (at end)
```

---

## ✅ Updated Methodology Checklist

When processing a PRD, now extract:

| Registry | What It Captures |
|----------|------------------|
| **SKILL Registry** | What the agent knows/decides |
| **TOOL Registry** | What the agent can DO (+ Build/Buy/OpenSource) |
| **INTEGRATION Registry** | What external systems to connect |
| **DATA Registry** | What information entities exist |
| **MEMORY Registry** | What the agent REMEMBERS ← **NEW** |

---

## 🔄 Complete Pipeline (Updated)

```
PRD → SKILLS → TOOLS → INTEGRATIONS → DATA → MEMORY → MCP SERVERS
```




