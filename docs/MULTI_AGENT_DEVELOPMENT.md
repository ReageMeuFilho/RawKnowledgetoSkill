# Multi-Agent Development Guide

> How to run multiple Claude Code agents in parallel using Git Worktrees

---

## 🎯 Overview

This guide enables **parallel development** where multiple agents work on different features simultaneously without conflicts.

**Key Concept**: Each agent works in its own **worktree** (isolated copy of the repo), on its own **branch**, then we merge the results.

---

## 📊 When to Use Multi-Agent Development

| Scenario | Use Single Agent | Use Multi-Agent |
|----------|------------------|-----------------|
| Sequential tasks | ✅ | ❌ |
| One feature at a time | ✅ | ❌ |
| Multiple independent features | ❌ | ✅ |
| Research + Implementation parallel | ❌ | ✅ |
| Bug fixes in parallel | ❌ | ✅ |
| Phase 1 skill research (6 groups) | ❌ | ✅ |

---

## 🛠️ Setup: Git Worktrees

### What is a Git Worktree?

A worktree is a **linked copy** of your repository at a different path, checked out to a different branch. Changes in one worktree don't affect others until merged.

```
Main Repo (C:\Users\wrios\Documents\GitHub\RawKnowledgetoSkill)
    └── branch: main

Worktree 1 (C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1)
    └── branch: feature/phase1-group1-communication

Worktree 2 (C:\Users\wrios\Documents\GitHub\worktrees\agent-research-2)
    └── branch: feature/phase1-group2-booking

Worktree 3 (C:\Users\wrios\Documents\GitHub\worktrees\agent-implementation)
    └── branch: feature/mvp-voice-agent
```

### Creating Worktrees

```bash
# Navigate to main repo
cd C:\Users\wrios\Documents\GitHub\RawKnowledgetoSkill

# Create worktree directory
mkdir -p C:\Users\wrios\Documents\GitHub\worktrees

# Create worktree for Agent 1 (Research - Group 1)
git worktree add C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1 -b feature/phase1-group1-communication

# Create worktree for Agent 2 (Research - Group 2)
git worktree add C:\Users\wrios\Documents\GitHub\worktrees\agent-research-2 -b feature/phase1-group2-booking

# Create worktree for Agent 3 (Implementation)
git worktree add C:\Users\wrios\Documents\GitHub\worktrees\agent-implementation -b feature/mvp-implementation
```

### Listing Worktrees

```bash
git worktree list
```

### Removing Worktrees (when done)

```bash
git worktree remove C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1
```

---

## 🚀 Parallel Development Workflow

### Phase 1: Setup (You do this once)

1. **Create worktrees** for each agent (see above)
2. **Open separate Cursor windows** for each worktree
3. **Assign each agent its task**

### Phase 2: Agent Work (Agents do this in parallel)

Each agent in its worktree:

```bash
# Agent 1 in worktree 1
cd C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1

# Do work...

# Commit changes
git add -A
git commit -m "Phase 1 Group 1: Communication skills research"
git push origin feature/phase1-group1-communication
```

### Phase 3: Merge (You or a coordinator does this)

```bash
# Return to main repo
cd C:\Users\wrios\Documents\GitHub\RawKnowledgetoSkill

# Fetch all branches
git fetch --all

# Merge each feature branch
git checkout main
git merge feature/phase1-group1-communication
git merge feature/phase1-group2-booking
git merge feature/mvp-implementation

# Push merged main
git push origin main
```

### Phase 4: Cleanup

```bash
# Remove worktrees
git worktree remove C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1
git worktree remove C:\Users\wrios\Documents\GitHub\worktrees\agent-research-2

# Delete remote branches if desired
git push origin --delete feature/phase1-group1-communication
```

---

## 📋 Agent Assignment Templates

### Research Agent Prompt (Worktree Template)

```markdown
YOUR ROLE: Research Agent
YOUR WORKTREE: C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1
YOUR BRANCH: feature/phase1-group1-communication

BEFORE STARTING:
1. cd C:\Users\wrios\Documents\GitHub\worktrees\agent-research-1
2. git pull origin main (sync with latest)
3. Read CLAUDE.md for context

YOUR TASK:
Follow the research prompt at:
docs/prompts/RESEARCH_PROMPT_PHASE1_GROUP1_COMMUNICATION.md

WHEN DONE:
1. git add -A
2. git commit -m "Research: Phase 1 Group 1 Communication skills"
3. git push origin feature/phase1-group1-communication
4. Notify coordinator that your branch is ready for merge
```

### Implementation Agent Prompt (Worktree Template)

