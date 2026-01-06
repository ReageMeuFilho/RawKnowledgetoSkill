# Research Prompt: Production Readiness Round 2 - Closing Infrastructure Gaps

## 🎯 MISSION CRITICAL RESEARCH ASSIGNMENT

**Gap ID**: INFRA-ROUND2  
**Gap Name**: Production Readiness - Remaining Infrastructure & Compliance Gaps  
**Priority**: P0/P1 (Blocks Production Deployment)  
**Total Items**: 14 specific gaps to close  
**Prerequisite**: Review `KD-OPEN-ITEMS-infrastructure-compliance-V4.md` first  

---

## 📋 CONTEXT: What V4 Already Established

**DO NOT RE-RESEARCH THESE - They are decided:**

| Decision | V4 Resolution | Reference |
|----------|---------------|-----------|
| Cloud Provider | **AWS** (primary), Latitude.sh (Brazil GPUs) | V4 §2.1 |
| Container Orchestration | **ECS/Fargate** (not EKS) | V4 §2.2 |
| Brazil Strategy | São Paulo deployment, SPSAV compliance, PIX-native | V4 §4, §9 |
| Voice AI Latency | **<300ms** via WebRTC, Groq LPU, edge GPUs | V4 §5 |
| LLM | **Claude 3.5 Sonnet** (general), **Groq/Llama** (voice) | V4 §5.5 |
| Database | **MongoDB Atlas** (docs), **TigerBeetle** (ledger) | V4 §3 |
| Workflow | **Temporal Cloud** | V4 §3.5 |
| Security | **Zero Trust** (Teleport), **MPC** (Fireblocks) | V4 §10, §12 |
| Data Retention | Full matrix with TTLs defined | V4 §7 |
| CRM Integrations | AppFolio, Yardi, Salesforce prioritized | V4 §8 |

**Your job is to fill the gaps V4 didn't cover in depth.**

---

## 📚 RESEARCH SECTIONS

---

# SECTION 1: State CAM/HOA Regulations (CRITICAL - P0)

**Gap**: V4 §8 mentions compliance but does NOT cover state-specific Community Association Manager (CAM) and HOA regulations that affect our AI agents.

## Context

Our AI agents will:
- Manage HOA/Condo associations in multiple US states
- Make recommendations about maintenance, violations, and architectural reviews
- Process and respond to owner/resident communications
- Potentially trigger inspections or vendor dispatch

Different states have **different licensing requirements** for property managers and **specific regulations** about what AI systems can/cannot do.

## Research Questions

### 1.1 California Regulations

**SB-721 (Balcony Inspections)**:
- What are the inspection requirements for elevated exterior elements?
- What triggers mandatory inspection? (Age of building? Occupancy type?)
- Can AI systems schedule or track these inspections?
- What liability does the PM company have if AI fails to flag a required inspection?
- Deadline enforcement and penalties?

**SB-326 (HOA Balcony Inspections)**:
- How does this differ from SB-721?
- What additional requirements exist for HOA-managed properties?
- Visual inspection vs. load-bearing inspection requirements?
- Professional qualifications required for inspectors?
- AI role: Can AI pre-screen for visual indicators via photos?

**California Civil Code 4041** (HOA communication requirements):
- Required response times for owner communications?
- Can AI respond on behalf of the association?
- What must be disclosed about AI use in communications?
- Document retention requirements for HOA communications?

**Research Sources**:
- [ ] California Department of Real Estate (DRE) regulations
- [ ] CAI (Community Associations Institute) California chapter
- [ ] SB-721 and SB-326 full legislative text
- [ ] California HOA attorney blogs (Davis-Stirling.com)
- [ ] Recent enforcement actions or case law

### 1.2 Florida Regulations

**HB-919 / SB-4D (Condo Safety - Post-Surfside)**:
- What structural inspections are now mandatory?
- Milestone inspection requirements (30-year buildings)?
- Structural Integrity Reserve Study (SIRS) requirements?
- Reserve funding requirements?
- Can AI systems help track compliance deadlines?
- What happens if AI fails to alert board about upcoming deadlines?

**Florida Statute 718 (Condominium Act)**:
- Board meeting notice requirements?
- Can AI send official notices on behalf of the board?
- Proxy and voting requirements - can AI facilitate?
- Budget disclosure requirements?

**Florida CAM Licensing (Chapter 468)**:
- What activities require a CAM license?
- Can unlicensed AI systems perform CAM functions?
- What human oversight is required for AI in CAM activities?
- Penalties for unlicensed practice?

**Research Sources**:
- [ ] Florida DBPR (Department of Business and Professional Regulation)
- [ ] Florida Statutes 718, 719, 720
- [ ] HB-919/SB-4D full text and DBPR guidance
- [ ] Florida CAI chapter publications
- [ ] Becker & Poliakoff (FL HOA law firm) resources

### 1.3 Texas Regulations

**Texas Property Code Chapter 209 (HOA)**:
- Notice requirements for rule enforcement?
- Can AI issue violation notices?
- Hearing requirements - can AI participate?
- Assessment collection rules?

**Texas Property Code Chapter 82 (Condo)**:
- How does this differ from Chapter 209?
- Management company requirements?

**Texas Occupations Code (Property Management)**:
- Licensing requirements for PM companies?
- What activities are exempt from licensing?
- Where does AI fit in the licensing framework?

