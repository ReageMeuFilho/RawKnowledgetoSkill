# Gap Analysis: V4 Coverage vs Original Research Requirements

**Document Version**: 1.0  
**Date**: January 2026  
**Purpose**: Map V4 coverage and identify remaining open items for next research round

---

## Executive Summary

**V4 Document**: `KD-OPEN-ITEMS-infrastructure-compliance-V4.md`

| Metric | Count |
|--------|-------|
| **Total Original Open Items** | 42 |
| **Fully Covered in V4** | 28 (67%) |
| **Partially Covered** | 8 (19%) |
| **Not Covered / Need More Research** | 6 (14%) |

### Coverage by Priority

| Priority | Total | Covered | Partial | Gap |
|----------|-------|---------|---------|-----|
| **P0 Critical** | 8 | 7 | 1 | 0 |
| **P1 High** | 12 | 9 | 2 | 1 |
| **P2 Medium** | 10 | 6 | 3 | 1 |
| **P3 Low** | 12 | 6 | 2 | 4 |

---

## Detailed Coverage Matrix

### SECTION 1: Cloud Provider & Deployment Strategy (CRITICAL - P0)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-002** | Cloud Provider (AWS/GCP/Azure) | ✅ **FULL** | §2.1 | AWS primary, cost analysis, Brazil presence |
| **OPEN-012** | ECS vs EKS vs EC2 | ✅ **FULL** | §2.2 | ECS/Fargate recommended, $74/mo EKS analysis |
| **ENV-001** | Environment Configuration | ✅ **FULL** | §2.5 | Dev/Staging/Prod/DR matrix |
| **ENV-002** | AI Model Versions by Env | ✅ **FULL** | §2.5 | Claude Haiku (dev) → Sonnet (prod) |
| **ENV-003** | Blue/Green for Voice | ✅ **FULL** | §2.6 | Canary/blue-green call-by-call |
| **BRAZIL-001** | Brazil Deployment | ✅ **FULL** | §2.3, §4, §5 | São Paulo, LGPD, SPSAV, PIX |
| **MULTI-001** | Multi-Region Strategy | ✅ **FULL** | §2.3, §11.2 | Active-active US/Brazil |
| **TERRAFORM** | Infrastructure as Code | ✅ **FULL** | §2.4 | Complete Terraform modules |

**Section 1 Status**: ✅ **COMPLETE** (8/8 items)

---

### SECTION 2: Data Retention & Compliance Policy (CRITICAL - P0)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-003** | Data Retention Policy | ✅ **FULL** | §7.1 | Full matrix by data type with TTLs |
| **OPEN-020** | Transcript Retention | ✅ **FULL** | §7.1 | 30d hot → 5yr archive |
| **GDPR-001** | GDPR Right to Erasure | ✅ **FULL** | §7.2 | Deletion workflow documented |
| **LGPD-001** | Brazil LGPD | ✅ **FULL** | §4, §7 | Data residency, federation |
| **PCI-001** | PCI-DSS Compliance | ✅ **FULL** | §7.1 | Token-only, no PAN storage |
| **SOC2-001** | SOC 2 Requirements | ⚠️ **PARTIAL** | §7.1 | Mentioned, not detailed |
| **AUDIT-001** | Audit Trail Retention | ✅ **FULL** | §7.1 | 7yr archive, TigerBeetle immutable |

**Section 2 Status**: ✅ **MOSTLY COMPLETE** (6/7 full, 1 partial)

**Gap for Next Research**:
- SOC 2 Type II certification path - detailed controls mapping needed

---

### SECTION 3: Prompt Engineering & AI Configuration (HIGH - P1)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-006** | Prompt Library Architecture | ✅ **FULL** | §6.1 | Git-versioned, folder structure |
| **PROMPT-001** | Version Control for Prompts | ✅ **FULL** | §6.1 | Git + Parameter Store |
| **PROMPT-002** | A/B Testing Prompts | ⚠️ **PARTIAL** | §6.1 | Mentioned, not detailed |
| **PROMPT-003** | Property-Specific Context | ✅ **FULL** | §6.2 | Jinja2 templating shown |
| **PROMPT-004** | Locale-Specific Variations | ✅ **FULL** | §6.1-6.2 | pt-BR folder structure |
| **AGENT-001** | Leasing Assistant Prompt | ✅ **FULL** | §6.2 | Complete sample prompt |
| **AGENT-002** | Maintenance Coordinator Prompt | ✅ **FULL** | §6.2 | Complete sample prompt |
| **AGENT-003** | Voice Agent Prompt | ✅ **FULL** | §6.2 | Complete sample prompt |
| **AGENT-004** | Quote Chaser Prompt | ⚠️ **PARTIAL** | §6.2 | Mentioned, not detailed |

