# STANDALONE Engineering Specification Prompt
## GAP-AF-001: AI Leasing Assistant

> **For**: Engineering Agent (No repo access)
> **Task**: Create comprehensive engineering specification
> **Output**: Return the completed specification document to the user
> **Expected Length**: 3,000-5,000 lines

---

# PART 1: YOUR MISSION

You are an **Engineering Agent** tasked with creating a **complete, implementation-ready Engineering Specification** for an AI Leasing Assistant system.

You have been provided with:
1. Research findings from competitive analysis (Part 2 below)
2. Detailed specification requirements (Part 3 below)

Your job is to fill in ALL engineering details to create a document that an engineering team can implement from.

---

# PART 2: RESEARCH FOUNDATION (Stage 1 Input)

## 2.1 Executive Summary

This document provides a comprehensive analysis of AI Leasing Assistants, a critical technology for modernizing property management operations. The research focuses on best-in-class implementations, core functionalities, and the strategic impact of these systems on the multifamily housing industry.

**Key Finding**: AI Leasing Assistants have evolved from simple chatbots to sophisticated agentic AI systems that can manage the entire leasing funnel, from initial inquiry to lease signing. These systems operate 24/7, provide instant responses to prospects, and automate a significant portion of the leasing team's workload.

## 2.2 Problem Statement

The multifamily leasing process is traditionally labor-intensive, with leasing agents spending significant time on repetitive tasks:

| Problem | Impact |
|---------|--------|
| **Missed Leads** | Significant portion of renter leads go unanswered, especially after hours |
| **Slow Response Times** | Renters expect quick responses; delays lead to lost opportunities |
| **High Operational Costs** | Large leasing teams needed to handle inquiries drives up costs |
| **Inconsistent Experience** | Quality varies depending on agent and workload |
| **Lack of Data Insights** | Manual processes make optimization difficult |

## 2.3 Best-in-Class Implementations

### EliseAI
- **Technology**: Agentic AI (beyond generative AI)
- **Channels**: Voice, SMS, Email, Chat
- **Key Metric**: High-performing teams achieve ~5% handoff rate (AI handles 95% autonomously)
- **Languages**: 50+ supported
- **Key Differentiator**: AI-Guided Tours

### AppFolio Realm-X
- **Technology**: Agentic AI (Lisa AI leasing assistant)
- **Channels**: Voice, SMS, Email, Chat
- **Key Feature**: Deep integration with AppFolio ecosystem
- **Key Differentiator**: Native PMS integration

### Funnel Leasing
- **Technology**: Machine Learning & NLP
- **Key Metric**: 72% of AI-scheduled tours happen after hours
- **Key Differentiator**: Strong focus on renter-centric journey

## 2.4 Key Features Identified

### Core Features
- **Unified Inbox**: Consolidates all communications (email, SMS, chat, voice) into single thread per prospect
- **Knowledge Bank**: Centralized repository of information the AI uses to answer questions
- **Calendar Integration**: Seamless integration with leasing agents' calendars for automated tour scheduling
- **Reporting and Analytics**: Dashboards for lead volume, conversion rates, response times

### Configuration Options
- **Tour Settings**: Configure tour types (in-person, self-guided, virtual), duration, availability, concurrency
- **Lead Qualification**: Define custom screening questions and criteria
- **Handoff Rules**: Set triggers for when AI should escalate to human agent
- **Branding**: Customize AI's name, personality, communication style

## 2.5 Research Questions Answered

### Q1: How are leads qualified automatically?
- AI collects key details: move-in dates, budget, pet ownership, bedroom preferences
- Custom screening criteria can be configured per community
- Lead scoring based on qualification criteria
- High-performing teams achieve ~5% handoff rate

### Q2: What questions can AI answer vs escalate?
**AI Answers:**
- Pricing and availability
- Lease terms
- Amenities
- Tour scheduling
- Community policies

**Escalate:**
- Complex/sensitive queries
- Fair housing questions
- Explicit human requests
- Best practice: escalate after 2 failed attempts or explicit request