**Research Sources**:
- [ ] Texas Real Estate Commission
- [ ] Texas Property Code Chapters 82, 209
- [ ] Texas HOA Management Company resources
- [ ] Recent Texas HOA legislation (2023-2025)

### 1.4 Other Key States

Provide brief summaries for:
- **New York**: HOA disclosure requirements, rent stabilization impact
- **Arizona**: Common-Interest Community regulations
- **Nevada**: NRS 116 requirements
- **Colorado**: CCIOA requirements

### 1.5 AI-Specific Requirements

For each state researched, answer:
1. **Disclosure**: Must we disclose AI use to residents/owners?
2. **Licensing**: Does AI use trigger any licensing requirements?
3. **Liability**: Who is liable for AI errors (PM company, HOA board, software vendor)?
4. **Records**: What records of AI decisions must be kept?
5. **Prohibited Actions**: What can AI NOT do (e.g., legal advice, discrimination)?

## Output Format Required

```markdown
## State CAM/HOA Regulations Matrix

### California
#### SB-721 Compliance
| Requirement | Description | AI Role | Implementation |
|-------------|-------------|---------|----------------|
| Inspection Trigger | Buildings 3+ stories, 3+ units | Track building age | Automated alerts at 5yr mark |
| ... | ... | ... | ... |

#### SB-326 Compliance
[Same format]

#### AI Disclosure Requirements
[Specific requirements]

### Florida
[Same structure]

### Texas
[Same structure]

### AI Compliance Checklist by State
| State | Disclosure Required | Licensing Impact | Record Retention | Prohibited Actions |
|-------|---------------------|------------------|------------------|-------------------|
| CA | Yes (specify) | None | 7 years | Legal advice |
| FL | ... | ... | ... | ... |
| TX | ... | ... | ... | ... |
```

---

# SECTION 2: SOC 2 Type II Certification Path (CRITICAL - P0)

**Gap**: V4 mentions SOC 2 compliance but does NOT provide the detailed controls mapping and certification path needed for enterprise customers.

## Context

- We will need SOC 2 Type II for **enterprise property management customers**
- Our system handles **financial data** (payments), **PII** (tenant info), and **AI decisions** (audit trail)
- We have **Treasury OS** (TigerBeetle + Formance) with built-in audit trails
- We use **AWS** (primary cloud) with **Teleport** (Zero Trust access)
- Timeline: Need certification within **12-18 months** of production launch

## Research Questions

### 2.1 Trust Services Criteria Mapping

For each TSC category, identify specific requirements:

**Security (Common Criteria - CC)**:
- CC6.1: Logical and physical access controls
- CC6.2: Prior to issuing access credentials
- CC6.3: Removal of access credentials
- CC6.6: Encryption in transit
- CC6.7: Data classification
- CC7.1: Detection of changes
- CC7.2: Monitoring of system components

**Questions**:
- Which CC criteria apply to our AI agents?
- How does Teleport satisfy access control requirements?
- How do we document AI decision-making for auditors?
- What additional controls needed beyond V4 architecture?

**Availability (A)**:
- A1.1: Capacity management
- A1.2: Recovery from disruptions

**Questions**:
- How do our RPO/RTO targets (V4 §11) align with A1.2?
- What availability documentation is needed?

**Processing Integrity (PI)**:
- PI1.1: Data processing objectives defined
- PI1.2: System inputs complete and accurate
- PI1.3: Processing is complete, valid, accurate
- PI1.5: Outputs are complete and accurate

**Questions**:
- How do we prove AI outputs are "accurate"?
- What testing/validation satisfies PI1.3 for AI systems?
- How do HITL decisions factor into processing integrity?

**Confidentiality (C)**:
- C1.1: Identification of confidential information
- C1.2: Destruction of confidential information

**Questions**:
- How does our data retention policy (V4 §7) satisfy C1.2?
- What additional classification scheme needed?

**Privacy (if applicable)**:
- P1-P8: Privacy criteria

**Questions**:
- Do we need the Privacy criteria for SOC 2?
- How does LGPD/GDPR compliance map to Privacy criteria?

### 2.2 Evidence Collection Requirements

What evidence do auditors need?

| Control Area | Evidence Type | Collection Method | Frequency |
|--------------|---------------|-------------------|-----------|
| Access Control | Access logs | Teleport export | Continuous |
| Change Management | Git commits + PRs | GitHub API | Continuous |
| Incident Response | Incident tickets | Jira/Linear export | Per incident |
| ... | ... | ... | ... |

### 2.3 AI-Specific Audit Requirements

**Questions**:
- How do auditors evaluate AI systems for SOC 2?
- What documentation is required for AI decision-making?
- How do we demonstrate AI "accuracy" to auditors?
- What HITL controls satisfy auditor requirements?
- Are there SOC 2 + AI-specific frameworks emerging?

### 2.4 Timeline and Cost

**Questions**:
- Typical timeline: Readiness assessment → Type I → Type II?
- Cost range for companies our size?
- Top SOC 2 auditors for fintech/AI companies?
- Can we start with Type I and upgrade?
- What's the minimum viable SOC 2 scope (which systems)?

### 2.5 Complementary Certifications

**Questions**:
- Should we pursue ISO 27001 alongside?
- PCI-DSS Level requirements for our payment volume?
- HIPAA considerations (health-related maintenance data)?
- Any property management-specific certifications?

