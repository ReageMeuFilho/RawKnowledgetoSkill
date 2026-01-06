# PSB Quick-Start Guide for Citadel OS

> **P**lan → **S**etup → **B**uild - The systematic approach to building with Claude Code

---

## 📍 Where We Are

| Phase | Status | What's Done |
|-------|--------|-------------|
| **PLAN** | ✅ Complete | 272 skills, 20 MVP specs, business plan, architecture |
| **SETUP** | ✅ Complete | CLAUDE.md, automated docs, agent guides |
| **BUILD** | 🔄 Starting | Implementation planning, Phase 1 research |

---

## 🚀 Quick Start for New Agents

### Step 1: Clone & Sync

```bash
# Clone both repos (if not already)
git clone https://github.com/ReageMeuFilho/RawKnowledgetoSkill.git
git clone https://github.com/ReageMeuFilho/UnifiedTreasuryOS.git

# Always sync first!
cd RawKnowledgetoSkill && git pull origin main
cd ../UnifiedTreasuryOS && git pull origin main
```

### Step 2: Read Context Files

```
1. CLAUDE.md           → Project memory (always in context)
2. STATUS.md           → Current state and next action
3. docs/AGENT_GUIDE.md → Your role-specific instructions
```

### Step 3: Identify Your Role

| If You Are | Read This | Your Output Goes To |
|------------|-----------|---------------------|
| Research Agent | `docs/prompts/RESEARCH_PROMPT_*.md` | `knowledge/[category]/KD-*.md` |
| Engineering Agent | `docs/prompts/ENGINEERING_SPEC_PROMPT_*.md` | `knowledge/[category]/ES-*.md` |
| Implementation Agent | `docs/prompts/IMPLEMENTATION_PLANNING_AGENT_PROMPT.md` | `UnifiedTreasuryOS/` code |
| Coordinator (Cursor AI) | Everything | `specs/`, `STATUS.md`, updates |

### Step 4: Do Your Work

Follow your role-specific prompt, then:

```bash
git add -A
git commit -m "Descriptive message about what you did"
git push
```

### Step 5: Update Status (Coordinator Only)

After merging agent work, update:
- `STATUS.md` - Current state
- `docs/CHANGELOG.md` - What changed
- `docs/PIPELINE_TRACKER.md` - If processing knowledge gaps

---

## 📂 Repository Map

```
RawKnowledgetoSkill/                  ← SPECIFICATIONS REPO
├── CLAUDE.md                         ← PROJECT MEMORY (read this!)
├── STATUS.md                         ← CURRENT STATE (check this!)
├── docs/
│   ├── AGENT_GUIDE.md               ← Agent instructions
│   ├── BUSINESS_PLAN_DRAFT.md       ← Vision & strategy
│   ├── COMPLETE_TECHNICAL_ARCHITECTURE.md
│   ├── CHANGELOG.md                 ← What changed when
│   ├── PIPELINE_TRACKER.md          ← Knowledge gap progress
│   ├── PHASE1_SKILL_TRACKER.md      ← Next 28 skills
│   ├── MULTI_AGENT_DEVELOPMENT.md   ← Parallel work guide
│   ├── architecture/
│   │   └── LAYER4_SKILLS_ARCHITECTURE.md
│   └── prompts/                     ← All agent prompts
├── specs/                           ← FINAL SPECIFICATIONS
├── knowledge/                       ← RESEARCH & ENGINEERING DOCS
├── registry/
│   └── MASTER_SKILL_REGISTRY.md     ← All 272 skills
└── competitors/                     ← Original PRD analysis

UnifiedTreasuryOS/                    ← IMPLEMENTATION REPO
├── CLAUDE.md                         ← PROJECT MEMORY (read this!)
├── README.md
├── docs/architecture/               ← Technical architecture
├── internal/                        ← Core implementations
├── adapters/                        ← External integrations
└── runtime/                         ← Python runtime
```

---

## 🎯 Current Priorities

### NOW: Implementation Planning
```
Agent: Implementation Planning Agent
Prompt: docs/prompts/IMPLEMENTATION_PLANNING_AGENT_PROMPT.md
Output: IMPLEMENTATION_ROADMAP.md, TASK_REGISTRY.md, SPRINT_BACKLOG.md
```

### PARALLEL: Phase 1 Research
```
6 Research Agents can work simultaneously on:
- Group 1: Communication (5 skills)
- Group 2: Booking (4 skills)
- Group 3: Channel (4 skills)
- Group 4: Financial (6 skills)
- Group 5: Operations (5 skills)
- Group 6: Cross-cutting (4 skills)

Prompts: docs/prompts/RESEARCH_PROMPT_PHASE1_GROUP*.md
```

### NEXT: MVP Implementation
```
After planning is complete:
- AI Workforce Architecture → deploy HITL framework
- Voice Agent → deploy Twilio + Deepgram
- HLP Pricing → integrate PriceLabs patterns
```

---

## 📊 Key Metrics

| Metric | Value |
|--------|-------|
| Total Skills Catalogued | 272 |
| MVP Skills Specified | 20 |
| Phase 1 Skills Remaining | 28 |
| Infrastructure Decisions | 42/42 resolved |
| Competitors Analyzed | 23 |
| Lines of Specifications | 87,000+ |

---

## 🔄 The 4-Stage Pipeline

Every knowledge gap goes through:

```
Stage 1: RESEARCH
Research Agent produces Knowledge Document (KD-*.md)
         ↓
Stage 2: ENGINEERING PROMPT
Cursor AI creates detailed prompt for Engineering Agent
         ↓
Stage 3: ENGINEERING SPEC
Engineering Agent produces full specification (ES-*.md)
         ↓
Stage 4: FINAL SPEC
Cursor AI creates final skill specification (SPEC-*.md)
```

---

## ⚡ Multi-Agent Setup (Parallel Work)

For parallel development, use Git Worktrees:

```bash
# Create worktree for each agent
git worktree add ../worktrees/agent-1 -b feature/task-1
git worktree add ../worktrees/agent-2 -b feature/task-2

# Each agent works in its worktree
cd ../worktrees/agent-1
# do work...
git commit -m "Task 1 complete"

# Coordinator merges all branches
cd ../RawKnowledgetoSkill
git merge feature/task-1
git merge feature/task-2
```

See `docs/MULTI_AGENT_DEVELOPMENT.md` for full details.

---

## 🚫 Don'ts

1. ❌ Don't push directly to main without review
2. ❌ Don't edit files outside your assigned area
3. ❌ Don't forget to update STATUS.md
4. ❌ Don't hardcode secrets
5. ❌ Don't skip reading CLAUDE.md

---

## ✅ Do's

1. ✅ Always `git pull` before starting
2. ✅ Read CLAUDE.md and STATUS.md first
3. ✅ Follow your role-specific prompt
4. ✅ Commit with descriptive messages
5. ✅ Update documentation after completing work

---

## 🔗 Quick Links

| Resource | Path |
|----------|------|
| Project Memory | `CLAUDE.md` |
| Current Status | `STATUS.md` |
| Agent Guide | `docs/AGENT_GUIDE.md` |
| Implementation Prompt | `docs/prompts/IMPLEMENTATION_PLANNING_AGENT_PROMPT.md` |
| Research Prompts | `docs/prompts/RESEARCH_PROMPT_PHASE1_GROUP*.md` |
| Multi-Agent Guide | `docs/MULTI_AGENT_DEVELOPMENT.md` |
| Changelog | `docs/CHANGELOG.md` |
| All Skills | `registry/MASTER_SKILL_REGISTRY.md` |

---

*This is the one-page guide. For details, follow the links above.*

