# Knowledge-to-Skill Workflow

> **Purpose**: Defines the multi-agent workflow for transforming knowledge gaps into implementable skill specifications
> **Version**: 1.0
> **Last Updated**: January 2026

---

## 🎯 Overview

This is a **4-stage pipeline** that transforms raw competitor knowledge into engineering-ready skill specifications:

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                     KNOWLEDGE-TO-SKILL PIPELINE                                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────┐      ┌──────────────┐      ┌──────────────┐      ┌──────────────┐ │
│  │   STAGE 1    │      │   STAGE 2    │      │   STAGE 3    │      │   STAGE 4    │ │
│  │              │      │              │      │              │      │              │ │
│  │  RESEARCH    │ ──▶  │   REVIEW &   │ ──▶  │ ENGINEERING  │ ──▶  │    SKILL     │ │
│  │   AGENT      │      │    PROMPT    │      │    AGENT     │      │    SPEC      │ │
│  │              │      │              │      │              │      │              │ │
│  │  Conceptual  │      │  Gap Check   │      │  Technical   │      │   Final      │ │
│  │  Knowledge   │      │  + Prompt    │      │    Spec      │      │   Output     │ │
│  └──────────────┘      └──────────────┘      └──────────────┘      └──────────────┘ │
│                                                                                      │
│       YOU                 CURSOR AI              YOU                 CURSOR AI      │
│    (triggers)            (reviews)            (triggers)            (finalizes)     │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📋 Stage Details

### STAGE 1: Research Agent → Conceptual Knowledge Document

**Who**: Research Agent (AI)
**Input**: Knowledge Gap ID from `docs/MVP_PRIORITY_GAPS.md`
**Guide**: `docs/RESEARCH_ANALYST_GUIDE.md`
**Output**: Conceptual Knowledge Document

**What Research Agent Produces**:
- Problem statement
- User workflow (high-level)
- Best-in-class implementation overview
- Basic data model
- Business rules
- Competitive analysis
- Sources cited

**Output Location**: `knowledge/[category]/KD-[SOURCE]-[NUMBER]-[skill-name].md`

**Quality Bar**: Answers "WHAT does this feature do and WHY"

---

### STAGE 2: Cursor AI → Quality Review + Engineering Prompt

**Who**: Cursor AI (me)
**Input**: Stage 1 Knowledge Document
**Output**: 
1. Quality assessment (pass/fail with feedback)
2. Custom Engineering Spec Prompt (if passed)

**What I Do**:
1. **Review** the Stage 1 document for completeness
2. **Identify** engineering gaps (missing schemas, state machines, APIs, etc.)
3. **Generate** a custom Engineering Spec Prompt tailored to that specific feature
4. **Store** the prompt in `docs/prompts/ENGINEERING_SPEC_PROMPT_[FEATURE].md`

**Quality Bar**: Prompt is specific enough that Engineering Agent can produce implementable specs

---

### STAGE 3: Engineering Agent → Technical Specification

**Who**: Engineering Agent (AI)
**Input**: Engineering Spec Prompt from Stage 2
**Guide**: The custom prompt from Stage 2
**Output**: Engineering Specification Document

**What Engineering Agent Produces**:
- Technical architecture diagrams
- Complete data schemas (JSON/YAML)
- State machines with all transitions
- API specifications (endpoints, request/response)
- Security model
- Error handling
- Performance requirements

**Output Location**: `knowledge/[category]/ES-[SOURCE]-[NUMBER]-[skill-name].md`

**Quality Bar**: Answers "HOW do we build this - exactly"

---

### STAGE 4: Cursor AI → Final Skill Specification

**Who**: Cursor AI (me)
**Input**: Stage 3 Engineering Specification
**Output**: 
1. Updated Master Skill Registry entries
2. Tool specifications (if applicable)
3. Implementation tickets/stories
4. Dependency mapping

**What I Produce**:
- Formal SKILL entries with full specifications
- TOOL entries (if the skill requires building tools)
- User stories / acceptance criteria
- Technical dependencies identified
- Integration points mapped
- Effort estimates (T-shirt sizing)

**Output Location**: 
- `registry/MASTER_SKILL_REGISTRY.md` (updated entries)
- `specs/[category]/SPEC-[SKILL-ID].md` (detailed specs)

**Quality Bar**: Engineering team can create tickets and start building

