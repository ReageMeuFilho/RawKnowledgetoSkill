# UnifiedOS Knowledge-to-Skills Methodology

## The Complete Framework for Converting Domain Knowledge into Production AI Skills

**Version:** 2.0.0  
**Date:** 2026-01-04  
**Status:** Canonical Framework

---

## 🎯 What This Is

This is the **master playbook** for converting raw domain knowledge (videos, documents, interviews, SOPs, tribal knowledge) into production-ready AI Skills that power all UnifiedOS verticals.

**Input:** Raw knowledge in any format  
**Output:** Tested, packaged, deployable AI Skills

---

## 📊 The Pipeline

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    KNOWLEDGE → SKILLS PIPELINE                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  RAW KNOWLEDGE                                                               │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐          │
│  │  Videos  │ │Documents │ │Interviews│ │   SOPs   │ │  Tribal  │          │
│  │          │ │          │ │          │ │          │ │ Knowledge│          │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘          │
│       └────────────┴────────────┼────────────┴────────────┘                 │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 1: SOURCE NORMALIZATION                                        ║  │
│  ║  Transcribe, extract, catalog all sources with timestamps/citations   ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 2: KNOWLEDGE EXTRACTION (AI BA Interview)                      ║  │
│  ║  Structured interviews to capture workflows, exact wording, edge cases║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 3: PROCEDURE CARD GENERATION                                   ║  │
│  ║  Transform knowledge into machine-readable YAML with full traceability║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 4: SKILL TAXONOMY & DEPENDENCY MAPPING                         ║  │
│  ║  Classify as Policy/Workflow/Tool-Use, map dependencies               ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 5: SKILL FOLDER GENERATION                                     ║  │
│  ║  Create SKILL.md, scripts/, references/, assets/                      ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 6: EVAL SUITE GENERATION                                       ║  │
│  ║  Create grounded tests, synthetic tests, rubrics                      ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 7: GAUNTLET TESTING                                            ║  │
│  ║  Run eval suite, require ≥85% score, 100% on critical dimensions      ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 8: PACKAGE & DEPLOY                                            ║  │
│  ║  Package .skill file, deploy to staging, promote to production        ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  ╔═══════════════════════════════════════════════════════════════════════╗  │
│  ║  PHASE 9: GOVERNANCE & ITERATION                                      ║  │
│  ║  Monitor, capture failures, add to evals, fix source of truth         ║  │
│  ╚═══════════════════════════════════════════════════════════════════════╝  │
│                                 │                                            │
│                                 ▼                                            │
│  PRODUCTION SKILLS                                                           │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │  Tested, Documented, Traceable, Deployable AI Skills                 │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📁 Directory Structure

```
docs/methodology/
├── README.md                           # This file - overview and quick start
│
├── phases/                             # Detailed phase documentation
│   ├── PHASE_01_SOURCE_NORMALIZATION.md
│   ├── PHASE_02_KNOWLEDGE_EXTRACTION.md
│   ├── PHASE_03_PROCEDURE_CARDS.md
│   ├── PHASE_04_SKILL_TAXONOMY.md
│   ├── PHASE_05_SKILL_GENERATION.md
│   ├── PHASE_06_EVAL_GENERATION.md
│   ├── PHASE_07_GAUNTLET_TESTING.md
│   ├── PHASE_08_PACKAGE_DEPLOY.md
│   └── PHASE_09_GOVERNANCE.md
│
├── templates/                          # Templates for each artifact
│   ├── source_manifest.yaml
│   ├── procedure_card.yaml
│   ├── skill_md_template.md
│   ├── eval_grounded.jsonl
│   ├── eval_synthetic.jsonl
│   └── rubric_template.yaml
│
├── scripts/                            # Automation scripts
│   ├── transcribe_video.py
│   ├── extract_document.py
│   ├── init_skill.py
│   ├── validate_skill.py
│   ├── generate_evals.py
│   ├── run_gauntlet.py
│   └── package_skill.py
│
├── examples/                           # Complete worked examples
│   ├── leak-triage-protocol/
│   └── guest-checkin/
│
└── AI_KNOWLEDGE_ENGINEER_PROMPT.md     # Master prompt for AI agent
```

---

## 🚀 Quick Start

### Option 1: Use AI Knowledge Engineer (Recommended)

1. **Initialize the AI agent:**
   ```
   Copy contents of: docs/methodology/AI_KNOWLEDGE_ENGINEER_PROMPT.md
   Paste into Claude/GPT-4
   ```

2. **Provide raw knowledge:**
   ```
   "Here is a training video transcript about handling maintenance requests.
   Please process this through the Knowledge-to-Skills pipeline."
   ```

3. **Receive production-ready skill:**
   - Source manifest
   - Procedure cards
   - SKILL.md with scripts
   - Eval suite
   - Gauntlet results
   - Packaged .skill file

### Option 2: Manual Pipeline

Follow each phase document in `phases/` directory sequentially.

---

## 📋 Phase Summary

