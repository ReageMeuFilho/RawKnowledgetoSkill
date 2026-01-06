# Stage 1: Research Agent Prompt Templates

> **Purpose**: Copy-paste prompts to trigger Research Agent for any gap
> **Last Updated**: January 2026

---

## 🚀 QUICK START TEMPLATE

Copy this template, replace the `[PLACEHOLDERS]`, and give to your Research Agent:

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research [GAP-ID] ([Gap Name])

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find [GAP-ID] section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

SAVE OUTPUT TO:
knowledge/[category]/KD-[GAP-ID]-[short-name].md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for [GAP-ID]
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: [GAP-ID] [Gap Name]" && git push
```

---

## 📋 READY-TO-USE PROMPTS

### GAP-AF-001: AI Leasing Assistant

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-AF-001 (AI Leasing Assistant)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-AF-001 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- How are leads qualified automatically?
- What questions can AI answer vs escalate?
- How is tour scheduling integrated?
- What's the 24/7 coverage model?

PRIMARY SOURCES:
- eliseai.com - All product pages
- AppFolio Realm-X documentation
- YouTube: "EliseAI demo"
- G2/Capterra reviews for EliseAI

SAVE OUTPUT TO:
knowledge/communication/KD-AF-001-ai-leasing-assistant.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-AF-001
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-AF-001 AI Leasing Assistant" && git push
```

---

### GAP-AF-002: AI Maintenance Coordinator

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-AF-002 (AI Maintenance Coordinator)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-AF-002 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- What troubleshooting can AI do remotely?
- How is vendor selection automated?
- How are emergencies handled?
- What's the escalation logic?

PRIMARY SOURCES:
- vendoroo.ai - All product pages
- AppFolio maintenance docs
- YouTube: "Vendoroo demo"
- Reddit: r/PropertyManagement "maintenance software"

SAVE OUTPUT TO:
knowledge/operations/KD-AF-002-ai-maintenance-coordinator.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-AF-002
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-AF-002 AI Maintenance Coordinator" && git push
```

---

### GAP-PL-001: HLP Dynamic Pricing Algorithm

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-PL-001 (HLP Dynamic Pricing Algorithm)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-PL-001 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- How does Hyper-Local Pulse work?
- What data inputs are used?
- How granular is the pricing (0.5km-5km)?
- How is elasticity calculated?

PRIMARY SOURCES:
- pricelabs.co - Help documentation
- YouTube: "PriceLabs tutorial", "PriceLabs review"
- PriceLabs blog posts
- Reddit: r/airbnb_hosts "PriceLabs"

SAVE OUTPUT TO:
knowledge/pricing/KD-PL-001-hlp-algorithm.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-PL-001
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-PL-001 HLP Algorithm" && git push
```

---

### GAP-PL-002: Event Detection ⭐ DETAILED PROMPT AVAILABLE

> **Full Research Prompt**: `docs/prompts/RESEARCH_PROMPT_PL-002_EVENT_DETECTION.md`

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-PL-002 (Four-Way Event Detection System)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/prompts/RESEARCH_PROMPT_PL-002_EVENT_DETECTION.md - DETAILED PROMPT (10 sections)

RESEARCH QUESTIONS TO ANSWER:
- How do the 4 detection signals work (YoY pacing, booking velocity, competitor prices, hotel ADR)?
- How is confidence scoring calculated from multiple signals?
- How are known events (calendar) vs unknown events (anomaly) detected?
- How is surge pricing triggered and what multipliers are applied?
- What event categories exist and how is impact radius determined?

PRIMARY SOURCES:
- PriceLabs help center - Event detection docs
- PriceLabs blog - Event pricing best practices
- YouTube: "PriceLabs event detection", "PriceLabs surge pricing"
- Reddit: r/airbnb_hosts "event pricing", r/STRowners "PriceLabs events"
- Wheelhouse, Beyond Pricing, AirDNA for competitive analysis

SAVE OUTPUT TO:
knowledge/pricing/KD-PL-002-event-detection.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-PL-002
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-PL-002 Event Detection System" && git push
```

---

### GAP-VEN-001: Maintenance Brain Architecture

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-VEN-001 (Maintenance Brain Architecture)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-VEN-001 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- What does "persistent learning" mean?
- How does it remember property history?
- How are decisions improved over time?
- What data is stored per property?

PRIMARY SOURCES:
- Vendoroo website deep-dive
- Founder interviews/podcasts
- Case studies

SAVE OUTPUT TO:
knowledge/operations/KD-VEN-001-maintenance-brain.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-VEN-001
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-VEN-001 Maintenance Brain" && git push
```

---

### GAP-AF-005: Unit Turn Board Design ⭐ DETAILED PROMPT AVAILABLE

