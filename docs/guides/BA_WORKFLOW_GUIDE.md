# Business Analyst Workflow Guide
## Requirements Gathering for Skills-Based Architecture

**Version:** 1.0  
**Date:** 2026-01-04  
**Audience:** Business Analysts, Product Managers, Domain Experts

---

## 📋 Table of Contents
1. [Overview: What Changed](#overview-what-changed)
2. [The New BA Process](#the-new-ba-process)
3. [Interview Technique](#interview-technique)
4. [From Interview to Skill Requirements](#from-interview-to-skill-requirements)
5. [Working with Developers](#working-with-developers)
6. [Examples](#examples)

---

## Overview: What Changed

### Traditional BA Role
```
┌─────────────────────────────────────────────────────────┐
│ TRADITIONAL BA WORKFLOW                                 │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1. Interview stakeholder                               │
│  2. Write functional requirements (100+ pages)          │
│  3. Create API contracts                                │
│  4. Define database schema                              │
│  5. Create sequence diagrams                            │
│  6. Write user stories with acceptance criteria         │
│  7. Developers interpret and code                       │
│  8. QA creates test cases                               │
│  9. Product owner reviews implementation                │
│  10. Iterate if misaligned                              │
│                                                         │
│  Timeline: 4-6 weeks from interview to code             │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Skills-Based BA Role
```
┌─────────────────────────────────────────────────────────┐
│ SKILLS-BASED BA WORKFLOW                                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1. Interview stakeholder (same)                        │
│  2. Write Skill Requirements Document (10-15 pages)     │
│     - When to activate                                  │
│     - Conversation flow                                 │
│     - Business logic                                    │
│     - Example conversations                             │
│     - Edge cases                                        │
│  3. Developers create SKILL.md + scripts                │
│  4. Test in Claude Code immediately                     │
│  5. Stakeholder reviews live conversation               │
│  6. Iterate in hours, not weeks                         │
│                                                         │
│  Timeline: 3-5 days from interview to working prototype │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Key Differences

| Aspect | Traditional | Skills-Based |
|--------|-------------|--------------|
| **Output** | Functional specs, API docs, DB schema | Skill Requirements Document |
| **Focus** | HOW to build | WHAT the conversation should do |
| **Detail Level** | Technical implementation | Business logic + conversation flow |
| **Validation** | After dev (weeks) | During dev (hours) |
| **Iteration** | Expensive (code changes) | Cheap (markdown changes) |
| **Stakeholder Review** | Screenshots, test environments | Live conversation with AI |

---

## The New BA Process

### Phase 1: Discovery (1-2 days)

**Goal:** Understand the workflow from the domain expert's perspective

**Activities:**
1. **Interview Stakeholder**
   - Focus on: "Walk me through what you do when X happens"
   - Not: "What fields should be in the database?"

2. **Observe (if possible)**
   - Watch the expert handle real scenarios
   - Note their decision-making process

3. **Collect Artifacts**
   - Screenshots of current tools
   - Example messages/emails
   - Existing checklists or SOPs

### Phase 2: Analysis (1 day)

**Goal:** Identify the conversation pattern and decision points

**Activities:**
1. **Map the Conversation Flow**
   ```
   User says X
     ├─ If condition A → Response 1
     ├─ If condition B → Response 2
     └─ Else → Response 3
   ```

2. **Identify Trigger Conditions**
   - What keywords/phrases should activate this skill?
   - What context is required?

3. **Extract Business Rules**
   - What are the MUST/MUST NOT rules?
   - What are the safety/compliance constraints?

4. **Define Data Needs**
   - What data is needed from the database?
   - What external APIs are involved?

### Phase 3: Documentation (1-2 days)

**Goal:** Create the Skill Requirements Document

**Use Template:** `docs/templates/SKILL_REQUIREMENTS_TEMPLATE.md`

**Key Sections to Focus On:**
1. **When to Activate** (triggers)
2. **Business Logic** (conversation flow)
3. **Conversation Examples** (actual dialogues)
4. **Edge Cases** (what could go wrong)

### Phase 4: Validation (ongoing)

**Goal:** Ensure the skill works as intended

**Activities:**
1. **Review with Stakeholder**
   - Walk through conversation examples
   - Confirm edge cases are covered

2. **Test with AI (once implemented)**
   - Have stakeholder chat with the AI
   - Iterate on SKILL.md based on feedback

---

## Interview Technique

### Do's ✅

1. **Start with "Walk me through..."**
   - "Walk me through what happens when a tenant reports an electrical issue."
   - "Walk me through how you decide if it's an emergency."

2. **Ask about exceptions**
   - "What if the electrician isn't available?"
   - "What if this happens at 2 AM?"
   - "What if the tenant doesn't speak Portuguese?"

3. **Get exact wording**
   - "What exactly do you say to the tenant in an emergency?"
   - "Show me an example of a message you'd send."

4. **Probe for safety/compliance**
   - "Are there any legal requirements here?"
   - "What could go wrong if we don't do this right?"
   - "What are you worried about?"

5. **Ask about data sources**
   - "Where do you look up the electrician's number?"
   - "How do you know where the electrical panel is?"

### Don'ts ❌

1. **Don't ask about implementation**
   - ❌ "Should this be a REST API or GraphQL?"
   - ❌ "What database fields do we need?"
   - ✅ "What information do you need to see?"

2. **Don't lead the witness**
   - ❌ "Would you want a dropdown menu here?"
   - ✅ "How do you currently categorize these issues?"

3. **Don't assume technical solutions**
   - ❌ "We'll build a intent classifier for this."
   - ✅ "How do you know when to call the electrician?"

4. **Don't skip edge cases**
   - ❌ "Let's focus on the happy path."
   - ✅ "What's the weirdest situation you've dealt with?"

---

## From Interview to Skill Requirements

### Example Transformation

**Stakeholder Says:**
> "When a tenant says there are sparks, I immediately tell them to leave the room and call 911. Then I call my electrician João and tell him it's an emergency. For regular power outages, I just tell them where the breaker is and send João if they can't fix it."

**BA Translates to Skill Requirements:**

```markdown
## 2. BUSINESS LOGIC

### Step 1: Classify Urgency

- **EMERGENCY**
  - Trigger: message contains "sparks", "fire", "smoke", "shock"
  - Action: Instruct to evacuate and call 911
  - Then: Dispatch electrician immediately

- **URGENT**
  - Trigger: message contains "no power", "breaker tripped", "outage"
  - Action: Provide panel location, offer reset guidance
  - Then: Dispatch electrician if needed

## 5. CONVERSATION EXAMPLES

### Example 1: EMERGENCY
Tenant: "There are sparks coming from an outlet!"

Expected Response:
"🚨 EMERGENCY - LEAVE THE ROOM NOW!
1. Exit the room immediately
2. Call 911 (fire department)
3. Do NOT touch anything electrical

I've dispatched João (electrician) to your location.
He will arrive in 20-30 minutes.

Are you safe? Please confirm."
```

### Mapping Checklist

Use this checklist to ensure you've captured everything:

- [ ] **Triggers:** What words/phrases activate this skill?
- [ ] **Decision Points:** What are the IF/THEN conditions?
- [ ] **Required Data:** What info is needed from database/APIs?
- [ ] **Outputs:** What actions are taken (create ticket, send SMS, etc.)?
- [ ] **Response Templates:** What exactly should the AI say?
- [ ] **Safety Rules:** What are the NEVER/ALWAYS rules?
- [ ] **Edge Cases:** What unusual situations could happen?
- [ ] **Success Metrics:** How do we measure if this works?

---

## Working with Developers

### What You Provide to Developers

**1. Skill Requirements Document** (see template)
- This is your primary deliverable
- Developers use this to create SKILL.md and scripts

**2. Conversation Examples** (critical!)
- Actual dialogues, not just "user reports issue"
- Include multi-turn conversations
- Include edge cases and errors

**3. Business Rules** (explicit and prioritized)
- Must have: "NEVER do X", "ALWAYS do Y"
- Nice to have: "Prefer X over Y"

### What Developers Give You Back

**1. SKILL.md file**
- Instructions for the AI
- You can read and edit this!

**2. Python scripts** (you don't need to understand these)
- Deterministic operations (calculations, API calls)

**3. Test results**
- Conversation logs showing the AI in action

### How to Review Developer Work

**DON'T review code** — Review conversations!

**DO THIS:**
1. Have a conversation with the AI (via Claude Code or test environment)
2. Try edge cases: "What if I say it's resolved?", "What if I say there's fire?"
3. Check if responses match your Skill Requirements Document
4. Provide feedback: "This response should mention X", "This is too technical"

**Iterate:**
- Small changes: Developer edits SKILL.md (minutes)
- New logic: Developer adds/modifies scripts (hours)
- New workflow: You create new Skill Requirements Document (days)

---

## Examples

### Example 1: Electrical Maintenance

**See:** `docs/PMSVertical/skill-requirements/SKILL_REQ_electrical_maintenance_triage.md`

**Key Takeaways:**
- Clear urgency classification (emergency/urgent/standard)
- Explicit safety rules ("NEVER instruct tenant to...")
- Detailed conversation examples with emoji and formatting
- Edge cases (after-hours, missing data, repeat issues)
- Exact wording stakeholder uses

### Example 2: Rent Payment Assistance

**Scenario:** Tenant wants to pay rent

**Skill Requirements Document would include:**

```markdown
## 1. WHEN TO ACTIVATE
- Tenant mentions: "pay rent", "pagar aluguel", "rent payment", "how do I pay"
- Context: Active lease, rent is due or overdue

## 2. BUSINESS LOGIC

Step 1: Check Rent Status
- Query: Get current rent amount, due date, past due amount
- If past due > 30 days: Escalate to property manager
- If past due < 30 days: Offer payment + late fee
- If current: Process normal payment

Step 2: Present Payment Options
- Credit card: 3x points, $50 fee
- Debit card: 2x points, $25 fee
- ACH: 1x points, no fee

Step 3: Process Payment
- Call: process_rent_payment.py
- Calculate points: accrue_points.py
- Generate receipt: generate_receipt.py

## 5. CONVERSATION EXAMPLES

Tenant: "I need to pay my January rent"

Response:
"Hi! Let me help you with that.

💰 January Rent: $2,500
📅 Due: January 1
✅ Status: On time

How would you like to pay?
1. Bank account (ACH) - No fee, earn 2,500 points
2. Debit card - $25 fee, earn 5,000 points
3. Credit card - $50 fee, earn 7,500 points"
```

### Example 3: Guest Check-In (STR Vertical)

**Scenario:** Guest arriving at short-term rental

**Skill Requirements Document would include:**

```markdown
## 1. WHEN TO ACTIVATE
- Guest messages within 24 hours of check-in
- Message contains: "arrived", "here", "check in", "door code", "keys"

## 2. BUSINESS LOGIC

Step 1: Verify Reservation
- Confirm booking is active
- Check if check-in time has arrived
- If early: Offer early check-in fee OR ask to wait

Step 2: Provide Access Instructions
- Retrieve property.access_instructions
- Include: door code, lockbox location, parking, WiFi password

Step 3: Welcome Message
- Property tour highlights
- Emergency contact
- Local recommendations

## 5. CONVERSATION EXAMPLES

Guest: "Hi! We just arrived. How do we get in?"

Response:
"Welcome to Casa Bonita! 🏡

🚪 ACCESS INSTRUCTIONS:
1. Find the lockbox on the right side of the front door
2. Code: 4829#
3. Your door code: 1234# (valid until Jan 7)

🚗 PARKING: Driveway #2

📶 WiFi: CasaBonita-Guest
Password: Sunshine2024

🆘 Emergency: Call João at (11) 98765-4321

Enjoy your stay! Let me know if you need anything."
```

---

## Quick Reference Card

**Before the Interview:**
- [ ] Review existing documentation (if any)
- [ ] Prepare open-ended questions
- [ ] Set up recording (with permission)

**During the Interview:**
- [ ] Focus on WHAT, not HOW
- [ ] Get exact wording for responses
- [ ] Ask "What if...?" for edge cases
- [ ] Note safety/compliance concerns
- [ ] Collect example messages/screenshots

**Writing Skill Requirements:**
- [ ] Use the template
- [ ] Write detailed conversation examples
- [ ] Be explicit about business rules
- [ ] Include edge cases
- [ ] Define success metrics

**Reviewing Implementation:**
- [ ] Chat with the AI yourself
- [ ] Try edge cases
- [ ] Compare to your conversation examples
- [ ] Check if safety rules are enforced
- [ ] Validate with stakeholder

---

## FAQs

**Q: Do I need to know how to code?**  
A: No. You write in plain English/Portuguese. Developers translate to scripts.

**Q: How detailed should conversation examples be?**  
A: Very detailed. Include exact wording, emoji, formatting. The AI will mimic these.

**Q: What if the stakeholder doesn't know what they want?**  
A: Start with a basic version, implement it quickly, and iterate. Skills are cheap to change.

**Q: How do I handle conflicting requirements from multiple stakeholders?**  
A: Document both in the Skill Requirements, let Product Manager prioritize, or create multiple skills.

**Q: What if the workflow is too complex for one skill?**  
A: Break it into multiple skills. Example: "rent-payment-initiation" + "rent-payment-confirmation" + "rent-payment-failure-handling"

**Q: How do I know if something should be a script vs. LLM decision?**  
A: If it's math/data lookup/deterministic → Script. If it's language/context/judgment → LLM.

---

## Resources

- **Template:** `docs/templates/SKILL_REQUIREMENTS_TEMPLATE.md`
- **Example:** `docs/PMSVertical/skill-requirements/SKILL_REQ_electrical_maintenance_triage.md`
- **Architecture:** `docs/architecture/MODEL_AGNOSTIC_ARCHITECTURE.md`

---

## Support

**Questions?** Contact:
- Technical Lead: Paulo Ferreira
- Product Manager: Ana Silva
- BA Lead: Maria Santos

