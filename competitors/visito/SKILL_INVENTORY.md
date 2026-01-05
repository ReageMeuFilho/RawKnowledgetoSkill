# Visito AI Platform - Skill Inventory

> **Source**: `visito_ai_platform_prd_original.md`
> **Extracted**: January 2026
> **Vertical**: No-Code Conversational AI Platform
> **Type**: Multi-Channel Agent Builder (SMB Focus)

---

## 📊 Extraction Summary

| Category | Count | New vs Existing |
|----------|-------|-----------------|
| Skills | 38 | 8 NEW, 30 overlap (with DEPTH) |
| Tools | 6 | 2 NEW |
| Memory Types | 4 | 1 NEW |
| Workflows | 6 | 2 NEW |

---

## 🎯 Visito AI Context

**Visito is a "No-Code AI Agent Platform"** with:
- **2-minute agent creation** (fastest setup)
- **100+ languages** natively (MOST comprehensive!)
- **90%+ AI resolution rate**
- **$49/month entry point** (most affordable)
- **Multi-LLM support** (ChatGPT, Gemini, Claude)
- **500M+ messages/month** capacity

**Target**: SMBs, hospitality, e-commerce, fitness, service businesses

**Key Differentiator**:
- **Visito** = No-code, SMB-focused, $49 entry
- **Inntelo** = Enterprise hotels (50-500 rooms)
- **Boom** = Full AiPMS replacement
- **Besty** = Revenue AI layer

---

## 🆕 NEW Skills (Not in Previous PRDs)

### NEW-VIS-001: No-Code Agent Builder
**Category**: builder
**Priority**: P1
**Status**: NEEDED

**Description**: 
Drag-and-drop interface to create AI agents in 2 minutes without coding.

**Unique Capabilities**:
- Guided 5-step wizard
- Pre-built templates (support, sales, booking, e-commerce, appointments)
- Personality/tone configuration (professional, friendly, casual, humorous)
- Boundary settings (topics to avoid, discount authority)
- One-click launch
- 95%+ customers use no-code (vs. API)

**Templates Available**:
1. Customer Support
2. Sales & Lead Qualification
3. Booking & Reservations
4. E-commerce
5. Appointment Scheduling
6. Custom

---

### NEW-VIS-002: 100+ Language Native Support
**Category**: communication
**Priority**: P1
**Status**: NEEDED

**Description**: 
Most comprehensive multilingual support available.

**Comparison**:
| Platform | Languages |
|----------|-----------|
| Visito | **100+** |
| Inntelo | 40+ |
| Boom | 5+ |
| Guesty | 10+ |
| Besty | 5+ |

**Unique Capabilities**:
- Auto-detection of customer language
- Native fluency (not just translation)
- Language-based routing (match agent to customer)

---

### NEW-VIS-003: Knowledge Gap Detection
**Category**: ai-control
**Priority**: P1
**Status**: NEEDED

**Description**: 
AI identifies questions it can't answer and suggests what to add.

**Unique Capabilities**:
- Automatic identification of unanswered questions
- Suggestions for missing information
- FAQ recommendations from common questions
- Knowledge coverage metrics
- Preview responses before going live

---

### NEW-VIS-004: Back-to-Bot Handoff
**Category**: escalation
**Priority**: P2
**Status**: NEEDED

**Description**: 
After human resolves issue, can hand back to AI with context.

**Unique Capabilities**:
- Human resolves specific issue
- Hands conversation back to AI
- AI resumes with full context
- Prevents re-escalation for same issue
- System learns from human resolution

---

### NEW-VIS-005: Pre-Chat Survey
**Category**: communication
**Priority**: P2
**Status**: NEEDED

**Description**: 
Collect customer information before first message.

**Unique Capabilities**:
- Custom survey fields
- Required vs optional fields
- Conditional logic
- Data passed to AI for personalization
- CRM integration

---

### NEW-VIS-006: Widget Analytics
**Category**: analytics
**Priority**: P2
**Status**: NEEDED

**Description**: 
Track web chat widget engagement and conversion.