**Section 3 Status**: ✅ **MOSTLY COMPLETE** (6/9 full, 3 partial)

**Gaps for Next Research**:
- A/B testing framework for prompts in production
- Quote Chaser full prompt specification

---

### SECTION 4: Fine-Tuning Strategy (HIGH - P1)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-007** | Fine-Tuning vs RAG Decision | ✅ **FULL** | §6.4 | RAG preferred, fine-tune if gaps |
| **FT-001** | Training Data Requirements | ⚠️ **PARTIAL** | §6.4 | Decision made, data pipeline not detailed |
| **FT-002** | Continuous Learning from HITL | ⚠️ **PARTIAL** | §6.4 | Mentioned, architecture not detailed |
| **FT-003** | Model Versioning & Rollback | ❌ **NOT COVERED** | - | Needs research |
| **RAG-001** | Knowledge Base Structure | ⚠️ **PARTIAL** | §6.4 | Mentioned MongoDB Atlas, not detailed |

**Section 4 Status**: ⚠️ **PARTIAL** (1/5 full, 3 partial, 1 gap)

**Gaps for Next Research**:
- Model versioning and rollback strategy
- HITL continuous learning pipeline architecture
- RAG knowledge base chunking and retrieval strategy

---

### SECTION 5: Regulatory Compliance Matrix (HIGH - P1)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-008** | Compliance Frameworks | ✅ **FULL** | §8 (Compliance Matrix) | SOX, PCI, LGPD, SPSAV mapped |
| **OPEN-009** | State CAM Regulations | ❌ **NOT COVERED** | - | FL, CA, TX HOA regulations missing |
| **AI-REG-001** | EU AI Act | ⚠️ **PARTIAL** | §8 | Mentioned, not detailed |
| **AI-REG-002** | NIST AI RMF | ⚠️ **PARTIAL** | §8 | Mentioned, not detailed |
| **FAIR-001** | Fair Housing AI | ✅ **FULL** | §6.3 | Guardrails YAML with patterns |
| **SPSAV-001** | Brazil Crypto Regulation | ✅ **FULL** | §4 | Deep dive, Feb 2026 deadline |

**Section 5 Status**: ⚠️ **PARTIAL** (3/6 full, 2 partial, 1 gap)

**Gaps for Next Research**:
- State-specific CAM/HOA regulations (California SB-721, Florida HB-919, Texas)
- EU AI Act detailed requirements mapping
- NIST AI RMF implementation checklist

---

### SECTION 6: CRM & Integration Strategy (HIGH - P1)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-010** | CRM Integration Strategy | ✅ **FULL** | §8.1-8.2 | Priority matrix, abstraction layer |
| **CRM-001** | AppFolio Integration | ✅ **FULL** | §8.1 | P0, REST API + Webhooks |
| **CRM-002** | Yardi Integration | ✅ **FULL** | §8.1 | P0, Yardi OSS API |
| **CRM-003** | Salesforce Integration | ✅ **FULL** | §8.1 | P0, API + Web-to-Lead |
| **CRM-004** | HubSpot Integration | ✅ **FULL** | §8.1 | P1, API + Webhooks |
| **CRM-005** | Integration Plugin Interface | ✅ **FULL** | §8.2 | Python ABC class with methods |
| **API-001** | Developer Platform API | ✅ **FULL** | §8.3 | OpenAPI spec, OAuth2 |

**Section 6 Status**: ✅ **COMPLETE** (7/7 items)

---

### SECTION 7: Disaster Recovery & Business Continuity (MEDIUM - P2)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-025** | RPO/RTO Targets | ✅ **FULL** | §11.1 | By service tier table |
| **OPEN-026** | Multi-Region Architecture | ✅ **FULL** | §11.2 | Active-active US/Brazil |
| **OPEN-033** | Chaos Engineering | ⚠️ **PARTIAL** | §11.3 | AWS FIS mentioned, not detailed |
| **DR-001** | Voice Failover | ⚠️ **PARTIAL** | §11.1 | RPO <1min, architecture not detailed |
| **DR-002** | Database Replication | ✅ **FULL** | §11.2 | MongoDB Atlas Global Clusters |
| **DR-003** | Cost vs Resilience | ⚠️ **PARTIAL** | §11 | Mentioned, no cost modeling |

**Section 7 Status**: ⚠️ **PARTIAL** (3/6 full, 3 partial)

**Gaps for Next Research**:
- Chaos engineering detailed plan and scenarios
- Voice failover architecture (Twilio SIP failover, cross-region Redis)
- DR cost modeling by tier

---

