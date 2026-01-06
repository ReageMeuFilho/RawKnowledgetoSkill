# Research Assignment: Final Production Readiness Gaps

## Your Mission

We need you to research and document **3 specific topics** to complete our production infrastructure documentation. We've already completed 87% of our infrastructure research. Your job is to close the final 13%.

**Deliverable**: A single comprehensive document (400-600 lines) covering all 3 topics below.

---

# TOPIC 1: AI Prompt Versioning & A/B Testing Framework

## Background

We're building an AI-powered property management platform with 4 AI agents:
- **Leasing Assistant**: Qualifies prospects, schedules tours
- **Maintenance Coordinator**: Triages issues, dispatches vendors  
- **Voice Agent**: Handles phone calls in real-time (<300ms latency)
- **Quote Chaser**: Sends payment reminders

We use **Claude 3.5 Sonnet** as our primary LLM (API-based, not self-hosted). Each agent has system prompts that evolve over time. We need a system to:
1. Track which prompt version was used with which model version
2. A/B test new prompts before full rollout
3. Instantly rollback if a prompt causes issues
4. Measure prompt effectiveness

## What We Need You to Research

### 1.1 Prompt Version Schema

Research how to track prompt + model combinations. We need a complete schema like:

```typescript
interface AIDeployment {
  id: string;
  agent_type: 'leasing' | 'maintenance' | 'voice' | 'quote_chaser';
  model_id: string;           // e.g., "claude-3-5-sonnet-20240620"
  prompt_version: string;     // semver like "1.2.3"
  prompt_hash: string;        // SHA-256 of prompt content
  config: { temperature, max_tokens, etc };
  traffic_allocation: number; // 0-100%
  status: 'canary' | 'stable' | 'deprecated';
  // What else is needed?
}
```

**Research questions**:
- How do LangSmith, Humanloop, Weights & Biases handle prompt versioning?
- What metadata should be logged with each LLM call for debugging/audit?
- Best practices from Anthropic/OpenAI for prompt management in production?

### 1.2 A/B Testing Framework for Prompts

**Research questions**:
- How to split traffic between prompt versions at the LLM call level?
- What tools support this? (LaunchDarkly, Statsig, LangSmith experiments?)
- Statistical significance: How many conversations needed to declare a winner?
- What metrics should we compare?
  - Task completion rate
  - Escalation rate (lower is better)
  - Response latency
  - Token usage / cost
  - Hallucination rate
- Auto-stop guardrails: Stop experiment if new version is X% worse?

### 1.3 Prompt Evaluation Suite

**Research questions**:
- How to automate prompt evaluation before deployment?
- LangSmith evaluators vs Braintrust vs custom pytest?
- What does a test case look like for property management AI?
- How many test cases per agent for adequate coverage?
- How to detect subtle regressions in tone or accuracy?

### 1.4 Rollback Procedures

**Research questions**:
- How fast can we rollback a prompt? (Target: <1 minute)
- What's the rollback scope: single agent or all agents?
- Do we preserve conversation context during rollback?

### 1.5 Model Provider Fallback

**Research questions**:
- What if Anthropic deprecates our model version?
- How to configure fallback chain (Claude → GPT-4 → Gemini)?
- How much notice does Anthropic typically give for deprecations?

## Expected Output for Topic 1

Provide:
1. Complete TypeScript interface for `AIDeployment` and `PromptVersion`
2. YAML configuration example for A/B test setup
3. Folder structure for prompt library with versioning
4. Rollback runbook with triggers and timing
5. Model fallback chain configuration

---

# TOPIC 2: Chaos Engineering Experiment Catalog

## Background

Our platform has:
- **Voice services** that can't drop calls (real-time, <300ms latency)
- **Financial transactions** via TigerBeetle (must be ACID compliant)
- **Multi-region deployment** (US East + Brazil São Paulo)
- **External dependencies**: Twilio, Deepgram (speech-to-text), ElevenLabs (text-to-speech), Claude API

We need to prove our system is resilient through structured chaos experiments.