## Research Sources

- [ ] AICPA SOC 2 Guide (official)
- [ ] SOC 2 for SaaS companies guides
- [ ] Drata, Vanta, Secureframe documentation
- [ ] SOC 2 for AI systems research papers
- [ ] Big 4 accounting firm SOC 2 guides
- [ ] Fintech SOC 2 case studies

## Output Format Required

```markdown
## SOC 2 Type II Certification Path

### Trust Services Criteria Mapping
| TSC | Criteria | V4 Control | Gap | Remediation |
|-----|----------|------------|-----|-------------|
| CC6.1 | Access control | Teleport | None | - |
| CC6.6 | Encryption | TLS 1.3, AES-256 | None | - |
| PI1.3 | Processing accuracy | ? | AI validation | Implement X |
| ... | ... | ... | ... | ... |

### Evidence Collection Plan
[Detailed table]

### AI-Specific Controls
[Detailed requirements]

### Timeline & Budget
| Phase | Duration | Cost Estimate |
|-------|----------|---------------|
| Readiness Assessment | 4-6 weeks | $X |
| Gap Remediation | 8-12 weeks | $X |
| Type I Audit | 4 weeks | $X |
| Type II Observation | 6-12 months | - |
| Type II Audit | 4 weeks | $X |

### Recommended Auditors
[List with rationale]
```

---

# SECTION 3: HITL Dashboard Collaboration Features (HIGH - P1)

**Gap**: V4 establishes HITL requirements but does NOT specify the real-time collaboration features needed for the operations team.

## Context

- Multiple operators will review AI decisions simultaneously
- High-stakes decisions (evictions, large payments, emergencies) need supervisor approval
- Need audit trail of WHO approved WHAT and WHEN
- Integration with existing tools (Slack, Teams) required
- Some decisions have **SLA timers** (e.g., emergency response within 15 minutes)

## Research Questions

### 3.1 Real-Time Presence

**Questions**:
- How do Figma, Google Docs, Notion implement cursor presence?
- WebSocket vs Server-Sent Events (SSE) for real-time updates?
- How to show "Maria is reviewing this decision" in the dashboard?
- Performance considerations at scale (100+ concurrent operators)?
- Handling network disconnects gracefully?

**Research Sources**:
- [ ] Figma engineering blog (multiplayer)
- [ ] Liveblocks documentation
- [ ] Socket.io best practices
- [ ] Y.js (CRDT for collaboration)

### 3.2 Comment Threads on AI Decisions

**Questions**:
- How to implement threaded comments on specific AI outputs?
- Should comments be editable? Deletable?
- How to @mention team members in comments?
- How to link comments to specific AI reasoning steps?
- Audit trail: How long to retain comments?

**Data Model Questions**:
```
Comment {
  id
  decision_id (FK to AI decision)
  author_id
  content
  created_at
  parent_comment_id (for threading)
  mentions: [user_ids]
  ...what else?
}
```

### 3.3 Approval Workflows

**Questions**:
- Multi-level approval (e.g., >$5K needs manager, >$25K needs director)?
- Sequential vs parallel approval?
- Delegation: What if approver is OOO?
- Escalation: What if no approval within SLA?
- Approval audit trail requirements?

**Workflow Engine Considerations**:
- Use Temporal for approval workflows? (We already have it)
- Or lightweight in-app state machine?
- How do competitors (Vendoroo, EliseAI) handle approvals?

### 3.4 Slack/Teams Integration

**Questions**:
- Push notifications to Slack channels for pending approvals?
- Can approvals happen **within Slack** (buttons/actions)?
- Slack Connect for external stakeholders (property owners)?
- Microsoft Teams equivalent features?
- Mobile push notifications for urgent items?

**Research Sources**:
- [ ] Slack Block Kit documentation
- [ ] Slack Workflow Builder
- [ ] Microsoft Teams Adaptive Cards
- [ ] PagerDuty Slack integration patterns

### 3.5 SLA Timers and Escalation

**Questions**:
- How to visualize SLA countdown in dashboard?
- Color coding: Green (>50% time left) → Yellow → Red?
- Auto-escalation rules when SLA breached?
- Historical SLA performance metrics?
- Alert fatigue prevention strategies?

### 3.6 Mobile Experience

**Questions**:
- Do we need native mobile apps for HITL?
- Progressive Web App (PWA) sufficient?
- Push notification strategies for mobile?
- Simplified mobile UI for quick approvals?

## Research Sources

- [ ] Linear, Notion, Asana approval workflows
- [ ] Retool HITL dashboard examples
- [ ] Temporal human-in-the-loop patterns
- [ ] Slack app development best practices
- [ ] Mobile HITL case studies

## Output Format Required

```markdown
## HITL Dashboard Collaboration Architecture

### Real-Time Presence
**Recommendation**: [WebSocket/SSE/Liveblocks]
**Architecture**:
[Diagram]
**Performance Considerations**:
[Details]

### Comment System Data Model
```typescript
interface Comment {
  // Full schema with all fields
}
```

### Approval Workflow Engine
**Recommendation**: [Temporal/Custom]
**Workflow Definition**:
```yaml
approval_workflow:
  levels:
    - threshold: 5000
      approvers: [role:manager]
      sla_hours: 4
    - threshold: 25000
      approvers: [role:director]
      sla_hours: 2
  escalation:
    ...