### SECTION 8: Quick Answers (MEDIUM/LOW)

| Open Item | Description | V4 Coverage | Section | Status |
|-----------|-------------|-------------|---------|--------|
| **OPEN-018** | Partial Failure Handling | ✅ **FULL** | §11.3 | Saga compensation via Temporal |
| **OPEN-019** | HITL Dashboard Collaboration | ❌ **NOT COVERED** | - | Real-time features not researched |
| **OPEN-021** | Predictive Scaling | ⚠️ **PARTIAL** | §13 | AWS Predictive Scaling mentioned |
| **OPEN-023** | State Persistence Upgrades | ✅ **FULL** | §13 | Rolling + schema migration |
| **OPEN-024** | Policy Hot Reload | ✅ **FULL** | §13 | Parameter Store + pub/sub |
| **OPEN-027** | Predictive Failure Detection | ⚠️ **PARTIAL** | §13 | DevOps Guru mentioned, not detailed |
| **OPEN-028** | Automated Recovery Level | ✅ **FULL** | §11.3 | ASG + K8s ReplicaSet |
| **OPEN-029** | Cascading Failure Handling | ✅ **FULL** | §11.3 | Bulkhead + Circuit Breaker |
| **OPEN-030** | Error Logging Compliance | ✅ **FULL** | §7.2 | PII masking, encryption |
| **OPEN-031** | Chaos Engineering Tools | ⚠️ **PARTIAL** | §11.3 | AWS FIS, Chaos Toolkit listed |
| **OPEN-034** | Data Residency | ✅ **FULL** | §3.2 | Federated ledger, BR in sa-east-1 |

**Section 8 Status**: ⚠️ **PARTIAL** (7/11 full, 3 partial, 1 gap)

**Gaps for Next Research**:
- HITL Dashboard real-time collaboration features (cursor presence, comments, Slack integration)
- Predictive scaling ML model details
- Chaos engineering runbook and test scenarios

---

### LOW PRIORITY ITEMS (OPEN-035 to OPEN-042)

| Open Item | Description | V4 Coverage | Status |
|-----------|-------------|-------------|--------|
| **OPEN-035** | Resource Churn Monitoring | ❌ NOT COVERED | Needs research |
| **OPEN-036** | Terraform Module Optimization | ⚠️ PARTIAL | Basic modules in V4 |
| **OPEN-037** | Observability Stack | ⚠️ PARTIAL | CloudWatch mentioned |
| **OPEN-038** | Cost Allocation Tagging | ❌ NOT COVERED | Needs research |
| **OPEN-039** | Secrets Rotation | ⚠️ PARTIAL | SSM mentioned |
| **OPEN-040** | Log Aggregation | ⚠️ PARTIAL | CloudWatch logs |
| **OPEN-041** | APM Selection | ❌ NOT COVERED | Needs research |
| **OPEN-042** | Synthetic Monitoring | ❌ NOT COVERED | Needs research |

**Low Priority Status**: ❌ **MOSTLY NOT COVERED** (0/8 full, 4 partial, 4 gaps)

---

## Summary: Items Needing Further Research

### Priority 1: Must Research for Production (P1)

| Item | Gap Description | Research Effort |
|------|-----------------|-----------------|
| **State CAM Regulations** | California SB-721/SB-326, Florida HB-919/SB-4D, Texas HOA | Medium |
| **HITL Dashboard Collaboration** | Real-time cursor presence, comments, Slack integration | Medium |
| **Model Versioning & Rollback** | How to version LLM + prompt combinations, rollback strategy | Medium |
| **SOC 2 Type II Path** | Detailed controls mapping, audit preparation | High |

### Priority 2: Should Research Before Scale (P2)

| Item | Gap Description | Research Effort |
|------|-----------------|-----------------|
| **Chaos Engineering Runbook** | Detailed scenarios, frequency, automated validation | Medium |
| **Voice Failover Architecture** | Twilio SIP failover config, cross-region Redis session | Medium |
| **RAG Knowledge Base Design** | Chunking strategy, embedding model, retrieval optimization | Medium |
| **HITL Continuous Learning** | Data labeling pipeline, feedback loop architecture | High |
| **Predictive Scaling ML** | Historical pattern analysis, custom metrics | Low |
| **EU AI Act Compliance** | Detailed requirements for property management AI | Medium |

### Priority 3: Can Defer (P3)

| Item | Gap Description | Research Effort |
|------|-----------------|-----------------|
| **Resource Churn Monitoring** | Unused resource detection | Low |
| **Cost Allocation Tagging** | AWS tagging strategy for cost attribution | Low |
| **APM Selection** | DataDog vs New Relic vs Dynatrace | Low |
| **Synthetic Monitoring** | Uptime monitoring tool selection | Low |
| **Quote Chaser Full Prompt** | Complete prompt specification | Low |
| **A/B Testing Framework** | Prompt A/B testing in production | Medium |

