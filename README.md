# Raw Knowledge to Skills Pipeline

> **Industrialized AI Skill Manufacturing** — Transform unstructured domain knowledge into production-ready AI Skills.

## 🎯 Purpose

This repository contains the complete methodology and tools for converting raw knowledge sources (videos, documents, interviews, SOPs) into deployable AI Skills compatible with Claude Code, OpenAI Codex, and other agentic runtimes.

## 🚀 Quick Start

### 1. Initialize Your AI Knowledge Engineer

Copy the contents of [`docs/methodology/INITIALIZE_KNOWLEDGE_ENGINEER.txt`](docs/methodology/INITIALIZE_KNOWLEDGE_ENGINEER.txt) and paste it into your AI agent (Claude, GPT-4, etc.).

### 2. Provide Raw Knowledge

```
Here is [a transcript / document / interview notes] about [topic].
Please process this through the Knowledge-to-Skills pipeline.
```

### 3. Get Production-Ready Skills

The AI will produce:
- ✅ Source Manifest (cataloged inputs)
- ✅ Procedure Cards (machine-readable workflows)
- ✅ SKILL.md files (deployable skills)
- ✅ Eval Suites (test cases)
- ✅ Gauntlet Report (quality validation)

---

## 📁 Repository Structure

```
RawKnowledgetoSkill/
├── README.md                           ← You are here
│
└── docs/
    ├── methodology/                    # CORE PIPELINE
    │   ├── INITIALIZE_KNOWLEDGE_ENGINEER.txt   ← Copy-paste to init agent
    │   ├── THE_BIG_PICTURE.md                  ← Context & ecosystem
    │   ├── README.md                           ← Full 9-phase pipeline
    │   ├── AI_KNOWLEDGE_ENGINEER_PROMPT.md     ← Complete agent prompt
    │   ├── QUICK_START.md                      ← Quick reference
    │   │
    │   ├── templates/
    │   │   ├── source_manifest.yaml            ← Catalog raw sources
    │   │   ├── procedure_card.yaml             ← Core workflow template
    │   │   └── rubric_template.yaml            ← Eval scoring rubric
    │   │
    │   └── phases/
    │       └── PHASE_01_SOURCE_NORMALIZATION.md
    │
    ├── guides/                         # SUPPORTING DOCS
    │   ├── knowledge-to-skills-methodology.md  ← Original methodology
    │   ├── BA_WORKFLOW_GUIDE.md                ← Interview techniques
    │   └── BA_ROLE_TRANSFORMATION.md           ← Role overview
    │
    ├── templates/
    │   └── SKILL_REQUIREMENTS_TEMPLATE.md      ← Alternative template
    │
    └── examples/
        └── SKILL_REQ_electrical_maintenance_triage.md  ← Worked example
```

---

## 📊 The 9-Phase Pipeline

```
RAW KNOWLEDGE ──────────────────────────────────────────► PRODUCTION AI SKILLS

┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐
│  1. SOURCE      │   │  2. KNOWLEDGE   │   │  3. PROCEDURE   │
│  NORMALIZATION  │──►│  EXTRACTION     │──►│  CARD GEN       │
│  Transcribe,    │   │  Structured     │   │  Machine-       │
│  catalog        │   │  analysis       │   │  readable YAML  │
└─────────────────┘   └─────────────────┘   └─────────────────┘
         │                                           │
         ▼                                           ▼
┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐
│  4. SKILL       │   │  5. SKILL       │   │  6. EVAL SUITE  │
│  TAXONOMY       │◄──│  FOLDER GEN     │──►│  GENERATION     │
│  Classify,      │   │  SKILL.md +     │   │  Test cases     │
│  map deps       │   │  scripts        │   │  from sources   │
└─────────────────┘   └─────────────────┘   └─────────────────┘
                              │                      │
                              ▼                      ▼
                     ┌─────────────────┐   ┌─────────────────┐
                     │  7. GAUNTLET    │   │  8. PACKAGE     │
                     │  TESTING        │◄──│  & DEPLOY       │
                     │  ≥85% score     │   │  .skill pkg     │
                     │  100% forbidden │   │  stage→prod     │
                     └─────────────────┘   └─────────────────┘
                              │
                              ▼
                     ┌─────────────────┐
                     │  9. GOVERNANCE  │
                     │  Monitor, fix   │
                     │  source, iterate│
                     └─────────────────┘
```

---

## 🔑 Core Principles

| Principle | Description |
|-----------|-------------|
| **100% Traceability** | Every claim cites a source (timestamp, section, quote) |
| **Exact Wording** | Use actual language from sources, never paraphrase |
| **Edge Case Coverage** | Document unusual situations and handling |
| **Forbidden Actions** | Explicitly define what AI must NEVER do |
| **Test Before Deploy** | Gauntlet testing is mandatory |
| **Fix Source, Not Symptoms** | Procedure card is truth; never auto-heal skills |

---

## 🎯 Target Verticals

This methodology was designed for **UnifiedOS** but works for any domain:

| Vertical | Examples |
|----------|----------|
| **LTR** | Long-Term Rentals (maintenance, leases, payments) |
| **STR** | Short-Term Rentals (guest check-in, housekeeping) |
| **HOA** | Community management (violations, assessments) |
| **Health** | Patient scheduling (Leona-BR) |
| **Loyalty** | Points/rewards (BILT) |
| **Treasury** | Payment processing, ledger operations |

---

## 📖 Reading Order for AI Agents

1. `docs/methodology/THE_BIG_PICTURE.md` — Understand the ecosystem
2. `docs/methodology/README.md` — Learn the 9-phase pipeline
3. `docs/methodology/AI_KNOWLEDGE_ENGINEER_PROMPT.md` — Complete instructions
4. `docs/methodology/templates/procedure_card.yaml` — Core output template
5. `docs/examples/SKILL_REQ_electrical_maintenance_triage.md` — See a worked example

---

## 🛠️ Skills Destination

When the AI produces skills, output them to:

```
skills/
├── [vertical]/
│   ├── [skill-name]/
│   │   ├── SKILL.md           # Main skill definition
│   │   ├── scripts/           # Deterministic helpers
│   │   └── references/        # Domain docs
```

Compatible with:
- **Claude Code**: `.claude/skills/` or `~/.claude/skills/`
- **OpenAI Codex**: `$CWD/.codex/skills`
- **Custom Runtime**: Any folder via skill loader

---

## 📝 License

Internal use for UnifiedOS ecosystem.

---

## 🔗 Related

- **UnifiedOS Main Repo**: Parent platform repository
- **Claude Code Skills Docs**: https://code.claude.com/docs/en/skills





