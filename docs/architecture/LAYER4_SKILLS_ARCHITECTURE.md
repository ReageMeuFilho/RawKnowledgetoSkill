# 🎯 Layer 4: Digital Workforce Skills Architecture
## The Claude Skills Framework Implementation for CitadelOS

**Version**: 1.0
**Date**: January 2026
**Status**: Approved Architecture Specification
**Standard**: [Agent Skills Specification](https://agentskills.io) + CitadelOS Extensions

---

## Executive Summary

This document defines the **official implementation strategy** for CitadelOS Layer 4 (Digital Workforce) using the [Anthropic Agent Skills Framework](https://github.com/anthropics/skills). This approach delivers:

| Benefit | Impact | How |
|---------|--------|-----|
| **Faster Time to Market** | 60-70% reduction | Skills are markdown files, not code. Non-engineers can author. |
| **Zero Context Bloat** | Scale to 1000+ skills | Progressive Disclosure loads only relevant skills per task. |
| **Hot/Cold Path Bridge** | AI + Financial guarantees | Skills call MCP servers that wrap Treasury OS. |
| **Vendor Independence** | No lock-in | Skills are portable markdown. Runtime can be Suna, LangGraph, or custom. |
| **Composable Platform** | Domain portability | Same skills work across STR, LTR, HOA with localization overrides. |

---

## 1. Architecture Overview: "Agent as Operating System"

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                                      │
│                              CITADELOS "AGENT AS OS" ARCHITECTURE                                   │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │                                                                                              │   │
│   │                    USER REQUEST: "My toilet is overflowing again!"                          │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  SUNA AGENT RUNTIME (The "Operating System")                                                 │   │
│   │  ─────────────────────────────────────────────                                               │   │
│   │                                                                                              │   │
│   │  • Multi-modal input (voice, text, WhatsApp, email)                                         │   │
│   │  • Sandbox execution environment                                                             │   │
│   │  • Browser/tool integration                                                                  │   │
│   │  • We extend Suna, not rebuild from scratch                                                  │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LANGGRAPH ROUTER (The "Process Manager")                                                    │   │
│   │  ────────────────────────────────────────                                                    │   │
│   │                                                                                              │   │
│   │  PROGRESSIVE DISCLOSURE - 3-Phase Loading:                                                  │   │
│   │                                                                                              │   │
│   │  ┌──────────────────────────────────────────────────────────────────────────────────────┐   │   │
│   │  │ PHASE 1: HEADER SCAN (~200 tokens)                                                    │   │   │
│   │  │ ─────────────────────────────────                                                     │   │   │
│   │  │ Scan YAML frontmatter of all skills in registry                                       │   │   │
│   │  │                                                                                       │   │   │
│   │  │ Input: "My toilet is overflowing again!"                                              │   │   │
│   │  │ Match: skills/domains/ltr/maintenance-triage/SKILL.md                                │   │   │
│   │  │        (triggers: ["overflow", "leak", "broken"])                                    │   │   │
│   │  └──────────────────────────────────────────────────────────────────────────────────────┘   │   │
│   │                                            │                                                │   │
│   │                                            ▼                                                │   │
│   │  ┌──────────────────────────────────────────────────────────────────────────────────────┐   │   │
│   │  │ PHASE 2: FULL SKILL LOAD (~800 tokens)                                                │   │   │
│   │  │ ────────────────────────────────────────                                              │   │   │
│   │  │ Load complete SKILL.md + referenced scripts                                           │   │   │
│   │  │                                                                                       │   │   │
│   │  │ Loaded:                                                                               │   │   │
│   │  │ • SKILL.md (instructions, SOPs, decision trees)                                      │   │   │
│   │  │ • scripts/check_warranty.py (Hot Path)                                               │   │   │
│   │  │ • scripts/dispatch_vendor.py (Cold Path trigger)                                     │   │   │
│   │  │ • references/escalation_matrix.md                                                    │   │   │
│   │  └──────────────────────────────────────────────────────────────────────────────────────┘   │   │
│   │                                            │                                                │   │
│   │                                            ▼                                                │   │
│   │  ┌──────────────────────────────────────────────────────────────────────────────────────┐   │   │
│   │  │ PHASE 3: CONTEXT INJECTION (~1500 tokens)                                             │   │   │
│   │  │ ─────────────────────────────────────────                                             │   │   │
│   │  │ Pull relevant data from Memory Architecture                                           │   │   │
│   │  │                                                                                       │   │   │
│   │  │ Injected:                                                                             │   │   │
│   │  │ • Entity: Mario Silva, Unit 5B, sentiment: frustrated                                │   │   │
│   │  │ • History: Same issue 7 days ago, João's Plumbing, R$180                             │   │   │
│   │  │ • Knowledge: Unit 5B has 2018 copper pipes, lime buildup risk                        │   │   │
│   │  │ • Financial: Warranty active (30 days), budget R$2,450 available                     │   │   │
│   │  └──────────────────────────────────────────────────────────────────────────────────────┘   │   │
│   │                                                                                              │   │
│   │  TOTAL CONTEXT: ~2,500 tokens (vs. 50,000+ if all skills loaded)                           │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│              ┌─────────────────────────────┼─────────────────────────────┐                          │
│              ▼                             │                             ▼                          │
│   ┌──────────────────────────┐             │             ┌──────────────────────────┐              │
│   │  🔥 HOT PATH             │             │             │  ❄️ COLD PATH             │              │
│   │  (AI Reasoning)          │             │             │  (Financial Guarantees)  │              │
│   │  ────────────────────    │             │             │  ────────────────────    │              │
│   │                          │             │             │                          │              │
│   │  SKILL SCRIPTS:          │             │             │  MCP SERVERS:            │              │
│   │  • check_warranty.py     │             │             │  • mcp://treasury/*      │              │
│   │  • classify_urgency.py   │             │             │  • mcp://temporal/*      │              │
│   │                          │             │             │  • mcp://formance/*      │              │
│   │  LLM OPERATIONS:         │             │             │                          │              │
│   │  • Intent understanding  │             │             │  TREASURY OS:            │              │
│   │  • Response generation   │             │             │  • TigerBeetle (txns)    │              │
│   │  • Tone adaptation       │             │             │  • Formance (ledger)     │              │
│   │  • Language translation  │             │             │  • Temporal (workflows)  │              │
│   │                          │             │             │                          │              │
│   │  LANGCHAIN + LITELLM:    │             │             │  GUARANTEES:             │              │
│   │  • Model selection       │             │             │  • ACID transactions     │              │
│   │  • Failover routing      │             │             │  • Audit trail           │              │
│   │  • RAG retrieval         │             │             │  • Compliance logging    │              │
│   │                          │             │             │  • Idempotency           │              │
│   └──────────────────────────┘             │             └──────────────────────────┘              │
│              │                             │                             │                          │
│              └─────────────────────────────┼─────────────────────────────┘                          │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  RESPONSE: "Olá Mario! Vejo que o vaso sanitário voltou a dar problema..."                  │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Skills Repository Structure

Following the [Agent Skills Specification](https://agentskills.io/specification) with CitadelOS extensions:

```
citadel-skills/
│
├── README.md                                    # Repository overview
├── CONTRIBUTING.md                              # How to create skills
├── skill-schema.json                            # JSON Schema for validation
│
├── /global/                                     # 🌍 PLATFORM DEFAULTS
│   │
│   ├── /communication/
│   │   ├── /intent-classifier/                  # P0: Route all messages
│   │   │   ├── SKILL.md
│   │   │   ├── scripts/
│   │   │   │   └── classify.py
│   │   │   └── tests/
│   │   │       └── test_classifier.py
│   │   │
│   │   ├── /message-responder/                  # P0: Generic responses
│   │   │   ├── SKILL.md
│   │   │   └── references/
│   │   │       └── tone_guidelines.md
│   │   │
│   │   └── /email-drafter/                      # P1: Email composition
│   │       ├── SKILL.md
│   │       └── assets/
│   │           └── email_templates.json
│   │
│   └── /finance/
│       ├── /invoice-coding/                     # P0: Categorize expenses
│       │   ├── SKILL.md
│       │   ├── scripts/
│       │   │   └── categorize.py
│       │   └── references/
│       │       └── chart_of_accounts.md
│       │
│       └── /payment-processing/                 # P0: Execute payments
│           ├── SKILL.md
│           └── scripts/
│               └── process_payment.py
│
├── /domains/                                    # 🏢 VERTICAL-SPECIFIC SKILLS
│   │
│   ├── /str/                                    # Short-Term Rental
│   │   ├── /dynamic-pricing/                    # P0: Revenue optimization
│   │   │   ├── SKILL.md
│   │   │   ├── scripts/
│   │   │   │   ├── price_calculator.py
│   │   │   │   └── competitor_analysis.py
│   │   │   └── references/
│   │   │       └── pricing_rules.md
│   │   │
│   │   ├── /guest-checkin/                      # P0: Check-in automation
│   │   │   ├── SKILL.md
│   │   │   └── scripts/
│   │   │       └── generate_instructions.py
│   │   │
│   │   └── /channel-sync/                       # P1: OTA management
│   │       ├── SKILL.md
│   │       └── scripts/
│   │           └── sync_availability.py
│   │
│   ├── /ltr/                                    # Long-Term Rental
│   │   ├── /maintenance-triage/                 # P0: THE MARIO SKILL 🚽
│   │   │   ├── SKILL.md
│   │   │   ├── scripts/
│   │   │   │   ├── check_warranty.py
│   │   │   │   ├── dispatch_vendor.py
│   │   │   │   └── classify_urgency.py
│   │   │   ├── references/
│   │   │   │   └── escalation_matrix.md
│   │   │   └── tests/
│   │   │       └── test_triage.py
│   │   │
│   │   ├── /lease-inquiry/                      # P0: Leasing questions
│   │   │   ├── SKILL.md
│   │   │   └── scripts/
│   │   │       └── check_availability.py
│   │   │
│   │   ├── /rent-collection/                    # P0: Payment reminders
│   │   │   ├── SKILL.md
│   │   │   └── scripts/
│   │   │       └── generate_reminder.py
│   │   │
│   │   └── /tenant-screening/                   # P1: Application processing
│   │       ├── SKILL.md
│   │       └── scripts/
│   │           └── screen_applicant.py
│   │
│   └── /hoa/                                    # HOA/Condo Management
│       ├── /violation-management/               # P0: Process violations
│       │   ├── SKILL.md
│       │   └── scripts/
│       │       └── process_violation.py
│       │
│       ├── /dues-collection/                    # P0: HOA payments
│       │   ├── SKILL.md
│       │   └── scripts/
│       │       └── collect_dues.py
│       │
│       └── /architectural-review/               # P1: ARC submissions
│           ├── SKILL.md
│           └── scripts/
│               └── review_submission.py
│
├── /localization/                               # 🌎 COUNTRY/MARKET OVERRIDES
│   │
│   ├── /br/                                     # 🇧🇷 Brazil
│   │   ├── /payment-collections/                # Overrides global
│   │   │   ├── SKILL.md                         # PIX + WhatsApp rules
│   │   │   └── scripts/
│   │   │       ├── pix_payment.py
│   │   │       └── boleto_payment.py
│   │   │
│   │   └── /communication/
│   │       └── /message-responder/              # Brazilian Portuguese
│   │           └── SKILL.md                     # Informal tone, emojis
│   │
│   ├── /us/                                     # 🇺🇸 United States
│   │   └── /payment-collections/
│   │       ├── SKILL.md                         # ACH + Email rules
│   │       └── scripts/
│   │           └── ach_payment.py
│   │
│   ├── /es/                                     # 🇪🇸 Spain
│   │   └── /payment-collections/
│   │       ├── SKILL.md                         # SEPA + Bizum
│   │       └── scripts/
│   │           └── sepa_payment.py
│   │
│   └── /pt/                                     # 🇵🇹 Portugal
│       └── /communication/
│           └── /message-responder/
│               └── SKILL.md                     # European Portuguese
│
└── /mcp-servers/                                # ❄️ COLD PATH BRIDGES
    │
    ├── /treasury-read/                          # Safe balance/transaction lookups
    │   ├── server.py
    │   ├── requirements.txt
    │   └── README.md
    │
    ├── /treasury-write/                         # Transfer execution (restricted)
    │   ├── server.py
    │   ├── requirements.txt
    │   └── README.md
    │
    ├── /temporal-trigger/                       # Workflow initiation
    │   ├── server.py
    │   ├── requirements.txt
    │   └── README.md
    │
    ├── /formance-ledger/                        # Accounting operations
    │   ├── server.py
    │   ├── requirements.txt
    │   └── README.md
    │
    └── /vector-context/                         # RAG retrieval
        ├── server.py
        ├── requirements.txt
        └── README.md
```

---

## 3. SKILL.md Golden Template

```yaml
---
# ══════════════════════════════════════════════════════════════════════════════
# REQUIRED FIELDS (Agent Skills Standard)
# ══════════════════════════════════════════════════════════════════════════════
name: maintenance-triage
description: |
  Diagnose maintenance issues, check warranties, and dispatch vendors.
  
  USE WHEN:
  - Resident reports something broken, leaking, or not working
  - Maintenance-related keywords detected (overflow, leak, broken, etc.)
  
  DO NOT USE FOR:
  - Payment questions → route to payment-processing
  - Lease questions → route to lease-inquiry
  - General inquiries → route to message-responder

# ══════════════════════════════════════════════════════════════════════════════
# CITADEL EXTENSIONS
# ══════════════════════════════════════════════════════════════════════════════
version: 1.2.0
priority: P0                    # P0=MVP, P1=Important, P2=Nice-to-have
domain: ltr                     # str | ltr | hoa | global
status: production              # draft | review | production | deprecated

# Routing Configuration
triggers:
  keywords:
    - "overflow"
    - "leak"
    - "broken"
    - "not working"
    - "flooding"
    - "vazando"                 # Portuguese
    - "quebrado"                # Portuguese
  intents:
    - maintenance_request
    - emergency_repair
  channels:
    - voice
    - whatsapp
    - email
    - chat

# Tool Dependencies
tools:
  # Hot Path - Local Scripts
  - name: classify_urgency
    type: script
    path: scripts/classify_urgency.py
    description: Determine if issue is emergency/high/medium/low
    
  - name: check_warranty
    type: script
    path: scripts/check_warranty.py
    description: Check if recent vendor work is under warranty
    
  # Cold Path - MCP Servers
  - name: get_unit_history
    type: mcp
    uri: mcp://vector-context/unit_history
    description: Retrieve maintenance history for unit
    
  - name: dispatch_vendor
    type: mcp
    uri: mcp://temporal-trigger/dispatch_vendor
    description: Trigger durable vendor dispatch workflow
    
  - name: create_work_order
    type: mcp
    uri: mcp://treasury-write/create_work_order
    description: Create work order with budget allocation

# Human-in-the-Loop Configuration
hitl:
  required: false
  escalate_on:
    - urgency == "emergency"
    - estimated_cost > 500
    - is_recurring == true && recurrence_count > 2
  approval_roles:
    - property_manager
    - maintenance_supervisor
  timeout_hours: 4
  escalation_contact: maintenance@citadelos.com

# Quality & Testing
evaluation:
  accuracy_target: 0.95
  latency_target_ms: 3000
  test_cases:
    - input: "My toilet is overflowing!"
      expected:
        intent: maintenance_request
        category: plumbing
        urgency: high
        
    - input: "The same toilet broke again, João fixed it last week"
      expected:
        intent: maintenance_request
        flags: [recurring, warranty_check]
        
    - input: "There's water everywhere and smoke from the outlet!"
      expected:
        urgency: emergency
        action: immediate_escalation
        hitl_required: true

# Observability
observability:
  log_level: info
  trace_header: x-citadel-trace
  metrics:
    - skill.invocation.count
    - skill.latency.p50
    - skill.latency.p99
    - skill.mcp_calls.count
    - skill.hitl_escalations.count
---

# Maintenance Triage

## Overview

This skill handles all maintenance-related requests from residents. It:
1. Classifies urgency (emergency → low)
2. Checks for recurring issues and active warranties
3. Dispatches appropriate vendors via Temporal workflow
4. Tracks costs against budget

## Standard Operating Procedure

### Step 1: Urgency Classification (Hot Path)

Run `scripts/classify_urgency.py` with the resident message.

**Emergency Indicators** (immediate escalation):
- Keywords: "flood", "fire", "smoke", "gas smell", "no electricity"
- Pattern: Multiple exclamation marks + water/fire keywords
- Action: Skip to Step 4 with HITL flag

**High Priority**:
- Keywords: "overflow", "leak", "no hot water", "AC broken" (in summer)
- Pattern: Repeated urgency words
- SLA: 4 hours

**Medium Priority**:
- Keywords: "broken", "not working", "stuck"
- SLA: 24 hours

**Low Priority**:
- Keywords: "squeaky", "minor", "cosmetic"
- SLA: 72 hours

### Step 2: History & Warranty Check (Hybrid Path)

1. Call `mcp://vector-context/unit_history` to retrieve:
   - Last 5 maintenance requests for this unit
   - Category match (same issue type?)
   - Days since last similar issue

2. Run `scripts/check_warranty.py`:
   ```python
   # If same category issue within 30 days of vendor payment
   if days_since_last_repair < 30 and same_category:
       return {
           "under_warranty": True,
           "original_vendor": vendor_id,
           "warranty_until": payment_date + 30_days,
           "action": "DISPATCH_SAME_VENDOR_WARRANTY_CLAIM"
       }
   ```

3. **Recurring Issue Protocol**:
   - If same issue type within 14 days: Flag as RECURRING
   - If RECURRING: Recommend senior technician or different vendor
   - If 3+ recurrences: Escalate to property manager (HITL)

### Step 3: Vendor Selection (Hot Path)

Based on warranty check and history:

| Scenario | Vendor Selection | Cost Code |
|----------|-----------------|-----------|
| Under warranty | Original vendor | WARRANTY-00 |
| Recurring (same vendor failed) | Alternative vendor | MAINTENANCE-01 |
| New issue | Best-rated available | MAINTENANCE-01 |
| Emergency | Nearest available | EMERGENCY-00 |

### Step 4: Dispatch (Cold Path)

Call `mcp://temporal-trigger/dispatch_vendor`:

```json
{
  "workflow_id": "wo-dispatch-v1",
  "vendor_id": "<selected_vendor>",
  "unit_id": "<unit_id>",
  "category": "<plumbing|hvac|electrical|...>",
  "urgency": "<emergency|high|medium|low>",
  "metadata": {
    "is_warranty": true,
    "is_recurring": false,
    "estimated_cost": 200,
    "resident_preferred_time": "afternoon"
  }
}
```

### Step 5: Response Generation (Hot Path)

Generate response using context:

**Template (Warranty Case)**:
```
Olá {resident_name}! Vejo que {issue_description} - isso não deveria ter 
acontecido, especialmente considerando que {vendor_name} esteve aí há 
apenas {days} dias.

O serviço dele ainda está na garantia de 30 dias, então vou acionar a 
garantia para você sem custo adicional. {vendor_name} pode estar aí em 
{eta}. Posso confirmar?
```

**Template (New Issue)**:
```
Olá {resident_name}! Entendi que {issue_description}. Já estou 
providenciando um técnico para resolver isso.

{vendor_name} ({rating}/5 ⭐) pode estar aí {eta}. O custo estimado é 
{estimated_cost}. Posso confirmar o agendamento?
```

## References

See `references/escalation_matrix.md` for complete escalation rules.

## Scripts

| Script | Purpose | Path |
|--------|---------|------|
| classify_urgency.py | Determine priority level | Hot |
| check_warranty.py | Verify warranty status | Hybrid |
| dispatch_vendor.py | Trigger Temporal workflow | Cold |

## Changelog

- **1.2.0** (2026-01-05): Added warranty check, recurring detection
- **1.1.0** (2025-12-15): Added Portuguese support
- **1.0.0** (2025-11-01): Initial release
```

---

## 4. Hot Path vs Cold Path Execution

### The Execution Bridge

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    SKILL EXECUTION PATHS                                             │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │                                                                                              │   │
│   │   SKILL: maintenance-triage                                                                 │   │
│   │   TASK: "Mario's toilet is overflowing again"                                               │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│                    ┌───────────────────────┼───────────────────────┐                               │
│                    │                       │                       │                               │
│                    ▼                       ▼                       ▼                               │
│   ┌────────────────────────┐ ┌────────────────────────┐ ┌────────────────────────┐                │
│   │  🔥 HOT PATH           │ │  🔄 HYBRID PATH        │ │  ❄️ COLD PATH          │                │
│   │  (Pure AI/Scripts)     │ │  (Script + MCP)        │ │  (MCP → Treasury)      │                │
│   │  ──────────────────    │ │  ─────────────────     │ │  ──────────────────    │                │
│   │                        │ │                        │ │                        │                │
│   │  classify_urgency.py   │ │  check_warranty.py     │ │  dispatch_vendor       │                │
│   │  ┌──────────────────┐  │ │  ┌──────────────────┐  │ │  ┌──────────────────┐  │                │
│   │  │ Input: message   │  │ │  │ 1. Run script    │  │ │  │ mcp://temporal/  │  │                │
│   │  │                  │  │ │  │    (parse logic) │  │ │  │ dispatch_vendor  │  │                │
│   │  │ Process:         │  │ │  │                  │  │ │  │                  │  │                │
│   │  │ • Keyword match  │  │ │  │ 2. Call MCP      │  │ │  │ → Temporal       │  │                │
│   │  │ • Pattern detect │  │ │  │    (get data)    │  │ │  │   Workflow       │  │                │
│   │  │ • LLM reasoning  │  │ │  │                  │  │ │  │                  │  │                │
│   │  │                  │  │ │  │ 3. Return result │  │ │  │ → TigerBeetle    │  │                │
│   │  │ Output: urgency  │  │ │  │                  │  │ │  │   (budget hold)  │  │                │
│   │  │ • emergency      │  │ │  │ Output:          │  │ │  │                  │  │                │
│   │  │ • high           │  │ │  │ • warranty_status│  │ │  │ → Formance       │  │                │
│   │  │ • medium         │  │ │  │ • vendor_id      │  │ │  │   (work order)   │  │                │
│   │  │ • low            │  │ │  │ • action         │  │ │  │                  │  │                │
│   │  └──────────────────┘  │ │  └──────────────────┘  │ │  └──────────────────┘  │                │
│   │                        │ │                        │ │                        │                │
│   │  Latency: <100ms       │ │  Latency: <500ms       │ │  Latency: <2000ms      │                │
│   │  Guarantees: None      │ │  Guarantees: Partial   │ │  Guarantees: ACID      │                │
│   │  Rollback: N/A         │ │  Rollback: Partial     │ │  Rollback: Full        │                │
│   │                        │ │                        │ │                        │                │
│   └────────────────────────┘ └────────────────────────┘ └────────────────────────┘                │
│                    │                       │                       │                               │
│                    └───────────────────────┼───────────────────────┘                               │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │                                                                                              │   │
│   │  RESULT AGGREGATION                                                                         │   │
│   │  ──────────────────                                                                         │   │
│   │                                                                                              │   │
│   │  {                                                                                           │   │
│   │    "urgency": "high",                           // From Hot Path                            │   │
│   │    "warranty_status": {                         // From Hybrid Path                         │   │
│   │      "under_warranty": true,                                                                │   │
│   │      "vendor_id": "vendor-joao",                                                            │   │
│   │      "warranty_until": "2026-01-12"                                                         │   │
│   │    },                                                                                        │   │
│   │    "dispatch_result": {                         // From Cold Path                           │   │
│   │      "work_order_id": "WO-2026-001234",                                                     │   │
│   │      "temporal_workflow_id": "dispatch-abc123",                                             │   │
│   │      "eta": "2 hours",                                                                       │   │
│   │      "budget_hold": 0.00                        // Warranty = no charge                     │   │
│   │    }                                                                                         │   │
│   │  }                                                                                           │   │
│   │                                                                                              │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### When to Use Each Path

| Path | Use When | Examples | Technology |
|------|----------|----------|------------|
| **🔥 Hot** | Pure reasoning, no side effects | Intent classification, response generation, translation | Suna + LangChain |
| **🔄 Hybrid** | Logic + data lookup, no mutations | Warranty check (script + read), availability check | Script + MCP Read |
| **❄️ Cold** | State changes, financial ops, workflows | Payment processing, vendor dispatch, ledger updates | MCP → Treasury OS |

---

## 5. MCP Server Architecture

### The Cold Path Bridge

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    MCP SERVER ARCHITECTURE                                           │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   SKILL (Hot Path)                                                                                  │
│         │                                                                                            │
│         │ mcp://treasury-write/transfer                                                             │
│         │                                                                                            │
│         ▼                                                                                            │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  MCP GATEWAY (API Gateway Pattern)                                                           │   │
│   │  ────────────────────────────────                                                            │   │
│   │                                                                                              │   │
│   │  • Authentication (Auth0 token validation)                                                   │   │
│   │  • Rate limiting (per skill, per tenant)                                                     │   │
│   │  • Request validation (JSON Schema)                                                          │   │
│   │  • Idempotency key enforcement                                                               │   │
│   │  • Audit logging                                                                             │   │
│   │                                                                                              │   │
│   └────────────────────────────────────────┬────────────────────────────────────────────────────┘   │
│                                            │                                                        │
│              ┌─────────────────────────────┼─────────────────────────────┐                          │
│              ▼                             ▼                             ▼                          │
│   ┌──────────────────────┐   ┌──────────────────────┐   ┌──────────────────────┐                   │
│   │  mcp-treasury-read   │   │  mcp-treasury-write  │   │  mcp-temporal-trigger│                   │
│   │  ──────────────────  │   │  ─────────────────── │   │  ────────────────────│                   │
│   │                      │   │                      │   │                      │                   │
│   │  TOOLS:              │   │  TOOLS:              │   │  TOOLS:              │                   │
│   │  • get_balance       │   │  • transfer          │   │  • start_workflow    │                   │
│   │  • get_transactions  │   │  • create_hold       │   │  • signal_workflow   │                   │
│   │  • get_account       │   │  • release_hold      │   │  • query_workflow    │                   │
│   │  • check_warranty    │   │  • create_work_order │   │  • cancel_workflow   │                   │
│   │                      │   │                      │   │                      │                   │
│   │  PERMISSIONS:        │   │  PERMISSIONS:        │   │  PERMISSIONS:        │                   │
│   │  • Read-only         │   │  • Write (restricted)│   │  • Workflow trigger  │                   │
│   │  • All skills        │   │  • Approved skills   │   │  • Approved skills   │                   │
│   │                      │   │                      │   │                      │                   │
│   │  BACKEND:            │   │  BACKEND:            │   │  BACKEND:            │                   │
│   │  • TigerBeetle       │   │  • TigerBeetle       │   │  • Temporal Server   │                   │
│   │  • Formance          │   │  • Formance          │   │                      │                   │
│   │  • Redis (cache)     │   │  • Temporal          │   │                      │                   │
│   │                      │   │                      │   │                      │                   │
│   └──────────────────────┘   └──────────────────────┘   └──────────────────────┘                   │
│              │                             │                             │                          │
│              └─────────────────────────────┼─────────────────────────────┘                          │
│                                            │                                                        │
│                                            ▼                                                        │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  TREASURY OS CORE (Cold Path Guarantees)                                                     │   │
│   │  ───────────────────────────────────────                                                     │   │
│   │                                                                                              │   │
│   │  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐              │   │
│   │  │ TigerBeetle  │    │   Formance   │    │   Temporal   │    │   Redpanda   │              │   │
│   │  │ ──────────── │    │ ──────────── │    │ ──────────── │    │ ──────────── │              │   │
│   │  │ Source of    │    │ Programmable │    │ Durable      │    │ Event        │              │   │
│   │  │ Truth        │    │ Ledger       │    │ Workflows    │    │ Streaming    │              │   │
│   │  │              │    │              │    │              │    │              │              │   │
│   │  │ • 384+ TPS   │    │ • Multi-curr │    │ • Saga       │    │ • Audit log  │              │   │
│   │  │ • ACID       │    │ • Compliance │    │ • Retry      │    │ • CDC        │              │   │
│   │  │ • Immutable  │    │ • Audit      │    │ • Compensate │    │ • Replay     │              │   │
│   │  └──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘              │   │
│   │                                                                                              │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 6. Localization Override Pattern

### Resolution Order

```
Unit 5B (São Paulo, Brazil) → Property → Market → Country → Global

Skill Request: "payment-processing"

Resolution:
1. Check: /localization/br/sao-paulo/property-123/unit-5b/payment-processing/ → NOT FOUND
2. Check: /localization/br/sao-paulo/property-123/payment-processing/ → NOT FOUND  
3. Check: /localization/br/sao-paulo/payment-processing/ → NOT FOUND
4. Check: /localization/br/payment-processing/ → FOUND ✓
5. Fallback: /global/finance/payment-processing/

Result: Use /localization/br/payment-processing/ (PIX + WhatsApp rules)
```

### Override Example

**Global Skill** (`/global/finance/payment-processing/SKILL.md`):
```yaml
---
name: payment-processing
description: Process payments using configured rails
---
# Payment Processing
## Supported Rails
- Credit Card
- Bank Transfer (ACH)
- Wire Transfer
```

**Brazil Override** (`/localization/br/payment-processing/SKILL.md`):
```yaml
---
name: payment-processing
description: Process payments using Brazilian rails (PIX primary)
extends: global/finance/payment-processing  # Inheritance
---
# Payment Processing (Brazil)

## Supported Rails (Priority Order)
1. **PIX** (instant, free) - PRIMARY
2. **Boleto** (3-day settlement)
3. **Credit Card** (2.5% fee)

## PIX-Specific Rules
- Generate QR code for amounts < R$5,000
- Request key type preference (CPF, email, phone, random)
- Confirm via WhatsApp (preferred) or SMS

## Communication
- Channel: WhatsApp (primary), SMS (fallback)
- Tone: Informal, emoji-friendly
- Language: pt-BR
```

---

## 7. Competitive Moat Analysis

### Why This Architecture Wins

| Advantage | Traditional Approach | CitadelOS Skills Approach | Impact |
|-----------|---------------------|---------------------------|--------|
| **Time to Market** | 6-8 weeks per feature | 1-2 weeks per skill | **4x faster** |
| **Non-Engineer Authoring** | Impossible | Product/Ops can write SKILL.md | **10x more contributors** |
| **Context Efficiency** | Load all code | Progressive Disclosure | **20x less tokens** |
| **Testing** | Unit tests + integration | Skill evaluation sets | **Continuous validation** |
| **Localization** | Code branches | File overrides | **Zero code changes** |
| **Model Independence** | Hardcoded prompts | Skill = model-agnostic instructions | **Swap models freely** |
| **Financial Guarantees** | Custom integration | MCP → Treasury OS | **Built-in ACID** |
| **Portability** | Monolithic | Skills work across domains | **Reuse 70%+ across verticals** |

### The Moat Stack

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    CITADELOS COMPETITIVE MOAT                                        │
├─────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 1: AGENT SKILLS STANDARD                                                              │   │
│   │  ────────────────────────────────                                                            │   │
│   │  • Open format (agentskills.io)         • 33.6k GitHub stars                                │   │
│   │  • Anthropic-backed                      • Industry adoption                                 │   │
│   │  → We're building on a winning standard, not proprietary format                             │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 2: SUNA OPEN SOURCE RUNTIME                                                           │   │
│   │  ─────────────────────────────────                                                           │   │
│   │  • Multi-modal (voice, text, browser)   • Active community                                   │   │
│   │  • Sandbox execution                     • We extend, not rebuild                            │   │
│   │  → 6+ months of development we don't have to do                                             │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 3: LANGGRAPH ORCHESTRATION                                                            │   │
│   │  ────────────────────────────────                                                            │   │
│   │  • State management                      • Multi-agent coordination                          │   │
│   │  • Human-in-the-loop hooks              • Checkpoint/resume                                  │   │
│   │  → Production-grade orchestration out of the box                                            │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 4: TREASURY OS COLD PATH                                                              │   │
│   │  ──────────────────────────────                                                              │   │
│   │  • TigerBeetle (384+ TPS, ACID)         • Already built & tested                            │   │
│   │  • Formance (compliance ledger)          • Double-entry verified                             │   │
│   │  • Temporal (durable workflows)          • 104 tests passing                                 │   │
│   │  → Financial guarantees no competitor can match                                             │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 5: 265+ SKILLS REGISTRY                                                               │   │
│   │  ─────────────────────────────                                                               │   │
│   │  • Competitor research complete          • Knowledge gaps identified                         │   │
│   │  • Knowledge-to-Skill pipeline           • Continuous expansion                              │   │
│   │  → Domain expertise encoded, not locked in engineers' heads                                 │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
│   ┌─────────────────────────────────────────────────────────────────────────────────────────────┐   │
│   │  LAYER 6: LOCALIZATION + FINTECH + LOYALTY                                                   │   │
│   │  ─────────────────────────────────────────                                                   │   │
│   │  • Global→Unit configuration             • PIX, SEPA, ACH, Crypto                           │   │
│   │  • Hybrid Fintech + Crypto Neobank       • Three-sided loyalty network                      │   │
│   │  → No competitor combines all three in property management                                  │   │
│   └─────────────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                                      │
│   RESULT: A platform that would take competitors 3+ years to replicate                             │
│                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 8. Implementation Roadmap

### Phase 1: Foundation (Weeks 1-4)

| Task | Owner | Deliverable |
|------|-------|-------------|
| Initialize `citadel-skills` repo | Engineering | Folder structure, CI/CD |
| Create skill schema validator | Engineering | JSON Schema + CLI tool |
| Implement Router (LangGraph) | Engineering | Progressive disclosure scan |
| Deploy 3 core MCP servers | Engineering | treasury-read, temporal-trigger, vector-context |

### Phase 2: Core Skills (Weeks 5-8)

| Skill | Priority | Domain |
|-------|----------|--------|
| intent-classifier | P0 | global |
| maintenance-triage | P0 | ltr |
| payment-processing | P0 | global |
| lease-inquiry | P0 | ltr |
| message-responder | P0 | global |

### Phase 3: Localization (Weeks 9-12)

| Market | Skills | Rails |
|--------|--------|-------|
| Brazil | payment-processing, message-responder | PIX, WhatsApp |
| US | payment-processing | ACH, Email |
| Spain | payment-processing | SEPA, Bizum |

### Phase 4: Domain Expansion (Weeks 13-16)

| Domain | Skills Count | Priority Skills |
|--------|-------------|-----------------|
| STR | 15 | dynamic-pricing, guest-checkin, channel-sync |
| HOA | 12 | violation-management, dues-collection, board-voting |

---

## 9. Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Skill Creation Time** | <1 week per skill | Time from spec to production |
| **Context Efficiency** | <3,000 tokens per task | Average loaded context |
| **Skill Accuracy** | >95% | Evaluation set pass rate |
| **Cold Path Latency** | <2 seconds | MCP round-trip time |
| **Localization Coverage** | 5 markets in 6 months | Brazil, US, Spain, Portugal, Italy |
| **Skill Reuse Rate** | >70% across domains | Skills used in multiple verticals |

---

**Document Status**: Approved Architecture Specification
**Next Action**: Initialize `citadel-skills` repository
**Owner**: Engineering Team