**Unique Capabilities**:
- Visitors who open chat
- Messages initiated vs abandoned
- Common entry points on website
- Bounce rate (close without chatting)
- Conversion tracking (chat → sale)
- ROI measurement

---

### NEW-VIS-007: RAG Hybrid Retrieval
**Category**: ai-control
**Priority**: P1
**Status**: NEEDED

**Description**: 
Combine semantic search + keyword matching for best results.

**Unique Capabilities**:
- Semantic search (find relevant documents)
- BM25 ranking (keyword matching)
- Hybrid combination
- Vector embeddings for similarity
- Source citation (show where answer came from)
- Reduces hallucination

---

### NEW-VIS-008: Tool Calling / Custom Actions
**Category**: integrations
**Priority**: P1
**Status**: NEEDED

**Description**: 
AI agent can call external APIs during conversation.

**Unique Capabilities**:
- Define tools (name, description, parameters)
- AI decides when to call
- Call inventory API, payment API, CRM, PMS
- Response parsing
- Error handling
- Agent determines parameters from conversation

**Example Tools**:
- Check inventory
- Process payment
- Look up customer
- Create booking
- Send email

---

## 🔄 Skills Overlapping with Other PRDs

### Feature Comparison Matrix

| Feature | Visito | Inntelo | Boom | Besty | Winner |
|---------|--------|---------|------|-------|--------|
| **Languages** | 100+ | 40+ | 5+ | 5+ | **Visito** |
| **Setup Time** | 2 min | Days | Days | 5 min | **Visito** |
| **No-Code** | Full | Limited | No | Yes | **Visito** |
| **Price Entry** | $49 | Custom | Custom | Commission | **Visito** |
| **Multi-Agent** | ⚠️ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ❌ | Inntelo |
| **CDP** | Basic | ⭐⭐⭐⭐⭐ | Basic | ❌ | Inntelo |
| **Voice AI** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ❌ | Boom |
| **Revenue Upsells** | Basic | ⭐⭐⭐⭐⭐ | Basic | ⭐⭐⭐⭐⭐ | Tie |
| **Operations** | ❌ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ❌ | Inntelo |

### Where Visito Excels

1. **Languages** - 100+ (most comprehensive)
2. **Setup Speed** - 2 minutes (fastest)
3. **No-Code** - Full drag-and-drop (most accessible)
4. **Price** - $49/month (most affordable)
5. **Knowledge Gap Detection** - Unique feature
6. **Back-to-Bot** - Unique handoff pattern

### Where Others Excel

1. **Inntelo** - CDP, Multi-Agent, Operations
2. **Boom** - Voice AI, BAM Architecture
3. **Besty** - Revenue psychology
4. **Guesty** - STR operations depth

---

## 📊 No-Code Builder Deep Dive

**5-Step Agent Creation Wizard**:

```
┌─────────────────────────────────────────────────────────────┐
│  STEP 1: Define Purpose                                     │
│  ├── Choose template (Support, Sales, Booking...)           │
│  └── Set personality (Professional, Friendly, Casual...)    │
├─────────────────────────────────────────────────────────────┤
│  STEP 2: Train Agent (Knowledge Base)                       │
│  ├── Upload documents (PDF, Word, Excel)                    │
│  ├── Crawl websites (auto-extract)                          │
│  ├── Import FAQs (CSV, structured)                          │
│  └── Free text (copy-paste)                                 │
├─────────────────────────────────────────────────────────────┤
│  STEP 3: Set Escalation Rules                               │
│  ├── Confidence threshold (>80%)                            │
│  ├── Keyword triggers ("cancel", "complaint")               │
│  ├── Intent detection (frustration, urgency)                │
│  └── Turn count (after N failed attempts)                   │
├─────────────────────────────────────────────────────────────┤
│  STEP 4: Connect Channels                                   │
│  ├── WhatsApp Business                                      │
│  ├── Instagram DM + Stories                                 │
│  ├── Web Chat Widget                                        │
│  ├── Facebook Messenger                                     │
│  └── Phone (Voice)                                          │
├─────────────────────────────────────────────────────────────┤
│  STEP 5: Launch & Monitor                                   │
│  └── One-click deploy → Live in seconds                     │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔧 NEW Tools Required

| ID | Tool Name | Purpose | Decision |
|----|-----------|---------|----------|
| TOOL-VIS-001 | detect_knowledge_gap | Identify unanswered questions | BUILD |
| TOOL-VIS-002 | execute_tool_call | AI-initiated API calls | BUILD |

---

## 💾 NEW Memory/Data Requirements

| ID | Memory Type | Description | Retention |
|----|-------------|-------------|-----------|
| MEM-VIS-001 | Knowledge Gap Log | Questions AI couldn't answer | 90 days |

---

## 🔀 NEW Workflows from Visito

| ID | Workflow | Trigger | Steps |
|----|----------|---------|-------|
| WF-VIS-001 | Back-to-Bot | Human resolution | Human resolves → Hands back → AI resumes |
| WF-VIS-002 | Knowledge Gap | Unanswered question | Log → Suggest → Add → Retrain |

---

## 📋 Knowledge Gaps from Visito

| ID | Knowledge Needed | Skills Blocked | Priority |
|----|------------------|----------------|----------|
| KG-VIS-001 | No-code builder UX | Agent Builder | MEDIUM |
| KG-VIS-002 | Knowledge gap detection algorithms | Gap Detection | MEDIUM |
| KG-VIS-003 | RAG hybrid retrieval | Retrieval | LOW |
| KG-VIS-004 | Tool calling patterns | Custom Actions | LOW |

---

## 🏆 What Visito Adds to Our Solution

**ADOPT (Critical)**:
1. **100+ Languages** - Most comprehensive (beats Inntelo's 40+)
2. **Knowledge Gap Detection** - Continuous improvement
3. **RAG Hybrid Retrieval** - Better accuracy than pure semantic

**ADOPT (Valuable)**:
1. **Back-to-Bot Handoff** - Efficient escalation pattern
2. **No-Code Templates** - Faster deployment
3. **Tool Calling** - AI-initiated API calls

**CONSIDER**:
1. **Widget Analytics** - Nice for web traffic
2. **Pre-Chat Survey** - Context collection

---

## 📊 Strategic Positioning Update (7 Competitors)

| Dimension | Visito | Inntelo | Boom | Besty | Guesty | Mews |
|-----------|--------|---------|------|-------|--------|------|
| **Type** | No-Code | Hotel AI | AiPMS | AI Layer | STR PMS | Hotel PMS |
| **Languages** | ⭐⭐⭐⭐⭐ (100+) | ⭐⭐⭐⭐ (40+) | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Setup** | ⭐⭐⭐⭐⭐ (2 min) | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **No-Code** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| **Price** | ⭐⭐⭐⭐⭐ ($49) | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **CDP** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ | ❌ | ⭐⭐⭐ | ⭐⭐⭐ |
| **Operations** | ❌ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ❌ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Target** | SMB | Hotels | STR | STR | STR | Hotels |

**Bottom Line**: Visito provides **100+ languages**, **2-minute setup**, and **knowledge gap detection** that no other competitor matches. Essential for rapid deployment and continuous improvement.

---

## 🎯 Complete Best-of-Breed Synthesis (7 Competitors)

| Feature | Best Source | Why |
|---------|-------------|-----|
| **STR Operations** | Guesty | 67 skills, comprehensive |
| **Voice AI** | Boom | 24/7 phone, BAM |
| **CDP** | Inntelo | Full stack |
| **Multi-Agent** | Inntelo | 5 specialized agents |
| **Revenue Upsells** | Besty | Psychology, 40-60% |
| **Digital Key** | Mews | Apple Wallet |
| **Languages** | **Visito** | 100+ native |
| **Setup Speed** | **Visito** | 2 minutes |
| **No-Code** | **Visito** | Full drag-and-drop |
| **Knowledge Gaps** | **Visito** | Auto-detection |
| **RAG Retrieval** | **Visito** | Hybrid semantic+keyword |

