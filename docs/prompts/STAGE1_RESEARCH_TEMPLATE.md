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

### GAP-PL-002: Event Detection

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-PL-002 (Event Detection)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-PL-002 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- What are the 4 detection methods?
- How is event impact quantified?
- How far in advance are events detected?
- How is this integrated into pricing?

PRIMARY SOURCES:
- PriceLabs help docs
- YouTube: "PriceLabs events"
- Conference presentations

SAVE OUTPUT TO:
knowledge/pricing/KD-PL-002-event-detection.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-PL-002
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-PL-002 Event Detection" && git push
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

### GAP-AF-005: Unit Turn Board Design

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-AF-005 (Unit Turn Board Design)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-AF-005 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- What stages/statuses are tracked?
- How are tasks assigned?
- How is timeline managed?
- How are vendors coordinated?

PRIMARY SOURCES:
- AppFolio maintenance documentation
- YouTube: "AppFolio unit turn"
- Multifamily operations best practices

SAVE OUTPUT TO:
knowledge/operations/KD-AF-005-unit-turn-board.md

AFTER COMPLETING:
1. Update STATUS.md - Mark Stage 1 complete for GAP-AF-005
2. Update docs/PIPELINE_TRACKER.md - Add completion date and document path
3. git add -A && git commit -m "Stage 1 COMPLETE: GAP-AF-005 Unit Turn Board" && git push
```

---

### GAP-GW-001: Quote Chaser Automation

```
BEFORE STARTING:
1. git pull origin main

YOUR TASK:
Research GAP-GW-001 (Quote Chaser Automation)

WHAT TO READ:
1. docs/AGENT_GUIDE.md - Your step-by-step process
2. docs/RESEARCH_ANALYST_GUIDE.md - Research methodology
3. docs/MVP_PRIORITY_GAPS.md - Find GAP-GW-001 section for:
   - Research questions to answer
   - Sources to check
   - Definition of done

RESEARCH QUESTIONS TO ANSWER:
- How many follow-ups in sequence?
- What timing between follow-ups?
- What personalization options?
- How is conversion tracked?

PRIMARY SOURCES:
- GuestWisely product pages
- Email marketing automation patterns
- CRM follow-up best practices

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

