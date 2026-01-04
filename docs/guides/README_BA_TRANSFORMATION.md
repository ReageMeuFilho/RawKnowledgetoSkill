# BA Transformation Guide - Summary

**Created:** 2026-01-04  
**Purpose:** Help Business Analysts understand their new role in Skills-based architecture

---

## 📦 What Was Created

This package contains everything your BA team needs to transition from traditional requirements gathering to Skills-based conversation design.

### 1. **Skill Requirements Template** 
📄 `docs/templates/SKILL_REQUIREMENTS_TEMPLATE.md`

**What it is:** A standardized template for capturing workflow requirements as conversation designs rather than technical specifications.

**Use it when:** Starting any new workflow requirement

**Key sections:**
- When to Activate (triggers)
- Business Logic (conversation flow)
- Required Data
- Safety Rules & Constraints
- **Conversation Examples** (most important!)
- Edge Cases
- Success Metrics

---

### 2. **Complete Example: Electrical Maintenance**
📄 `docs/PMSVertical/skill-requirements/SKILL_REQ_electrical_maintenance_triage.md`

**What it is:** A fully fleshed-out skill requirements document based on a real landlord interview

**Use it as:** Your reference example when writing new skill requirements

**Highlights:**
- Real interview transcript included
- Detailed conversation examples with exact wording
- Emergency/Urgent/Standard urgency classification
- Edge cases (after-hours, missing data, repeat issues)
- Safety compliance (NR-10 Brazil electrical standards)

---

### 3. **BA Workflow Guide**
📄 `docs/guides/BA_WORKFLOW_GUIDE.md`

**What it is:** Step-by-step guide for BAs on the new workflow

**Covers:**
- The 4-phase BA process (Discovery → Analysis → Documentation → Validation)
- Interview techniques (Do's and Don'ts)
- How to transform interview notes into skill requirements
- How to work with developers
- How to review AI conversations (not code!)

---

### 4. **BA Role Transformation**
📄 `docs/guides/BA_ROLE_TRANSFORMATION.md`

**What it is:** Big-picture overview of how the BA role changes

**Covers:**
- Side-by-side comparison: Traditional vs Skills-based
- What changes for the BA (responsibilities, skills, deliverables)
- Real examples of good vs bad interviews
- Impact on project timelines (4.5 months → 3 weeks)
- Key mindset shifts

---

## 🎯 The Core Answer to Your Question

> "When my analyst is working with a landlord who explains the electricity workflow, what does the BA need to do? How does he create requirements based on this new architecture?"

### The Answer:

**OLD WAY (Traditional):**
1. Interview landlord
2. Write 100-page functional requirements document
3. Define API contracts, database schemas, UI mockups
4. Hand off to developers
5. Wait 6-8 weeks for implementation
6. Landlord sees result, often says "That's not what I meant"

**NEW WAY (Skills-Based):**
1. **Interview landlord** - Same as before, but focus on conversation flow
   - "Walk me through what you do when..."
   - "What exactly do you say to the tenant?"
   - "What if X happens?"

2. **Write Skill Requirements Document** (15 pages, using template)
   - Section 1: When to activate ("tenant says 'electricity'")
   - Section 2: Business logic (IF sparks → evacuate, IF no power → share panel location)
   - Section 3: Required data (panel_location, electrician_phone)
   - Section 4: Safety rules (NEVER tell tenant to touch sparking panel)
   - Section 5: **Conversation examples** - 10-15 real dialogues with exact wording
   - Section 6: Edge cases (after-hours, missing data, repeat issues)
   - Section 7: Success metrics

3. **Developer implements** (2-3 days)
   - Creates `SKILL.md` (AI instructions based on your requirements)
   - Creates Python scripts for deterministic operations (create ticket, send SMS, etc.)

4. **Landlord validates** (Day 4)
   - Landlord chats with the AI
   - AI responds exactly as specified in your conversation examples
   - Landlord says "Yes! That's perfect!" or "Change X"

5. **Iterate** (30 minutes - 2 hours per change)
   - Developer edits `SKILL.md` based on feedback
   - No code rewrite needed

**Timeline:** 3-5 days from interview to validated working AI (vs 6-8 weeks traditional)

---

## 🔑 Key Insight

**The BA is no longer defining HOW to build the system.**

**The BA is defining WHAT the conversation should be.**

Your Skill Requirements Document is essentially a **script for how the AI should converse**, not a technical blueprint for developers.

### What You DON'T Do Anymore:
- ❌ Design database schemas
- ❌ Define API contracts
- ❌ Create UI wireframes
- ❌ Write 100+ user stories in Jira
- ❌ Create sequence diagrams

