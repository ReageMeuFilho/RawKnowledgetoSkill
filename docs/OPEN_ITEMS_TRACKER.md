# Open Items & Areas Needing Attention Tracker

> **Purpose**: Track gaps, open questions, and incomplete specifications discovered during pipeline processing
> **Last Updated**: January 2026
> **Review Frequency**: After each Stage 4 completion

---

## 📊 OPEN ITEMS DASHBOARD

```
╔═══════════════════════════════════════════════════════════════════════════════════════╗
║                           OPEN ITEMS STATUS                                            ║
╠═══════════════════════════════════════════════════════════════════════════════════════╣
║                                                                                        ║
║   Total Open Items:       42                                                           ║
║   🔴 Critical (P0):        3                                                           ║
║   🟠 High (P1):           12                                                           ║
║   🟡 Medium (P2):         19                                                           ║
║   🟢 Low (P3):             8                                                           ║
║                                                                                        ║
║   Source: GAP-HOAI-001    Items: 42 (from Engineering Spec + Quality Assessment)       ║
║                                                                                        ║
╚═══════════════════════════════════════════════════════════════════════════════════════╝
```

---

## 🔴 CRITICAL ITEMS (P0) - Must Address Before MVP

### From Quality Assessment (GAP-HOAI-001)

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-001 | **Testing Strategy** - No complete testing section. Need unit test coverage requirements, integration test scenarios, load testing benchmarks, AI agent testing methodology | Testing | Quality Assessment | Engineering | ⏳ Open | Blocks implementation |
| OPEN-002 | **Deployment Environment** - AWS vs GCP vs Azure decision not made. ECS vs EKS vs EC2 not specified. Environment configs (dev/staging/prod) not defined | Infrastructure | Quality Assessment | DevOps | ⏳ Open | Blocks deployment |
| OPEN-003 | **Data Retention Period** - Specific retention period for audit logs and HITL decisions not defined | Compliance | ES Section 1.3.2 | Legal/Compliance | ⏳ Open | Regulatory requirement |

---

## 🟠 HIGH PRIORITY ITEMS (P1) - Address Before Phase 1

### From Quality Assessment (GAP-HOAI-001)

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-004 | **Voice Model Selection** - Exact Twilio WebSocket integration details, speech-to-text model selection, TTS voice configuration | Voice Agent | Quality Assessment | AI/Engineering | ⏳ Open | Impacts voice quality |
| OPEN-005 | **LLM Model Assignments** - Which models for which agent types (Voice, AP, Research, Budget) not specified | AI Configuration | Quality Assessment | AI/Engineering | ⏳ Open | Cost/quality tradeoff |
| OPEN-006 | **Prompt Templates** - Prompt library for each agent type not defined | AI Configuration | Quality Assessment | AI/Engineering | ⏳ Open | Consistency requirement |
| OPEN-007 | **Fine-tuning Strategy** - Whether/how to fine-tune models for CAM domain | AI Configuration | Quality Assessment | AI/Engineering | ⏳ Open | Performance optimization |

### From Engineering Spec Open Questions (GAP-HOAI-001)

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-008 | Compliance frameworks beyond NIST AI RMF (SOX, HIPAA, GDPR) | Compliance | ES Section 1.3.2 | Legal | ⏳ Open | |
| OPEN-009 | State-level CAM regulations for policy engine | Compliance | ES Section 1.3.2 | Legal | ⏳ Open | |
| OPEN-010 | Integration with existing CRM systems beyond Vantaca | Integration | ES Section 1.3.2 | Product | ⏳ Open | |
| OPEN-011 | FastAPI vs Flask for async support with LangChain | Architecture | ES Section 3.6.5 | Engineering | ⏳ Open | |
| OPEN-012 | Deployment target: AWS ECS, EKS, or EC2 | Infrastructure | ES Section 3.6.5 | DevOps | ⏳ Open | |
| OPEN-013 | Microservices vs monolith per agent type | Architecture | ES Section 3.6.5 | Engineering | ⏳ Open | |
| OPEN-014 | Encryption requirements (at rest, in transit) | Security | ES Section 3.6.5 | Security | ⏳ Open | |
| OPEN-015 | MongoDB Atlas vs self-managed for production | Infrastructure | ES Section 3.6.5 | DevOps | ⏳ Open | |