### Q3: How is tour scheduling integrated?
- Three tour types: in-person, self-guided, live virtual
- Calendar integration with agent availability
- Configurable: duration, start times, advance notice, concurrency
- 72% of AI-scheduled tours happen after hours (Funnel data)

### Q4: What's the 24/7 coverage model?
- Multi-channel: voice, SMS, email, web chat
- Responds within 5 minutes even during off-hours
- Emergency escalation with live call or message relay options
- Supports 50+ languages (EliseAI)

## 2.6 Sample Data Model (From Research)

```json
{
  "prospect_id": "12345",
  "full_name": "John Doe",
  "email": "john.doe@example.com",
  "phone_number": "+15551234567",
  "communication_channel": "email",
  "status": "lead",
  "source": "Apartments.com",
  "move_in_date_preference": "2026-03-01",
  "budget_preference": 2500,
  "pet_friendly_preference": true,
  "tour_scheduled": {
    "tour_id": "67890",
    "tour_type": "in-person",
    "tour_date": "2026-01-15T14:00:00Z",
    "agent_id": "agent-007"
  },
  "conversation_history": [
    {
      "timestamp": "2026-01-10T10:00:00Z",
      "sender": "prospect",
      "message": "Hi, I'm interested in a 2-bedroom apartment."
    },
    {
      "timestamp": "2026-01-10T10:00:05Z",
      "sender": "ai_assistant",
      "message": "Great! We have a few 2-bedroom apartments available. What is your desired move-in date?"
    }
  ]
}
```

## 2.7 Business Rules Identified

| Rule | Description |
|------|-------------|
| **Escalation** | AI escalates to human after 2 failed attempts or explicit request |
| **Fair Housing** | AI must provide consistent, compliant answers to fair housing questions |
| **Emergency** | Emergency maintenance requests escalated immediately |
| **Privacy** | Must comply with GDPR, CCPA |

## 2.8 Integration Requirements

| System | Purpose | Priority |
|--------|---------|----------|
| **PMS** | Real-time pricing, availability, resident info | Critical |
| **CRM** | Unified prospect/resident interactions | High |
| **Calendar** | Agent availability for tour scheduling | Critical |
| **Smart Locks** | Self-guided tour access | Medium |

## 2.9 Competitive Comparison

| Feature | EliseAI | AppFolio Realm-X | Funnel Leasing |
|---------|---------|------------------|----------------|
| Core Technology | Agentic AI | Agentic AI | ML & NLP |
| Channels | Voice, SMS, Email, Chat | Voice, SMS, Email, Chat | Voice, SMS, Email, Chat |
| Tour Scheduling | In-person, self-guided, virtual | In-person, self-guided, virtual | In-person, self-guided, virtual |
| CRM Integration | Yes | Native to AppFolio | Yes |
| Customization | High | Moderate | High |
| Key Differentiator | AI-Guided Tours | Deep ecosystem integration | Renter-centric journey |

---

# PART 3: SPECIFICATION REQUIREMENTS

You must create a complete engineering specification with ALL of the following sections. Do not skip any section. Do not use placeholders like "TBD" or "[TODO]".

---

## SECTION 1: System Architecture Overview

### 1.1 High-Level Architecture Diagram

Create an ASCII architecture diagram showing:
- AI Leasing Assistant core components
- External integrations (PMS, CRM, Calendar, ILS)
- Communication channels (Voice, SMS, Email, Chat)
- Data flows between components

### 1.2 Component Inventory

Create a table listing ALL system components:

| Component | Purpose | Technology | Interfaces |
|-----------|---------|------------|------------|
| [List every component] | | | |

### 1.3 Deployment Model

- Deployment architecture (Microservices vs Monolith)
- Cloud services used
- Scaling strategy

---

## SECTION 2: Conversation Engine

### 2.1 Conversation State Machine

Create a COMPLETE state machine showing ALL states:
- Initial contact states
- Qualification states
- Tour scheduling states
- Escalation states
- Completion states
- Error states

