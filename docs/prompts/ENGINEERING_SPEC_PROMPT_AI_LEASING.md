# Engineering Specification Prompt: AI Leasing Assistant

> **Gap ID**: GAP-AF-001
> **Skill ID**: SKILL-253
> **Stage**: 2 → 3 (Research → Engineering Spec)
> **Input Document**: `knowledge/communication/KD-AF-001-ai-leasing-assistant.md`
> **Created**: January 2026
> **Quality Score of Input**: 7.5/10 - Good foundation, needs engineering depth

---

## 🎯 YOUR MISSION

You are an **Engineering Agent** tasked with transforming the Stage 1 Knowledge Document into a **complete, implementation-ready Engineering Specification**.

The research document provides good conceptual understanding but lacks the technical depth needed for implementation. Your job is to fill in ALL engineering details.

---

## 📋 REQUIRED OUTPUT SECTIONS

Your specification MUST include ALL of the following sections with complete detail. Do not skip any section. Do not use placeholders.

---

## SECTION 1: System Architecture Overview

### 1.1 High-Level Architecture Diagram

Create an ASCII architecture diagram showing:
- AI Leasing Assistant core components
- External integrations (PMS, CRM, Calendar, ILS)
- Communication channels (Voice, SMS, Email, Chat)
- Data flows between components

### 1.2 Component Inventory

| Component | Purpose | Technology | Interfaces |
|-----------|---------|------------|------------|
| [List ALL components] | | | |

### 1.3 Deployment Model

- How is this deployed? (Microservices? Monolith?)
- What cloud services are used?
- How does it scale?

---

## SECTION 2: Conversation Engine

### 2.1 Conversation State Machine

Create a COMPLETE state machine diagram (ASCII or mermaid) showing:

```
[START] → [GREETING] → [INTENT_DETECTION] → [...]
```

Include ALL states:
- Initial contact states
- Qualification states
- Tour scheduling states
- Escalation states
- Completion states
- Error states

### 2.2 Intent Recognition System

| Intent ID | Intent Name | Example Utterances | Required Slots | Next Action |
|-----------|-------------|-------------------|----------------|-------------|
| INT-001 | availability_inquiry | "Do you have 2BR available?" | bedrooms, move_date | Check inventory |
| INT-002 | pricing_inquiry | "How much is rent?" | unit_type | Provide pricing |
| INT-003 | tour_request | "Can I schedule a tour?" | date_preference | Start tour flow |
| [Continue for ALL intents...] | | | | |

**REQUIRED**: List at least 20 intents with full detail.

### 2.3 Slot Filling Logic

For each intent, define:
- Required slots
- Optional slots
- Validation rules
- Default values
- Re-prompt messages when slot is missing

### 2.4 Response Generation

Define response templates for:
- Greeting messages (by channel)
- Information responses
- Clarification requests
- Tour confirmations
- Escalation notices
- Error messages

Include actual example responses (not placeholders).

---

## SECTION 3: Lead Qualification Engine

### 3.1 Qualification Criteria

| Criterion | Weight | Scoring Logic | Data Source |
|-----------|--------|---------------|-------------|
| Move-in timeline | 25% | <30 days = 100pts, 30-60 = 75pts, >60 = 50pts | User input |
| Budget match | 30% | Within range = 100pts, ±10% = 75pts | User input |
| [Continue...] | | | |

### 3.2 Lead Scoring Algorithm

```python
# Provide actual pseudocode or Python for the scoring algorithm
def calculate_lead_score(prospect: Prospect) -> int:
    """
    Calculate lead score from 0-100 based on qualification criteria.
    
    Args:
        prospect: Prospect object with qualification data
        
    Returns:
        Integer score from 0-100
    """
    # Your implementation here with actual logic
```

### 3.3 Qualification Questions Flow

Define the exact question sequence:
1. Question 1: [Exact wording]
   - If answer X → Go to Q2
   - If answer Y → Go to Q3
2. Question 2: [Exact wording]
   - ...

### 3.4 Disqualification Rules

| Rule | Trigger | Action |
|------|---------|--------|
| Budget mismatch | Budget < min_rent - 20% | Soft disqualify, suggest alternatives |
| [Continue...] | | |

---

## SECTION 4: Tour Scheduling System

### 4.1 Tour Types

| Tour Type | Description | Requirements | Duration |
|-----------|-------------|--------------|----------|
| In-person | Agent-guided tour | Agent availability | 30-60 min |
| Self-guided | Prospect uses smart lock | Smart lock integration | 15-30 min |
| Virtual | Live video tour | Video platform | 20-30 min |

