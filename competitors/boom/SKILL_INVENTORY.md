# Boom AI (AiPMS) - Skill Inventory

> **Source**: `boom_aipms_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: Full AiPMS (AI-powered Property Management System)
> **Type**: Unified Platform with Agentic AI (BAM)

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 34 | 7 NEW, 27 overlap (with DEPTH) |
| Tools | 12 | 3 NEW |
| Memory Types | 6 | 2 NEW |
| Workflows | 8 | 3 NEW |

---

## 🎯 Boom AI Context

**Boom is the "world's first AiPMS"** - a unified platform with:
- **BAM (Business Agentic Manager)** - Autonomous AI agent
- **75% guest communication automation**
- **100% review response automation**
- **80%+ faster response times**
- **NPS 86** (vs. industry average ~40)
- **$12.7M funding** (October 2025)
- **5,000+ properties** in 20+ countries

**Key Differentiator from Besty**:
- Boom = **Full PMS replacement** (unified platform)
- Besty = **AI copilot layer** (works with existing PMS)

**Key Differentiator from Guesty**:
- Boom = **AI-native architecture** (built from ground up with AI)
- Guesty = **Traditional PMS** with AI bolted on

---

## 🆕 NEW Skills (Not in Previous PRDs)

### NEW-BOOM-001: Voice AI Concierge
**Category**: communication
**Priority**: P1
**Status**: Coming Soon (Q1 2026)

**Description**: 
AI-powered phone answering for 24/7 voice support.

**Unique Capabilities**:
- Answer all incoming calls 24/7
- Natural language understanding
- Make reservations via phone
- Process payments by voice
- Handle service requests
- Sentiment detection (frustration, urgency)
- 5+ languages (English, Spanish, Portuguese, German, French)
- Seamless handoff to human when needed
- Call recording and transcription
- Voicemail to SMS/email conversion

**Integration**:
- Real-time PMS access for availability
- Guest history context in every call
- Immediate reservation creation

**Knowledge Required**:
- KG-BOOM-001: Voice AI implementation patterns

---

### NEW-BOOM-002: Multi-Function Agentic Execution
**Category**: ai-control
**Priority**: P0
**Description**: 
BAM handles messaging, reviews, and reporting simultaneously (not isolated task automation).

**Unique Capabilities**:
- Simultaneous multi-function execution
- Cross-function context awareness
- Pattern learning across operations
- Autonomous decision-making
- Transparent reasoning (can see why BAM took action)
- Continuous learning from results

**Architecture**:
- Reinforcement learning for optimal responses
- Multi-modal learning (text, images, voice)
- Real-time data ingestion
- Feedback loops improve model
- Daily model updates

**Knowledge Required**:
- KG-BOOM-002: Agentic AI architecture

---

### NEW-BOOM-003: Predictive Guest Outreach
**Category**: communication
**Priority**: P1
**Description**: 
AI proactively reaches out with offers based on guest profile analysis.

**Unique Capabilities**:
- Predict guest needs before they ask
- Timing optimization (when to send for max conversion)
- Content personalization to guest profile
- Dynamic pricing for offers by segment
- Booking behavior analysis (lead time, length patterns)

---

### NEW-BOOM-004: Call Recording & Transcription
**Category**: communication
**Priority**: P2
**Description**: 
Automatic call recording with searchable transcription.

**Unique Capabilities**:
- Call recording (compliance-aware)
- Real-time transcription
- Searchable call history
- Sentiment analysis of calls
- Key topic extraction
- Follow-up task creation from calls

---

### NEW-BOOM-005: Voicemail to SMS/Email Conversion
**Category**: communication
**Priority**: P2
**Description**: 
Automatically convert voicemails to text and route to appropriate channel.

**Unique Capabilities**:
- Voicemail transcription
- SMS delivery of voicemail content
- Email backup of voicemails
- Priority routing based on content
- Guest callback scheduling

---

### NEW-BOOM-006: Beyond Dynamic Pricing Integration
**Category**: pricing
**Priority**: P1
**Description**: 
Native integration with Beyond for ML-powered dynamic pricing.

**Unique Capabilities**:
- Direct data flow from Beyond
- <15 minute rate sync to all channels
- Decade of STR pricing data
- Market demand analysis
- Competitor rate monitoring
- Seasonal pattern optimization

---

### NEW-BOOM-007: Causal AI Understanding
**Category**: ai-control
**Priority**: P2
**Description**: 
AI that understands cause-and-effect relationships, not just correlations.

**Unique Capabilities**:
- Understand WHY guests ask questions
- Predict impact of actions
- Root cause analysis for issues
- Intervention recommendations
- Outcome forecasting

---

## 🔄 Skills Overlapping with Other PRDs

Boom provides **unified platform depth** for skills that exist across multiple PRDs:

### Platform Features (vs. Guesty)

| Feature | Boom | Guesty | Winner |
|---------|------|--------|--------|
| Reservation Management | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Tie |
| Channel Manager | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Tie |
| Guest Messaging | ⭐⭐⭐⭐⭐ (AI) | ⭐⭐⭐⭐ | Boom |
| Task Management | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Guesty |
| Reporting | ⭐⭐⭐⭐⭐ (AI) | ⭐⭐⭐⭐ | Boom |
| Dynamic Pricing | ⭐⭐⭐⭐⭐ (Beyond) | ⭐⭐⭐ | Boom |
| Payments | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Tie |
| Mobile App | ⭐⭐⭐⭐⭐ (60%+) | ⭐⭐⭐⭐ | Boom |

### AI Features (vs. Besty)

| Feature | Boom | Besty | Winner |
|---------|------|-------|--------|
| Guest Messaging | 75% automation | 75% automation | Tie |
| Review Response | 100% auto | 100% auto | Tie |
| Gap Night Upselling | Basic | ⭐⭐⭐⭐⭐ | Besty |
| Inquiry Winback | No | ⭐⭐⭐⭐⭐ | Besty |
| Journeys | Basic | ⭐⭐⭐⭐⭐ | Besty |
| Voice AI | ⭐⭐⭐⭐⭐ | ❌ | Boom |
| Multi-Function Agent | ⭐⭐⭐⭐⭐ | ❌ | Boom |
| Predictive Outreach | ⭐⭐⭐⭐⭐ | Basic | Boom |

---

## 📊 BAM (Business Agentic Manager) Deep Dive

**What Makes BAM Different**:

Traditional automation:
> "When guest sends message, generate response"

BAM agentic automation:
> "Continuously monitor operations, evaluate patterns, make autonomous decisions across messaging + reviews + reporting + marketing simultaneously"

**BAM Capabilities**:

| Capability | Description | Automation |
|------------|-------------|------------|
| Guest Messaging | Answer FAQs, pre-arrival, during-stay | 75% |
| Review Response | Generate contextual responses | 100% |
| Reporting | Daily/weekly/monthly reports | 100% |
| Marketing | Campaigns, upsells, loyalty | 80% |
| Pattern Learning | Learn property-specific patterns | Continuous |
| Multi-Task | Handle all above simultaneously | Yes |

**BAM Technical Architecture**:
- Reinforcement learning (learns optimal actions)
- Large language models (NLU/NLG)
- Multi-modal (text, images, voice)
- Continuous training (daily updates)
- Context awareness (guest history + booking + local events)
- Privacy-preserving (no direct guest data in external model)

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-BOOM-001 | process_voice_call | Handle incoming phone call | BUILD |
| TOOL-BOOM-002 | transcribe_call | Convert call audio to text | BUY (Whisper API) |
| TOOL-BOOM-003 | voicemail_to_text | Convert voicemail to SMS/email | BUILD |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-BOOM-001 | Call Recordings | Audio files of guest calls | 90 days |
| MEM-BOOM-002 | Call Transcripts | Searchable text of calls | 1 year |

---

## 🔀 NEW Workflows from Boom

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-BOOM-001 | Voice Call Handling | Incoming call | Answer → Identify → Resolve/Escalate |
| WF-BOOM-002 | Voicemail Processing | Voicemail received | Transcribe → Route → Notify |
| WF-BOOM-003 | Multi-Function Monitoring | Continuous | Monitor → Evaluate → Act across all functions |

---

## 📋 Knowledge Gaps from Boom

| ID | Knowledge Needed | Skills Blocked | Priority |
|----|------------------|----------------|----------|
| KG-BOOM-001 | Voice AI implementation | Voice Concierge | HIGH |
| KG-BOOM-002 | Agentic AI architecture | Multi-Function | HIGH |
| KG-BOOM-003 | Beyond pricing integration | Dynamic Pricing | MEDIUM |
| KG-BOOM-004 | Call transcription accuracy | Call Recording | LOW |

---

## 🏆 What Boom Adds to Our Solution

**ADOPT (Critical)**:
1. **Voice AI Concierge** - 24/7 phone answering is game-changer
2. **Multi-Function Agent** - Simultaneous handling vs. isolated tasks
3. **Predictive Outreach** - Proactive vs. reactive

**ADOPT (Valuable)**:
1. **Beyond Integration** - Proven dynamic pricing
2. **Call Recording** - Compliance and training
3. **Voicemail Conversion** - Never miss a message

**CONSIDER**:
1. **Causal AI** - Advanced, may be over-engineering for MVP

---

## 📊 Competitive Positioning

| Dimension | Boom | Guesty | Host OS | Besty | Mews |
|-----------|------|--------|---------|-------|------|
| **Type** | Full AiPMS | Full PMS | Concept | AI Layer | Hotel PMS |
| **Voice AI** | ⭐⭐⭐⭐⭐ | ❌ | ⭐⭐⭐ | ❌ | ❌ |
| **Agentic AI** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **Messaging** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Revenue** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Operations** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **NPS** | 86 | ~65 | N/A | >70 | ~70 |

**Bottom Line**: Boom provides **Voice AI** and **multi-function agentic architecture** that no other competitor has. Use Boom patterns for voice handling and true agentic behavior.

---

## 🎯 Strategic Insight

**The Boom vs. Besty Decision**:

| Factor | Choose Boom | Choose Besty |
|--------|-------------|--------------|
| Existing PMS? | No (replace) | Yes (keep) |
| Voice support? | Critical | Not needed |
| Implementation | 4-6 weeks | 5 minutes |
| Data migration | Required | None |
| Monthly cost | Higher ($500+) | Commission only |
| Unified platform? | Yes | No (layer) |

**Our Solution**: Combine BOTH approaches
- Use Boom's **Voice AI** and **agentic architecture** patterns
- Use Besty's **revenue upselling** and **journey** patterns
- Build on Kortix/Suna for implementation