Format as ASCII diagram showing all transitions.

### 2.2 Intent Recognition System

Create a comprehensive intent table with AT LEAST 20 intents:

| Intent ID | Intent Name | Example Utterances (3+) | Required Slots | Next Action |
|-----------|-------------|------------------------|----------------|-------------|
| INT-001 | availability_inquiry | "Do you have 2BR?", "What's available?", "Any openings?" | bedrooms, move_date | Check inventory |
| [Continue for 20+ intents] | | | | |

### 2.3 Slot Filling Logic

For each major intent, define:
- Required slots with validation rules
- Optional slots with defaults
- Re-prompt messages when slot is missing

### 2.4 Response Templates

Provide actual response templates (not placeholders) for:
- Greetings (by channel: web, SMS, email, voice)
- Information responses
- Clarification requests
- Tour confirmations
- Escalation notices
- Error messages

---

## SECTION 3: Lead Qualification Engine

### 3.1 Qualification Criteria

| Criterion | Weight | Scoring Logic | Data Source |
|-----------|--------|---------------|-------------|
| Move-in timeline | 25% | <30 days = 100pts, 30-60 = 75pts, >60 = 50pts | User input |
| [Continue for all criteria] | | | |

### 3.2 Lead Scoring Algorithm

Provide actual pseudocode or Python implementation:

```python
def calculate_lead_score(prospect: Prospect) -> int:
    """
    Calculate lead score from 0-100.
    """
    # Provide actual implementation logic
```

### 3.3 Qualification Questions Flow

Define exact question sequence with branching logic:
1. Question 1: [Exact wording]
   - If X → Q2
   - If Y → Q3
2. [Continue...]

### 3.4 Disqualification Rules

| Rule | Trigger | Action |
|------|---------|--------|
| [Define all rules] | | |

---

## SECTION 4: Tour Scheduling System

### 4.1 Tour Types

| Tour Type | Description | Requirements | Duration | Integration Needed |
|-----------|-------------|--------------|----------|-------------------|
| In-person | Agent-guided | Agent availability | 30-60 min | Calendar |
| Self-guided | Prospect alone | Smart lock | 15-30 min | Lock API |
| Virtual | Live video | Video platform | 20-30 min | Video API |

### 4.2 Scheduling State Machine

Create complete state machine for tour scheduling flow.

### 4.3 Calendar Integration

Define:
- API endpoints needed
- Availability check format
- Booking creation format
- Conflict handling
- Timezone handling

### 4.4 Self-Guided Tour Flow

- Access code generation
- Smart lock triggering
- Instructions sent to prospect
- Tour completion tracking

---

## SECTION 5: Knowledge Bank

### 5.1 Knowledge Bank Schema

Define complete JSON schema for property knowledge:

```json
{
  "property_id": "string",
  "community_info": { /* complete schema */ },
  "unit_types": [ /* complete schema */ ],
  "faq": [ /* complete schema */ ],
  "policies": { /* complete schema */ }
}
```

### 5.2 Knowledge Retrieval

- Retrieval strategy (semantic search, keyword, hybrid)
- Embedding model recommendation
- Context window management

### 5.3 Knowledge Updates

- Update triggers
- Sync frequency
- Conflict resolution

---

## SECTION 6: Human Handoff Protocol

### 6.1 Escalation Triggers

| Trigger ID | Condition | Priority | SLA |
|------------|-----------|----------|-----|
| ESC-001 | Explicit human request | High | Immediate |
| ESC-002 | 2 failed understanding attempts | Medium | <2 min |
| [Continue for all triggers] | | | |

### 6.2 Handoff State Machine

Create complete state machine for escalation flow.

### 6.3 Context Transfer

Define exact data structure passed to human agent:
- Conversation history format
- Prospect profile format
- Qualification status
- Escalation reason

### 6.4 Fallback Behavior

When no agent available:
- Message templates
- Callback options
- Lead preservation

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

How incoming messages are routed.

### 7.3 Cross-Channel Continuity

How conversations continue across channels.

---