### 4.2 Scheduling State Machine

```
[TOUR_INTENT_DETECTED]
    ↓
[ASK_TOUR_TYPE]
    ↓
[CHECK_AVAILABILITY]
    ↓ (slots available)
[PRESENT_OPTIONS] ← (slots unavailable) → [OFFER_ALTERNATIVES]
    ↓
[CONFIRM_SELECTION]
    ↓
[COLLECT_CONTACT_INFO]
    ↓
[CREATE_BOOKING]
    ↓
[SEND_CONFIRMATION]
    ↓
[COMPLETE]
```

### 4.3 Calendar Integration

Define the calendar integration:
- API endpoints needed
- Data format for availability check
- Data format for booking creation
- Handling conflicts
- Timezone handling

### 4.4 Self-Guided Tour Flow

For self-guided tours specifically:
- How is access code generated?
- How is smart lock triggered?
- What instructions are sent?
- How is tour completion tracked?

---

## SECTION 5: Knowledge Bank

### 5.1 Knowledge Bank Schema

```json
{
  "property_id": "string",
  "community_info": {
    "name": "string",
    "address": {},
    "description": "string",
    "amenities": [],
    "pet_policy": {},
    "parking": {},
    "utilities": {}
  },
  "unit_types": [
    {
      "type_id": "string",
      "bedrooms": "number",
      "bathrooms": "number",
      "sqft_range": {},
      "price_range": {},
      "features": [],
      "availability": []
    }
  ],
  "faq": [
    {
      "question": "string",
      "answer": "string",
      "category": "string",
      "keywords": []
    }
  ],
  "office_hours": {},
  "contact_info": {},
  "policies": {}
}
```

### 5.2 Knowledge Retrieval

- How does the AI retrieve relevant knowledge?
- What embedding model is used?
- What is the retrieval strategy (semantic search, keyword, hybrid)?
- How is context window managed?

### 5.3 Knowledge Updates

- How is knowledge kept current?
- What triggers a knowledge update?
- How are conflicts resolved?

---

## SECTION 6: Human Handoff Protocol

### 6.1 Escalation Triggers

| Trigger ID | Condition | Priority | SLA |
|------------|-----------|----------|-----|
| ESC-001 | Explicit human request | High | Immediate |
| ESC-002 | 2 failed understanding attempts | Medium | <2 min |
| ESC-003 | Fair housing question detected | High | Immediate |
| ESC-004 | Emergency maintenance (resident) | Critical | Immediate |
| ESC-005 | Pricing negotiation request | Medium | <5 min |
| [Continue...] | | | |

### 6.2 Handoff State Machine

```
[ESCALATION_TRIGGERED]
    ↓
[CHECK_AGENT_AVAILABILITY]
    ↓ (agent available)
[TRANSFER_TO_AGENT] ← (no agent) → [QUEUE_CALLBACK]
    ↓                                    ↓
[PROVIDE_CONTEXT]                   [CONFIRM_CALLBACK]
    ↓                                    ↓
[AGENT_TAKES_OVER]               [SCHEDULE_FOLLOWUP]
```

### 6.3 Context Transfer

What information is passed to the human agent:
- Conversation history
- Prospect profile
- Qualification status
- Questions asked
- Reason for escalation

Define the exact data structure.

### 6.4 Fallback Behavior

If no agent is available:
- What message is sent?
- What callback options are offered?
- How is the lead preserved?

---

## SECTION 7: Multi-Channel Communication

### 7.1 Channel-Specific Behavior

| Channel | Greeting Style | Message Length | Media Support | Response SLA |
|---------|---------------|----------------|---------------|--------------|
| Web Chat | Conversational | Short | Images, links | <5 sec |
| SMS | Brief | <160 chars | None | <30 sec |
| Email | Formal | Full | Attachments | <5 min |
| Voice | Natural | N/A | N/A | Real-time |

### 7.2 Channel Detection & Routing

- How is incoming channel detected?
- How are conversations routed?
- How is channel preference stored?

### 7.3 Cross-Channel Continuity

- How does conversation continue across channels?
- How is context preserved?
- How is prospect identity unified?

---

## SECTION 8: Voice Agent Specification

### 8.1 Voice Flow Diagram

Create a complete call flow:
```
[INCOMING_CALL]
    ↓
[GREETING] → "Thank you for calling [Property]. How can I help you today?"
    ↓
[INTENT_RECOGNITION]
    ↓
[BRANCH BY INTENT]
    ↓
...
```

### 8.2 Speech Recognition