```markdown
YOUR ROLE: Implementation Agent
YOUR WORKTREE: C:\Users\wrios\Documents\GitHub\worktrees\agent-implementation
YOUR BRANCH: feature/mvp-voice-agent

WORKING ACROSS TWO REPOS:
- Specs from: C:\Users\wrios\Documents\GitHub\RawKnowledgetoSkill
- Code to: C:\Users\wrios\Documents\GitHub\UnifiedTreasuryOS

BEFORE STARTING:
1. cd C:\Users\wrios\Documents\GitHub\worktrees\agent-implementation
2. git pull origin main
3. Read CLAUDE.md for context
4. Read specs/communication/SPEC-SKILL-269-MULTI-CHANNEL-VOICE.md

YOUR TASK:
Implement the Multi-Channel Voice Agent per specification

WHEN DONE:
1. Commit to your branch
2. Create PR or notify coordinator
```

---

## 🎯 Recommended Multi-Agent Configuration

### For Phase 1 Research (6 parallel agents)

| Agent | Worktree | Branch | Task |
|-------|----------|--------|------|
| Research-1 | `worktrees/research-1` | `feature/phase1-group1` | Communication skills (5) |
| Research-2 | `worktrees/research-2` | `feature/phase1-group2` | Booking skills (4) |
| Research-3 | `worktrees/research-3` | `feature/phase1-group3` | Channel skills (4) |
| Research-4 | `worktrees/research-4` | `feature/phase1-group4` | Financial skills (6) |
| Research-5 | `worktrees/research-5` | `feature/phase1-group5` | Operations skills (5) |
| Research-6 | `worktrees/research-6` | `feature/phase1-group6` | Cross-cutting skills (4) |

### For Implementation (2 parallel agents)

| Agent | Worktree | Task |
|-------|----------|------|
| Impl-Treasury | `worktrees/impl-treasury` | Treasury OS (TigerBeetle, Formance) |
| Impl-AI | `worktrees/impl-ai` | AI Layer (Suna, LangGraph, Skills) |

---

## ⚠️ Conflict Prevention

### Rules to Avoid Merge Conflicts

1. **Different files**: Assign agents to work on different folders/files
2. **Clear boundaries**: Research agents don't edit specs; Implementation agents don't edit research
3. **STATUS.md updates**: Only coordinator updates STATUS.md after merging
4. **CHANGELOG.md**: Each agent adds entries for their own work; coordinator consolidates

### File Ownership by Role

| Agent Type | Can Create/Edit | Cannot Edit |
|------------|-----------------|-------------|
| Research Agent | `knowledge/*.md` | `specs/*.md`, `STATUS.md` |
| Engineering Agent | `knowledge/ES-*.md` | `specs/*.md`, `STATUS.md` |
| Implementation Agent | Code files | `knowledge/*.md` |
| Coordinator (You) | Everything | - |

---

## 📊 Monitoring Parallel Work

### Check All Branches

```bash
git branch -a
```

### Check Worktree Status

```bash
# From main repo
git worktree list

# From any worktree
git status
```

### See What Changed in Each Branch

```bash
git log main..feature/phase1-group1-communication --oneline
```

---

## 🔄 Integration with GitHub Issues

For even better organization, create GitHub issues for each parallel task:

```bash
# Create issues for Phase 1 groups
gh issue create --title "Phase 1 Group 1: Communication Skills Research" --body "Research 5 skills: SKILL-001, SKILL-002, SKILL-006, SKILL-046, SKILL-085"

# Assign to branches
git checkout -b feature/phase1-group1-communication
# Work...
git commit -m "Closes #1: Phase 1 Group 1 research complete"
```

---

## 📋 Quick Reference Commands

```bash
# === SETUP ===
git worktree add <path> -b <branch>     # Create worktree
git worktree list                        # List worktrees
git worktree remove <path>               # Remove worktree

# === DURING WORK ===
cd <worktree-path>                       # Enter worktree
git status                               # Check status
git add -A && git commit -m "msg"        # Commit
git push origin <branch>                 # Push

# === MERGE ===
cd <main-repo>                           # Return to main
git fetch --all                          # Get all branches
git merge <branch>                       # Merge branch
git push origin main                     # Push merged

# === CLEANUP ===
git worktree remove <path>               # Remove worktree
git branch -d <branch>                   # Delete local branch
git push origin --delete <branch>        # Delete remote branch
```

---

## 🎯 Summary

1. **Create worktrees** for parallel agents
2. **Assign clear tasks** with file boundaries
3. **Each agent commits to its branch**
4. **Coordinator merges** all branches
5. **Cleanup** worktrees when done

This enables 6+ agents working simultaneously without stepping on each other!

---

*Last Updated: January 6, 2026*