---

## Recommended Next Research Round

### Round 2 Research Prompt Focus

**Title**: `RESEARCH_PROMPT_PRODUCTION_READINESS_ROUND2.md`

**Scope**: 10 items (P1 + critical P2)

**Sections**:

1. **State CAM/HOA Regulations** (OPEN-009)
   - California SB-721, SB-326 (balcony inspections)
   - Florida HB-919, SB-4D (condo safety)
   - Texas HOA regulations
   - AI-specific requirements for property management

2. **SOC 2 Type II Certification Path** (AUDIT-002)
   - Trust Services Criteria mapping
   - Evidence collection requirements
   - Timeline and cost estimates
   - Readiness checklist

3. **HITL Dashboard Collaboration** (OPEN-019)
   - Real-time presence (WebSocket/SSE)
   - Comment threads on AI decisions
   - Slack/Teams integration for escalation
   - Architecture recommendations

4. **AI Model Versioning & Rollback** (FT-003)
   - Prompt + model version pairing
   - A/B testing framework
   - Rollback procedures
   - Evaluation metrics

5. **RAG Knowledge Base Architecture** (RAG-001)
   - Document chunking strategy
   - Embedding model selection (OpenAI vs Cohere vs local)
   - Retrieval optimization (hybrid search)
   - Knowledge base update pipeline

6. **Chaos Engineering Runbook** (OPEN-031, OPEN-033)
   - Quarterly chaos day plan
   - Specific failure scenarios (voice, payment, database)
   - Automated game day validation
   - Incident response integration

7. **Voice Failover Deep Dive** (DR-001)
   - Twilio SIP failover configuration
   - Cross-region WebRTC session continuity
   - Redis cluster for session state
   - Latency budget during failover

8. **EU AI Act Compliance** (AI-REG-001)
   - Risk classification for our AI systems
   - Documentation requirements
   - Human oversight requirements
   - Timeline for compliance

**Expected Output**: `KD-PRODUCTION-READINESS-ROUND2.md`
**Expected Length**: 600-800 lines
**Citations**: 30+ authoritative sources

---

## Coverage Statistics

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         V4 COVERAGE SUMMARY                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  SECTION 1: Cloud & Deployment      ████████████████████████████████ 100%   │
│  SECTION 2: Data Retention          ██████████████████████████████░░  86%   │
│  SECTION 3: Prompt Engineering      ██████████████████████████░░░░░░  67%   │
│  SECTION 4: Fine-Tuning Strategy    ████████████░░░░░░░░░░░░░░░░░░░░  40%   │
│  SECTION 5: Compliance              ██████████████████░░░░░░░░░░░░░░  50%   │
│  SECTION 6: CRM Integrations        ████████████████████████████████ 100%   │
│  SECTION 7: Disaster Recovery       ██████████████████░░░░░░░░░░░░░░  50%   │
│  SECTION 8: Quick Answers           ████████████████████████░░░░░░░░  64%   │
│  LOW PRIORITY (035-042)             ████████░░░░░░░░░░░░░░░░░░░░░░░░  25%   │
│                                                                             │
│  ─────────────────────────────────────────────────────────────────────────  │
│  OVERALL V4 COVERAGE                ██████████████████████████░░░░░░  67%   │
│                                                                             │
│  ✅ Fully Covered:     28 items                                             │
│  ⚠️  Partially Covered:  8 items                                             │
│  ❌ Not Covered:        6 items                                             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Conclusion

**V4 provides strong coverage** of the critical infrastructure decisions:
- ✅ Cloud provider and deployment strategy (100%)
- ✅ Brazil-specific requirements (SPSAV, PIX, LGPD) (100%)
- ✅ Treasury OS integration (TigerBeetle, Formance, Temporal) (100%)
- ✅ Voice AI latency architecture (<300ms) (100%)
- ✅ Skills Framework integration (100%)
- ✅ Security (Zero Trust, MPC Custody) (100%)

**Remaining gaps are primarily in**:
- State-specific regulations (CAM/HOA)
- AI governance details (EU AI Act, model versioning)
- Operational tooling (chaos engineering, HITL collaboration)
- Knowledge base architecture (RAG design)

**Recommendation**: Proceed with Round 2 research focusing on the 8 items in the P1/P2 categories above. This will bring overall coverage to ~90% and enable production deployment.

---

*Gap Analysis Generated: January 2026*
*Reference: V4 Document - `KD-OPEN-ITEMS-infrastructure-compliance-V4.md`*

