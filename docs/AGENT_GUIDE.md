# 🤖 Agent Guide: How to Work on This Repository

> **Purpose**: Standard instructions for ANY AI agent working on this project
> **First Step**: Always read `STATUS.md` in the root directory first
> **Last Updated**: January 2026

---

## 🚀 GETTING STARTED (For Any Agent)

### Step 0: Sync Your Local Repository ⚠️
```bash
# ALWAYS RUN THIS FIRST - Before doing anything else!
cd [your-local-repo-path]
git pull origin main
```

> **CRITICAL**: Multiple agents may be working on this repo. Always pull the latest changes before starting any work to avoid conflicts and ensure you have the most current state.

### Step 1: Read the Status File
```
ALWAYS START BY READING: STATUS.md (in repo root)
```

This file tells you:
- Current active work item
- What stage it's at
- What action is needed next
- Who should do it

### Step 2: Identify Your Role

| If You Are Asked To... | You Are | Read |
|------------------------|---------|------|
| Research a knowledge gap | Research Agent | `docs/RESEARCH_ANALYST_GUIDE.md` |
| Review and create engineering prompt | Cursor AI (Stage 2) | `docs/KNOWLEDGE_TO_SKILL_WORKFLOW.md` |
| Create engineering specification | Engineering Agent | The prompt in `docs/prompts/` |
| Create final skill specs | Cursor AI (Stage 4) | `docs/KNOWLEDGE_TO_SKILL_WORKFLOW.md` |
| Check status | Any Agent | `STATUS.md` |

---

## 📂 REPOSITORY STRUCTURE

```
RawKnowledgetoSkill/
│
├── STATUS.md                    ← 🔴 READ THIS FIRST (current state)
│
├── docs/
│   ├── AGENT_GUIDE.md           ← You are here (how to work)
│   ├── PIPELINE_TRACKER.md      ← Detailed gap progress
│   ├── MVP_PRIORITY_GAPS.md     ← Gap definitions
│   ├── OPEN_ITEMS_TRACKER.md    ← Open questions
│   ├── KNOWLEDGE_TO_SKILL_WORKFLOW.md  ← Process docs
│   ├── RESEARCH_ANALYST_GUIDE.md       ← Stage 1 guide
│   └── prompts/
│       └── ENGINEERING_SPEC_PROMPT_*.md ← Stage 2 outputs
│
├── knowledge/
│   ├── ai-workforce/
│   │   ├── KD-*.md              ← Stage 1 outputs
│   │   └── ES-*.md              ← Stage 3 outputs
│   └── [other categories]/
│
├── specs/
│   └── ai-workforce/
│       └── SPEC-*.md            ← Stage 4 outputs
│
├── registry/
│   └── MASTER_SKILL_REGISTRY.md ← Final skills
│
└── competitors/
    └── [competitor]/
        ├── SKILL_INVENTORY.md
        └── KNOWLEDGE_GAPS.md
```

---

## 🔄 THE 4-STAGE PIPELINE

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                          KNOWLEDGE-TO-SKILL PIPELINE                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  Stage 1              Stage 2              Stage 3              Stage 4              │
│  RESEARCH             REVIEW               ENGINEERING          SKILL SPEC           │
│  AGENT                CURSOR AI            AGENT                CURSOR AI            │
│                                                                                      │
│  ┌──────────┐        ┌──────────┐        ┌──────────┐        ┌──────────┐          │
│  │ Research │   →    │ Quality  │   →    │ Build    │   →    │ Create   │          │
│  │ the gap  │        │ Review + │        │ Tech     │        │ Final    │          │
│  │          │        │ Prompt   │        │ Spec     │        │ Skills   │          │
│  └──────────┘        └──────────┘        └──────────┘        └──────────┘          │
│       ↓                   ↓                   ↓                   ↓                 │
│    KD-*.md            PROMPT_*.md          ES-*.md            SPEC-*.md             │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📋 AGENT-SPECIFIC INSTRUCTIONS

### Research Agent (Stage 1)

**Your Job**: Research knowledge gaps and produce conceptual documentation

**How to Start**:
1. Read `STATUS.md` → Check "Upcoming Work Queue"
2. Find your assigned gap (e.g., GAP-AF-001)
3. Read `docs/RESEARCH_ANALYST_GUIDE.md` for detailed instructions
4. Look up the gap in `docs/MVP_PRIORITY_GAPS.md` for research questions

**Your Output**:
- Save to: `knowledge/[category]/KD-[GAP-ID]-[name].md`
- Example: `knowledge/ai-workforce/KD-HOAI-001-ai-workforce-architecture.md`

**After Completion**:
1. Update `STATUS.md`:
   - Change your gap's Stage 1 status to ✅ Complete
   - Add document path
2. Update `docs/PIPELINE_TRACKER.md` with completion details

---

### Cursor AI - Stage 2 (Review & Prompt)

**Your Job**: Review Stage 1 output, create engineering prompt

**How to Start**:
1. User provides Stage 1 knowledge document
2. Quality assess the document
3. Create custom engineering prompt

