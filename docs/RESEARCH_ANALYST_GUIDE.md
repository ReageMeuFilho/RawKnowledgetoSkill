# Research Analyst Guide: Closing Knowledge Gaps

> **Purpose**: Systematic guide for researching and documenting the expertise needed to close knowledge gaps in the Master Skill Registry
> **Version**: 1.0
> **Last Updated**: January 2026

---

## 🎯 Mission

Your mission is to transform **Knowledge Gaps** into **Actionable Specifications** by researching how best-in-class competitors implement specific skills, then documenting that knowledge in sufficient detail that our engineering team can build equivalent or superior functionality.

---

## 📋 Table of Contents

1. [Understanding the System](#1-understanding-the-system)
2. [Priority Framework](#2-priority-framework)
3. [Research Process](#3-research-process)
4. [Source Strategy](#4-source-strategy)
5. [Output Format](#5-output-format)
6. [Quality Standards](#6-quality-standards)
7. [Current Priority Gaps](#7-current-priority-gaps)

---

## 1. Understanding the System

### 1.1 What is a Skill?

A **Skill** is a discrete capability that our platform needs to perform. Each skill has:

| Field | Description |
|-------|-------------|
| **Skill ID** | Unique identifier (e.g., SKILL-001) |
| **Name** | Descriptive name (e.g., "unified-inbox-management") |
| **Category** | Functional grouping (e.g., communication, pricing, operations) |
| **Priority** | P0 (MVP), P1 (Phase 1), P2 (Phase 2), P3 (Phase 3) |
| **Status** | NEEDED, IN PROGRESS, DOCUMENTED, IMPLEMENTED |
| **Best Implementation** | Which competitor does this best |

### 1.2 What is a Knowledge Gap?

A **Knowledge Gap** is missing information that prevents us from building a skill. Gaps typically fall into these categories:

| Gap Type | Example | Research Needed |
|----------|---------|-----------------|
| **Architecture** | "How does the system handle X?" | Technical deep-dive |
| **Workflow** | "What are the steps in process Y?" | UX/process research |
| **Algorithm** | "How is Z calculated?" | Technical/domain research |
| **Integration** | "How does it connect to external system?" | API/technical docs |
| **Business Logic** | "What rules govern this feature?" | Domain expertise |

### 1.3 Where to Find Gaps

- **Master Registry**: `registry/MASTER_SKILL_REGISTRY.md` - All skills with status
- **Competitor Gaps**: `competitors/[name]/KNOWLEDGE_GAPS.md` - Per-competitor gaps
- **Priority View**: Filter by P0 first, then P1

---

## 2. Priority Framework

### 2.1 MVP Focus (P0 Skills)

**These are CRITICAL - research these FIRST:**

| Category | Focus Areas |
|----------|-------------|
| **Communication** | Unified inbox, message routing, AI response |
| **Booking** | Reservations, calendar sync, availability |
| **Operations** | Cleaning scheduling, maintenance workflow |
| **Financial** | Payments, payouts, basic accounting |
| **Channel** | OTA integrations (Airbnb, Vrbo, Booking.com) |

### 2.2 Phase 1 Focus (P1 Skills)

**Important but not blocking MVP:**

| Category | Focus Areas |
|----------|-------------|
| **Pricing** | Dynamic pricing, revenue management |
| **AI Features** | AI messaging, guest summaries, sentiment |
| **Owner Portal** | Statements, reporting, communication |
| **Analytics** | Performance dashboards, forecasting |

### 2.3 Strategic Priorities (Regardless of Phase)

**Research these for competitive advantage:**

1. **AI Workforce Model** (from HOAi) - How do specialized AI agents work?
2. **Human-in-the-Loop Dashboard** - How to build trust with AI decisions?
3. **Multi-Channel Voice** - Phone + SMS + Chat unified
4. **Dynamic Pricing Algorithms** - HLP, elasticity models
5. **Maintenance AI** - Vendoroo's approach

---

## 3. Research Process

### 3.1 For Each Knowledge Gap, Follow This Process:

```
┌─────────────────────────────────────────────────────────────────┐
│                    RESEARCH WORKFLOW                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. UNDERSTAND THE GAP                                          │
│     └─→ Read the gap description carefully                      │
│     └─→ Identify what specific information is missing           │
│     └─→ Note the "Best Implementation" competitor               │
│                                                                  │
│  2. IDENTIFY SOURCES                                            │
│     └─→ Competitor website (primary)                            │
│     └─→ Help docs / Knowledge base                              │
│     └─→ YouTube demos and tutorials                             │
│     └─→ Reddit discussions (r/airbnb_hosts, r/vrbo, etc.)      │
│     └─→ Industry forums and communities                         │
│     └─→ Podcast interviews with founders                        │
│     └─→ Conference presentations                                │
│                                                                  │
│  3. EXTRACT KNOWLEDGE                                           │
│     └─→ Document the workflow step-by-step                      │
│     └─→ Screenshot/describe the UI                              │
│     └─→ Note the data model (what entities, fields)            │
│     └─→ Identify the business rules                             │
│     └─→ Document edge cases and error handling                  │
│                                                                  │
│  4. SYNTHESIZE & DOCUMENT                                       │
│     └─→ Create structured knowledge document                    │
│     └─→ Include all sources with links                          │
│     └─→ Add your analysis and recommendations                   │
│     └─→ Flag any remaining unknowns                             │
│                                                                  │
│  5. VALIDATE                                                    │
│     └─→ Cross-reference with multiple sources                   │
│     └─→ Check for consistency                                   │
│     └─→ Note confidence level                                   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### 3.2 Research Questions Template

For each gap, answer these questions:

**Functional Questions:**
- What problem does this feature solve?
- What is the user workflow (step-by-step)?
- What inputs are required?
- What outputs are produced?
- What are the success criteria?

**Technical Questions:**
- What data entities are involved?
- What are the key data fields?
- What integrations are required?
- What are the performance requirements?
- How does it scale?

**Business Logic Questions:**
- What rules govern the behavior?
- What are the edge cases?
- How are errors handled?
- What are the configurable options?
- What defaults are used?

**UX Questions:**
- How does the user interact with it?
- What is the visual design?
- What feedback does the user receive?
- How is status communicated?
- What actions can the user take?

---

## 4. Source Strategy

### 4.1 Primary Sources (Start Here)

| Source Type | How to Access | What to Extract |
|-------------|---------------|-----------------|
| **Competitor Website** | Visit product pages, feature pages | Feature descriptions, screenshots, positioning |
| **Help Documentation** | Find "Help", "Support", "Docs" links | Step-by-step workflows, configuration options |
| **API Documentation** | Developer docs, API reference | Data models, endpoints, field names |
| **Demo Videos** | Website demos, product tours | UI walkthrough, workflow visualization |
| **Pricing Pages** | Pricing, Plans pages | Feature tiers, what's included at each level |

### 4.2 YouTube Research

**Search Strategies:**
```
"[Competitor Name] demo"
"[Competitor Name] tutorial"
"[Competitor Name] review"
"[Competitor Name] walkthrough"
"[Feature Name] property management"
"best [feature] for Airbnb hosts"
"how to [task] in [Competitor]"
```

**Valuable Channels:**
- Competitor official channels
- Property management consultants
- STR coaching channels
- Tech review channels (Capterra, G2)
- Conference recordings (VRMA, DARM)

**What to Extract:**
- Screen recordings of actual product usage
- User feedback and pain points
- Feature comparisons
- Workflow demonstrations
- Tips and best practices

### 4.3 Reddit Research

**Relevant Subreddits:**
| Subreddit | Focus |
|-----------|-------|
| r/airbnb_hosts | Airbnb host discussions |
| r/vrbo | VRBO host discussions |
| r/ShortTermRentals | General STR discussion |
| r/realestateinvesting | Property investors |
| r/PropertyManagement | PM professionals |
| r/SaaS | Software discussions |

**Search Strategies:**
```
site:reddit.com "[Competitor Name]"
site:reddit.com "[Feature] property management"
site:reddit.com "best PMS for"
site:reddit.com "[Competitor] vs [Competitor]"
```

**What to Extract:**
- Real user experiences
- Pain points and complaints
- Feature requests
- Comparison discussions
- Workarounds and tips

### 4.4 Industry Forums & Communities

| Community | URL | Focus |
|-----------|-----|-------|
| **VRMA** | vrma.org | Vacation Rental Managers |
| **BiggerPockets** | biggerpockets.com | Real estate investors |
| **Hospitable Community** | Facebook groups | STR hosts |
| **Airbnb Host Forums** | community.withairbnb.com | Airbnb hosts |
| **Short Term Rental University** | Facebook group | Education |

**What to Extract:**
- Industry best practices
- Common workflows
- Vendor comparisons
- Feature wishlists
- Implementation challenges

### 4.5 Additional Sources

| Source | How to Access | Value |
|--------|---------------|-------|
| **G2 Reviews** | g2.com | Feature lists, user reviews, comparisons |
| **Capterra Reviews** | capterra.com | Detailed feature breakdowns |
| **Crunchbase** | crunchbase.com | Company info, funding, size |
| **LinkedIn** | linkedin.com | Employee posts, company updates |
| **Podcasts** | Search "[Competitor] podcast" | Founder interviews, strategy |
| **Webinars** | Competitor websites | Deep dives on features |
| **Case Studies** | Competitor websites | Real implementation details |

---

## 5. Output Format

### 5.1 Knowledge Document Template

For each closed gap, create a document using this structure:

```markdown
# Knowledge Document: [Skill Name]

> **Skill ID**: SKILL-XXX
> **Gap ID**: GAP-XXX-XXX
> **Research Date**: [Date]
> **Researcher**: [Your Name]
> **Confidence Level**: High / Medium / Low

---

## 1. Executive Summary

[2-3 sentence summary of what this skill does and why it matters]

---

## 2. Problem Statement

### What problem does this solve?
[Description of the user pain point]

### Who has this problem?
[User personas affected]

### How is it solved today without this feature?
[Current workarounds]

---

## 3. Best-in-Class Implementation

### Primary Reference: [Competitor Name]

#### 3.1 Feature Overview
[Description of how the competitor implements this]

#### 3.2 User Workflow
1. Step 1: [Description]
2. Step 2: [Description]
3. Step 3: [Description]
...

#### 3.3 UI/UX Description
[Describe the interface, include screenshots if available]

#### 3.4 Configuration Options
| Option | Description | Default |
|--------|-------------|---------|
| [Option 1] | [What it does] | [Default value] |
| [Option 2] | [What it does] | [Default value] |

---

## 4. Data Model

### 4.1 Core Entities
| Entity | Description | Key Fields |
|--------|-------------|------------|
| [Entity 1] | [What it represents] | [field1, field2, field3] |

### 4.2 Relationships
[Describe how entities relate]

### 4.3 Sample Data
```json
{
  "example": "data structure"
}
```

---

## 5. Business Rules

### 5.1 Core Rules
1. Rule 1: [Description]
2. Rule 2: [Description]

### 5.2 Edge Cases
| Scenario | Expected Behavior |
|----------|-------------------|
| [Edge case 1] | [What happens] |
| [Edge case 2] | [What happens] |

### 5.3 Error Handling
| Error Condition | User Feedback | System Behavior |
|-----------------|---------------|-----------------|
| [Error 1] | [Message shown] | [What system does] |

---

## 6. Integration Requirements

### 6.1 External Systems
| System | Integration Type | Data Exchanged |
|--------|------------------|----------------|
| [System 1] | API / Webhook / Import | [What data] |

### 6.2 Internal Dependencies
- Depends on: [Other skills/modules]
- Used by: [Other skills/modules]

---

## 7. Performance Considerations

- Expected volume: [X per day/hour]
- Response time requirement: [X seconds]
- Scalability notes: [Any concerns]

---

## 8. Competitive Analysis

| Competitor | Has Feature | Quality | Notes |
|------------|-------------|---------|-------|
| [Competitor 1] | ✅/❌ | ⭐⭐⭐⭐⭐ | [Notes] |
| [Competitor 2] | ✅/❌ | ⭐⭐⭐⭐ | [Notes] |

---

## 9. Recommendations

### 9.1 Must Have (MVP)
- [Capability 1]
- [Capability 2]

### 9.2 Should Have (Phase 1)
- [Capability 3]
- [Capability 4]

### 9.3 Nice to Have (Future)
- [Capability 5]

---

## 10. Sources

| Source | URL | Date Accessed | Notes |
|--------|-----|---------------|-------|
| [Source 1] | [URL] | [Date] | [What was learned] |
| [Source 2] | [URL] | [Date] | [What was learned] |

---

## 11. Open Questions

- [ ] Question 1 that still needs answering
- [ ] Question 2 that still needs answering

---

## 12. Appendix

### Screenshots
[Include relevant screenshots]

### Video Timestamps
| Video | Timestamp | Content |
|-------|-----------|---------|
| [Video URL] | 3:45 | [What's shown] |

### Raw Notes
[Any additional notes from research]
```

### 5.2 File Naming Convention

Save completed knowledge documents to:

```
knowledge/
├── communication/
│   ├── KD-001-unified-inbox-management.md
│   └── KD-002-message-triage-routing.md
├── pricing/
│   ├── KD-101-dynamic-pricing-hlp.md
│   └── KD-102-event-detection.md
├── operations/
│   └── KD-201-cleaning-automation.md
└── ai-workforce/
    ├── KD-301-ai-voice-agent.md
    └── KD-302-hitl-dashboard.md
```

---

## 6. Quality Standards

### 6.1 Definition of Done

A knowledge gap is considered **CLOSED** when:

- [ ] All research questions answered
- [ ] Multiple sources consulted (minimum 3)
- [ ] Workflow documented step-by-step
- [ ] Data model identified
- [ ] Business rules documented
- [ ] Edge cases identified
- [ ] Competitive comparison complete
- [ ] Recommendations provided
- [ ] Sources cited with URLs
- [ ] Open questions flagged

### 6.2 Confidence Levels

| Level | Criteria | Action |
|-------|----------|--------|
| **High** | Multiple sources agree, official docs available, clear understanding | Ready for engineering |
| **Medium** | Some sources conflict, partial docs, reasonable inference | Need validation |
| **Low** | Limited sources, speculation required, significant unknowns | Need more research |

### 6.3 Quality Checklist

Before submitting a knowledge document:

- [ ] Is the problem clearly stated?
- [ ] Is the workflow actionable (could someone build from this)?
- [ ] Are all sources linked?
- [ ] Are screenshots/visuals included where helpful?
- [ ] Are edge cases addressed?
- [ ] Is there a clear recommendation?
- [ ] Are open questions explicitly flagged?

---

## 7. Current Priority Gaps

### 7.1 Immediate Focus (P0 - MVP)

Start with these gaps - they block MVP:

| Gap ID | Skill | Description | Best Source |
|--------|-------|-------------|-------------|
| GAP-AF-001 | AI Leasing Assistant | 24/7 autonomous lead response | EliseAI, AppFolio |
| GAP-AF-002 | AI Maintenance Coordinator | Full maintenance workflow AI | Vendoroo, AppFolio |
| GAP-HOAI-001 | AI Workforce Architecture | Multi-agent orchestration | HOAi |
| GAP-HOAI-002 | HITL Dashboard | AI approval workflow | HOAi |
| GAP-HOAI-004 | Multi-Channel Voice | Phone+SMS+Chat unified | HOAi, Boom AI |

### 7.2 High-Value Research (P1)

These provide competitive advantage:

| Gap ID | Skill | Description | Best Source |
|--------|-------|-------------|-------------|
| GAP-PL-001 | HLP Algorithm | Hyper-local pricing | PriceLabs |
| GAP-VEN-001 | Maintenance Brain | Persistent learning | Vendoroo |
| GAP-HOAI-003 | AI AP Agent | Invoice automation | HOAi, AppFolio |
| GAP-GW-001 | Quote Chaser | Lead follow-up automation | GuestWisely |
| GAP-GW-002 | Branded Guest App | White-label mobile | GuestWisely |

### 7.3 Strategic Research (When Time Permits)

| Gap ID | Skill | Description | Best Source |
|--------|-------|-------------|-------------|
| GAP-AF-003 | Waterfall Distributions | Investment calculations | AppFolio |
| GAP-AF-004 | Architectural Review | HOA workflow | AppFolio, HOAi |
| GAP-BL-001 | Integrated Banking | Fintech model | Baselane |
| GAP-BILT-001 | Rent Rewards | Consumer loyalty | BILT |

---

## 8. Research Tracker

### 8.1 Progress Template

Track your progress using this format:

```markdown
## Research Progress Tracker

### Week of [Date]

| Gap ID | Status | Hours Spent | Confidence | Notes |
|--------|--------|-------------|------------|-------|
| GAP-AF-001 | In Progress | 4 | Medium | Found good YouTube demos |
| GAP-HOAI-002 | Complete | 6 | High | Ready for review |
| GAP-PL-001 | Not Started | 0 | - | Next priority |

### Blockers
- [Any blockers or challenges]

### Insights
- [Any cross-cutting insights discovered]
```

### 8.2 Weekly Output Expectations

| Experience Level | Expected Output |
|------------------|-----------------|
| Junior Analyst | 2-3 completed knowledge documents per week |
| Senior Analyst | 4-5 completed knowledge documents per week |
| Complex gaps | May take full week for single document |

---

## 9. Tips for Effective Research

### 9.1 YouTube Research Tips

1. **Watch at 1.5x-2x speed** - Get through more content
2. **Use timestamps** - Note exactly where key info appears
3. **Check comments** - Often contain user insights
4. **Look for "vs" videos** - Great for comparisons
5. **Find customer reviews** - More honest than vendor demos

### 9.2 Reddit Research Tips

1. **Sort by "Top" or "Best"** - Find highest quality content
2. **Check post age** - Prefer recent (last 2 years)
3. **Read full threads** - Best info often in replies
4. **Search with quotes** - `"exact phrase"` for precision
5. **Check user history** - Verify credibility

### 9.3 Documentation Tips

1. **Use screenshots liberally** - A picture saves many words
2. **Create diagrams** - Workflow diagrams are invaluable
3. **Quote directly** - Use exact language from sources
4. **Note uncertainty** - Be explicit about what you don't know
5. **Cross-reference** - Multiple sources increase confidence

### 9.4 Common Pitfalls to Avoid

| Pitfall | Why It's Bad | How to Avoid |
|---------|--------------|--------------|
| Single source | May be outdated or biased | Always use 3+ sources |
| Marketing speak | Doesn't describe actual functionality | Look for demos, user reviews |
| Assumptions | Can lead to wrong implementation | Flag as "assumed" or "needs validation" |
| Too high-level | Not actionable for engineering | Push for specific details |
| No sources cited | Can't validate or update later | Always include URLs |

---

## 10. Getting Started

### 10.1 Your First Assignment

1. **Read this guide completely**
2. **Review the Master Registry**: `registry/MASTER_SKILL_REGISTRY.md`
3. **Pick a P0 gap** from Section 7.1
4. **Create your first Knowledge Document** using the template
5. **Submit for review**

### 10.2 Questions?

If you have questions about:
- **The process**: Ask your manager
- **A specific gap**: Check the competitor's KNOWLEDGE_GAPS.md file
- **Technical details**: Flag in your document as "needs engineering input"

### 10.3 Success Metrics

You're succeeding when:
- Engineering can build from your docs without asking questions
- Your confidence levels are calibrated (what you say is "High" is actually high)
- Knowledge documents are comprehensive but not bloated
- Research time is decreasing as you learn the domain

---

## Appendix A: Competitor Quick Reference

| Competitor | Focus | Website | Best For |
|------------|-------|---------|----------|
| **Guesty** | Enterprise STR PMS | guesty.com | Scale operations |
| **Hostaway** | Enterprise STR PMS | hostaway.com | Trust accounting |
| **OwnerRez** | Mid-market accounting | ownerrez.com | QuickBooks integration |
| **GuestWisely** | Professional all-in-one | guestwisely.io | Quote chaser, guest app |
| **Lodgify** | SMB website-first | lodgify.com | Direct booking |
| **Hospitable** | SMB automation | hospitable.com | AI messaging |
| **PriceLabs** | Dynamic pricing | pricelabs.co | HLP algorithm |
| **Vendoroo** | Maintenance AI | vendoroo.ai | AI agents |
| **EliseAI** | Leasing AI | eliseai.com | Leasing automation |
| **AppFolio** | Enterprise multi-vertical | appfolio.com | HOA, Investment |
| **HOAi** | HOA AI workforce | hoai.com | AI agent model |
| **Baselane** | Fintech for landlords | baselane.com | Banking integration |
| **BILT** | Consumer loyalty | biltrewards.com | Rent rewards |
| **Hemlane** | Hybrid PM | hemlane.com | Services + software |

---

## Appendix B: Glossary

| Term | Definition |
|------|------------|
| **PMS** | Property Management System |
| **STR** | Short-Term Rental |
| **LTR** | Long-Term Rental |
| **OTA** | Online Travel Agency (Airbnb, Vrbo, etc.) |
| **HOA** | Homeowners Association |
| **HITL** | Human-in-the-Loop |
| **HLP** | Hyper-Local Pulse (PriceLabs algorithm) |
| **CAM** | Common Area Maintenance |
| **RAG** | Retrieval-Augmented Generation |
| **NLU** | Natural Language Understanding |
| **OCR** | Optical Character Recognition |
| **GL** | General Ledger |
| **AP** | Accounts Payable |
| **AR** | Accounts Receivable |

---

**Good luck with your research! The quality of your knowledge documents directly impacts the quality of our product.**


