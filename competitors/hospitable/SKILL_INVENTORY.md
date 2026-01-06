# Hospitable - Skill Inventory

> **Source**: HOSPITABLE (v2.0)PRD.md
> **Analysis Date**: January 2026
> **Focus**: AI-Native Automation Platform for Solo Hosts (1-50 properties)

---

## 🎯 **CRITICAL: Hospitable = Automation-First for SMB**

While Lodgify is website-first, Hospitable is **automation-first**:
- **90% message automation** target (AI + rules)
- **Native smart device management** (locks + thermostats)
- **Knowledge Hub AI** (reads guidebooks to answer FAQs)
- **Orphan night detection** (AI finds and fills gaps)

This is the **AI leader for SMB market**.

---

## Executive Summary

| Metric | Count |
|--------|-------|
| **Total Features Analyzed** | 50+ |
| **New Unique Skills** | 7 |
| **Overlapping with Registry** | 40+ |
| **Knowledge Gaps Identified** | 6 |

---

## 🆕 Unique Skills (New to Registry)

### 1. SKILL-193: knowledge-hub-ai-answers

**Priority**: P0
**Category**: ai-knowledge

**Description**: 
Central repository of host guidebooks, rules, and policies that AI reads to automatically answer guest FAQs.

**How It Works**:
- Host uploads guidebooks/house rules/policies
- AI indexes and understands content
- Guest asks question → AI searches knowledge
- AI drafts response using guidebook info
- Host can override or approve

**Key Differentiator**: AI doesn't just use templates - it **reads and understands** your actual guidebooks.

**Components**:
- Knowledge Hub (document repository)
- Guidebook parsing and indexing
- FAQ auto-detection
- Context-aware response generation
- Host override capability

---

### 2. SKILL-194: smart-device-orchestration

**Priority**: P0
**Category**: iot-automation

**Description**: 
Native management of smart locks and thermostats tied directly to booking events.

**Device Types**:
- **Smart Locks**: Auto-generate codes, send at appropriate times, expire after checkout
- **Thermostats**: Adjust temperature based on occupancy, energy-saving when vacant

**Orchestration Flow**:
1. Booking confirmed → Generate unique door code
2. Pre-arrival time → Send code to guest
3. Check-in → Adjust thermostat to comfort
4. Check-out → Expire code + energy-saving mode
5. Cleaning done → Reset for next guest

**Key Differentiator**: **Native integration** vs "via partners" - no separate apps needed.

---

### 3. SKILL-195: ai-orphan-night-detection

**Priority**: P1
**Category**: revenue-optimization

**Description**: 
AI automatically detects "orphan nights" (gap nights between bookings) and sends targeted offers to fill them.

**How It Works**:
1. AI scans calendar for 1-2 night gaps
2. Identifies guests who could extend
3. Calculates optimal discount to offer
4. Sends personalized offer to guest
5. Tracks conversion and revenue impact

**Key Differentiator**: **Proactive revenue recovery** vs waiting for guests to request.

**Related**: Similar to Besty AI's inquiry winback but for existing bookings.

---

### 4. SKILL-196: sentiment-escalation

**Priority**: P0
**Category**: ai-safety

**Description**: 
AI detects guest frustration or issues in messages and automatically flags for human escalation.

**Trigger Signals**:
- Negative sentiment words/phrases
- Complaint patterns
- Urgent language
- Safety concerns
- Legal/liability mentions

**Escalation Actions**:
- Flag conversation as "needs-review"
- Pause automated responses
- Notify host immediately
- Optionally transfer to human

**Key Differentiator**: **Safety net** for AI automation - prevents bad AI responses to upset guests.

---

### 5. SKILL-197: ai-guest-summaries

**Priority**: P1
**Category**: guest-intelligence

**Description**: 
AI generates pre-check-in summaries of guest profiles to help hosts prepare.

**Summary Contents**:
- Booking details
- Previous stays (if any)
- Communication history analysis
- Preferences mentioned
- Potential concerns flagged
- Suggested personalization

**Key Differentiator**: Know your guest **before they arrive** vs reacting during stay.

---

### 6. SKILL-198: cross-system-workflows

**Priority**: P0
**Category**: automation-orchestration

**Description**: 
Combined triggers that span messaging, devices, and tasks in a single automated workflow.

**Example Workflow**:
```
Booking Confirmed →
  1. Send welcome message
  2. Create cleaning task (day before)
  3. Generate door code
  4. Schedule code delivery (4 hours before check-in)
  5. Set thermostat schedule
  6. Create checkout reminder
  7. Schedule review request (day after checkout)
```

**Key Differentiator**: **Single workflow** spans all systems vs separate automations per system.

---

### 7. SKILL-199: ai-review-pattern-detection

**Priority**: P1
**Category**: analytics

**Description**: 
AI analyzes guest reviews to identify recurring issues and improvement opportunities.

**Analysis Types**:
- Common complaint themes
- Recurring praise areas
- Property-specific issues
- Seasonal patterns
- Comparison across properties

**Outputs**:
- Issue alerts
- Improvement suggestions
- Priority ranking
- Trend reports