## What We Need You to Research

### 2.1 Voice-Specific Chaos Experiments

Create detailed experiment definitions for:

**EXP-VOICE-001: Speech-to-Text Provider Failure**
- What happens when Deepgram returns 500 errors mid-call?
- Expected: Failover to backup STT (Google) within 2 seconds
- How to inject this fault?

**EXP-VOICE-002: Text-to-Speech Provider Failure**
- What happens when ElevenLabs fails mid-response?
- Expected: Failover to backup TTS or cached response
- Impact on call quality?

**EXP-VOICE-003: LLM API Timeout**
- What happens when Claude API takes >5 seconds?
- Expected: Return fallback response, don't hang the call
- How to test this safely?

**EXP-VOICE-004: WebSocket Connection Drop**
- What happens when connection to Twilio drops?
- Expected: Auto-reconnection within 3 seconds
- Session state preservation?

**EXP-VOICE-005: Network Latency Injection**
- Add 200ms latency to all external calls
- At what latency does voice quality become unacceptable?

### 2.2 Financial/Treasury Chaos Experiments

**EXP-FIN-001: Database Leader Failure**
- What happens when TigerBeetle leader node fails?
- Expected: Automatic leader election within 30 seconds
- Zero incorrect transactions during failover

**EXP-FIN-002: Network Partition Between Replicas**
- What happens during split-brain scenario?
- How does consensus protocol handle this?

### 2.3 Multi-Region Chaos Experiments

**EXP-REGION-001: Primary Region Complete Outage**
- What happens when US-East goes down?
- Expected: Brazil serves all traffic within 60 seconds
- Data consistency guarantees?

**EXP-REGION-002: Cross-Region Network Partition**
- What happens when US-East can't communicate with Brazil?
- Expected: Each region operates independently
- Reconciliation when connectivity restored?

### 2.4 Chaos Tools Research

Compare and recommend:
- **AWS Fault Injection Service (FIS)**: Capabilities for ECS/Fargate? Cost?
- **Chaos Toolkit**: Application-level chaos? Custom extensions?
- **Gremlin**: Enterprise features? Worth the cost?

### 2.5 Game Day Operations

**Research questions**:
- Pre-requisites before running chaos in production?
- Abort criteria and rollback procedures?
- How often: Weekly staging? Monthly production? Quarterly full game day?
- Post-chaos analysis template?

## Expected Output for Topic 2

Provide:
1. **10+ experiment definitions** in YAML format with:
   - Objective
   - Blast radius (scope of impact)
   - Pre-requisites
   - Execution steps
   - Expected results
   - Abort criteria
   - Success metrics

2. **AWS FIS experiment template** (JSON) for at least 2 experiments

3. **Quarterly game day schedule** covering:
   - Q2: Voice resilience
   - Q3: Financial resilience
   - Q4: Multi-region resilience
   - Q1 next year: Full system

4. **Game day checklist** with all preparation steps

---

# TOPIC 3: EU AI Act Compliance Implementation

## Background

We plan to expand to Europe (Spain, Portugal, Italy). The EU AI Act classifies AI systems by risk level, with high-risk systems having significant compliance requirements.

Our AI systems:
- **Leasing Assistant**: Makes recommendations about housing access → likely HIGH-RISK
- **Maintenance Coordinator**: Has safety implications → possibly HIGH-RISK
- **Voice Agent**: Customer service chatbot → LIMITED RISK
- **Quote Chaser**: Payment reminders → MINIMAL RISK

High-risk AI obligations apply from **August 2026**.

## What We Need You to Research

### 3.1 Risk Classification Confirmation

**Research questions**:
- Confirm risk level for each of our 4 AI systems under EU AI Act Annex III
- Does our human-in-the-loop (HITL) oversight change the classification?
- What triggers "high-risk" for housing-related AI?

### 3.2 High-Risk Requirements (Articles 9-15)

For each article, we need:
1. What the article requires
2. What we need to implement
3. Implementation checklist