| Phase | Input | Output | Quality Gate |
|-------|-------|--------|--------------|
| **1. Source Normalization** | Raw videos, documents, notes | Timestamped transcripts, markdown docs, manifest | All sources catalogued |
| **2. Knowledge Extraction** | Normalized sources, SME access | Interview transcripts, exact wording captured | Edge cases documented |
| **3. Procedure Cards** | Interview + sources | YAML procedure cards with citations | 100% traceability |
| **4. Skill Taxonomy** | Procedure cards | Classified skills, dependency map | No circular deps |
| **5. Skill Generation** | Procedure cards | SKILL.md, scripts, references, assets | Validates with script |
| **6. Eval Generation** | Skill + sources | Grounded tests, synthetic tests, rubric | ≥10 grounded, ≥20 synthetic |
| **7. Gauntlet Testing** | Skill + evals | Test results, scores | ≥85% score, 100% critical |
| **8. Package & Deploy** | Validated skill | .skill package, deployed | Staging verified |
| **9. Governance** | Production skill | Updated skill, expanded evals | Continuous improvement |

---

## 🎯 Supported Verticals

This methodology creates skills for all UnifiedOS verticals:

| Vertical | Example Skills |
|----------|---------------|
| **LTR (Long-Term Rentals)** | Maintenance triage, lease renewal, rent payment |
| **STR (Short-Term Rentals)** | Guest check-in, housekeeping, review management |
| **HOA (Community)** | Violation reports, amenity reservations, governance |
| **Health (Leona-BR)** | Patient scheduling, appointment reminders, triage |
| **BILT Loyalty** | Points accrual, redemption, status tiers |
| **Treasury/Cinema** | Payment processing, ticket workflows |

---

## 📊 Quality Standards

### Skill Must Have:
- ✅ YAML frontmatter with comprehensive description
- ✅ All triggers derived from real user language
- ✅ 10-15 conversation examples with exact wording
- ✅ All edge cases documented with handling
- ✅ Forbidden actions explicitly stated
- ✅ Source citations for every decision point
- ✅ Scripts for deterministic operations
- ✅ Eval suite with ≥30 test cases
- ✅ Gauntlet score ≥85%
- ✅ 100% score on forbidden action avoidance

### Skill Must NOT:
- ❌ Have uncited decision logic
- ❌ Have vague conversation examples
- ❌ Skip edge cases
- ❌ Auto-heal without human approval
- ❌ Deploy without gauntlet pass

---

## 🔧 Tooling

| Tool | Purpose | Usage |
|------|---------|-------|
| `transcribe_video.py` | Transcribe videos with timestamps | `python transcribe_video.py video.mp4` |
| `extract_document.py` | Extract document sections to markdown | `python extract_document.py doc.pdf` |
| `init_skill.py` | Initialize skill folder structure | `python init_skill.py skill-name` |
| `validate_skill.py` | Validate skill structure | `python validate_skill.py skill-folder/` |
| `generate_evals.py` | Generate eval suite from procedure card | `python generate_evals.py card.yaml` |
| `run_gauntlet.py` | Run eval suite against skill | `python run_gauntlet.py --skill name` |
| `package_skill.py` | Package skill for distribution | `python package_skill.py skill-folder/` |

---

## 📚 Documentation

### Phase Documentation
- [Phase 1: Source Normalization](phases/PHASE_01_SOURCE_NORMALIZATION.md)
- [Phase 2: Knowledge Extraction](phases/PHASE_02_KNOWLEDGE_EXTRACTION.md)
- [Phase 3: Procedure Cards](phases/PHASE_03_PROCEDURE_CARDS.md)
- [Phase 4: Skill Taxonomy](phases/PHASE_04_SKILL_TAXONOMY.md)
- [Phase 5: Skill Generation](phases/PHASE_05_SKILL_GENERATION.md)
- [Phase 6: Eval Generation](phases/PHASE_06_EVAL_GENERATION.md)
- [Phase 7: Gauntlet Testing](phases/PHASE_07_GAUNTLET_TESTING.md)
- [Phase 8: Package & Deploy](phases/PHASE_08_PACKAGE_DEPLOY.md)
- [Phase 9: Governance](phases/PHASE_09_GOVERNANCE.md)

### Templates
- [Source Manifest Template](templates/source_manifest.yaml)
- [Procedure Card Template](templates/procedure_card.yaml)
- [SKILL.md Template](templates/skill_md_template.md)
- [Eval Rubric Template](templates/rubric_template.yaml)

### AI Agent
- [AI Knowledge Engineer Prompt](AI_KNOWLEDGE_ENGINEER_PROMPT.md)

---

## 🏁 Get Started Now

**To process your first piece of raw knowledge:**

1. Read this README
2. Copy `AI_KNOWLEDGE_ENGINEER_PROMPT.md` to your AI agent
3. Provide your raw knowledge (video transcript, document, interview notes)
4. Follow the agent's guidance through each phase
5. Receive production-ready skill

---

**This methodology is the canonical framework for all skill creation in UnifiedOS.**