---

## 🔄 Complete Workflow Steps

### Step-by-Step Process

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ STEP 1: You trigger Research Agent                                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│   You → Research Agent:                                                              │
│   "Research GAP-HOAI-001 using docs/RESEARCH_ANALYST_GUIDE.md"                      │
│                                                                                      │
│   Research Agent → Output:                                                           │
│   knowledge/ai-workforce/KD-HOAI-001-ai-workforce-architecture.md                   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ STEP 2: You bring Stage 1 output to Cursor AI                                        │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│   You → Cursor AI:                                                                   │
│   "Review this knowledge document and create engineering prompt"                     │
│   [attach/share the Stage 1 document]                                               │
│                                                                                      │
│   Cursor AI → Output:                                                                │
│   1. Quality assessment (7/10, missing X, Y, Z)                                     │
│   2. docs/prompts/ENGINEERING_SPEC_PROMPT_[FEATURE].md                              │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ STEP 3: You trigger Engineering Agent                                                │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│   You → Engineering Agent:                                                           │
│   "Produce engineering spec using docs/prompts/ENGINEERING_SPEC_PROMPT_[FEATURE].md"│
│                                                                                      │
│   Engineering Agent → Output:                                                        │
│   knowledge/ai-workforce/ES-HOAI-001-ai-workforce-architecture.md                   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ STEP 4: You bring Stage 3 output to Cursor AI                                        │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│   You → Cursor AI:                                                                   │
│   "Create final skill specs from this engineering document"                          │
│   [attach/share the Stage 3 document]                                               │
│                                                                                      │
│   Cursor AI → Output:                                                                │
│   1. Updated MASTER_SKILL_REGISTRY.md entries                                       │
│   2. specs/ai-workforce/SPEC-SKILL-261-268.md (detailed specs)                      │
│   3. TOOL definitions (if needed)                                                    │
│   4. User stories / tickets                                                          │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📁 File Structure

```
RawKnowledgetoSkill/
│
├── docs/
│   ├── RESEARCH_ANALYST_GUIDE.md        ← Stage 1 guide
│   ├── MVP_PRIORITY_GAPS.md             ← What to research
│   ├── KNOWLEDGE_TO_SKILL_WORKFLOW.md   ← This file
│   └── prompts/
│       └── ENGINEERING_SPEC_PROMPT_*.md ← Stage 2 outputs (custom prompts)
│
├── knowledge/
│   ├── README.md
│   ├── ai-workforce/
│   │   ├── KD-HOAI-001-*.md             ← Stage 1 outputs
│   │   └── ES-HOAI-001-*.md             ← Stage 3 outputs
│   ├── communication/
│   ├── pricing/
│   └── operations/
│
├── specs/                                ← NEW: Stage 4 outputs
│   ├── README.md
│   ├── ai-workforce/
│   │   └── SPEC-SKILL-261-268.md
│   ├── communication/
│   └── pricing/
│
├── registry/
│   └── MASTER_SKILL_REGISTRY.md         ← Updated in Stage 4
│
└── competitors/
    └── [competitor]/
        ├── SKILL_INVENTORY.md
        └── KNOWLEDGE_GAPS.md            ← Source of gaps
```

---

## 📝 Naming Conventions

| Stage | Prefix | Example |
|-------|--------|---------|
| Stage 1 (Conceptual) | `KD-` | `KD-HOAI-001-ai-workforce-architecture.md` |
| Stage 2 (Prompt) | `ENGINEERING_SPEC_PROMPT_` | `ENGINEERING_SPEC_PROMPT_AI_WORKFORCE.md` |
| Stage 3 (Engineering) | `ES-` | `ES-HOAI-001-ai-workforce-architecture.md` |
| Stage 4 (Skill Spec) | `SPEC-` | `SPEC-SKILL-261-268.md` |

---

## 🎯 Your Role (Orchestrator)

You are the **orchestrator** who:

1. **Triggers** Stage 1 by giving Research Agent a gap to research
2. **Bridges** Stage 1→2 by bringing output to Cursor AI
3. **Triggers** Stage 3 by giving Engineering Agent the prompt
4. **Bridges** Stage 3→4 by bringing output to Cursor AI
5. **Approves** final specs before they go to engineering team