### What You DO Now:
- ✅ Map conversation flows (IF user says X, respond with Y)
- ✅ Write example dialogues (exact wording)
- ✅ Identify edge cases (what if data is missing?)
- ✅ Define safety rules (NEVER do X, ALWAYS do Y)
- ✅ Validate by chatting with the AI

---

## 📊 Real Impact

### Example: Landlord Electrical Issue Workflow

**Traditional Approach:**
- Requirements document: 87 pages
- Implementation: 6 weeks
- Codebase: ~1,200 lines (PaymentService, PointsService, NotificationService, TierService)
- Validation: After dev complete
- Changes: Expensive (code changes)

**Skills Approach:**
- Skill Requirements: 15 pages
- Implementation: 2-3 days
- Codebase: ~400 lines (SKILL.md + 4 Python scripts)
- Validation: Immediately (chat with AI)
- Changes: Cheap (edit markdown)

**Efficiency Gain:** 90% faster, 70% less code

---

## 🚀 Getting Started

### For Your BA Team:

1. **Read these documents in order:**
   - Start: `BA_ROLE_TRANSFORMATION.md` (big picture)
   - Then: `BA_WORKFLOW_GUIDE.md` (how-to)
   - Reference: `SKILL_REQUIREMENTS_TEMPLATE.md` (template)
   - Example: `SKILL_REQ_electrical_maintenance_triage.md` (concrete example)

2. **Try it on a small workflow:**
   - Pick a simple workflow (e.g., "Tenant reports broken light")
   - Interview a stakeholder
   - Write a Skill Requirements Document using the template
   - Work with a developer to implement it
   - Validate by chatting with the AI

3. **Iterate and improve:**
   - Refine your interview technique
   - Build a library of conversation examples
   - Learn what makes a good vs. bad skill requirement

### For Your Landlord (or any domain expert):

1. **What changes for them:**
   - Interviews are more conversational ("Walk me through...")
   - They see results MUCH faster (days, not months)
   - They validate by chatting with AI, not reviewing mockups
   - They can request changes easily (markdown edits, not code rewrites)

2. **What they should expect:**
   - BA will ask for exact wording ("What would you say to the tenant?")
   - BA will ask for edge cases ("What if the electrician isn't available?")
   - They'll get to chat with the AI on Day 4
   - Iteration is fast (hours, not weeks)

---

## 💡 The Mental Model

### Traditional: "I'm a translator"
```
Business ──[BA translates]──> Tech Specs ──[Dev codes]──> Software
   ↓                                                           ↓
   └──────────────── (6-8 weeks later) ────────────────────────┘
                    "That's not what I meant!"
```

### Skills-Based: "I'm a conversation designer"
```
Business ──[BA designs conversation]──> Skill Requirements ──[Dev implements]──> AI
   ↓                                                                            ↓
   └─────────────────── (3 days later) ──────────────────────────────────────┘
                    "Perfect! Change this one thing?"
                    └──────── (30 min) ──────────┘ "Done!"
```

---

## 📚 Additional Resources

- **Architecture Deep Dive:** `docs/architecture/MODEL_AGNOSTIC_ARCHITECTURE.md`
- **Skills Framework:** `~/.claude/skills/` (look at existing skills)
- **Runtime Details:** `runtime/unified_runtime.py` (how the AI loads skills)

---

## ❓ Questions?

**"Do I need to learn to code?"**  
No. You write in plain English/Portuguese. The AI and scripts handle execution.

**"How do I validate the AI is correct?"**  
Chat with it. The AI should respond exactly as specified in your conversation examples.

**"What if the workflow is too complex?"**  
Break it into multiple skills. One skill = one logical workflow.

**"What if I'm not sure about technical details (like database fields)?"**  
You don't need them! Just specify what information is needed ("electrician's phone number"). Developers figure out where it comes from.

**"How detailed should conversation examples be?"**  
Very detailed. Include exact words, emoji, formatting. The AI learns from these.

---

## 🎉 Summary

Your BA team is transitioning from **technical translators** to **conversation designers**.

The goal is no longer to define HOW to build the system, but to define WHAT the conversation should achieve.

The documents provided give your team:
- ✅ A template for capturing workflows as conversation designs
- ✅ A complete example to learn from
- ✅ Step-by-step guides for the new process
- ✅ Big-picture understanding of the transformation

**Result:** Faster delivery (weeks vs months), better quality (stakeholders validate actual behavior), easier iteration (markdown vs code).

---

**Ready to transform your BA workflow? Start with the example, then try it on a small workflow.**