- What ASR (Automatic Speech Recognition) is used?
- How are intents extracted from speech?
- How is noise handled?
- What is the expected accuracy?

### 8.3 Text-to-Speech

- What TTS engine is used?
- What voice options are available?
- How is prosody controlled?

### 8.4 Voice-Specific Intents

| Intent | Voice Command Examples | Response Type |
|--------|----------------------|---------------|
| REPEAT | "Can you say that again?" | Repeat last |
| SLOWER | "Speak slower please" | Adjust rate |
| TRANSFER | "Let me talk to someone" | Escalate |
| [Continue...] | | |

### 8.5 DTMF Handling

- What menu options are available via keypad?
- How is DTMF input processed?

---

## SECTION 9: Data Model (Complete)

### 9.1 Core Entities

Define complete schemas for:

**Prospect**
```typescript
interface Prospect {
  id: string;
  // Define ALL fields with types
}
```

**Conversation**
```typescript
interface Conversation {
  id: string;
  // Define ALL fields
}
```

**Tour**
```typescript
interface Tour {
  id: string;
  // Define ALL fields
}
```

**LeadScore**
```typescript
interface LeadScore {
  // Define ALL fields
}
```

### 9.2 Entity Relationships

Create an ER diagram (ASCII) showing all relationships.

### 9.3 Database Design

- What database(s) are used?
- What indexes are needed?
- What is the partitioning strategy?

---

## SECTION 10: API Specification

### 10.1 External APIs Consumed

| API | Purpose | Auth Method | Rate Limits |
|-----|---------|-------------|-------------|
| PMS API | Inventory, pricing | API Key | 1000/min |
| Calendar API | Availability | OAuth 2.0 | 100/min |
| [Continue...] | | | |

### 10.2 APIs Exposed

Define REST endpoints:

**POST /api/v1/conversations**
- Purpose: Start new conversation
- Request body schema
- Response schema
- Error codes

**POST /api/v1/conversations/{id}/messages**
- Purpose: Send message in conversation
- Request body schema
- Response schema
- Error codes

[Continue for ALL endpoints...]

### 10.3 Webhook Events

| Event | Trigger | Payload |
|-------|---------|---------|
| conversation.started | New prospect contact | { prospect, channel, timestamp } |
| tour.scheduled | Tour booked | { tour, prospect } |
| escalation.requested | Human handoff | { conversation, reason } |
| [Continue...] | | |

---

## SECTION 11: Security & Compliance

### 11.1 Authentication

- How are prospects identified?
- How are agents authenticated?
- What session management is used?

### 11.2 Authorization

Define RBAC roles and permissions:

| Role | Permissions |
|------|-------------|
| Prospect | Send messages, schedule tours |
| Agent | View all conversations, override AI |
| Admin | Configure knowledge, manage settings |

### 11.3 Fair Housing Compliance

- What questions are flagged?
- How is consistent treatment ensured?
- What audit trail is maintained?

### 11.4 Data Privacy

- What PII is collected?
- How long is data retained?
- How are deletion requests handled?

---

## SECTION 12: Performance & Observability

### 12.1 Performance Requirements

| Metric | Target | Measurement |
|--------|--------|-------------|
| Response latency (chat) | <2 sec | P95 |
| Response latency (voice) | <500ms | P95 |
| Availability | 99.9% | Monthly |
| Concurrent conversations | 10,000 | Per property |

### 12.2 Metrics to Capture

| Metric | Description | Alert Threshold |
|--------|-------------|-----------------|
| intent_recognition_accuracy | % of correctly identified intents | <85% |
| escalation_rate | % of conversations escalated | >15% |
| tour_conversion_rate | % of conversations resulting in tour | <10% |
| [Continue...] | | |

### 12.3 Logging Strategy

- What is logged?
- What format?
- What retention?

### 12.4 Alerting Rules

Define alerts for:
- System health
- Business metrics
- Security events

---

## SECTION 13: Error Handling

### 13.1 Error Categories

| Category | Examples | User Message | Recovery |
|----------|----------|--------------|----------|
| Understanding | Can't parse intent | "I didn't quite catch that..." | Retry |
| System | PMS unavailable | "Let me check on that..." | Queue |
| [Continue...] | | | |

### 13.2 Fallback Behaviors

For each error type, define:
- What message is shown
- What recovery is attempted
- When to escalate
- How to log

### 13.3 Circuit Breaker Pattern

Define circuit breaker configuration for external dependencies.

---

## SECTION 14: Testing Strategy

### 14.1 Unit Tests

What components need unit tests?

### 14.2 Integration Tests