```

### Slack Integration
**Features**:
- [ ] Pending approval notifications
- [ ] In-Slack approval buttons
- [ ] Thread creation for discussion
- [ ] @mention notifications

**Slack App Architecture**:
[Details]

### SLA Visualization
[Mockup or description]
```

---

# SECTION 4: AI Model Versioning & Rollback Strategy (HIGH - P1)

**Gap**: V4 specifies which models to use but does NOT address how to version, test, and rollback AI model + prompt combinations in production.

## Context

- We use **Claude 3.5 Sonnet** (API-based, not self-hosted)
- Prompts are **versioned in Git** (V4 §6.1)
- Different agents have different prompts (Leasing, Maintenance, Voice, Quote)
- Anthropic may update Claude without notice
- We need to **test new prompts** before full rollout
- If a prompt causes issues, we need **instant rollback**

## Research Questions

### 4.1 Model + Prompt Version Pairing

**Questions**:
- How to track which prompt version was used with which model version?
- Schema for version tracking:
  ```
  AIConfig {
    agent_type: "leasing"
    model: "claude-3-5-sonnet-20240620"
    prompt_version: "1.2.3"
    deployed_at: timestamp
    traffic_percentage: 100
    ...what else?
  }
  ```
- How do LangSmith, Weights & Biases handle this?
- How does Anthropic version Claude API releases?

### 4.2 A/B Testing Framework

**Questions**:
- How to split traffic between prompt versions?
- Statistical significance: How many conversations before declaring winner?
- Metrics to compare:
  - Task completion rate
  - User satisfaction (if measurable)
  - Escalation rate (lower is better)
  - Response latency
  - Cost per conversation
- Guardrails: Auto-stop experiment if new version performs X% worse?
- A/B testing for voice (real-time) vs async (email/SMS)?

**Research Sources**:
- [ ] LaunchDarkly AI experimentation
- [ ] Statsig for ML experimentation
- [ ] Optimizely feature flags
- [ ] Academic papers on LLM A/B testing

### 4.3 Canary Deployments for Prompts

**Questions**:
- Deploy new prompt to 5% of traffic, monitor, expand?
- How to ensure same user gets consistent prompt version (sticky sessions)?
- Automated rollback triggers:
  - Error rate exceeds X%
  - Latency exceeds Xms
  - Sentiment drops below X
- How long should canary run before full rollout?

### 4.4 Rollback Procedures

**Questions**:
- How fast can we rollback? (Target: <5 minutes)
- Rollback scope: Single agent vs all agents?
- Do we keep conversation context during rollback?
- Notification to operations team during rollback?
- Post-mortem process for rollback events?

### 4.5 Model Provider Changes

**Questions**:
- What if Anthropic deprecates claude-3-5-sonnet-20240620?
- Grace period for model version changes?
- Testing strategy for new model versions?
- Fallback to different provider (GPT-4, Gemini) if Claude fails?
- LiteLLM fallback configuration:
  ```python
  fallback_chain = [
    "anthropic/claude-3-5-sonnet-20240620",
    "openai/gpt-4o",
    "google/gemini-1.5-pro",
  ]
  ```

### 4.6 Evaluation & Regression Testing

**Questions**:
- Automated eval suite before deployment?
- LangSmith, Braintrust, or custom evaluation?
- Test cases per agent type (how many? what coverage?)?
- How to detect **subtle** regressions (tone, accuracy)?
- Human evaluation sampling?

**Research Sources**:
- [ ] LangSmith evaluation documentation
- [ ] Braintrust AI evaluation framework
- [ ] Anthropic prompt evaluation guides
- [ ] OpenAI evals repository
- [ ] MLOps best practices for LLMs

## Output Format Required

```markdown
## AI Model Versioning & Rollback Strategy

### Version Schema
```typescript
interface AIDeployment {
  id: string;
  agent_type: AgentType;
  model_id: string;  // "claude-3-5-sonnet-20240620"
  prompt_version: string;  // semver
  prompt_hash: string;  // SHA of prompt content
  config: {
    temperature: number;
    max_tokens: number;
    // ...
  };
  traffic_allocation: number;  // 0-100
  status: "canary" | "stable" | "deprecated";
  created_at: Date;
  created_by: string;
  rollback_to?: string;  // Previous deployment ID
}
```

### A/B Testing Configuration
[Detailed specification]

### Canary Deployment Process
1. Deploy to 5% traffic
2. Monitor for 2 hours
3. If metrics pass: Expand to 25%
4. ...

### Rollback Runbook
| Trigger | Action | Timeline |
|---------|--------|----------|
| Error rate >5% | Auto-rollback | <2 min |
| Manual trigger | Rollback | <5 min |
| ... | ... | ... |

### Evaluation Suite
[Test case structure and coverage requirements]
```

---

# SECTION 5: RAG Knowledge Base Architecture (HIGH - P1)

**Gap**: V4 mentions MongoDB Atlas Vector Search but does NOT specify the knowledge base design, chunking strategy, or retrieval optimization.

## Context

- Our AI agents need access to:
  - **Property-specific** information (rules, amenities, contacts)
  - **Legal documents** (leases, HOA CCRs, bylaws)
  - **Maintenance history** (past issues, vendor performance)
  - **Fair housing guidelines** (what NOT to say)
  - **Company SOPs** (how to handle specific situations)
