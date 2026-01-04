# Knowledge-to-Skills Methodology

## A Complete Framework for Converting Domain Knowledge into Anthropic-Compatible AI Skills

**Version:** 1.0.0  
**Last Updated:** 2025-01-04  
**Author:** Wesley (UnifiedOS)

---

## Executive Summary

This document provides a complete, step-by-step methodology for converting unstructured domain knowledge (video transcripts, SOPs, documents, tribal knowledge) into production-ready AI Skills compatible with Anthropic's Skills framework.

The methodology follows a manufacturing-line approach with quality gates at each stage:

```
Source Material → Normalized References → Procedure Cards → Skill Taxonomy 
    → Skill Folders → Eval Generation → Gauntlet Testing → Package & Deploy
```

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Phase 1: Source Normalization](#2-phase-1-source-normalization)
3. [Phase 2: Atomization into Procedure Cards](#3-phase-2-atomization-into-procedure-cards)
4. [Phase 3: Skill Taxonomy Classification](#4-phase-3-skill-taxonomy-classification)
5. [Phase 4: Skill Folder Generation](#5-phase-4-skill-folder-generation)
6. [Phase 5: SKILL.md Authoring](#6-phase-5-skillmd-authoring)
7. [Phase 6: Eval Suite Generation](#7-phase-6-eval-suite-generation)
8. [Phase 7: Gauntlet Testing](#8-phase-7-gauntlet-testing)
9. [Phase 8: Package and Deploy](#9-phase-8-package-and-deploy)
10. [Phase 9: Governance and Iteration](#10-phase-9-governance-and-iteration)
11. [Appendix A: Procedure Card Schema](#appendix-a-procedure-card-schema)
12. [Appendix B: Eval Rubric Template](#appendix-b-eval-rubric-template)
13. [Appendix C: Common Failure Modes](#appendix-c-common-failure-modes)

---

## 1. Prerequisites

### 1.1 Required Tools

```bash
# Anthropic's skill creation scripts (copy from skill-creator)
scripts/
├── init_skill.py      # Initialize new skill folders
├── package_skill.py   # Package skills for distribution
└── quick_validate.py  # Validate skill structure

# Transcription tools
whisper                # OpenAI Whisper for video transcription
# OR
assembly.ai            # AssemblyAI API for transcription with timestamps
```

### 1.2 Directory Structure

Create this structure in your project:

```
knowledge-to-skills/
├── 01-sources/                    # Raw source materials
│   ├── videos/
│   ├── documents/
│   └── transcripts/
├── 02-references/                 # Normalized reference documents
│   ├── policies/
│   ├── procedures/
│   └── contacts/
├── 03-procedure-cards/            # Intermediate YAML representations
├── 04-skills/                     # Generated skill folders
├── 05-evals/                      # Evaluation test suites
│   ├── grounded/
│   ├── synthetic/
│   └── rubrics/
├── 06-packaged/                   # Distributable .skill files
└── scripts/                       # Tooling
```

### 1.3 Mental Model

**Skills are NOT summaries.** They are:
- Procedural knowledge packaged for AI consumption
- Triggered by user intent or system events
- Designed for progressive disclosure (load details only when needed)
- Tested like software with eval suites

---

## 2. Phase 1: Source Normalization

### 2.1 Objective

Transform raw source materials into clean, timestamped, citable references.

### 2.2 Process

#### Step 1: Inventory Source Materials

Create a manifest of all knowledge sources:

```yaml
# 01-sources/manifest.yaml
sources:
  - id: VID-001
    type: video
    title: "Property Manager Training - Emergency Protocols"
    path: videos/emergency-protocols-training.mp4
    duration: "45:32"
    date_recorded: 2024-06-15
    subject_matter_expert: "Maria Santos"
    
  - id: DOC-001
    type: document
    title: "Condo Bylaws v2.3"
    path: documents/bylaws_v2.3.pdf
    effective_date: 2024-01-01
    
  - id: DOC-002
    type: document
    title: "Vendor SLA Master Agreement"
    path: documents/vendor_sla.pdf
    effective_date: 2023-07-01
```

#### Step 2: Transcribe Videos with Timestamps

Use Whisper or AssemblyAI to generate timestamped transcripts:

```bash
# Using Whisper
whisper videos/emergency-protocols-training.mp4 \
  --model large-v3 \
  --output_format json \
  --output_dir transcripts/

# Output: transcripts/emergency-protocols-training.json
```

Ensure the transcript includes word-level or segment-level timestamps:

```json
{
  "segments": [
    {
      "id": 0,
      "start": 0.0,
      "end": 4.5,
      "text": "Today we're going to cover emergency leak protocols."
    },
    {
      "id": 1,
      "start": 4.5,
      "end": 12.3,
      "text": "The first thing you need to do when you get a leak report is classify the severity."
    }
  ]
}
```

#### Step 3: Extract and Normalize Reference Documents

For each document, extract the relevant sections into markdown:

```markdown
<!-- 02-references/policies/leak-escalation-policy.md -->
# Leak Escalation Policy

**Source:** Condo Bylaws v2.3, Section 4.2
**Effective Date:** 2024-01-01

## Severity Classifications

### Emergency (Immediate Response Required)
- Standing water affecting multiple units
- Active flooding from burst pipe
- Water intrusion near electrical panels

### Urgent (Response within 2 hours)
- Active leak contained to single unit
- Water damage spreading to adjacent areas

### Routine (Response within 24 hours)
- Minor drip, no active spreading
- Cosmetic water damage only

## Escalation Matrix

| Severity  | Owner Contact | Vendor Dispatch | Management Alert |
|-----------|---------------|-----------------|------------------|
| Emergency | Concurrent    | Immediate       | Immediate        |
| Urgent    | First (15min) | If unreachable  | Within 1 hour    |
| Routine   | First (24h)   | After approval  | Daily summary    |
```

### 2.3 Quality Gate

Before proceeding, verify:

- [ ] All videos have timestamped transcripts
- [ ] All policy documents are extracted to markdown
- [ ] Each reference file has source attribution (document, section, date)
- [ ] References are deduplicated (no conflicting information)

---

## 3. Phase 2: Atomization into Procedure Cards

### 3.1 Objective

Transform transcripts and documents into structured, machine-readable Procedure Cards that serve as the **single source of truth** for skill generation.

### 3.2 What is a Procedure Card?

A Procedure Card is a YAML file that captures:
- **Triggers**: What user says or what system event occurs
- **Inputs**: What information is required
- **Decision Logic**: If/then branching rules
- **Steps**: Ordered actions to take
- **Outputs**: What gets produced
- **Citations**: Links back to source material

### 3.3 Process

#### Step 1: Identify Discrete Procedures

Watch/read through source material and identify distinct procedures. A procedure is a discrete, repeatable process with:
- A clear trigger condition
- Defined inputs
- A sequence of steps
- Expected outputs

**Example identification from transcript:**

```
Timestamp 12:34-15:22: Maria explains how to handle leak reports
  → Procedure: "Leak Triage Protocol"

Timestamp 28:10-32:45: Maria covers after-hours emergency escalation
  → Procedure: "After-Hours Emergency Escalation"

Timestamp 45:00-48:30: Maria demonstrates the ticketing system
  → Procedure: "Ticket Creation Workflow"
```

#### Step 2: Create Procedure Cards

For each identified procedure, create a YAML file:

```yaml
# 03-procedure-cards/leak-triage.yaml
procedure_id: LEAK-001
version: 1.0.0
name: Leak Triage Protocol
category: workflow  # policy | workflow | tool-use

trigger_signals:
  user_intent:
    - "water leak"
    - "flooding"
    - "pipe burst"
    - "water damage"
    - "water coming from"
  system_events:
    - event_type: sensor_alert
      sensor_type: water_sensor
      condition: "value > 0"

required_inputs:
  - field: unit_number
    type: string
    required: true
    prompt: "What unit is affected?"
    
  - field: severity
    type: enum
    values: [emergency, urgent, routine]
    required: true
    determination: "Use classification criteria to determine"
    
  - field: description
    type: string
    required: true
    prompt: "Describe what you're seeing"
    
  - field: photos
    type: image[]
    required: false
    prompt: "Can you share any photos?"

decision_tree:
  - condition: "severity == 'emergency'"
    actions:
      - dispatch_vendor_immediately
      - notify_management
      - contact_owner_concurrent
    escalation_time: immediate
    
  - condition: "severity == 'urgent' AND owner_unreachable_after_15min"
    actions:
      - dispatch_vendor
      - notify_management
    escalation_time: 15min
    
  - condition: "severity == 'urgent' AND owner_reachable"
    actions:
      - confirm_with_owner
      - schedule_vendor_if_approved
    escalation_time: 2h
    
  - condition: "severity == 'routine'"
    actions:
      - contact_owner
      - schedule_maintenance
    escalation_time: 24h

steps:
  - id: step_1_classify
    name: "Classify Severity"
    action: "Determine severity using classification criteria"
    inputs: [description, photos]
    outputs: [severity]
    reference: "references/policies/leak-escalation-policy.md#severity-classifications"
    
  - id: step_2_gather_info
    name: "Gather Required Information"
    action: "Collect unit number, contact info, and detailed description"
    inputs: [user_message]
    outputs: [unit_number, owner_contact, description]
    
  - id: step_3_contact_owner
    name: "Contact Owner"
    action: "Attempt owner contact via WhatsApp"
    inputs: [unit_number, owner_contact]
    outputs: [owner_contact_status]
    tools: [whatsapp_send]
    max_attempts: 2
    timeout: 15min
    skip_if: "severity == 'emergency'"
    
  - id: step_4_dispatch
    name: "Execute Dispatch Decision"
    action: "Follow decision tree for vendor dispatch"
    inputs: [severity, owner_contact_status]
    outputs: [dispatch_status, vendor_assigned]
    tools: [vendor_dispatch, ticket_create]
    
  - id: step_5_document
    name: "Create Documentation"
    action: "Generate ticket and notifications"
    inputs: [all_previous_outputs]
    outputs: [ticket_id, notification_status]
    tools: [ticket_create, notification_send]

outputs:
  - type: ticket
    template: "assets/templates/leak_ticket.md"
    required: true
    
  - type: notification
    channels: [owner_whatsapp, management_slack]
    template: "assets/templates/leak_notification.md"
    required: true
    
  - type: vendor_dispatch
    template: "assets/templates/vendor_dispatch.md"
    required_if: "dispatch_status == 'dispatched'"

forbidden_actions:
  - "Never dispatch vendor for routine issues without owner approval"
  - "Never share owner contact information with third parties"
  - "Never approve expenses over $500 without management approval"

source_citations:
  - source_id: VID-001
    timestamps: ["12:34-15:22", "28:10-29:45"]
    description: "Maria explains triage classification and owner contact protocol"
    
  - source_id: DOC-001
    sections: ["4.2.1", "4.2.3"]
    description: "Bylaw requirements for leak response and escalation"
    
  - source_id: DOC-002
    sections: ["3.1", "3.4"]
    description: "Vendor SLA response times and dispatch requirements"
```

#### Step 3: Validate Procedure Cards Against Sources

For each procedure card, verify:

```bash
# Create a validation checklist
echo "Validating LEAK-001..."
echo "[ ] Triggers match language used in VID-001 @ 12:34"
echo "[ ] Decision tree matches policy in DOC-001 Section 4.2"
echo "[ ] Forbidden actions derived from DOC-001 Section 4.2.3"
echo "[ ] All steps traceable to source timestamps"
```

### 3.4 Quality Gate

Before proceeding, verify:

- [ ] Each procedure has a unique `procedure_id`
- [ ] All trigger signals are derived from actual user language (from transcripts)
- [ ] Decision trees match policy documents exactly
- [ ] Every step has at least one source citation
- [ ] Forbidden actions are explicitly stated in source material

---

## 4. Phase 3: Skill Taxonomy Classification

### 4.1 Objective

Classify each procedure card into the appropriate skill type to enable composability and reduce skill size.

### 4.2 The Three Skill Types

#### Policy Skills
**Purpose:** Encode rules, constraints, and compliance requirements

**Characteristics:**
- Read-only knowledge (no actions taken)
- Define what CAN and CANNOT be done
- Referenced by other skills for decision-making

**Examples:**
- Quiet hours policy
- Expense approval limits
- Data privacy requirements
- Escalation thresholds

**Typical Structure:**
```
policy-skill/
├── SKILL.md           # Policy overview and quick reference
└── references/
    ├── full-policy.md # Complete policy text
    └── exceptions.md  # Edge cases and exceptions
```

#### Workflow Skills
**Purpose:** Encode step-by-step playbooks for handling specific scenarios

**Characteristics:**
- Procedural (ordered steps)
- May reference Policy Skills for constraints
- May invoke Tool-Use Skills for actions

**Examples:**
- Leak triage protocol
- Guest check-in workflow
- Complaint resolution process
- Maintenance request handling

**Typical Structure:**
```
workflow-skill/
├── SKILL.md           # Workflow overview and decision tree
├── references/
│   └── detailed-steps.md
├── scripts/
│   └── classify_input.py
└── assets/
    └── templates/
        └── output_template.md
```

#### Tool-Use Skills
**Purpose:** Encode how to operate specific systems and tools

**Characteristics:**
- Focused on a single tool/system
- Provides API patterns and examples
- May include scripts for common operations

**Examples:**
- How to use PropertyOS ticketing
- How to send WhatsApp templates
- How to query the vendor database
- How to generate reports

**Typical Structure:**
```
tool-use-skill/
├── SKILL.md           # Quick start and common operations
├── references/
│   └── api-reference.md
└── scripts/
    ├── common_operations.py
    └── templates.py
```

### 4.3 Classification Process

For each procedure card:

```yaml
# Classification worksheet
procedure_id: LEAK-001
procedure_name: "Leak Triage Protocol"

classification_analysis:
  has_decision_logic: true
  has_ordered_steps: true
  invokes_external_tools: true
  defines_constraints_only: false
  
  depends_on_policies:
    - "escalation-policy"
    - "expense-limits"
    
  uses_tools:
    - "whatsapp-messaging"
    - "ticketing-system"
    - "vendor-dispatch"

classification: workflow

rationale: |
  This is a workflow skill because it defines a multi-step procedure
  with decision points. It will reference the escalation-policy skill
  for constraints and invoke tool-use skills for actions.
```

### 4.4 Dependency Mapping

Create a skill dependency graph:

```
┌─────────────────────────────────────────────────────────────┐
│                      POLICY LAYER                           │
│  ┌─────────────────┐  ┌─────────────────┐                  │
│  │ escalation-     │  │ expense-        │                  │
│  │ policy          │  │ limits          │                  │
│  └────────┬────────┘  └────────┬────────┘                  │
└───────────┼────────────────────┼────────────────────────────┘
            │                    │
            ▼                    ▼
┌─────────────────────────────────────────────────────────────┐
│                     WORKFLOW LAYER                          │
│  ┌─────────────────────────────────────────┐               │
│  │         leak-triage-protocol            │               │
│  │  (references policies, invokes tools)   │               │
│  └─────────────────┬───────────────────────┘               │
└────────────────────┼────────────────────────────────────────┘
                     │
      ┌──────────────┼──────────────┐
      ▼              ▼              ▼
┌─────────────────────────────────────────────────────────────┐
│                    TOOL-USE LAYER                           │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐        │
│  │ whatsapp-    │ │ ticketing-   │ │ vendor-      │        │
│  │ messaging    │ │ system       │ │ dispatch     │        │
│  └──────────────┘ └──────────────┘ └──────────────┘        │
└─────────────────────────────────────────────────────────────┘
```

### 4.5 Quality Gate

Before proceeding, verify:

- [ ] Each procedure card has been classified
- [ ] No single skill tries to do everything (decompose if needed)
- [ ] Dependencies between skills are documented
- [ ] No circular dependencies exist

---

## 5. Phase 4: Skill Folder Generation

### 5.1 Objective

Create properly structured skill folders using Anthropic's conventions.

### 5.2 Process

#### Step 1: Initialize Skill Folder

Use the `init_skill.py` script:

```bash
# From your project root
python scripts/init_skill.py leak-triage-protocol --path 04-skills

# Output:
# ✅ Created skill directory: 04-skills/leak-triage-protocol
# ✅ Created SKILL.md
# ✅ Created scripts/example.py
# ✅ Created references/api_reference.md
# ✅ Created assets/example_asset.txt
```

#### Step 2: Populate References

Copy relevant reference documents:

```bash
# From 02-references to skill folder
cp 02-references/policies/leak-escalation-policy.md \
   04-skills/leak-triage-protocol/references/

cp 02-references/contacts/vendor-list.md \
   04-skills/leak-triage-protocol/references/
```

#### Step 3: Create Templates in Assets

```bash
mkdir -p 04-skills/leak-triage-protocol/assets/templates
```

Create output templates:

```markdown
<!-- assets/templates/leak_ticket.md -->
# Leak Incident Report

**Ticket ID:** {{ticket_id}}
**Created:** {{timestamp}}
**Unit:** {{unit_number}}

## Severity Classification
**Level:** {{severity}}
**Rationale:** {{severity_rationale}}

## Description
{{description}}

## Actions Taken
{{#each actions}}
- {{timestamp}}: {{action}}
{{/each}}

## Owner Contact
- **Status:** {{owner_contact_status}}
- **Attempts:** {{contact_attempts}}

## Vendor Dispatch
- **Dispatched:** {{dispatch_status}}
- **Vendor:** {{vendor_name}}
- **ETA:** {{vendor_eta}}
```

#### Step 4: Create Helper Scripts

If the procedure requires deterministic logic:

```python
# scripts/classify_severity.py
#!/usr/bin/env python3
"""
Classify leak severity based on description and photos.

Usage:
    python classify_severity.py --description "..." [--photos path1 path2]
    
Returns:
    JSON with severity classification and rationale
"""

import argparse
import json
import sys

EMERGENCY_KEYWORDS = [
    "flooding", "burst", "gushing", "multiple units", 
    "electrical", "ceiling collapsed"
]

URGENT_KEYWORDS = [
    "spreading", "active leak", "getting worse", 
    "soaking", "dripping fast"
]

def classify(description: str, has_photos: bool = False) -> dict:
    description_lower = description.lower()
    
    # Check for emergency indicators
    emergency_matches = [kw for kw in EMERGENCY_KEYWORDS if kw in description_lower]
    if emergency_matches:
        return {
            "severity": "emergency",
            "confidence": "high",
            "rationale": f"Emergency keywords detected: {emergency_matches}",
            "requires_confirmation": False
        }
    
    # Check for urgent indicators
    urgent_matches = [kw for kw in URGENT_KEYWORDS if kw in description_lower]
    if urgent_matches:
        return {
            "severity": "urgent",
            "confidence": "medium" if not has_photos else "high",
            "rationale": f"Urgent keywords detected: {urgent_matches}",
            "requires_confirmation": not has_photos
        }
    
    # Default to routine
    return {
        "severity": "routine",
        "confidence": "medium",
        "rationale": "No emergency or urgent indicators detected",
        "requires_confirmation": True
    }

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("--description", required=True)
    parser.add_argument("--photos", nargs="*", default=[])
    args = parser.parse_args()
    
    result = classify(args.description, bool(args.photos))
    print(json.dumps(result, indent=2))

if __name__ == "__main__":
    main()
```

#### Step 5: Remove Unused Example Files

```bash
# Delete the auto-generated example files you don't need
rm 04-skills/leak-triage-protocol/scripts/example.py
rm 04-skills/leak-triage-protocol/references/api_reference.md
rm 04-skills/leak-triage-protocol/assets/example_asset.txt
```

### 5.3 Final Folder Structure

```
04-skills/leak-triage-protocol/
├── SKILL.md                          # Main skill file (edit in Phase 5)
├── references/
│   ├── leak-escalation-policy.md     # Policy constraints
│   └── vendor-list.md                # Vendor contact info
├── scripts/
│   └── classify_severity.py          # Deterministic classification
└── assets/
    └── templates/
        ├── leak_ticket.md            # Ticket output template
        └── leak_notification.md      # Notification template
```

### 5.4 Quality Gate

Before proceeding, verify:

- [ ] Skill folder created via `init_skill.py`
- [ ] All referenced documents exist in `references/`
- [ ] All output templates exist in `assets/templates/`
- [ ] Scripts are executable and tested
- [ ] No example/placeholder files remain

---

## 6. Phase 5: SKILL.md Authoring

### 6.1 Objective

Write the SKILL.md file following Anthropic's conventions for maximum effectiveness.

### 6.2 SKILL.md Structure

```markdown
---
name: skill-name-in-kebab-case
description: |
  [CRITICAL: This is the primary trigger mechanism. Be comprehensive.]
  One-paragraph description of what the skill does AND when to use it.
  Include specific scenarios, keywords, and trigger conditions.
---

# Skill Title

## Quick Reference
[Immediate lookup for common cases - 5-10 lines max]

## Workflow / Decision Tree
[Visual or structured decision logic]

## Detailed Steps
[Only if needed beyond quick reference]

## Scripts
[Brief description of available scripts and when to use them]

## References
[List of reference files and when to load them]
```

### 6.3 Writing the Description (Most Important)

The `description` field in the YAML frontmatter is the **primary trigger mechanism**. It must:

1. Explain what the skill does
2. List specific scenarios when it should trigger
3. Include keywords users might say

**Bad Example:**
```yaml
description: Handles leaks in buildings
```

**Good Example:**
```yaml
description: |
  Handles water leak incidents in residential properties including severity 
  triage, owner notification, vendor dispatch, and incident documentation. 
  Use when: (1) User reports water leak, flooding, pipe burst, or water damage,
  (2) Water sensor triggers alert, (3) Maintenance requests involve plumbing 
  emergencies, (4) User asks about leak procedures or escalation policies.
```

### 6.4 Complete SKILL.md Example

```markdown
---
name: leak-triage-protocol
description: |
  Handles water leak incidents in residential properties including severity 
  triage, owner notification, vendor dispatch, and incident documentation. 
  Use when: (1) User reports water leak, flooding, pipe burst, or water damage,
  (2) Water sensor triggers alert, (3) Maintenance requests involve plumbing 
  emergencies, (4) User asks about leak procedures or escalation policies.
---

# Leak Triage Protocol

## Quick Reference

| Severity  | Response Time | Owner Contact | Dispatch        |
|-----------|---------------|---------------|-----------------|
| Emergency | Immediate     | Concurrent    | Immediate       |
| Urgent    | 2 hours       | First (15min) | If unreachable  |
| Routine   | 24 hours      | Required      | After approval  |

**Emergency indicators:** flooding, burst pipe, multiple units, near electrical  
**Urgent indicators:** active leak, spreading, getting worse  
**Routine indicators:** minor drip, no spreading, cosmetic only

## Workflow

### 1. Classify Severity

Determine severity using `scripts/classify_severity.py` or manual assessment:

```bash
python scripts/classify_severity.py --description "user's description" --photos photo1.jpg
```

If confidence is not "high", ask clarifying questions before proceeding.

### 2. Gather Required Information

Collect before taking action:
- Unit number (required)
- Description of issue (required)
- Photos if available (helps classification)
- Owner contact status (will be determined)

### 3. Execute Based on Severity

**Emergency Path:**
1. Dispatch vendor immediately
2. Notify management via Slack
3. Contact owner (concurrent, informational)
4. Create incident ticket

**Urgent Path:**
1. Attempt owner contact via WhatsApp (2 attempts, 15 min total)
2. If unreachable → dispatch vendor, notify management
3. If reachable → confirm dispatch with owner
4. Create incident ticket

**Routine Path:**
1. Contact owner via WhatsApp
2. Schedule maintenance upon owner approval
3. Create ticket for tracking

### 4. Documentation

Create ticket using template: `assets/templates/leak_ticket.md`

All incidents require:
- Severity classification with rationale
- Timeline of actions taken
- Owner contact attempts and outcomes
- Vendor dispatch details (if applicable)

## Forbidden Actions

- **Never** dispatch vendor for routine issues without owner approval
- **Never** approve expenses over $500 without management approval
- **Never** share owner personal contact info with vendors

## Scripts

- `scripts/classify_severity.py` - Classify leak severity from description
  - Input: `--description "text" [--photos path1 path2]`
  - Output: JSON with severity, confidence, rationale

## References

- `references/leak-escalation-policy.md` - Full policy with all edge cases
- `references/vendor-list.md` - Approved vendors with contact info and SLAs

Load references when:
- User asks about specific policy details
- Edge case not covered in quick reference
- Need vendor contact information
```

### 6.5 Quality Gate

Before proceeding, verify:

- [ ] YAML frontmatter has `name` and comprehensive `description`
- [ ] Description includes trigger scenarios and keywords
- [ ] Quick reference fits on one screen
- [ ] Decision tree is clear and unambiguous
- [ ] All scripts and references are documented
- [ ] Forbidden actions are explicitly stated
- [ ] SKILL.md is under 500 lines (use references for overflow)

---

## 7. Phase 6: Eval Suite Generation

### 7.1 Objective

Create evaluation test suites that validate skill behavior against ground truth.

### 7.2 Two-Tier Eval Strategy

#### Tier 1: Grounded Tests
- Derived directly from source material
- Each test case traceable to timestamp or document section
- Represent real-world scenarios captured in training

#### Tier 2: Synthetic Tests
- Mutations of grounded tests
- Test edge cases, combinations, and stress scenarios
- Must link back to grounded test via `derived_from`

### 7.3 Grounded Test Format

```jsonl
// 05-evals/grounded/leak-triage-protocol.jsonl
{"id": "LEAK-GT-001", "source": {"type": "video", "id": "VID-001", "timestamp": "12:34-12:58"}, "input": "There's water pouring from my ceiling in unit 405!", "expected": {"severity": "urgent", "first_action": "classify_severity", "questions_to_ask": ["Is it still actively leaking?", "Can you see where it's coming from?"]}}
{"id": "LEAK-GT-002", "source": {"type": "video", "id": "VID-001", "timestamp": "13:45-14:12"}, "input": "Small drip under my kitchen sink, noticed it yesterday", "expected": {"severity": "routine", "first_action": "contact_owner", "questions_to_ask": ["Is it getting worse?", "Have you turned off the water valve?"]}}
{"id": "LEAK-GT-003", "source": {"type": "document", "id": "DOC-001", "section": "4.2.1"}, "input": "FLOOD! Water everywhere in the hallway, coming from multiple units!", "expected": {"severity": "emergency", "first_action": "dispatch_vendor_immediately", "concurrent_actions": ["notify_management", "contact_owners"]}}
```

### 7.4 Synthetic Test Format

```jsonl
// 05-evals/synthetic/leak-triage-protocol.jsonl
{"id": "LEAK-SYN-001", "derived_from": "LEAK-GT-001", "mutation": "conflicting_info", "input": "Water from ceiling in 405, but my neighbor says it already stopped", "expected": {"action": "ask_clarifying_question", "question_type": "verify_current_status"}}
{"id": "LEAK-SYN-002", "derived_from": "LEAK-GT-002", "mutation": "severity_escalation", "input": "That small drip I mentioned? It's now spreading to my living room carpet", "expected": {"severity_change": "routine_to_urgent", "action": "reclassify_and_escalate"}}
{"id": "LEAK-SYN-003", "derived_from": "LEAK-GT-001", "mutation": "missing_info", "input": "There's a leak", "expected": {"action": "gather_information", "required_questions": ["What unit?", "Can you describe what you're seeing?", "Is water actively flowing?"]}}
{"id": "LEAK-SYN-004", "derived_from": "LEAK-GT-003", "mutation": "after_hours", "input": "FLOOD in hallway! It's 2am and I can't reach anyone!", "expected": {"severity": "emergency", "action": "dispatch_vendor_immediately", "note": "after_hours_does_not_change_emergency_protocol"}}
```

### 7.5 Mutation Types

Use these standard mutations for synthetic tests:

| Mutation Type | Description | Example |
|---------------|-------------|---------|
| `conflicting_info` | Add contradictory information | "leak" + "stopped" |
| `missing_info` | Remove required context | No unit number |
| `severity_escalation` | Increase severity mid-conversation | Drip → flooding |
| `severity_deescalation` | Decrease severity mid-conversation | Flood → contained |
| `after_hours` | Add time constraint | 2am scenario |
| `owner_unreachable` | Owner cannot be contacted | No response after attempts |
| `budget_constraint` | Near or over expense limit | $450 repair estimate |
| `multi_issue` | Multiple problems at once | Leak + electrical concern |
| `adversarial` | User pushes back on process | "Just send someone now!" |

### 7.6 Creating the Eval Rubric

```yaml
# 05-evals/rubrics/leak-triage-protocol.yaml
skill_id: leak-triage-protocol
version: 1.0.0

dimensions:
  - name: severity_classification
    weight: 0.25
    description: "Correctly classifies leak severity"
    scoring:
      correct: 1.0
      partially_correct: 0.5  # Right category, wrong rationale
      incorrect: 0.0
    
  - name: information_gathering
    weight: 0.20
    description: "Asks appropriate questions before acting"
    scoring:
      all_required_questions: 1.0
      some_required_questions: 0.5
      acted_without_required_info: 0.0
    
  - name: procedure_adherence
    weight: 0.25
    description: "Follows correct procedure for severity level"
    scoring:
      correct_procedure: 1.0
      minor_deviation: 0.7
      wrong_procedure: 0.0
    
  - name: forbidden_action_avoidance
    weight: 0.20
    description: "Does not perform forbidden actions"
    scoring:
      no_violations: 1.0
      violation: 0.0
    negative: true  # Any violation is critical
    
  - name: output_compliance
    weight: 0.10
    description: "Uses correct templates and formats"
    scoring:
      correct_format: 1.0
      minor_issues: 0.7
      wrong_format: 0.3

passing_threshold: 0.85
critical_dimensions: ["forbidden_action_avoidance"]  # Must score 1.0
```

### 7.7 Quality Gate

Before proceeding, verify:

- [ ] Grounded tests cover all major scenarios from source material
- [ ] Each grounded test has source citation
- [ ] Synthetic tests link back to grounded tests via `derived_from`
- [ ] Rubric covers all critical behaviors
- [ ] Forbidden actions have dedicated test cases
- [ ] At least 10 grounded tests per skill
- [ ] At least 20 synthetic tests per skill

---

## 8. Phase 7: Gauntlet Testing

### 8.1 Objective

Run the eval suite against the skill and measure performance.

### 8.2 Test Runner Setup

```python
# scripts/run_gauntlet.py
#!/usr/bin/env python3
"""
Run evaluation gauntlet against a skill.

Usage:
    python run_gauntlet.py --skill leak-triage-protocol --eval-dir 05-evals
"""

import argparse
import json
from pathlib import Path
import yaml

def load_rubric(skill_name: str, eval_dir: Path) -> dict:
    rubric_path = eval_dir / "rubrics" / f"{skill_name}.yaml"
    with open(rubric_path) as f:
        return yaml.safe_load(f)

def load_test_cases(skill_name: str, eval_dir: Path) -> list:
    cases = []
    
    # Load grounded tests
    grounded_path = eval_dir / "grounded" / f"{skill_name}.jsonl"
    if grounded_path.exists():
        with open(grounded_path) as f:
            for line in f:
                case = json.loads(line)
                case["test_type"] = "grounded"
                cases.append(case)
    
    # Load synthetic tests
    synthetic_path = eval_dir / "synthetic" / f"{skill_name}.jsonl"
    if synthetic_path.exists():
        with open(synthetic_path) as f:
            for line in f:
                case = json.loads(line)
                case["test_type"] = "synthetic"
                cases.append(case)
    
    return cases

def run_test_case(case: dict, skill_path: Path) -> dict:
    """
    Run a single test case against the skill.
    
    This is where you integrate with your AI runtime.
    Returns scores for each rubric dimension.
    """
    # TODO: Integrate with your AI agent runtime
    # This will depend on your specific setup (Claude API, etc.)
    
    # Placeholder return
    return {
        "case_id": case["id"],
        "test_type": case["test_type"],
        "scores": {
            "severity_classification": 1.0,
            "information_gathering": 0.8,
            "procedure_adherence": 1.0,
            "forbidden_action_avoidance": 1.0,
            "output_compliance": 0.9
        },
        "response": "...",
        "notes": ""
    }

def calculate_final_score(results: list, rubric: dict) -> dict:
    dimensions = {d["name"]: d for d in rubric["dimensions"]}
    
    # Calculate weighted average per dimension
    dimension_scores = {}
    for dim_name in dimensions:
        scores = [r["scores"].get(dim_name, 0) for r in results]
        dimension_scores[dim_name] = sum(scores) / len(scores)
    
    # Calculate weighted final score
    final_score = 0
    for dim_name, dim_config in dimensions.items():
        final_score += dimension_scores[dim_name] * dim_config["weight"]
    
    # Check critical dimensions
    critical_pass = True
    for critical_dim in rubric.get("critical_dimensions", []):
        if dimension_scores[critical_dim] < 1.0:
            critical_pass = False
    
    return {
        "final_score": final_score,
        "dimension_scores": dimension_scores,
        "passing": final_score >= rubric["passing_threshold"] and critical_pass,
        "critical_pass": critical_pass,
        "threshold": rubric["passing_threshold"]
    }

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("--skill", required=True)
    parser.add_argument("--eval-dir", default="05-evals")
    parser.add_argument("--skill-dir", default="04-skills")
    parser.add_argument("--output", default="gauntlet_results.json")
    args = parser.parse_args()
    
    eval_dir = Path(args.eval_dir)
    skill_path = Path(args.skill_dir) / args.skill
    
    print(f"🏃 Running gauntlet for: {args.skill}")
    
    # Load rubric and test cases
    rubric = load_rubric(args.skill, eval_dir)
    test_cases = load_test_cases(args.skill, eval_dir)
    
    print(f"📋 Loaded {len(test_cases)} test cases")
    print(f"📊 Rubric dimensions: {[d['name'] for d in rubric['dimensions']]}")
    
    # Run all test cases
    results = []
    for i, case in enumerate(test_cases):
        print(f"  Running {case['id']} ({i+1}/{len(test_cases)})...")
        result = run_test_case(case, skill_path)
        results.append(result)
    
    # Calculate final score
    summary = calculate_final_score(results, rubric)
    
    # Output results
    output = {
        "skill": args.skill,
        "summary": summary,
        "results": results
    }
    
    with open(args.output, "w") as f:
        json.dump(output, f, indent=2)
    
    # Print summary
    print("\n" + "="*50)
    print("GAUNTLET RESULTS")
    print("="*50)
    print(f"Final Score: {summary['final_score']:.2%}")
    print(f"Threshold: {summary['threshold']:.2%}")
    print(f"Critical Pass: {'✅' if summary['critical_pass'] else '❌'}")
    print(f"Overall: {'✅ PASS' if summary['passing'] else '❌ FAIL'}")
    print("\nDimension Scores:")
    for dim, score in summary["dimension_scores"].items():
        print(f"  {dim}: {score:.2%}")

if __name__ == "__main__":
    main()
```

### 8.3 Running the Gauntlet

```bash
python scripts/run_gauntlet.py --skill leak-triage-protocol

# Output:
# 🏃 Running gauntlet for: leak-triage-protocol
# 📋 Loaded 35 test cases
# 📊 Rubric dimensions: ['severity_classification', 'information_gathering', ...]
#   Running LEAK-GT-001 (1/35)...
#   Running LEAK-GT-002 (2/35)...
#   ...
#
# ==================================================
# GAUNTLET RESULTS
# ==================================================
# Final Score: 91.2%
# Threshold: 85.0%
# Critical Pass: ✅
# Overall: ✅ PASS
#
# Dimension Scores:
#   severity_classification: 94.0%
#   information_gathering: 88.0%
#   procedure_adherence: 92.0%
#   forbidden_action_avoidance: 100.0%
#   output_compliance: 85.0%
```

### 8.4 Failure Analysis

When tests fail, analyze the pattern:

```bash
# Extract failing cases
jq '.results[] | select(.scores.procedure_adherence < 0.7)' gauntlet_results.json

# Common failure patterns:
# 1. Classification errors → Update classify_severity.py or add examples
# 2. Missing questions → Add to SKILL.md required_inputs
# 3. Wrong procedure → Clarify decision tree in SKILL.md
# 4. Forbidden actions → Add explicit warnings
```

### 8.5 Quality Gate

Before proceeding, verify:

- [ ] All grounded tests pass (100%)
- [ ] Synthetic tests pass at ≥85% rate
- [ ] No forbidden action violations (critical pass)
- [ ] Failure patterns are understood and documented

---

## 9. Phase 8: Package and Deploy

### 9.1 Objective

Package the validated skill for distribution.

### 9.2 Pre-Packaging Checklist

```bash
# Final validation
python scripts/quick_validate.py 04-skills/leak-triage-protocol

# Expected output:
# ✅ Skill 'leak-triage-protocol' is valid
```

### 9.3 Package the Skill

```bash
python scripts/package_skill.py 04-skills/leak-triage-protocol 06-packaged/

# Output:
# 📦 Packaging skill: 04-skills/leak-triage-protocol
#    Output directory: 06-packaged/
#
# 🔍 Validating skill...
# ✅ Skill 'leak-triage-protocol' is valid
#
#   Added: leak-triage-protocol/SKILL.md
#   Added: leak-triage-protocol/references/leak-escalation-policy.md
#   Added: leak-triage-protocol/references/vendor-list.md
#   Added: leak-triage-protocol/scripts/classify_severity.py
#   Added: leak-triage-protocol/assets/templates/leak_ticket.md
#   Added: leak-triage-protocol/assets/templates/leak_notification.md
#
# ✅ Successfully packaged skill to: 06-packaged/leak-triage-protocol.skill
```

### 9.4 Deployment

The `.skill` file is a zip archive that can be:

1. **Uploaded to Claude** via the Skills interface
2. **Deployed to Claude Code** in the skills directory
3. **Distributed** to team members for local use

### 9.5 Quality Gate

Before deploying to production:

- [ ] Package created successfully
- [ ] Gauntlet score ≥ 85%
- [ ] No critical dimension failures
- [ ] Skill tested in staging environment
- [ ] Rollback plan documented

---

## 10. Phase 9: Governance and Iteration

### 10.1 Objective

Maintain skill quality over time through systematic governance.

### 10.2 Version Control

Add version metadata to procedure cards:

```yaml
# In procedure card YAML
procedure_id: LEAK-001
version: 1.2.0
last_updated: 2025-01-04
changelog:
  - version: 1.2.0
    date: 2025-01-04
    changes: "Added photo classification step"
    author: "Wesley"
  - version: 1.1.0
    date: 2024-12-15
    changes: "Updated escalation matrix per new vendor SLA"
    author: "Wesley"
  - version: 1.0.0
    date: 2024-11-01
    changes: "Initial version"
    author: "Wesley"
```

### 10.3 Iteration Workflow

When a skill fails in production:

```
┌─────────────────────────────────────────────────────────────┐
│  1. CAPTURE FAILURE                                         │
│     - Document the failing scenario                         │
│     - Record actual vs expected behavior                    │
│     - Note any user feedback                                │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  2. ADD TO EVAL SUITE                                       │
│     - Create new test case in 05-evals/grounded/ or        │
│       05-evals/synthetic/                                   │
│     - Include source citation if from real scenario         │
│     - Run gauntlet to confirm it fails                      │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  3. TRACE TO ROOT CAUSE                                     │
│     - Is it a procedure card issue? → Update YAML           │
│     - Is it a reference gap? → Update references/           │
│     - Is it a script bug? → Fix and test script             │
│     - Is it a SKILL.md clarity issue? → Revise wording      │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  4. IMPLEMENT FIX                                           │
│     - Update relevant files                                 │
│     - Increment version number                              │
│     - Add changelog entry                                   │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  5. VALIDATE                                                │
│     - Run full gauntlet                                     │
│     - Confirm new test case passes                          │
│     - Confirm no regression in other tests                  │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  6. DEPLOY                                                  │
│     - Package updated skill                                 │
│     - Deploy to staging first                               │
│     - Monitor for 24-48 hours                               │
│     - Promote to production                                 │
└─────────────────────────────────────────────────────────────┘
```

### 10.4 What NOT to Do

**Never "self-heal" by rewriting prompts automatically.**

The correct approach:
1. Add failing case to evals
2. Trace back to source material
3. Update procedure card or reference if source supports change
4. If source doesn't support change, flag for human review
5. Regenerate SKILL.md only after human approval

### 10.5 Governance Checklist

Periodic review (monthly):

- [ ] Review gauntlet scores for all skills
- [ ] Check for skills with declining performance
- [ ] Audit procedure cards against current source materials
- [ ] Update references if policies have changed
- [ ] Archive deprecated skills

---

## Appendix A: Procedure Card Schema

Complete YAML schema for procedure cards:

```yaml
# Required fields
procedure_id: string          # Unique identifier (e.g., "LEAK-001")
version: string               # Semantic version (e.g., "1.2.0")
name: string                  # Human-readable name
category: enum                # "policy" | "workflow" | "tool-use"

# Trigger configuration
trigger_signals:
  user_intent: string[]       # Keywords/phrases that trigger this procedure
  system_events:              # Optional: system event triggers
    - event_type: string
      condition: string

# Input requirements
required_inputs:
  - field: string             # Field name
    type: string              # string | enum | number | boolean | image[]
    required: boolean
    values: string[]          # For enum type
    prompt: string            # Question to ask user
    determination: string     # How to determine if not from user

# Decision logic
decision_tree:
  - condition: string         # Boolean expression
    actions: string[]         # Actions to take
    escalation_time: string   # Time constraint (e.g., "15min", "immediate")

# Procedure steps
steps:
  - id: string                # Step identifier
    name: string              # Step name
    action: string            # Description of action
    inputs: string[]          # Required inputs for this step
    outputs: string[]         # Outputs produced
    tools: string[]           # Tools/APIs to invoke
    reference: string         # Path to reference doc
    skip_if: string           # Condition to skip step
    max_attempts: number      # For retryable steps
    timeout: string           # Timeout duration

# Output configuration
outputs:
  - type: string              # Output type
    template: string          # Path to template
    channels: string[]        # For notifications
    required: boolean
    required_if: string       # Conditional requirement

# Constraints
forbidden_actions: string[]   # Actions that must never be taken

# Traceability
source_citations:
  - source_id: string         # Reference to source manifest
    timestamps: string[]      # For video sources
    sections: string[]        # For document sources
    description: string       # What this citation supports

# Metadata
changelog:
  - version: string
    date: string              # ISO date
    changes: string
    author: string
```

---

## Appendix B: Eval Rubric Template

```yaml
skill_id: string
version: string

dimensions:
  - name: string              # Dimension identifier
    weight: number            # 0.0 to 1.0, all weights must sum to 1.0
    description: string       # What this dimension measures
    scoring:
      # Define score values and their meanings
      # Example:
      correct: 1.0
      partially_correct: 0.5
      incorrect: 0.0
    negative: boolean         # If true, any failure is critical

passing_threshold: number     # 0.0 to 1.0
critical_dimensions: string[] # Dimensions that must score 1.0
```

---

## Appendix C: Common Failure Modes

### Classification Failures
**Symptom:** Skill misclassifies severity or category  
**Root Cause:** Insufficient examples or unclear criteria  
**Fix:** Add more examples to SKILL.md, improve classify script, add test cases

### Information Gathering Failures
**Symptom:** Skill acts without required information  
**Root Cause:** Required inputs not clear in SKILL.md  
**Fix:** Add explicit "gather before acting" instruction, list required fields

### Procedure Adherence Failures
**Symptom:** Skill follows wrong procedure for situation  
**Root Cause:** Decision tree ambiguous or incomplete  
**Fix:** Clarify decision tree, add edge case handling, improve condition specificity

### Forbidden Action Violations
**Symptom:** Skill performs forbidden action  
**Root Cause:** Forbidden actions not prominent enough  
**Fix:** Move forbidden actions to top of SKILL.md, add explicit warnings in relevant sections

### Template/Format Failures
**Symptom:** Output doesn't match expected format  
**Root Cause:** Template not clear or not referenced  
**Fix:** Add explicit template usage instructions, provide examples

### Trigger Failures
**Symptom:** Skill doesn't activate when it should  
**Root Cause:** Description field missing trigger keywords  
**Fix:** Add more trigger scenarios to description, include user language variations

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────┐
│  KNOWLEDGE → SKILLS PIPELINE                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. NORMALIZE SOURCES                                       │
│     └─ Transcribe videos with timestamps                    │
│     └─ Extract documents to markdown                        │
│     └─ Create source manifest                               │
│                                                             │
│  2. ATOMIZE TO PROCEDURE CARDS                              │
│     └─ One YAML per discrete procedure                      │
│     └─ Include source citations                             │
│     └─ Validate against sources                             │
│                                                             │
│  3. CLASSIFY TAXONOMY                                       │
│     └─ Policy | Workflow | Tool-Use                         │
│     └─ Map dependencies                                     │
│                                                             │
│  4. GENERATE SKILL FOLDER                                   │
│     └─ python init_skill.py <name> --path <dir>             │
│     └─ Populate references/, scripts/, assets/              │
│                                                             │
│  5. AUTHOR SKILL.MD                                         │
│     └─ Comprehensive description (triggers!)                │
│     └─ Quick reference table                                │
│     └─ Decision tree                                        │
│     └─ Forbidden actions                                    │
│                                                             │
│  6. GENERATE EVALS                                          │
│     └─ Grounded tests (with citations)                      │
│     └─ Synthetic tests (with derived_from)                  │
│     └─ Rubric with dimensions                               │
│                                                             │
│  7. RUN GAUNTLET                                            │
│     └─ python run_gauntlet.py --skill <name>                │
│     └─ Target: ≥85% score, 100% critical                    │
│                                                             │
│  8. PACKAGE                                                 │
│     └─ python package_skill.py <path> <output>              │
│                                                             │
│  9. GOVERN                                                  │
│     └─ Add failing cases to evals first                     │
│     └─ Trace to procedure card                              │
│     └─ Never auto-rewrite prompts                           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

**Document Version:** 1.0.0  
**Created:** 2025-01-04  
**Framework Compatibility:** Anthropic Skills Framework (Claude Code, Claude.ai)