```
You ──trigger──▶ Research Agent
                      │
                      ▼ (output)
You ◀──receive───────┘
  │
  └──bring to──▶ Cursor AI
                      │
                      ▼ (prompt)
You ◀──receive───────┘
  │
  └──trigger──▶ Engineering Agent
                      │
                      ▼ (output)
You ◀──receive───────┘
  │
  └──bring to──▶ Cursor AI
                      │
                      ▼ (final specs)
You ◀──receive───────┘
  │
  └──approve──▶ Engineering Team
```

---

## ✅ Quality Gates

### Gate 1: After Stage 1 (Research)
- [ ] Problem clearly stated
- [ ] User workflow documented
- [ ] At least 3 sources cited
- [ ] Competitive analysis included
- [ ] Recommendations provided

### Gate 2: After Stage 2 (Prompt)
- [ ] All engineering gaps identified
- [ ] Prompt requests specific schemas
- [ ] Prompt requests state machines
- [ ] Prompt requests API specs
- [ ] Quality checklist included

### Gate 3: After Stage 3 (Engineering Spec)
- [ ] All prompt sections completed
- [ ] Schemas are valid JSON/YAML
- [ ] State machines are complete
- [ ] APIs have request/response
- [ ] No placeholder text

### Gate 4: After Stage 4 (Skill Spec)
- [ ] SKILL entries updated in registry
- [ ] User stories are actionable
- [ ] Dependencies identified
- [ ] Effort estimated
- [ ] Ready for sprint planning

---

## 📊 Progress Tracking

### Per-Gap Tracking Template

```markdown
## GAP-HOAI-001: AI Workforce Architecture

| Stage | Status | Output | Date |
|-------|--------|--------|------|
| Stage 1 | ✅ Complete | KD-HOAI-001-*.md | 2026-01-05 |
| Stage 2 | ✅ Complete | ENGINEERING_SPEC_PROMPT_AI_WORKFORCE.md | 2026-01-05 |
| Stage 3 | 🔄 In Progress | - | - |
| Stage 4 | ⏳ Pending | - | - |

### Notes:
- Research agent completed Stage 1
- Prompt created for Engineering agent
- Waiting for Engineering agent output
```

---

## 🚀 Getting Started

### For Your Next Gap:

1. **Pick a gap** from `docs/MVP_PRIORITY_GAPS.md`
2. **Tell Research Agent**: 
   ```
   Research [GAP-ID] using docs/RESEARCH_ANALYST_GUIDE.md
   Save output to knowledge/[category]/KD-[SOURCE]-[NUMBER]-[name].md
   ```
3. **Bring output to me** (Cursor AI) for review + prompt generation
4. **Give prompt to Engineering Agent**
5. **Bring engineering spec to me** for final skill specification

---

## 📞 Communication Templates

### To Research Agent:
```
Research GAP-[ID]: [Name]

Use this guide: docs/RESEARCH_ANALYST_GUIDE.md
Reference: competitors/[name]/KNOWLEDGE_GAPS.md

Save output to: knowledge/[category]/KD-[SOURCE]-[NUMBER]-[name].md

Focus on: WHAT this feature does, WHY it matters, WHO does it best
```

### To Cursor AI (Stage 2):
```
Review this Stage 1 knowledge document and:
1. Provide quality assessment
2. Create custom Engineering Spec Prompt

Document: [path or paste content]
```

### To Engineering Agent:
```
Produce an engineering specification using this prompt:
docs/prompts/ENGINEERING_SPEC_PROMPT_[FEATURE].md

Save output to: knowledge/[category]/ES-[SOURCE]-[NUMBER]-[name].md

Include: schemas, state machines, APIs, security, performance
```

### To Cursor AI (Stage 4):
```
Create final skill specifications from this engineering document:
1. Update MASTER_SKILL_REGISTRY.md
2. Create detailed spec in specs/[category]/
3. Generate user stories
4. Identify dependencies

Document: [path or paste content]
```

---

## 🎉 Expected Outcomes

After completing all 4 stages for a gap, you will have:

1. **Conceptual understanding** (Stage 1) - What & Why
2. **Custom prompt** (Stage 2) - Tailored engineering questions
3. **Technical specification** (Stage 3) - How, exactly
4. **Implementation-ready specs** (Stage 4):
   - Updated skill registry
   - Detailed spec document
   - User stories
   - Dependency map
   - Effort estimates

**Your engineering team can then create tickets and start building!**