**Your Output**:
- Save to: `docs/prompts/ENGINEERING_SPEC_PROMPT_[FEATURE].md`
- Example: `docs/prompts/ENGINEERING_SPEC_PROMPT_AI_WORKFORCE.md`

**Also Do**:
- Log open questions to `docs/OPEN_ITEMS_TRACKER.md`
- Update `STATUS.md` with Stage 2 completion
- Update `docs/PIPELINE_TRACKER.md`

---

### Engineering Agent (Stage 3)

**Your Job**: Produce detailed technical specification

**How to Start**:
1. Read `STATUS.md` → Find gap awaiting Stage 3
2. Read the prompt at `docs/prompts/ENGINEERING_SPEC_PROMPT_[FEATURE].md`
3. Follow ALL sections in the prompt

**Your Output**:
- Save to: `knowledge/[category]/ES-[GAP-ID]-[name].md`
- Example: `knowledge/ai-workforce/ES-HOAI-001-ai-workforce-architecture.md`

**Quality Requirements**:
- Complete ALL sections from the prompt
- Include actual code/schemas (not placeholders)
- Document open questions

**After Completion**:
1. Update `STATUS.md`:
   - Change your gap's Stage 3 status to ✅ Complete
2. Update `docs/PIPELINE_TRACKER.md`

---

### Cursor AI - Stage 4 (Final Specs)

**Your Job**: Create final skill specifications from engineering doc

**How to Start**:
1. User provides Stage 3 engineering specification
2. Extract skills, tools, user stories
3. Update master registry

**Your Outputs**:
- Spec file: `specs/[category]/SPEC-SKILL-[ID].md`
- Update: `registry/MASTER_SKILL_REGISTRY.md`
- Update: `STATUS.md`
- Update: `docs/PIPELINE_TRACKER.md`

**Also Do**:
- Resolve any open items if possible
- Update coverage metrics
- Queue next gap

---

## 📊 STATUS REPORTING

### When Asked "What is the status?"

ANY agent should produce this format:

```
╔═══════════════════════════════════════════════════════════════════════════════════════╗
║                              PIPELINE STATUS SUMMARY                                   ║
╠═══════════════════════════════════════════════════════════════════════════════════════╣
║                                                                                        ║
║   ACTIVE WORK ITEM: [GAP-ID] ([Name])                                                 ║
║   CURRENT STAGE:    Stage [X] - [Status]                                              ║
║   NEXT ACTION:      [What needs to happen]                                            ║
║   BLOCKING:         [Any blockers or "Nothing"]                                       ║
║                                                                                        ║
╠═══════════════════════════════════════════════════════════════════════════════════════╣
║                                                                                        ║
║   GAPS:     [X]/10 Complete | [Y]/10 In Progress | [Z]/10 Pending                     ║
║   SKILLS:   [X]/79 P0 Skills specified ([X]%)                                         ║
║   OPEN:     [X] items ([X] Critical, [X] High, [X] Medium, [X] Low)                   ║
║                                                                                        ║
╚═══════════════════════════════════════════════════════════════════════════════════════╝

NEXT ACTIONS:
1. [Priority 1 action] - [Agent needed]
2. [Priority 2 action] - [Agent needed]
3. [Priority 3 action] - [Agent needed]
```

### To Generate This Status:

1. Read `STATUS.md` for current state
2. Read `docs/PIPELINE_TRACKER.md` for gap details
3. Read `docs/OPEN_ITEMS_TRACKER.md` for open item counts
4. Produce the standardized format above

---

## ✅ UPDATE CHECKLIST

After completing ANY work, update these files:

| File | What to Update |
|------|----------------|
| `STATUS.md` | Current state, stage completion, next action |
| `docs/PIPELINE_TRACKER.md` | Gap stage status, dates, document paths |
| `docs/OPEN_ITEMS_TRACKER.md` | New open items or resolved items |
| `registry/MASTER_SKILL_REGISTRY.md` | Only after Stage 4 |

---

## 🔑 KEY RULES

1. **Always read `STATUS.md` first** - It's the source of truth
2. **Update status after every action** - Keep it current
3. **Use standardized format** - Same output format every time
4. **Document everything** - Path, date, agent, result
5. **Push to GitHub** - After every significant update

---

## 📞 HANDOFF PROTOCOL

When handing off to another agent:

1. Update `STATUS.md` with:
   - What you completed
   - What the next agent needs to do
   - Any blocking issues

2. Commit and push to GitHub

3. **Tell the next agent to run `git pull` first!**

4. The next agent reads `STATUS.md` and knows exactly where to start

> ⚠️ **Reminder for Users**: When switching agents, always instruct the new agent to **sync their local repo** with `git pull origin main` before starting work.

---

## 🆘 IF YOU'RE STUCK

1. Read `STATUS.md` - What's the current state?
2. Read `docs/KNOWLEDGE_TO_SKILL_WORKFLOW.md` - What's the process?
3. Check `docs/OPEN_ITEMS_TRACKER.md` - Is there a known issue?
4. Ask the user for clarification

---

**Remember**: `STATUS.md` is your entry point. Always start there.