- Using **MongoDB Atlas Vector Search** (decided in V4)
- Need to support **multi-tenant** (each property has its own KB)
- Need to support **multiple languages** (English, Portuguese, Spanish)

## Research Questions

### 5.1 Document Chunking Strategy

**Questions**:
- Optimal chunk size for property management documents?
  - Legal documents (leases, CCRs): Dense text
  - SOPs: Procedural with steps
  - FAQs: Q&A format
- Overlapping chunks: How much overlap?
- Hierarchical chunking (document → section → paragraph)?
- How to preserve table structure in chunks?
- PDF parsing challenges and solutions?

**Research Sources**:
- [ ] LangChain text splitters documentation
- [ ] LlamaIndex chunking strategies
- [ ] Unstructured.io for document parsing
- [ ] Research papers on optimal chunk sizes

### 5.2 Embedding Model Selection

**Questions**:
- OpenAI text-embedding-3-large vs Cohere embed-v3 vs local models?
- Multilingual embedding models (for Portuguese, Spanish)?
- Cost comparison at scale:
  - OpenAI: $0.13/1M tokens
  - Cohere: $0.10/1M tokens
  - Local (sentence-transformers): Compute cost only
- Embedding dimension tradeoffs (1536 vs 3072)?
- Re-embedding strategy when model improves?

### 5.3 Retrieval Strategy

**Questions**:
- Pure vector search vs hybrid (vector + keyword)?
- MongoDB Atlas Vector Search configuration:
  ```javascript
  {
    index: "vector_index",
    path: "embedding",
    queryVector: [...],
    numCandidates: 100,
    limit: 5,
    filter: { property_id: "prop_123" }
  }
  ```
- Re-ranking after initial retrieval?
- Cross-encoder models for re-ranking?
- How many chunks to retrieve per query?
- Context window management (Claude 200K allows more context)?

### 5.4 Multi-Tenant Architecture

**Questions**:
- Separate collection per property? Or single collection with property_id filter?
- Index strategy for multi-tenant:
  ```
  Option A: Global index + filter
  Option B: Index per property
  ```
- Access control: Ensure property A can't access property B's KB?
- Tenant data isolation requirements?

### 5.5 Knowledge Base Update Pipeline

**Questions**:
- How do new documents get into the KB?
  - Manual upload by property manager?
  - Automatic ingestion from integrations?
  - Scheduled re-sync?
- How to handle document updates (re-embed changed chunks only)?
- Versioning: Keep old versions or replace?
- Notification when KB is stale?

### 5.6 RAG Evaluation

**Questions**:
- How to measure retrieval quality?
  - Precision@K
  - Recall@K
  - Mean Reciprocal Rank (MRR)
- Ground truth creation for property management queries?
- How to detect when RAG retrieves wrong information?
- RAGAS framework applicability?

**Research Sources**:
- [ ] MongoDB Atlas Vector Search documentation
- [ ] RAGAS (RAG Assessment) framework
- [ ] LangChain RAG best practices
- [ ] LlamaIndex retrieval evaluation
- [ ] Property management document structures

## Output Format Required

```markdown
## RAG Knowledge Base Architecture

### Document Processing Pipeline
```
Source Documents → Parser → Chunker → Embedder → MongoDB Atlas
     ↓                ↓          ↓           ↓
  [PDF, DOCX]    [Unstructured]  [500 tokens]  [text-embedding-3-large]
```

### Chunking Configuration
| Document Type | Chunk Size | Overlap | Strategy |
|---------------|------------|---------|----------|
| Lease | 500 tokens | 50 | Semantic |
| CCRs | 400 tokens | 40 | Paragraph |
| SOPs | 300 tokens | 30 | Step-based |
| FAQs | Full Q&A | 0 | Q&A pair |

### Embedding Model Decision
**Selected**: [Model name]
**Rationale**: [Why]
**Cost at Scale**: [Monthly estimate]

### MongoDB Schema
```javascript
{
  _id: ObjectId,
  property_id: "prop_123",
  document_type: "lease",
  document_id: "doc_456",
  chunk_index: 0,
  content: "...",
  embedding: [...],  // 1536 or 3072 dim
  metadata: {
    source_file: "lease_2024.pdf",
    page_number: 3,
    section: "Pet Policy",
    language: "en"
  }
}
```

### Retrieval Configuration
[Detailed settings]

### Update Pipeline
[Architecture diagram and process]
```

---

# SECTION 6: Chaos Engineering Runbook (MEDIUM - P1)

**Gap**: V4 mentions AWS FIS and Chaos Toolkit but does NOT provide the detailed runbook for chaos experiments.

## Context

- We have **critical voice services** that can't drop calls
- We have **financial transactions** that must be ACID
- We're **multi-region** (US East + Brazil)
- We use **Temporal** for durable workflows
- We need to **prove resilience** before production and quarterly thereafter

## Research Questions

### 6.1 Chaos Experiment Categories

**Questions**:
- What failure modes should we test?
  - Network failures (latency, packet loss, partition)
  - Instance failures (kill container, kill node)
  - Dependency failures (MongoDB down, Redis down, Twilio down)
  - Resource exhaustion (CPU, memory, disk)
  - Data corruption scenarios
