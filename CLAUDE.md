# Citadel OS - Digital Workforce Specifications Repository

> **This file is always included in context. Keep it focused and link to detailed docs.**

---

## 🎯 Project Goal

Build a **Digital Workforce** platform for property management - AI agents that work as employees, not just tools.

**Core Thesis**: Agent = Operating System, Skills = Applications, Context = RAM

---

## 📁 Repository Structure

```
RawKnowledgetoSkill/
├── CLAUDE.md                    ← You are here (always in context)
├── STATUS.md                    ← Current project state (READ FIRST)
├── docs/
│   ├── BUSINESS_PLAN_DRAFT.md   ← Vision, strategy, moat
│   ├── COMPLETE_TECHNICAL_ARCHITECTURE.md  ← Full tech stack
│   ├── PIPELINE_TRACKER.md      ← Knowledge gap progress
│   ├── PHASE1_SKILL_TRACKER.md  ← Phase 1 skills (28 remaining)
│   ├── OPEN_ITEMS_TRACKER.md    ← Infrastructure decisions (all resolved)
│   ├── architecture/
│   │   └── LAYER4_SKILLS_ARCHITECTURE.md  ← Claude Skills framework
│   └── prompts/                 ← Agent prompts (research, engineering)
├── specs/                       ← Final skill specifications (Stage 4)
│   ├── ai-workforce/            ← SKILL-261-268
│   ├── communication/           ← SKILL-253, SKILL-269
│   ├── pricing/                 ← SKILL-101-103, SKILL-146
│   ├── operations/              ← SKILL-254, SKILL-257, SKILL-270-272
│   └── channel/                 ← SKILL-232
├── knowledge/                   ← Research & engineering docs (Stages 1-3)
│   ├── ai-workforce/
│   ├── communication/
│   ├── pricing/
│   ├── operations/
│   ├── channel/
│   └── infrastructure/          ← KD-PRODUCTION-INFRASTRUCTURE-FINAL.md
├── registry/
│   └── MASTER_SKILL_REGISTRY.md ← All 272 skills catalogued
└── competitors/                 ← Original PRD analysis
```

---

## 🔑 Key Files to Reference

| When You Need | Read This |
|---------------|-----------|
| Current status | `STATUS.md` |
| What are we building | `docs/BUSINESS_PLAN_DRAFT.md` |
| Technical architecture | `docs/COMPLETE_TECHNICAL_ARCHITECTURE.md` |
| Skills framework | `docs/architecture/LAYER4_SKILLS_ARCHITECTURE.md` |
| Infrastructure decisions | `knowledge/infrastructure/KD-PRODUCTION-INFRASTRUCTURE-FINAL.md` |
| All skills | `registry/MASTER_SKILL_REGISTRY.md` |
| MVP skill specs | `specs/` folder |
| Progress tracking | `docs/PIPELINE_TRACKER.md` |

---

## 🏗️ Architecture Overview

**6-Layer Stack**:
```
Layer 6: Consumer Apps (Loyalty, Rewards)
Layer 5: Domain Skills (STR, LTR, HOA)
Layer 4: Digital Workforce (Suna + LangGraph + Claude Skills)  ← THIS REPO
Layer 3: Treasury OS (Formance + TigerBeetle + Temporal)       ← UnifiedTreasuryOS repo
Layer 2: Platform Services (Auth0, Redis, MongoDB)
Layer 1: Infrastructure (AWS ECS/Fargate)
```

**Companion Repository**: `C:\Users\wrios\Documents\GitHub\UnifiedTreasuryOS`
- Contains: TigerBeetle ledger, Formance accounting, Temporal workflows
- Status: Partially built, needs integration with Layer 4

---

## 📊 Current Progress

- **Skills Catalogued**: 272
- **MVP Skills Specified**: 20 (Stage 4 complete)
- **Phase 1 Skills**: 28 (research prompts ready)
- **Infrastructure Decisions**: 42/42 resolved

---

## ⚡ Workflow Rules

### For Any Agent Starting Work:
1. **First**: Run `git pull origin main`
2. **Second**: Read `STATUS.md` for current state
3. **Third**: Read this file (`CLAUDE.md`) for context
4. **Fourth**: Check `docs/AGENT_GUIDE.md` for your role

### For Research Agents:
- Use prompts in `docs/prompts/RESEARCH_PROMPT_*.md`
- Save output to `knowledge/[category]/KD-[GAP-ID]-*.md`
- Update `STATUS.md` when complete

### For Engineering Agents:
- Use prompts in `docs/prompts/ENGINEERING_SPEC_PROMPT_*.md`
- Save output to `knowledge/[category]/ES-[GAP-ID]-*.md`
- Update `STATUS.md` when complete

### For Implementation Agents:
- Read `docs/prompts/IMPLEMENTATION_PLANNING_AGENT_PROMPT.md`
- Write code to `UnifiedTreasuryOS` repository
- Create GitHub issues for tracking

---

## 🚫 Constraints & Policies

1. **Never** push directly to main without review
2. **Always** update `STATUS.md` after completing work
3. **Always** commit with descriptive messages
4. **Never** hardcode secrets - use environment variables
5. **Always** follow the 4-stage pipeline (Research → Eng Prompt → Eng Spec → Final Spec)

---

## 🛠️ Frequently Used Commands

```bash
# Check status
cat STATUS.md

# Update after work
git add -A
git commit -m "descriptive message"
git push

# Check what skills need work
cat docs/PHASE1_SKILL_TRACKER.md

# Find a specific skill
grep -r "SKILL-269" specs/
```

---

## 📝 Documentation Updates

After completing any significant work, update:
1. `STATUS.md` - Current state and next action
2. `docs/PIPELINE_TRACKER.md` - If processing a knowledge gap
3. `registry/MASTER_SKILL_REGISTRY.md` - If skills were added/updated

---

## 🔗 Related Resources

- **Anthropic Skills Standard**: https://github.com/anthropics/skills
- **Suna Framework**: https://github.com/kortix-ai/suna
- **LangGraph**: https://github.com/langchain-ai/langgraph

---

*Last Updated: January 6, 2026*