Define integration test scenarios:
1. Happy path: Prospect inquires → schedules tour → confirms
2. Escalation path: Prospect requests human → transfer
3. [Continue...]

### 14.3 Conversation Tests

Define test conversations:
```
User: "Hi, do you have any 2 bedrooms available?"
Expected: [Intent: availability_inquiry, Slots: {bedrooms: 2}]
AI: "[Checks inventory] Yes, we have [X] 2-bedroom units available..."
```

---

## SECTION 15: User Stories & Acceptance Criteria

### 15.1 Prospect Stories

**US-001: As a prospect, I want to ask about availability**
- Given: I'm on the website chat
- When: I ask "Do you have 2BR apartments?"
- Then: AI responds with available 2BR units and pricing

**US-002: As a prospect, I want to schedule a tour**
- Given: I'm interested in a unit
- When: I ask "Can I schedule a tour?"
- Then: AI presents available time slots
- And: AI confirms my booking
- And: I receive a confirmation message

[Continue for at least 15 user stories...]

### 15.2 Agent Stories

**US-020: As a leasing agent, I want to see conversation context**
- Given: A conversation is escalated to me
- When: I open the conversation
- Then: I see full conversation history
- And: I see prospect qualification status
- And: I see reason for escalation

[Continue...]

---

## SECTION 16: Implementation Phases

### 16.1 MVP Scope

| Feature | Included | Rationale |
|---------|----------|-----------|
| Web chat | ✅ | Primary channel |
| Basic FAQ answering | ✅ | Core functionality |
| Tour scheduling | ✅ | High value |
| Lead qualification | ✅ | Core functionality |
| Voice agent | ❌ | Phase 2 |
| Self-guided tours | ❌ | Phase 2 |

### 16.2 Phase 1 Additions

| Feature | Effort | Dependencies |
|---------|--------|--------------|
| SMS channel | 2 weeks | Twilio integration |
| Email channel | 1 week | SendGrid integration |
| Voice agent | 4 weeks | ASR/TTS selection |

### 16.3 Phase 2 Additions

| Feature | Effort | Dependencies |
|---------|--------|--------------|
| Self-guided tours | 3 weeks | Smart lock integration |
| AI-guided video tours | 4 weeks | Video platform |
| Multi-language | 3 weeks | Translation service |

---

## SECTION 17: Open Questions

Document any questions that need product/business decisions:

| ID | Question | Impact | Suggested Answer |
|----|----------|--------|------------------|
| OQ-001 | Should AI disclose it's an AI? | UX, Trust | Yes, upfront |
| OQ-002 | What's the max conversation length before escalation? | Cost, UX | 20 exchanges |
| [Continue...] | | | |

---

## 📤 OUTPUT REQUIREMENTS

### Format
- Markdown document
- All diagrams in ASCII or mermaid syntax
- All code in appropriate syntax-highlighted blocks
- All tables properly formatted

### Length
- Expected: 3,000-5,000 lines
- Every section must have substantive content
- No placeholders or "TBD" entries

### Quality Criteria
- Every intent defined with examples
- Every state machine complete with all transitions
- Every API endpoint with full schema
- Every error case with recovery strategy
- Every user story with acceptance criteria

### Save Location
```
knowledge/communication/ES-AF-001-ai-leasing-assistant.md
```

---

## 📚 REFERENCE MATERIALS

### Input Document
- `knowledge/communication/KD-AF-001-ai-leasing-assistant.md`

### Related Specifications
- `specs/ai-workforce/SPEC-SKILL-261-268.md` (Agent architecture patterns)

### Industry References
- EliseAI documentation (cited in KD)
- AppFolio Realm-X documentation
- Funnel Leasing documentation

---

## ✅ COMPLETION CHECKLIST

Before submitting, verify:

- [ ] All 17 sections completed with full detail
- [ ] State machines include ALL states and transitions
- [ ] At least 20 intents defined with examples
- [ ] At least 15 user stories with acceptance criteria
- [ ] All API endpoints have request/response schemas
- [ ] All error cases have recovery strategies
- [ ] Implementation phases clearly defined
- [ ] Open questions documented

---

## AFTER COMPLETING

1. Save to: `knowledge/communication/ES-AF-001-ai-leasing-assistant.md`
2. Update `STATUS.md` - Mark Stage 3 complete for GAP-AF-001
3. Update `docs/PIPELINE_TRACKER.md`
4. Commit: `git add -A && git commit -m "Stage 3 COMPLETE: GAP-AF-001 AI Leasing Assistant Engineering Spec"`
5. Push: `git push`

