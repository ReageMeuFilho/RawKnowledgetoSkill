# Hospitable - Knowledge Gaps

> **Source**: HOSPITABLE (v2.0)PRD.md
> **Analysis Date**: January 2026
> **Total New Gaps**: 6

---

## 📊 Gap Summary

| Priority | Count | Focus Area |
|----------|-------|------------|
| **P0 - Critical** | 3 | Knowledge Hub, devices, sentiment |
| **P1 - Important** | 2 | Orphan nights, guest summaries |
| **P2 - Nice-to-have** | 1 | Review patterns |

---

## 🔴 P0 - Critical Knowledge Gaps

### GAP-HSP-001: Knowledge Hub Architecture

**Skill**: SKILL-193 (knowledge-hub-ai-answers)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Document Ingestion**
   - What document formats are supported?
   - How is content parsed and indexed?
   - How are guidebooks structured?

2. **Knowledge Retrieval**
   - How are relevant sections found?
   - What RAG approach is used?
   - How is context window managed?

3. **Response Generation**
   - How are answers composed?
   - How is hallucination prevented?
   - What confidence thresholds exist?

4. **Host Override**
   - How can hosts correct AI?
   - How are corrections learned?
   - What approval workflows exist?

**Why Critical**: This is the core AI capability - without it, we're just templates.

**Ideal Source**:
- [ ] RAG implementation patterns
- [ ] Property management FAQ datasets
- [ ] Conversational AI best practices

---

### GAP-HSP-002: Smart Device Integration Architecture

**Skill**: SKILL-194 (smart-device-orchestration)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Lock Integration**
   - Which lock brands/models supported?
   - How are codes generated and synced?
   - What's the code delivery timing?
   - How is code expiration handled?

2. **Thermostat Integration**
   - Which thermostat brands supported?
   - What are occupancy-based rules?
   - How is energy savings calculated?
   - What's the fallback if device offline?

3. **Device Discovery & Management**
   - How are devices discovered?
   - How is health monitored?
   - What happens on device failure?

**Why Critical**: Smart devices are differentiator vs other SMB platforms.

**Ideal Source**:
- [ ] RemoteLock API documentation
- [ ] Smart thermostat APIs (Nest, Ecobee)
- [ ] IoT orchestration patterns

---

### GAP-HSP-003: Sentiment Detection System

**Skill**: SKILL-196 (sentiment-escalation)
**Status**: 🔴 BLOCKING

**What We Need**:
1. **Detection Signals**
   - What words/phrases trigger detection?
   - How is sentiment scored?
   - What's the escalation threshold?

2. **Escalation Logic**
   - When to pause AI?
   - When to notify host?
   - When to transfer to human?

3. **False Positive Handling**
   - How to tune for accuracy?
   - How to handle cultural differences?
   - What about sarcasm/jokes?

**Why Critical**: **Safety net** - without this, AI can make things worse.

**Ideal Source**:
- [ ] Sentiment analysis models
- [ ] Customer service escalation patterns
- [ ] AI safety research

---

## 🟡 P1 - Important Knowledge Gaps

### GAP-HSP-004: Orphan Night Detection Algorithm

**Skill**: SKILL-195 (ai-orphan-night-detection)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Gap Detection**
   - What counts as "orphan" (1 night? 2?)
   - How are extendable bookings identified?
   - What minimum stay rules apply?

2. **Offer Calculation**
   - How is discount calculated?
   - What's the optimal offer timing?
   - What acceptance rates are typical?

3. **Guest Targeting**
   - Which guests are best candidates?
   - How are offers personalized?
   - What about guests who already left?

**Ideal Source**:
- [ ] Revenue management patterns
- [ ] Gap-filling strategies
- [ ] Discount optimization research

---

### GAP-HSP-005: Guest Summary Generation

**Skill**: SKILL-197 (ai-guest-summaries)
**Status**: 🟡 NEEDED

**What We Need**:
1. **Data Sources**
   - What data is used for summaries?
   - How is history incorporated?
   - What about privacy concerns?

2. **Summary Structure**
   - What sections are included?
   - What format is used?
   - How long is typical summary?

3. **Actionable Insights**
   - What personalization is suggested?
   - What concerns are flagged?
   - How are preferences highlighted?

**Ideal Source**:
- [ ] Guest profile patterns
- [ ] Pre-arrival preparation guides
- [ ] Personalization strategies

---

## 🟢 P2 - Nice-to-Have Knowledge Gaps

### GAP-HSP-006: Review Pattern Analysis

**Skill**: SKILL-199 (ai-review-pattern-detection)
**Status**: 🟢 OPTIONAL

**What We Need**:
1. **Theme Extraction**
   - How are common themes identified?
   - What NLP techniques are used?
   - How are themes categorized?

2. **Trend Detection**
   - How are patterns over time found?
   - What's statistically significant?
   - How are property comparisons made?

**Ideal Source**:
- [ ] Review analysis tools
- [ ] NLP topic modeling
- [ ] Trend detection algorithms

---

## 📋 Knowledge Collection Plan

### Phase 1: AI Core (Week 1-2)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HSP-001 | RAG implementation research | TBD |
| GAP-HSP-003 | Sentiment analysis models | TBD |

### Phase 2: Smart Devices (Week 3-4)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HSP-002 | Smart lock/thermostat APIs | TBD |

### Phase 3: Revenue (Week 5)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HSP-004 | Revenue management research | TBD |
| GAP-HSP-005 | Guest profiling patterns | TBD |

### Phase 4: Analytics (Week 6)
| Gap | Source Strategy | Owner |
|-----|-----------------|-------|
| GAP-HSP-006 | NLP topic modeling | TBD |

---

## 🎯 Strategic Priorities

### For SMB Market Entry

If we want to compete with Hospitable:
1. **Must have**: Knowledge Hub (GAP-HSP-001)
2. **Must have**: Sentiment detection (GAP-HSP-003)
3. **Should have**: Smart devices (GAP-HSP-002)
4. **Nice to have**: Orphan nights (GAP-HSP-004)

### Implementation Order

```
1. Knowledge Hub (RAG) → Enables AI answers
2. Sentiment Detection → Safety for AI
3. Cross-System Workflows → Orchestration
4. Smart Devices → IoT integration
5. Orphan Night AI → Revenue optimization
```

---

## 🏆 Competitive Intelligence

### Hospitable's Moat

1. **Knowledge Hub** - First to market with guidebook AI
2. **Smart Device Native** - Deep integration, not partnership
3. **Cross-System** - Single workflow across all systems
4. **AI-First Culture** - Every feature considers AI

### How to Compete

| Approach | Pros | Cons |
|----------|------|------|
| **Match Hospitable** | Capture automation-first hosts | Development time |
| **Focus Enterprise** | Leave SMB to Hospitable | Miss 95% of market |
| **Partner** | Integrate Hospitable for SMB | Revenue share |
| **Differentiate** | Better AI (multi-model) | Need to prove value |

**Recommendation**: Match Hospitable's core AI features (Knowledge Hub, sentiment), add our differentiation (open-source, multi-model, international).

---

## 📊 SMB Market Complete

With Lodgify + Hospitable analyzed, SMB market is now fully mapped:

| Platform | Focus | Best For |
|----------|-------|----------|
| **Lodgify** | Website-first | Brand-focused hosts |
| **Hospitable** | Automation-first | Efficiency-focused hosts |

### Our SMB Strategy

Combine both approaches:
- Lodgify's **website builder** simplicity
- Hospitable's **AI automation** depth
- Our **open-source flexibility** + **international reach**

This creates a compelling SMB tier that neither can match alone.


