# Knowledge-to-Skills: Quick Start Guide

## 🎯 What You Have

A complete methodology for converting **ANY raw knowledge** into **production AI Skills**.

---

## 📁 Files Created

```
docs/methodology/
├── README.md                           # Full overview of the 9-phase pipeline
├── QUICK_START.md                      # This file
├── INITIALIZE_KNOWLEDGE_ENGINEER.txt   # Copy-paste to initialize AI agent
├── AI_KNOWLEDGE_ENGINEER_PROMPT.md     # Complete AI agent system prompt
│
├── phases/
│   └── PHASE_01_SOURCE_NORMALIZATION.md  # Detailed phase guidance
│   (Other phases reference the main methodology doc)
│
├── templates/
│   ├── source_manifest.yaml            # Template for cataloging sources
│   ├── procedure_card.yaml             # Template for procedure cards
│   └── rubric_template.yaml            # Template for eval rubrics
│
├── scripts/                            # (Scripts to be added)
└── examples/                           # (Examples to be added)
```

---

## 🚀 How to Use (3 Options)

### Option A: Use AI Knowledge Engineer (Recommended)

1. **Copy** the contents of `INITIALIZE_KNOWLEDGE_ENGINEER.txt`
2. **Paste** into Claude, GPT-4, or another capable AI
3. **Provide** your raw knowledge (transcript, document, interview, etc.)
4. **Receive** complete skill package

### Option B: Follow Manual Pipeline

1. **Read** `README.md` for full pipeline overview
2. **Follow** each phase (1-9) using the templates
3. **Use** templates in `templates/` folder
4. **Validate** at each quality gate

### Option C: Hybrid Approach

1. Use AI for initial processing (Phases 1-5)
2. Human review at Phase 6 (Eval Generation)
3. Human approval at Phase 7 (Gauntlet Testing)
4. AI for packaging (Phase 8)

---

## 📊 The Pipeline at a Glance

```
RAW KNOWLEDGE                          PRODUCTION SKILL
     │                                       ▲
     ▼                                       │
┌──────────────┐                    ┌──────────────┐
│ 1. Normalize │                    │ 8. Package   │
│    Sources   │                    │    & Deploy  │
└──────┬───────┘                    └──────┬───────┘
       │                                   │
       ▼                                   │
┌──────────────┐                    ┌──────┴───────┐
│ 2. Extract   │                    │ 7. Gauntlet  │
│    Knowledge │                    │    Testing   │
└──────┬───────┘                    └──────┬───────┘
       │                                   │
       ▼                                   │
┌──────────────┐                    ┌──────┴───────┐
│ 3. Procedure │                    │ 6. Generate  │
│    Cards     │                    │    Evals     │
└──────┬───────┘                    └──────┬───────┘
       │                                   │
       ▼                                   │
┌──────────────┐    ┌──────────────┐      │
│ 4. Classify  │───▶│ 5. Generate  │──────┘
│    Taxonomy  │    │    Skill     │
└──────────────┘    └──────────────┘
```

---

## 🎯 What Each Phase Produces

| Phase | Output | Purpose |
|-------|--------|---------|
| 1. Source Normalization | `source_manifest.yaml` | Catalog all knowledge sources |
| 2. Knowledge Extraction | `extraction_summary.md` | Structured workflow knowledge |
| 3. Procedure Cards | `[ID].yaml` | Machine-readable procedures |
| 4. Skill Taxonomy | Classification + deps | Organize skills logically |
| 5. Skill Generation | `SKILL.md` + scripts | Deployable skill folder |
| 6. Eval Generation | `.jsonl` + rubric | Test suite |
| 7. Gauntlet Testing | Test report | Validation results |
| 8. Package & Deploy | `.skill` file | Deployable package |
| 9. Governance | Updated skills | Continuous improvement |

---

## ✅ Quality Standards

### Every Skill Must Have:
- ✅ 100% source traceability (every claim cited)
- ✅ 10-15 conversation examples with exact wording
- ✅ All edge cases documented with handling
- ✅ Forbidden actions explicitly stated
- ✅ Eval suite with ≥30 test cases
- ✅ Gauntlet score ≥85%
- ✅ 100% on forbidden action avoidance

### Skills Must NOT:
- ❌ Have uncited decision logic
- ❌ Have vague conversation examples
- ❌ Skip edge cases
- ❌ Auto-heal without human approval

---

## 🔑 Key Concepts

### Procedure Card
Machine-readable YAML that captures a complete workflow with full traceability. This is the **source of truth** - all other artifacts are derived from it.

### Grounded Tests
Test cases derived directly from source material. Each test traces back to a specific timestamp or document section.

### Synthetic Tests
Mutations of grounded tests that test edge cases: missing info, conflicting info, adversarial inputs, etc.

### Gauntlet
The formal test suite that validates a skill before deployment. Must pass before production.

### Governance
The process of maintaining skills over time. Key rule: **never auto-heal** - always fix the procedure card first.

---

## 📚 Reference Documents

### This Methodology
- `docs/methodology/README.md` - Full pipeline documentation
- `docs/methodology/AI_KNOWLEDGE_ENGINEER_PROMPT.md` - Complete AI agent prompt

### Original Source
- `docs/guides/knowledge-to-skills-methodology.md` - Original methodology (incorporated and enhanced)

### Example Output
- `docs/PMSVertical/skill-requirements/SKILL_REQ_electrical_maintenance_triage.md` - Complete skill example

### BA Guides (Earlier Version)
- `docs/guides/BA_WORKFLOW_GUIDE.md` - Interview techniques
- `docs/guides/BA_ROLE_TRANSFORMATION.md` - Role overview

---

## 💡 Tips for Success

1. **Start with quality sources** - Better input = better skills
2. **Capture exact wording** - Don't paraphrase, quote directly
3. **Ask "What if?"** - Edge cases are critical
4. **Test before deploy** - Gauntlet exists for a reason
5. **Fix source, not symptoms** - Procedure card is truth

---

## 🆘 Getting Help

### If skill doesn't activate correctly:
→ Check description field has all trigger keywords

### If classification is wrong:
→ Check classify script, add more examples

### If procedure is wrong:
→ Clarify decision tree in procedure card

### If forbidden action occurs:
→ Add explicit warning, more tests

---

## 🚀 Start Now

1. **Read:** `README.md` (10 min)
2. **Initialize:** Copy `INITIALIZE_KNOWLEDGE_ENGINEER.txt` to your AI
3. **Provide:** Your first piece of raw knowledge
4. **Receive:** Production-ready skill

---

**Questions?** Review the detailed documentation in `README.md` and `AI_KNOWLEDGE_ENGINEER_PROMPT.md`.