**Article 9: Risk Management System**
- What constitutes a "risk management system" for AI?
- Is this a document? A process? A technical system?
- What risks must be identified?

**Article 10: Data and Data Governance**
- Data quality requirements?
- How to document our RAG knowledge base data?
- Bias detection requirements?

**Article 11: Technical Documentation**
- What must be documented?
- Template or format requirements?
- Retention period?

**Article 12: Record-Keeping**
- What AI decisions must be logged?
- Log retention period?
- Format requirements?

**Article 13: Transparency and Information**
- What must we tell users?
- Exact disclosure language for voice calls?
- Disclosure language for chat/SMS?
- Disclosure language for email?

**Article 14: Human Oversight**
- What level of human oversight is required?
- Can AI make final decisions?
- Real-time oversight vs audit-based?

**Article 15: Accuracy, Robustness, Cybersecurity**
- What accuracy metrics are required?
- How to prove "robustness"?
- Testing requirements?

### 3.3 Transparency for Limited Risk Systems

Even for our LIMITED RISK systems (Voice Agent, Quote Chaser):
- What disclosures are required?
- Exact wording for "You are interacting with AI"?
- Where must this appear?

### 3.4 Timeline and Penalties

- Exact compliance timeline?
- Penalties for non-compliance? (€35M or 7% of revenue?)
- Do we need third-party conformity assessment?

## Expected Output for Topic 3

Provide:
1. **Risk classification matrix** confirming level for all 4 AI systems with legal citations

2. **Article-by-article implementation guide** with:
   - Requirement summary
   - Implementation checklist
   - Gap analysis (what we likely have vs need)

3. **Exact disclosure wording** for:
   - Voice calls (what to say at start of call)
   - Chat/SMS messages
   - Email communications

4. **Implementation timeline** with milestones from now to August 2026

5. **Compliance checklist** we can use to track progress

---

# Output Requirements

## Format

Create a single document with:

```
# Final Production Readiness Research

## Executive Summary
[2-3 paragraphs summarizing key findings]

## 1. AI Prompt Versioning & A/B Testing
### 1.1 Version Schema
### 1.2 A/B Testing Framework
### 1.3 Evaluation Suite
### 1.4 Rollback Procedures
### 1.5 Model Fallback

## 2. Chaos Engineering Experiment Catalog
### 2.1 Voice Experiments (5 experiments)
### 2.2 Financial Experiments (2-3 experiments)
### 2.3 Regional Experiments (2 experiments)
### 2.4 Tool Recommendations
### 2.5 Game Day Schedule & Checklist

## 3. EU AI Act Compliance
### 3.1 Risk Classification Matrix
### 3.2 High-Risk Requirements (Articles 9-15)
### 3.3 Transparency Requirements
### 3.4 Implementation Timeline

## 4. References
[25+ authoritative sources]
```

## Length

400-600 lines total. Be comprehensive but concise.

## Sources

Prioritize authoritative sources:
- Official documentation (EU AI Act text, AWS FIS docs, LangSmith docs)
- Engineering blogs from major tech companies
- Legal analyses from reputable law firms
- Academic papers where relevant

Cite at least **25 sources** across all topics.

## Quality Standards

- **Actionable**: Every recommendation should be implementable
- **Specific**: Include exact configurations, not just concepts
- **Complete**: Include all schemas, templates, and checklists mentioned
- **Cited**: Every major claim should have a source

---

# Success Criteria

Your research is complete when:

- [ ] Prompt versioning has complete TypeScript interfaces
- [ ] A/B testing has YAML configuration with all parameters
- [ ] 10+ chaos experiments are fully defined
- [ ] AWS FIS templates are provided in JSON
- [ ] Game day schedule covers 4 quarters
- [ ] EU AI Act risk levels are confirmed with citations
- [ ] Articles 9-15 each have implementation checklists
- [ ] Disclosure wording is exact and ready to use
- [ ] Timeline has specific dates
- [ ] 25+ sources are cited

---

**Thank you! This research will complete our production infrastructure documentation.**