**Key Differentiator**: **Proactive improvement** vs reactive problem-solving.

---

## 🔄 Overlapping Skills (Enhanced by Hospitable)

| Existing Skill | Hospitable Enhancement |
|----------------|------------------------|
| SKILL-178 (93% automation) | 90% target + AI answers |
| SKILL-185 (AI messaging) | + Knowledge Hub integration |
| SKILL-177 (status updates) | + Cross-system workflows |
| SKILL-XXX (task management) | + Device triggers |
| SKILL-190 (Google VR) | Also supported |

---

## 🏆 Best-in-Class Features

| Feature | Why Best | For Whom |
|---------|----------|----------|
| **Knowledge Hub AI** | Only platform with guidebook reading | FAQ-heavy hosts |
| **Smart Device Native** | No separate apps | Tech-forward hosts |
| **Sentiment Detection** | Safety net for AI | Risk-averse hosts |
| **Orphan Night AI** | Proactive revenue | Revenue-focused |
| **Cross-System Workflows** | Single automation span | Efficiency seekers |

---

## 📊 SMB Platform Comparison

### Hospitable vs Lodgify

| Dimension | Hospitable | Lodgify |
|-----------|------------|---------|
| **Primary Focus** | Automation | Website |
| **AI Depth** | **DEEP** | Basic |
| **Smart Devices** | **Native** | Limited |
| **Website Builder** | Simple | **Advanced** |
| **Entry Price** | $29/month | $16/month |
| **Best For** | Automation-first | Brand-first |

### Positioning Matrix

```
                    LOW                    HIGH
                    AI DEPTH
              ┌─────────────────────────────┐
    HIGH      │                    │        │
    WEBSITE   │     Lodgify       │        │
    FOCUS     │                    │        │
              ├────────────────────┼────────┤
    LOW       │                    │Hospitable
    WEBSITE   │     Basic PMS     │        │
    FOCUS     │                    │        │
              └─────────────────────────────┘
```

---

## 📈 Architectural Insights

### Hospitable Architecture Pattern
```
┌─────────────────────────────────────────────────────────────────┐
│                    HOSPITABLE PLATFORM                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ┌──────────────────────────────────────────────────────────┐  │
│   │                AI LAYER (Primary)                         │  │
│   │  ┌────────────┐ ┌────────────┐ ┌────────────┐            │  │
│   │  │ Knowledge  │ │ Sentiment  │ │ Orphan     │            │  │
│   │  │ Hub        │ │ Detection  │ │ Night AI   │            │  │
│   │  └────────────┘ └────────────┘ └────────────┘            │  │
│   └──────────────────────────────────────────────────────────┘  │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              CROSS-SYSTEM WORKFLOW ENGINE                  │ │
│   │  ┌────────────┐ ┌────────────┐ ┌────────────┐             │ │
│   │  │ Messaging  │ │ Devices    │ │ Tasks      │             │ │
│   │  │ Triggers   │ │ Triggers   │ │ Triggers   │             │ │
│   │  └────────────┘ └────────────┘ └────────────┘             │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │                   UNIFIED INBOX                            │ │
│   │         Airbnb | Vrbo | Booking.com | Direct               │ │
│   └───────────────────────────────────────────────────────────┘ │
│                              │                                   │
│   ┌──────────────────────────┴────────────────────────────────┐ │
│   │              SMART DEVICE ORCHESTRATION                    │ │
│   │         Locks (auto-codes) | Thermostats (occupancy)      │ │
│   └───────────────────────────────────────────────────────────┘ │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Key Insight for Our Platform

Hospitable validates that **AI-first architecture** works for SMB:
- Knowledge Hub = RAG for property operations
- Cross-system workflows = agentic orchestration
- Sentiment detection = AI safety rails
- Orphan night AI = proactive revenue optimization

This aligns with our Kortix/Suna base!

---

## 🎯 Strategic Implications

### What Hospitable Teaches Us

1. **Knowledge Hub is critical** - AI needs property-specific context
2. **Cross-system workflows** - Single automation across all systems
3. **Sentiment safety rails** - Essential for AI automation
4. **Proactive revenue** - AI should find opportunities, not just respond

### Our Competitive Response

| Hospitable Strength | Our Counter |
|--------------------|-------------|
| Knowledge Hub | RAG with property docs |
| Smart devices | MCP device integrations |
| Sentiment detection | Built into AI layer |
| Orphan night AI | Revenue optimization skill |
| Cross-system | Agentic orchestration |

### SMB Strategy

For SMB market (1-50 properties), we should offer:
1. **Hospitable-level AI** (Knowledge Hub, sentiment, workflows)
2. **Lodgify-level simplicity** (website builder, easy setup)
3. **Our unique value** (open-source, multi-model, international)

---

## Next Steps

1. **Document Knowledge Hub design** - How to implement RAG for property docs
2. **Smart device MCP servers** - Lock + thermostat integrations
3. **Sentiment detection patterns** - What triggers escalation
4. **Cross-system workflow engine** - Single automation graph