> **Full Research Prompt**: `docs/prompts/RESEARCH_PROMPT_AF-005_UNIT_TURN_BOARD.md`

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-AF-005 (Unit Turn Board Design)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/prompts/RESEARCH_PROMPT_AF-005_UNIT_TURN_BOARD.md - DETAILED PROMPT (10 sections)

RESEARCH QUESTIONS TO ANSWER:
- What are the standard turn stages (Move-Out → Inspection → Repairs → Paint → Clean → Final)?
- How is the visual Kanban board structured?
- How are tasks assigned to vendors vs in-house staff?
- What scheduling/dependency logic optimizes parallel task execution?
- What metrics are tracked (turn time, cost per turn, vacancy days)?
- How does turn board integrate with PMS, vendor portal, mobile?

PRIMARY SOURCES:
- AppFolio Help Center - Unit Turn Board documentation
- AppFolio Blog - Turn management best practices
- YouTube: "AppFolio unit turn board", "make ready process property management"
- NARPM - National Association of Residential Property Managers
- Multifamily Executive Magazine - Turn process articles
- Reddit: r/PropertyManagement "unit turn"

SAVE OUTPUT TO:
knowledge/operations/KD-AF-005-unit-turn-board.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-AF-005
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-AF-005 Unit Turn Board Design" && git push
```

---

### GAP-GW-001: Quote Chaser Automation

**📄 DETAILED PROMPT AVAILABLE**: `docs/prompts/RESEARCH_PROMPT_GW-001_QUOTE_CHASER.md`

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-GW-001 (Quote Chaser Automation)

DETAILED PROMPT:
Read docs/prompts/RESEARCH_PROMPT_GW-001_QUOTE_CHASER.md for comprehensive requirements including:
- 12 detailed sections to research
- Quote lifecycle state machine design
- Follow-up sequence patterns (3-5 emails)
- Multi-channel strategy (Email → SMS → WhatsApp)
- Message template variables
- Conversion tracking & attribution
- A/B testing framework
- AI enhancement opportunities
- Complete data model (JSON schemas)
- Compliance requirements (CAN-SPAM, TCPA, GDPR)
- E-commerce abandoned cart parallels

KEY INSIGHT:
Quote Chaser = "Abandoned Cart Recovery" for Property Management
Research e-commerce patterns (Klaviyo, Shopify, Mailchimp) in addition to PMS sources.

SAVE OUTPUT TO:
knowledge/channel/KD-GW-001-quote-chaser.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-GW-001
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-GW-001 Quote Chaser" && git push
```

---

## 📊 GAP REFERENCE TABLE

| Gap ID | Name | Category | Output Path |
|--------|------|----------|-------------|
| GAP-AF-001 | AI Leasing Assistant | communication | `knowledge/communication/KD-AF-001-ai-leasing-assistant.md` |
| GAP-AF-002 | AI Maintenance Coordinator | operations | `knowledge/operations/KD-AF-002-ai-maintenance-coordinator.md` |
| GAP-PL-001 | HLP Algorithm | pricing | `knowledge/pricing/KD-PL-001-hlp-algorithm.md` |
| GAP-PL-002 | Event Detection | pricing | `knowledge/pricing/KD-PL-002-event-detection.md` |
| GAP-VEN-001 | Maintenance Brain | operations | `knowledge/operations/KD-VEN-001-maintenance-brain.md` |
| GAP-AF-005 | Unit Turn Board | operations | `knowledge/operations/KD-AF-005-unit-turn-board.md` |
| GAP-GW-001 | Quote Chaser | channel | `knowledge/channel/KD-GW-001-quote-chaser.md` |

---

## ✅ CHECKLIST FOR RESEARCH AGENT

Before submitting your work, verify:

- [ ] Git pulled latest before starting
- [ ] Read all 3 required docs (AGENT_GUIDE, RESEARCH_ANALYST_GUIDE, MVP_PRIORITY_GAPS)
- [ ] Answered ALL research questions for the gap
- [ ] Consulted at least 3 sources
- [ ] Used the Knowledge Document template from RESEARCH_ANALYST_GUIDE
- [ ] Assigned confidence level (High/Medium/Low)
- [ ] Saved to correct path
- [ ] Updated STATUS.md
- [ ] Updated PIPELINE_TRACKER.md
- [ ] Committed and pushed to GitHub

---

## 🔄 WHAT HAPPENS NEXT

After Research Agent completes Stage 1:

1. **User** brings the knowledge document to **Cursor AI**
2. **Cursor AI** does quality review and creates engineering prompt (Stage 2)
3. **User** gives prompt to **Engineering Agent** (Stage 3)
4. **User** brings engineering spec back to **Cursor AI** (Stage 4)
5. **Cursor AI** creates final skill specifications

See `docs/KNOWLEDGE_TO_SKILL_WORKFLOW.md` for the full pipeline.