---

## 🟡 MEDIUM PRIORITY ITEMS (P2) - Address During Implementation

### From Engineering Spec Open Questions (GAP-HOAI-001)

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-016 | Maximum latency for voice agent during peak load | Performance | ES Section 4.3.4 | Engineering | ⏳ Open | |
| OPEN-017 | Circuit breaker failure thresholds for external services | Resilience | ES Section 4.3.4 | Engineering | ⏳ Open | |
| OPEN-018 | Partial failure handling - compensation vs retry | Resilience | ES Section 4.3.4 | Engineering | ⏳ Open | |
| OPEN-019 | HITL dashboard real-time collaboration features | UX | ES Section 4.3.4 | Product | ⏳ Open | |
| OPEN-020 | Conversation transcript data retention | Compliance | ES Section 4.3.4 | Legal | ⏳ Open | |
| OPEN-021 | Predictive scaling based on historical patterns | Infrastructure | ES Section 4.3.4 | DevOps | ⏳ Open | |
| OPEN-022 | Service mesh (Istio/Linkerd) for inter-service security | Security | ES Section 5.4.6 | DevOps | ⏳ Open | |
| OPEN-023 | Agent state persistence during system upgrades | Operations | ES Section 5.4.6 | Engineering | ⏳ Open | |
| OPEN-024 | Real-time policy updates without service restart | Operations | ES Section 5.4.6 | Engineering | ⏳ Open | |
| OPEN-025 | Maximum acceptable RPO for conversation history | DR | ES Section 5.4.6 | DevOps | ⏳ Open | |
| OPEN-026 | Maximum recovery time for critical system failures | DR | ES Section 6.9.3 | DevOps | ⏳ Open | |
| OPEN-027 | Predictive failure detection based on error patterns | Operations | ES Section 6.9.3 | Engineering | ⏳ Open | |
| OPEN-028 | Automated recovery level without human oversight | Operations | ES Section 6.9.3 | Engineering | ⏳ Open | |
| OPEN-029 | Cascading failure handling across components | Resilience | ES Section 6.9.3 | Engineering | ⏳ Open | |
| OPEN-030 | Error logging compliance requirements | Compliance | ES Section 6.9.3 | Legal | ⏳ Open | |
| OPEN-031 | Chaos engineering for resilience testing | Testing | ES Section 6.9.3 | QA | ⏳ Open | |
| OPEN-032 | Container orchestration: Kubernetes vs Docker Swarm vs cloud-native | Infrastructure | ES Section 6.3.5 | DevOps | ⏳ Open | |
| OPEN-033 | Multi-region deployment for disaster recovery | Infrastructure | ES Section 6.3.5 | DevOps | ⏳ Open | |
| OPEN-034 | Data residency and cross-border transfer requirements | Compliance | ES Section 6.3.5 | Legal | ⏳ Open | |

---

## 🟢 LOW PRIORITY ITEMS (P3) - Address Post-MVP

### From Engineering Spec Open Questions (GAP-HOAI-001)

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-035 | GraphQL federation for complex multi-service queries | API | ES Section 6.3.5 | Engineering | ⏳ Open | |
| OPEN-036 | Webhook retry policies for external systems | Integration | ES Section 6.3.5 | Engineering | ⏳ Open | |
| OPEN-037 | API versioning at gateway vs service level | API | ES Section 6.3.5 | Engineering | ⏳ Open | |
| OPEN-038 | Data residency requirements for webhook payloads | Compliance | ES Section 6.3.5 | Legal | ⏳ Open | |
| OPEN-039 | Batch API operations for high-volume sync | API | ES Section 6.3.5 | Engineering | ⏳ Open | |
| OPEN-040 | GDPR automatic data classification and labeling | Compliance | ES Section 6.2.2 | Legal | ⏳ Open | |
| OPEN-041 | Vector search performance during peak usage | Performance | ES Section 6.2.2 | Engineering | ⏳ Open | |
| OPEN-042 | Database migration between MongoDB versions | Operations | ES Section 6.2.2 | DevOps | ⏳ Open | |

