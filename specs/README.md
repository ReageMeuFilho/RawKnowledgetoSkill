# Skill Specifications

> **Purpose**: Final, implementation-ready specifications produced in Stage 4
> **Source**: Engineering Specifications (ES-*) processed by Cursor AI
> **Last Updated**: January 2026

---

## 📁 Directory Structure

```
specs/
├── README.md                    ← You are here
├── ai-workforce/               ← AI agent specifications
├── communication/              ← Messaging, voice, chat specs
├── pricing/                    ← Dynamic pricing specs
├── operations/                 ← Maintenance, cleaning specs
└── [other categories]/
```

---

## 📋 Naming Convention

```
SPEC-SKILL-[ID]-[name].md

Examples:
- SPEC-SKILL-261-268-ai-workforce.md
- SPEC-SKILL-232-quote-chaser.md
- SPEC-SKILL-253-ai-leasing-assistant.md
```

---

## 📄 What Each Spec Contains

Each specification document includes:

1. **Skill Definition** - Formal entry for registry
2. **Tool Definitions** - If tools are needed
3. **User Stories** - Acceptance criteria
4. **Data Models** - Final schemas
5. **API Contracts** - Endpoint specifications
6. **Dependencies** - What this needs
7. **Effort Estimate** - T-shirt sizing
8. **Implementation Notes** - Gotchas and recommendations

---

## ✅ Spec Status

| Spec | Status | Skills | Date |
|------|--------|--------|------|
| (none yet) | - | - | - |

---

## 🔄 Workflow

Specs are created in **Stage 4** of the Knowledge-to-Skill workflow:

```
Stage 1: Research Agent → Conceptual Knowledge (KD-*)
Stage 2: Cursor AI → Engineering Prompt
Stage 3: Engineering Agent → Technical Spec (ES-*)
Stage 4: Cursor AI → THIS FOLDER (SPEC-*)  ← Final output
```

See `docs/KNOWLEDGE_TO_SKILL_WORKFLOW.md` for full process.

