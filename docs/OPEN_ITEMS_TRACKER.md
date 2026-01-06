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
║   ✅ Resolved (Internal): 9  ← Found in existing specs!                               ║
║   🔴 Critical (P0):        3  (2 need research)                                        ║
║   🟠 High (P1):           12  (7 need research)                                        ║
║   🟡 Medium (P2):         19                                                           ║
║   🟢 Low (P3):             8                                                           ║
║                                                                                        ║
║   📋 RESEARCH PROMPT READY: docs/prompts/RESEARCH_PROMPT_OPEN_ITEMS_INFRASTRUCTURE.md  ║
║                                                                                        ║
╚═══════════════════════════════════════════════════════════════════════════════════════╝
```

---

## ✅ RESOLVED ITEMS (Found in Existing Specs!)

These items were answered in our 87,000+ lines of engineering specifications:

| ID | Item | Resolution | Source |
|----|------|------------|--------|
| **OPEN-004** | Voice Model Selection | **ConversationRelay + Deepgram + ElevenLabs + Google STT + Amazon Polly** | ES-HOAI-004 §1.1.1, §3.4.2 |
| **OPEN-005** | LLM Model Assignments | **Claude 3.5 Sonnet (200K context)** for conversation, streaming responses | ES-HOAI-004 §3.4.2 |
| **OPEN-011** | FastAPI vs Flask | **FastAPI for voice/async (ES-HOAI-004), Flask for other services (ES-VEN-001, ES-GW-001)** | Multiple specs |
| **OPEN-013** | Microservices vs monolith | **Microservices with event-driven communication** | ES-HOAI-004 §5.1.1 |
| **OPEN-014** | Encryption requirements | **AES-256 at rest, TLS 1.3 in transit, SRTP for voice** | ES-HOAI-004 §3.7.1, ES-VEN-001 |
| **OPEN-015** | MongoDB Atlas vs self-managed | **MongoDB Atlas with Vector Search** | ES-HOAI-004 §3.5.1 |
| **OPEN-016** | Voice agent latency | **Sub-second target: ASR <300ms, TTS <1s** | ES-HOAI-004 §1.2.3 |
| **OPEN-017** | Circuit breaker thresholds | **Circuit breakers activate at 1000 concurrent requests** | ES-VEN-001 §Performance |
| **OPEN-022** | Service mesh | **mTLS for service-to-service, RBAC for access control** | ES-VEN-001 |

### Testing Strategy (OPEN-001) - PARTIALLY RESOLVED:
| Aspect | Resolution | Source |
|--------|------------|--------|
| Framework | **pytest + pytest-asyncio** | ES-HOAI-004 §6.6.1 |
| Coverage | **80% minimum code coverage** | ES-HOAI-004 §3.6.4 |
| Voice Testing | **Custom audio fixtures, >90% coverage** | ES-HOAI-004 §6.6.1 |
| E2E Testing | **Playwright** | ES-HOAI-004 §3.6.4 |
| CI/CD | **GitHub Actions with quality gates** | ES-HOAI-004 §3.6.4 |

**Still Needed for OPEN-001**: AI agent testing methodology (evaluation sets, conversation testing)

---

## 🔴 CRITICAL ITEMS (P0) - Must Address Before MVP

### Remaining Critical Items

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-001 | **Testing Strategy** - AI agent testing methodology (evaluation sets, conversation quality testing) | Testing | Quality Assessment | Engineering | 🔄 Partially Resolved | Framework decided, need AI-specific approach |
| OPEN-002 | **Deployment Environment** - AWS vs GCP vs Azure decision. ECS vs EKS not specified. Environment configs (dev/staging/prod) not defined | Infrastructure | Quality Assessment | DevOps | ⏳ **NEEDS RESEARCH** | Research prompt created |
| OPEN-003 | **Data Retention Period** - Specific retention period for audit logs and HITL decisions not defined | Compliance | ES Section 1.3.2 | Legal/Compliance | ⏳ **NEEDS RESEARCH** | Research prompt created |

---

## 🟠 HIGH PRIORITY ITEMS (P1) - Address Before Phase 1

### Remaining High Priority Items

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| OPEN-006 | **Prompt Templates** - Prompt library for each agent type not defined | AI Configuration | Quality Assessment | AI/Engineering | ⏳ **NEEDS RESEARCH** | Research prompt created |
| OPEN-007 | **Fine-tuning Strategy** - Whether/how to fine-tune models for property management domain | AI Configuration | Quality Assessment | AI/Engineering | ⏳ **NEEDS RESEARCH** | Research prompt created |
| OPEN-008 | Compliance frameworks beyond NIST AI RMF (SOX, HIPAA, GDPR) | Compliance | ES Section 1.3.2 | Legal | ⏳ **NEEDS RESEARCH** | Research prompt created |
| OPEN-009 | State-level CAM regulations for policy engine | Compliance | ES Section 1.3.2 | Legal | ⏳ **NEEDS RESEARCH** | Research prompt created |
| OPEN-010 | Integration with existing CRM systems beyond Vantaca | Integration | ES Section 1.3.2 | Product | ⏳ **NEEDS RESEARCH** | Research prompt created |
| OPEN-012 | Deployment target: AWS ECS, EKS, or EC2 | Infrastructure | ES Section 3.6.5 | DevOps | ⏳ **NEEDS RESEARCH** | Linked to OPEN-002 |

### Resolved High Priority Items ✅

| ID | Item | Resolution |
|----|------|------------|
| ~~OPEN-004~~ | Voice Model Selection | ✅ ConversationRelay + Deepgram + ElevenLabs + Google STT |
| ~~OPEN-005~~ | LLM Model Assignments | ✅ Claude 3.5 Sonnet (200K context) |
| ~~OPEN-011~~ | FastAPI vs Flask | ✅ FastAPI for voice, Flask for other services |
| ~~OPEN-013~~ | Microservices vs monolith | ✅ Microservices with event-driven |
| ~~OPEN-014~~ | Encryption requirements | ✅ AES-256 at rest, TLS 1.3 in transit |
| ~~OPEN-015~~ | MongoDB Atlas vs self-managed | ✅ MongoDB Atlas with Vector Search |

---

## 🟡 MEDIUM PRIORITY ITEMS (P2) - Address During Implementation

| ID | Item | Category | Source | Owner | Status | Notes |
|----|------|----------|--------|-------|--------|-------|
| ~~OPEN-016~~ | Maximum latency for voice agent | Performance | ES Section 4.3.4 | Engineering | ✅ **Resolved** | ASR <300ms, TTS <1s |
| ~~OPEN-017~~ | Circuit breaker failure thresholds | Resilience | ES Section 4.3.4 | Engineering | ✅ **Resolved** | 1000 concurrent |
| OPEN-018 | Partial failure handling - compensation vs retry | Resilience | ES Section 4.3.4 | Engineering | ⏳ Open | Research prompt |
| OPEN-019 | HITL dashboard real-time collaboration features | UX | ES Section 4.3.4 | Product | ⏳ Open | Research prompt |
| OPEN-020 | Conversation transcript data retention | Compliance | ES Section 4.3.4 | Legal | ⏳ Open | Linked to OPEN-003 |
| OPEN-021 | Predictive scaling based on historical patterns | Infrastructure | ES Section 4.3.4 | DevOps | ⏳ Open | Research prompt |
| ~~OPEN-022~~ | Service mesh (Istio/Linkerd) | Security | ES Section 5.4.6 | DevOps | ✅ **Resolved** | mTLS + RBAC |
| OPEN-023 | Agent state persistence during system upgrades | Operations | ES Section 5.4.6 | Engineering | ⏳ Open | Research prompt |
| OPEN-024 | Real-time policy updates without service restart | Operations | ES Section 5.4.6 | Engineering | ⏳ Open | Research prompt |
| OPEN-025 | Maximum acceptable RPO for conversation history | DR | ES Section 5.4.6 | DevOps | ⏳ Open | Research prompt |
| OPEN-026 | Maximum recovery time for critical system failures | DR | ES Section 6.9.3 | DevOps | ⏳ Open | Research prompt |
| OPEN-027 | Predictive failure detection based on error patterns | Operations | ES Section 6.9.3 | Engineering | ⏳ Open | Research prompt |
| OPEN-028 | Automated recovery level without human oversight | Operations | ES Section 6.9.3 | Engineering | ⏳ Open | Research prompt |
| OPEN-029 | Cascading failure handling across components | Resilience | ES Section 6.9.3 | Engineering | ⏳ Open | Research prompt |
| OPEN-030 | Error logging compliance requirements | Compliance | ES Section 6.9.3 | Legal | ⏳ Open | Research prompt |
| OPEN-031 | Chaos engineering for resilience testing | Testing | ES Section 6.9.3 | QA | ⏳ Open | Research prompt |
| OPEN-032 | Container orchestration: Kubernetes vs Docker Swarm | Infrastructure | ES Section 6.3.5 | DevOps | ⏳ Open | Linked to OPEN-002 |
| OPEN-033 | Multi-region deployment for disaster recovery | Infrastructure | ES Section 6.3.5 | DevOps | ⏳ Open | Research prompt |
| OPEN-034 | Data residency and cross-border transfer requirements | Compliance | ES Section 6.3.5 | Legal | ⏳ Open | Research prompt |

---

## 🟢 LOW PRIORITY ITEMS (P3) - Address Post-MVP

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

## 📋 BY CATEGORY SUMMARY (Updated)

| Category | Resolved | Critical | High | Medium | Low | Total |
|----------|----------|----------|------|--------|-----|-------|
| Testing | 1 (partial) | 1 | 0 | 1 | 0 | 3 |
| Infrastructure | 0 | 1 | 1 | 3 | 0 | 5 |
| Compliance | 0 | 1 | 2 | 3 | 2 | 8 |
| AI Configuration | 2 | 0 | 2 | 0 | 0 | 4 |
| Architecture | 2 | 0 | 0 | 0 | 0 | 2 |
| Resilience | 1 | 0 | 0 | 2 | 0 | 3 |
| Security | 2 | 0 | 0 | 0 | 0 | 2 |
| Operations | 0 | 0 | 0 | 4 | 1 | 5 |
| Performance | 1 | 0 | 0 | 0 | 1 | 2 |
| UX | 0 | 0 | 0 | 1 | 0 | 1 |
| API | 0 | 0 | 0 | 0 | 3 | 3 |
| Integration | 0 | 0 | 1 | 0 | 1 | 2 |
| DR | 0 | 0 | 0 | 2 | 0 | 2 |
| **TOTAL** | **9** | **3** | **6** | **16** | **8** | **42** |

---

## 📚 RESEARCH PROMPT CREATED

A comprehensive research prompt has been created to address remaining open items:

**File**: `docs/prompts/RESEARCH_PROMPT_OPEN_ITEMS_INFRASTRUCTURE.md`

**Sections Covered**:
1. Deployment Environment & Cloud Strategy (OPEN-002, OPEN-012)
2. Data Retention & Audit Policy (OPEN-003)
3. Prompt Engineering Library (OPEN-006)
4. Fine-Tuning Strategy (OPEN-007)
5. Compliance & Regulatory (OPEN-008, OPEN-009)
6. CRM & Third-Party Integrations (OPEN-010)
7. Disaster Recovery & Business Continuity (OPEN-025, OPEN-026, OPEN-033)
8. Remaining Medium/Low Priority Items

**Expected Output**: 800-1,200 line knowledge document with 50+ citations

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
- **NEW**: `docs/prompts/RESEARCH_PROMPT_OPEN_ITEMS_INFRASTRUCTURE.md` - Research prompt for remaining items

---

**Next Action**: Research Agent to produce `knowledge/infrastructure/KD-OPEN-ITEMS-infrastructure-compliance.md`
