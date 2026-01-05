# MVP Priority Knowledge Gaps

> **Purpose**: Focused list of P0 knowledge gaps that must be closed for MVP
> **Total P0 Skills**: 79
> **Last Updated**: January 2026

---

## 🎯 Research Priority Order

Research these gaps in order - each builds on the previous:

---

## TIER 1: Foundation (Research First)

These gaps inform all other decisions:

### 1. GAP-HOAI-001: AI Workforce Architecture
**Skill**: SKILL-261-268 (AI Workforce Model)
**Source**: HOAi

**Why First**: This is a new paradigm. Understanding how specialized AI agents work as "digital employees" will inform how we build ALL our AI features.

**Research Questions**:
- How do multiple agents coordinate?
- What's the task handoff pattern?
- How is quality measured per agent?
- What's the pricing model (per agent? per task?)

**Sources to Check**:
- [ ] hoai.com - Product pages, demos
- [ ] YouTube: "HOAi demo", "HOAi review"
- [ ] Vantaca partnership announcements
- [ ] LinkedIn: HOAi employees posts

---

### 2. GAP-HOAI-002: Human-in-the-Loop Dashboard
**Skill**: SKILL-265 (managerial-hub-hitl)
**Source**: HOAi

**Why Second**: Every AI feature needs human oversight. This is THE control layer.

**Research Questions**:
- How is the task queue structured?
- What info is shown per task?
- What's the one-click approval flow?
- How is feedback captured?

**Sources to Check**:
- [ ] HOAi product screenshots
- [ ] ML Ops approval patterns (Google "human-in-the-loop ML")
- [ ] Content moderation queue designs
- [ ] Fraud review system patterns

---

## TIER 2: Core AI Capabilities

### 3. GAP-AF-001: AI Leasing Assistant Architecture
**Skill**: SKILL-253 (ai-leasing-assistant)
**Sources**: EliseAI, AppFolio

**Research Questions**:
- How are leads qualified automatically?
- What questions can AI answer vs escalate?
- How is tour scheduling integrated?
- What's the 24/7 coverage model?

**Sources to Check**:
- [ ] eliseai.com - All product pages
- [ ] AppFolio Realm-X documentation
- [ ] YouTube: "EliseAI demo"
- [ ] G2/Capterra reviews for EliseAI
- [ ] LinkedIn: EliseAI employees

---

### 4. GAP-AF-002: AI Maintenance Coordinator Architecture
**Skill**: SKILL-254 (ai-maintenance-coordinator)
**Sources**: Vendoroo, AppFolio

**Research Questions**:
- What troubleshooting can AI do remotely?
- How is vendor selection automated?
- How are emergencies handled?
- What's the escalation logic?

**Sources to Check**:
- [ ] vendoroo.ai - All product pages
- [ ] AppFolio maintenance docs
- [ ] YouTube: "Vendoroo demo"
- [ ] Reddit: r/PropertyManagement "maintenance software"

---

### 5. GAP-HOAI-004: Multi-Channel Voice Agent
**Skill**: SKILL-261 (ai-voice-agent-multichannel)
**Sources**: HOAi, Boom AI

**Research Questions**:
- How is phone + SMS + chat + email unified?
- How does resident identification work?
- What actions can the agent take?
- How is escalation handled?

**Sources to Check**:
- [ ] HOAi Voice product page
- [ ] Twilio conversational AI docs
- [ ] YouTube: "AI phone answering property management"
- [ ] Contact center AI vendors (Five9, NICE, etc.)

---

## TIER 3: Pricing & Revenue

### 6. GAP-PL-001: HLP Dynamic Pricing Algorithm
**Skill**: SKILL-XXX (pricing-algorithm)
**Source**: PriceLabs

**Research Questions**:
- How does Hyper-Local Pulse work?
- What data inputs are used?
- How granular is the pricing (0.5km-5km)?
- How is elasticity calculated?

**Sources to Check**:
- [ ] pricelabs.co - Help documentation
- [ ] YouTube: "PriceLabs tutorial", "PriceLabs review"
- [ ] PriceLabs blog posts
- [ ] Reddit: r/airbnb_hosts "PriceLabs"

---

### 7. GAP-PL-002: Event Detection
**Skill**: SKILL-XXX (event-detection)
**Source**: PriceLabs

**Research Questions**:
- What are the 4 detection methods?
- How is event impact quantified?
- How far in advance are events detected?
- How is this integrated into pricing?

**Sources to Check**:
- [ ] PriceLabs help docs
- [ ] YouTube: "PriceLabs events"
- [ ] Conference presentations

---

## TIER 4: Operations

### 8. GAP-VEN-001: Maintenance Brain Architecture
**Skill**: SKILL-XXX (maintenance-brain)
**Source**: Vendoroo

**Research Questions**:
- What does "persistent learning" mean?
- How does it remember property history?
- How are decisions improved over time?
- What data is stored per property?

**Sources to Check**:
- [ ] Vendoroo website deep-dive
- [ ] Founder interviews/podcasts
- [ ] Case studies

---

### 9. GAP-AF-005: Unit Turn Board Design
**Skill**: SKILL-257 (unit-turn-board)
**Source**: AppFolio

**Research Questions**:
- What stages/statuses are tracked?
- How are tasks assigned?
- How is timeline managed?
- How are vendors coordinated?

**Sources to Check**:
- [ ] AppFolio maintenance documentation
- [ ] YouTube: "AppFolio unit turn"
- [ ] Multifamily operations best practices

---

## TIER 5: Automation & Workflows

### 10. GAP-GW-001: Quote Chaser Automation
**Skill**: SKILL-232 (quote-chaser-automation)
**Source**: GuestWisely

**Research Questions**:
- How many follow-ups in sequence?
- What timing between follow-ups?
- What personalization options?
- How is conversion tracked?

**Sources to Check**:
- [ ] GuestWisely product pages
- [ ] Email marketing automation patterns
- [ ] CRM follow-up best practices

---

## 📊 Research Tracker Template

Copy and use this for tracking:

```markdown
## Week of [DATE]

### Completed
| Gap ID | Document | Confidence | Hours |
|--------|----------|------------|-------|
| | | | |

### In Progress
| Gap ID | Status | Blockers |
|--------|--------|----------|
| | | |

### Insights Discovered
- 

### Questions for Engineering
- 
```

---

## 📁 Where to Save Completed Research

```
knowledge/
├── ai-workforce/
│   ├── KD-HOAI-001-workforce-architecture.md
│   └── KD-HOAI-002-hitl-dashboard.md
├── communication/
│   └── KD-AF-001-ai-leasing-assistant.md
├── operations/
│   ├── KD-AF-002-ai-maintenance-coordinator.md
│   └── KD-AF-005-unit-turn-board.md
├── pricing/
│   ├── KD-PL-001-hlp-algorithm.md
│   └── KD-PL-002-event-detection.md
└── financial/
    └── (future)
```

---

## ✅ Definition of Done

A gap is **CLOSED** when:
- [ ] Knowledge document created using template
- [ ] Workflow documented step-by-step
- [ ] Data model identified
- [ ] Business rules documented
- [ ] 3+ sources consulted
- [ ] Confidence level assigned
- [ ] Saved to correct knowledge/ folder
- [ ] Linked from competitor's KNOWLEDGE_GAPS.md

---

## 🚀 Get Started

1. Start with **GAP-HOAI-001** (AI Workforce Architecture)
2. Use the Research Analyst Guide for detailed instructions
3. Create knowledge documents using the template
4. Track progress weekly
5. Ask questions early - don't get stuck

**Target**: Close 2-3 P0 gaps per week

Good luck! 🎯