- Which failures are safe to test in staging vs production?
- Blast radius control strategies?

### 6.2 Voice-Specific Chaos Tests

**Questions**:
- What happens when Deepgram STT fails mid-call?
- What happens when ElevenLabs TTS fails mid-response?
- What happens when LLM API times out?
- What happens when WebSocket connection drops?
- Network jitter simulation for voice quality testing?
- Failover time measurement (how long until backup kicks in)?

### 6.3 Payment/Treasury Chaos Tests

**Questions**:
- What happens when TigerBeetle leader fails?
- What happens when Formance is unavailable?
- What happens during network partition between TigerBeetle replicas?
- Temporal workflow recovery after worker crash?
- Redis cluster failover time?

### 6.4 Chaos Tool Selection

**Questions**:
- AWS Fault Injection Service (FIS) capabilities?
  - Supported actions
  - Integration with ECS/Fargate
  - Costs
- Chaos Toolkit for Kubernetes/ECS?
- Gremlin vs LitmusChaos vs Chaos Monkey?
- Can we use multiple tools together?

**Research Sources**:
- [ ] AWS FIS documentation and experiment templates
- [ ] Chaos Toolkit experiment catalog
- [ ] Gremlin attack library
- [ ] Netflix chaos engineering practices
- [ ] Temporal chaos testing documentation

### 6.5 Runbook Structure

**Questions**:
- Pre-requisites before running chaos?
- Notification process (who knows, when)?
- Abort criteria and procedures?
- Observation and metrics during chaos?
- Post-chaos analysis template?
- Frequency: Weekly? Monthly? Quarterly?

### 6.6 Automated Game Days

**Questions**:
- Can chaos experiments run automatically on schedule?
- Integration with CI/CD pipeline?
- Automated validation that system recovered?
- Alerting if chaos reveals a real issue?

## Output Format Required

```markdown
## Chaos Engineering Runbook

### Experiment Catalog

#### EXP-001: Voice STT Provider Failure
**Objective**: Verify graceful degradation when Deepgram fails
**Blast Radius**: Single voice session
**Environment**: Staging first, then production (low traffic)
**Pre-requisites**:
- [ ] Backup STT provider (Google STT) configured
- [ ] Monitoring dashboards ready
- [ ] On-call engineer aware

**Execution**:
1. Start test call
2. Inject Deepgram API failure (500 response)
3. Observe: Does call continue with backup STT?
4. Measure: Failover time, user experience impact

**Expected Result**: Failover to Google STT within 2 seconds
**Abort Criteria**: Failover time >5 seconds
**Rollback**: Remove fault injection

#### EXP-002: TigerBeetle Leader Failure
[Same format]

#### EXP-003: Regional Network Partition
[Same format]

### Quarterly Game Day Schedule
| Quarter | Focus Area | Experiments | Date |
|---------|------------|-------------|------|
| Q2 2025 | Voice resilience | EXP-001, EXP-002 | TBD |
| Q3 2025 | Payment resilience | EXP-003, EXP-004 | TBD |
| Q4 2025 | Multi-region | EXP-005, EXP-006 | TBD |

### Automated Chaos Configuration
```yaml
# AWS FIS experiment template
chaos_experiments:
  voice_failover:
    schedule: "0 3 * * SAT"  # 3 AM Saturday
    targets: [ecs:voice-agent]
    actions:
      - aws:ecs:stop-task
    stop_conditions:
      - cloudwatch:ErrorRate > 10%
```
```

---

# SECTION 7: Voice Failover Deep Dive (MEDIUM - P1)

**Gap**: V4 specifies RPO <1min for voice but does NOT detail the failover architecture.

## Context

- Voice calls are **real-time** - can't buffer like API requests
- We use **Twilio ConversationRelay** with WebSocket to our backend
- Our voice backend runs in **US East** and **Brazil (São Paulo)**
- We use **Redis** for session state during calls
- If US East fails, Brazilian users should continue without interruption

## Research Questions

### 7.1 Twilio SIP Failover Configuration

**Questions**:
- How does Twilio handle endpoint failover?
- Can we configure primary/secondary webhook endpoints?
- What's the failover detection time?
- Does ConversationRelay support multi-region natively?
- SIP trunk configuration for geo-redundancy?

**Research Sources**:
- [ ] Twilio ConversationRelay documentation
- [ ] Twilio Global Infrastructure documentation
- [ ] Twilio failover configuration guides
- [ ] Twilio engineering blog posts

### 7.2 WebSocket Session Continuity

**Questions**:
- How to migrate an active WebSocket session to a new server?
- Is session migration even possible, or must we reconnect?
- Reconnection strategy:
  - Client-side reconnect with exponential backoff?
  - Server-side session state restoration?
- What state must be preserved?
  - Conversation history
  - Current turn/intent
  - User context loaded
- Redis for session state:
  ```
  session:{call_id}:
    user_context: {...}
    conversation_history: [...]
    current_intent: "maintenance_request"
  ```

### 7.3 Cross-Region Redis Strategy

**Questions**:
- Redis Cluster vs Redis Sentinel for HA?
- AWS ElastiCache Global Datastore for cross-region?
- Replication lag acceptable for voice sessions?
- What if Redis fails during a call?
- Session reconstruction from conversation history?

### 7.4 DNS and Load Balancing