---

## 📋 BY CATEGORY SUMMARY

| Category | Critical | High | Medium | Low | Total |
|----------|----------|------|--------|-----|-------|
| Testing | 1 | 0 | 1 | 0 | 2 |
| Infrastructure | 1 | 2 | 4 | 0 | 7 |
| Compliance | 1 | 2 | 4 | 3 | 10 |
| AI Configuration | 0 | 4 | 0 | 0 | 4 |
| Architecture | 0 | 2 | 0 | 0 | 2 |
| Resilience | 0 | 0 | 3 | 0 | 3 |
| Security | 0 | 1 | 1 | 0 | 2 |
| Operations | 0 | 0 | 4 | 1 | 5 |
| Performance | 0 | 0 | 1 | 1 | 2 |
| UX | 0 | 0 | 1 | 0 | 1 |
| API | 0 | 0 | 0 | 3 | 3 |
| Integration | 0 | 1 | 0 | 0 | 1 |
| **TOTAL** | **3** | **12** | **19** | **8** | **42** |

---

## 🔄 HOW TO USE THIS TRACKER

### When Processing a New Gap:

1. **During Stage 2 (Quality Assessment)**
   - Review engineering spec for "OPEN QUESTIONS" sections
   - Note any areas I identify as "Areas Needing Attention"
   - Add all items to this tracker with appropriate priority

2. **During Stage 4 (Final Specs)**
   - Review open items related to the gap
   - Mark any resolved items as ✅ Resolved
   - Add new items discovered during spec creation

3. **Before MVP Release**
   - All P0 (Critical) items must be ✅ Resolved
   - All P1 (High) items should be addressed or have a plan

### Status Values:

| Status | Meaning |
|--------|---------|
| ⏳ Open | Not yet addressed |
| 🔄 In Progress | Being worked on |
| ✅ Resolved | Completed and documented |
| 🚫 Deferred | Intentionally postponed to future phase |
| ❌ Won't Fix | Decided not to address (with reason) |

---

## 📝 RESOLUTION TEMPLATE

When resolving an item, update it like this:

```markdown
| OPEN-XXX | [Item description] | Category | Source | Owner | ✅ Resolved | **Resolution**: [How it was resolved]. **Doc**: [Link to document/decision] |
```

---

## 🆕 ADDING NEW ITEMS

When you discover a new open item, add it using this template:

```markdown
| OPEN-XXX | **[Brief title]** - [Detailed description of what needs to be decided/defined] | [Category] | [Where discovered] | [Team/Role] | ⏳ Open | [Notes] |
```

Priority guidelines:
- **P0 Critical**: Blocks MVP launch
- **P1 High**: Blocks Phase 1 completion
- **P2 Medium**: Should address during implementation
- **P3 Low**: Can address post-MVP

---

## 📅 REVIEW SCHEDULE

| When | Action |
|------|--------|
| After each Stage 4 | Add new items from that gap |
| Weekly | Review P0/P1 items for progress |
| Before each Phase | Ensure appropriate items are resolved |
| MVP Review | All P0 items must be ✅ |

---

## 🔗 RELATED DOCUMENTS

- `PIPELINE_TRACKER.md` - Gap processing progress
- `MVP_PRIORITY_GAPS.md` - Gap definitions
- `MASTER_SKILL_REGISTRY.md` - Skills being built
- Engineering Specs (`ES-*.md`) - Source of open questions

---

**Next Review**: After GAP-HOAI-001 Stage 4 completion