## SECTION 8: Voice Agent Specification

### 8.1 Voice Flow Diagram

Complete call flow from incoming call to resolution.

### 8.2 Speech Recognition

- ASR recommendation
- Intent extraction from speech
- Noise handling
- Expected accuracy

### 8.3 Text-to-Speech

- TTS engine recommendation
- Voice options
- Prosody control

### 8.4 Voice-Specific Intents

| Intent | Voice Examples | Response Type |
|--------|---------------|---------------|
| REPEAT | "Say that again" | Repeat last |
| SLOWER | "Speak slower" | Adjust rate |
| [Continue...] | | |

### 8.5 DTMF Handling

Menu options via keypad.

---

## SECTION 9: Complete Data Model

### 9.1 Core Entity Schemas

Define TypeScript interfaces for ALL entities:

```typescript
interface Prospect {
  id: string;
  // ALL fields with types, descriptions, constraints
}

interface Conversation {
  // ALL fields
}

interface Tour {
  // ALL fields
}

interface LeadScore {
  // ALL fields
}

interface Message {
  // ALL fields
}

interface Agent {
  // ALL fields
}
```

### 9.2 Entity Relationships

Create ER diagram (ASCII) showing all relationships.

### 9.3 Database Design

- Database recommendation
- Index strategy
- Partitioning strategy

---

## SECTION 10: API Specification

### 10.1 External APIs Consumed

| API | Purpose | Auth Method | Rate Limits |
|-----|---------|-------------|-------------|
| PMS API | Inventory, pricing | API Key | 1000/min |
| [Continue...] | | | |

### 10.2 APIs Exposed

Define REST endpoints with full schemas:

**POST /api/v1/conversations**
```json
// Request schema
// Response schema
// Error codes
```

**POST /api/v1/conversations/{id}/messages**
```json
// Request schema
// Response schema
// Error codes
```

[Continue for ALL endpoints]

### 10.3 Webhook Events

| Event | Trigger | Payload Schema |
|-------|---------|----------------|
| conversation.started | New contact | { /* schema */ } |
| tour.scheduled | Tour booked | { /* schema */ } |
| [Continue...] | | |

---

## SECTION 11: Security & Compliance

### 11.1 Authentication

- Prospect identification
- Agent authentication
- Session management

### 11.2 Authorization (RBAC)

| Role | Permissions |
|------|-------------|
| Prospect | Send messages, schedule tours |
| Agent | View conversations, override AI |
| Admin | Configure knowledge, manage settings |

### 11.3 Fair Housing Compliance

- Flagged questions
- Consistent treatment rules
- Audit trail requirements

### 11.4 Data Privacy

- PII collected
- Retention policy
- Deletion handling

---

## SECTION 12: Performance & Observability

### 12.1 Performance Requirements

| Metric | Target | Measurement |
|--------|--------|-------------|
| Response latency (chat) | <2 sec | P95 |
| Response latency (voice) | <500ms | P95 |
| Availability | 99.9% | Monthly |

### 12.2 Metrics to Capture

| Metric | Description | Alert Threshold |
|--------|-------------|-----------------|
| intent_recognition_accuracy | % correct intents | <85% |
| escalation_rate | % escalated | >15% |
| [Continue...] | | |

### 12.3 Logging Strategy

What, format, retention.

### 12.4 Alerting Rules

System health, business metrics, security events.

---

## SECTION 13: Error Handling

### 13.1 Error Categories

| Category | Examples | User Message | Recovery |
|----------|----------|--------------|----------|
| Understanding | Can't parse intent | "I didn't catch that..." | Retry |
| System | PMS unavailable | "Let me check..." | Queue |
| [Continue...] | | | |

### 13.2 Fallback Behaviors

For each error type:
- Message shown
- Recovery attempted
- When to escalate
- Logging

### 13.3 Circuit Breaker Pattern

Configuration for external dependencies.

---

## SECTION 14: Testing Strategy

### 14.1 Unit Tests

Components needing unit tests.

### 14.2 Integration Tests