**Questions**:
- Route 53 latency-based routing for voice endpoints?
- Health check configuration for voice services?
- TTL settings for fast failover?
- Anycast vs unicast considerations?

### 7.5 Failover Testing

**Questions**:
- How to test failover without affecting real users?
- Synthetic call testing during failover?
- Measuring user-perceived impact of failover?
- Acceptable call quality degradation during failover?

## Output Format Required

```markdown
## Voice Failover Architecture

### Architecture Diagram
```
[User in São Paulo]
        │
        ▼
[Twilio Edge (São Paulo)]
        │
        ├──Primary──▶ [Voice Backend US-East]
        │                    │
        │                    ▼
        │              [Redis US-East]
        │                    │
        │              [Global Datastore Replication]
        │                    │
        └──Failover──▶ [Voice Backend São Paulo]
                             │
                             ▼
                       [Redis São Paulo]
```

### Twilio Configuration
```json
{
  "webhook_url": "https://voice.citadelos.com/webhook",
  "fallback_url": "https://voice-br.citadelos.com/webhook",
  "status_callback_url": "https://voice.citadelos.com/status",
  "fallback_method": "POST"
}
```

### Redis Session Schema
```json
{
  "session_id": "call_abc123",
  "user_id": "user_456",
  "property_id": "prop_789",
  "conversation": [...],
  "context": {...},
  "created_at": "...",
  "ttl": 3600
}
```

### Failover Sequence
1. US-East health check fails
2. Route 53 detects within 10 seconds
3. New calls route to São Paulo
4. Active calls: [behavior described]
5. Session state available via Global Datastore

### Failover Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Detection time | <10s | Route 53 health check |
| Failover time | <30s | DNS TTL |
| Active call impact | <5% drop | Call completion rate |
```

---

# SECTION 8: EU AI Act Compliance (MEDIUM - P1)

**Gap**: V4 mentions EU AI Act but does NOT detail the specific requirements for our AI systems.

## Context

- We plan to expand to **Europe (Spain, Portugal, Italy)**
- Our AI agents make **automated decisions** about:
  - Lease applications (could be high-risk?)
  - Maintenance prioritization
  - Communication responses
  - Payment reminders
- EU AI Act comes into force in **2025-2026** with phased requirements
- We need to understand if we're "high-risk" or not

## Research Questions

### 8.1 Risk Classification

**Questions**:
- How are AI systems classified under EU AI Act?
  - Unacceptable risk
  - High-risk
  - Limited risk
  - Minimal risk
- Are our AI agents "high-risk"?
  - Leasing assistant: Involves housing decisions → likely high-risk?
  - Maintenance coordinator: Safety implications?
  - Voice agent: Customer service → limited risk?
- What factors determine high-risk classification?

**Research Sources**:
- [ ] EU AI Act official text (Regulation 2024/1689)
- [ ] European Commission AI Act guidance
- [ ] Article 6 (high-risk classification criteria)
- [ ] Annex III (high-risk use cases)

### 8.2 High-Risk AI Requirements

If classified as high-risk, what's required?

**Questions**:
- Risk management system (Article 9)
- Data governance (Article 10)
- Technical documentation (Article 11)
- Record-keeping (Article 12)
- Transparency (Article 13)
- Human oversight (Article 14)
- Accuracy, robustness, cybersecurity (Article 15)

For each requirement:
- What specifically must we do?
- How does V4 architecture already satisfy this?
- What gaps remain?

### 8.3 Transparency Obligations

**Questions**:
- Must we tell users they're interacting with AI?
- Specific disclosure language required?
- Voice AI: Announce "This call may be handled by AI"?
- Written communications: AI-generated disclaimer?

### 8.4 Human Oversight Requirements

**Questions**:
- What level of human oversight is required?
- Does our HITL dashboard satisfy Article 14?
- Can AI make final decisions, or must humans approve?
- Specific requirements for housing-related AI?

### 8.5 Documentation Requirements

**Questions**:
- What technical documentation is required?
- How to document AI training data?
- Bias testing documentation?
- Model performance documentation?
- How often must documentation be updated?

### 8.6 Timeline and Penalties

**Questions**:
- When do requirements become enforceable?
- Prohibited AI practices: August 2025
- High-risk obligations: August 2026
- Penalties for non-compliance?
- Enforcement authority?

### 8.7 Interaction with GDPR

**Questions**:
- How does EU AI Act interact with GDPR?
- Data protection impact assessments required?
- Right to explanation for AI decisions?

## Research Sources

- [ ] EU AI Act full text (2024/1689)
- [ ] European Commission implementation guidance
- [ ] IAPP (International Association of Privacy Professionals) EU AI Act resources
- [ ] Law firm analyses (Baker McKenzie, DLA Piper)
- [ ] Property management industry guidance on EU AI Act

## Output Format Required

```markdown
## EU AI Act Compliance Assessment

### Risk Classification Matrix
| AI System | Use Case | Risk Level | Rationale |
|-----------|----------|------------|-----------|
| Leasing Assistant | Housing decisions | HIGH | Article 6 + Annex III |
| Maintenance Coordinator | Safety-related | LIMITED | Not in Annex III |
| Voice Agent | Customer service | LIMITED | Chatbot provisions |
| Quote Chaser | Payment reminders | MINIMAL | No significant risk |

### High-Risk Requirements (Leasing Assistant)
| Article | Requirement | V4 Compliance | Gap | Remediation |
|---------|-------------|---------------|-----|-------------|
| Art. 9 | Risk management | Partial | Need formal RMS | Implement by Q3 |
| Art. 10 | Data governance | Yes (§7) | None | - |
| Art. 11 | Technical docs | Partial | Need template | Create docs |
| Art. 12 | Record-keeping | Yes (TigerBeetle) | None | - |
| Art. 13 | Transparency | Partial | Need disclosures | Add UI text |
| Art. 14 | Human oversight | Yes (HITL) | Document process | - |
| Art. 15 | Accuracy/security | Yes (§12) | None | - |

### Required Disclosures
**Voice**: "You are speaking with an AI assistant. A human agent can join at any time."
**Chat/SMS**: "This conversation is AI-assisted. [Learn more]"
**Email**: Footer: "This message was composed with AI assistance."

### Timeline
| Milestone | Date | Action Required |
|-----------|------|-----------------|
| Prohibited practices | Aug 2025 | Review for prohibited uses |
| High-risk compliance | Aug 2026 | Full documentation ready |
| Penalties active | Aug 2026 | €35M or 7% revenue risk |

### Implementation Roadmap
[Detailed steps]
```

---

# 📊 OUTPUT DELIVERABLE

## File Details

**File Name**: `KD-PRODUCTION-READINESS-ROUND2.md`  
**Save To**: `knowledge/infrastructure/`  
**Expected Length**: 1,200-1,800 lines  
**Citations**: 60+ authoritative sources  

## Document Structure

```markdown
# Knowledge Document: Production Readiness Round 2

## Executive Summary
- Key findings per section
- Critical decisions made
- Remaining risks/gaps

## 1. State CAM/HOA Regulations
- California (SB-721, SB-326, Civil Code)
- Florida (HB-919, SB-4D, Statute 718)
- Texas (Property Code 209, 82)
- AI Compliance Checklist by State

## 2. SOC 2 Type II Certification Path
- Trust Services Criteria Mapping
- Evidence Collection Plan
- AI-Specific Controls
- Timeline & Budget
- Recommended Auditors

## 3. HITL Dashboard Collaboration
- Real-Time Presence Architecture
- Comment System Design
- Approval Workflow Engine
- Slack/Teams Integration
- SLA Visualization

## 4. AI Model Versioning & Rollback
- Version Schema
- A/B Testing Framework
- Canary Deployment Process
- Rollback Runbook
- Evaluation Suite

## 5. RAG Knowledge Base Architecture
- Document Processing Pipeline
- Chunking Strategy
- Embedding Model Decision
- MongoDB Schema
- Retrieval Optimization

## 6. Chaos Engineering Runbook
- Experiment Catalog (10+ experiments)
- Voice-Specific Tests
- Payment/Treasury Tests
- Quarterly Schedule
- Automated Chaos Config

## 7. Voice Failover Architecture
- Twilio Configuration
- WebSocket Session Continuity
- Cross-Region Redis
- DNS/Load Balancing
- Failover Testing Plan

## 8. EU AI Act Compliance
- Risk Classification Matrix
- High-Risk Requirements
- Transparency Disclosures
- Human Oversight Documentation
- Implementation Timeline

## 9. Decision Summary Table
| Section | Key Decision | Rationale | Cost Impact | Timeline |

## 10. References
- 60+ citations organized by section
```

---

# 🎯 SUCCESS CRITERIA

Your research is complete when:

- [ ] All 8 sections have comprehensive answers
- [ ] Each section has specific, actionable recommendations
- [ ] State regulations cover CA, FL, TX with statute citations
- [ ] SOC 2 has TSC mapping and timeline
- [ ] HITL collaboration has technical architecture
- [ ] Model versioning has schema and runbook
- [ ] RAG has chunking/embedding decisions
- [ ] Chaos engineering has 10+ experiment definitions
- [ ] Voice failover has architecture diagram
- [ ] EU AI Act has risk classification and gap analysis
- [ ] 60+ authoritative sources cited
- [ ] Total length: 1,200-1,800 lines

---

# 💡 KEY INSIGHT

**This research closes the gap between "architecturally sound" and "production-ready."**

V4 established WHAT we're building and WHERE. This research establishes:
- **HOW we comply** with regulations (state CAM, EU AI Act)
- **HOW we prove** compliance (SOC 2, documentation)
- **HOW we operate** (HITL, chaos testing, failover)
- **HOW we iterate** (model versioning, A/B testing)

**Think like a VP of Engineering preparing for an enterprise customer audit and a production incident simultaneously.**

---

# 🔄 AFTER COMPLETING

1. Save document to `knowledge/infrastructure/KD-PRODUCTION-READINESS-ROUND2.md`
2. Update `GAP_ANALYSIS_V4_COVERAGE.md` with new coverage percentages
3. Update `STATUS.md` - Note Round 2 research completion
4. Commit and push:
```bash
git add -A
git commit -m "Round 2 COMPLETE: Production Readiness - Closing Infrastructure Gaps"
git push
```

---

**Research Assignment Created**: January 2026  
**Builds On**: `KD-OPEN-ITEMS-infrastructure-compliance-V4.md`  
**Gap Analysis**: `GAP_ANALYSIS_V4_COVERAGE.md`