| Scenario | Steps | Expected Outcome |
|----------|-------|------------------|
| Happy path tour | Prospect inquires → schedules → confirms | Tour created |
| [Continue for 10+ scenarios] | | |

### 14.3 Conversation Tests

Define 10+ test conversations:
```
User: "Hi, do you have any 2 bedrooms available?"
Expected Intent: availability_inquiry
Expected Slots: {bedrooms: 2}
AI Response: "[Checks inventory] Yes, we have X 2-bedroom units..."
```

---

## SECTION 15: User Stories & Acceptance Criteria

### 15.1 Prospect Stories (10+ required)

**US-001: As a prospect, I want to ask about availability**
- Given: I'm on the website chat
- When: I ask "Do you have 2BR apartments?"
- Then: AI responds with available 2BR units and pricing
- Acceptance: Response includes unit count, price range, availability

**US-002: As a prospect, I want to schedule a tour**
[Continue for 10+ prospect stories]

### 15.2 Agent Stories (5+ required)

**US-020: As a leasing agent, I want to see conversation context**
[Continue for 5+ agent stories]

### 15.3 Admin Stories (3+ required)

**US-030: As an admin, I want to configure the knowledge bank**
[Continue...]

---

## SECTION 16: Implementation Phases

### 16.1 MVP Scope (Phase 0)

| Feature | Included | Effort | Rationale |
|---------|----------|--------|-----------|
| Web chat | ✅ | 3 weeks | Primary channel |
| Basic FAQ | ✅ | 2 weeks | Core functionality |
| Tour scheduling | ✅ | 3 weeks | High value |
| Lead qualification | ✅ | 2 weeks | Core functionality |
| Voice agent | ❌ | - | Phase 1 |

### 16.2 Phase 1 Scope

| Feature | Effort | Dependencies |
|---------|--------|--------------|
| SMS channel | 2 weeks | Twilio |
| Email channel | 1 week | SendGrid |
| Voice agent | 4 weeks | ASR/TTS |

### 16.3 Phase 2 Scope

| Feature | Effort | Dependencies |
|---------|--------|--------------|
| Self-guided tours | 3 weeks | Smart lock integration |
| AI-guided video tours | 4 weeks | Video platform |
| Multi-language | 3 weeks | Translation service |

---

## SECTION 17: Open Questions

Document questions needing product/business decisions:

| ID | Question | Impact | Suggested Answer |
|----|----------|--------|------------------|
| OQ-001 | Should AI disclose it's an AI? | UX, Trust | Yes, upfront |
| OQ-002 | Max conversation length before escalation? | Cost, UX | 20 exchanges |
| [Continue...] | | | |

---

# PART 4: OUTPUT REQUIREMENTS

## Format
- Markdown document
- All diagrams in ASCII or mermaid syntax
- All code in syntax-highlighted blocks
- All tables properly formatted

## Length
- Expected: 3,000-5,000 lines
- Every section must have substantive content
- No placeholders or "TBD" entries

## Quality Checklist

Before submitting, verify:

- [ ] All 17 sections completed with full detail
- [ ] State machines include ALL states and transitions
- [ ] At least 20 intents defined with examples
- [ ] At least 15 user stories with acceptance criteria
- [ ] All API endpoints have request/response schemas
- [ ] All error cases have recovery strategies
- [ ] Implementation phases clearly defined with effort estimates
- [ ] Open questions documented

---

# PART 5: DOCUMENT HEADER

Start your output with this header:

```markdown
# Engineering Specification: AI Leasing Assistant

> **Skill ID**: SKILL-253
> **Gap ID**: GAP-AF-001
> **Version**: 1.0
> **Created**: [Date]
> **Author**: Engineering Agent
> **Status**: Draft

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [Date] | Engineering Agent | Initial specification |

---
```

---

# DELIVERABLE

Return the complete engineering specification document to the user. They will save it to the repository and continue the pipeline.

**Expected Output**: A single markdown document, 3,000-5,000 lines, covering all 17 sections with implementation-ready detail.

