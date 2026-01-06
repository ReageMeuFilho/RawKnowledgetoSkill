# Research Prompt: Phase 1 Group 6 - Cross-Cutting Platform Features

## 🎯 RESEARCH OBJECTIVE

Research and document the **4 cross-cutting platform skills**. These are foundational capabilities that every other skill depends on - permissions, audit logging, notifications, and analytics.

---

## 📋 SKILLS TO RESEARCH

| Skill ID | Name | Priority | Category |
|----------|------|----------|----------|
| SKILL-059 | permission-management | P0 | cross-cutting |
| SKILL-060 | audit-logging | P0 | cross-cutting |
| SKILL-061 | notification-management | P0 | cross-cutting |
| SKILL-042 | analytics-dashboard | P0 | analytics |

---

## 🏢 PLATFORMS TO ANALYZE

### Primary (Best-in-Class)
| Platform | Why | Focus Areas |
|----------|-----|-------------|
| **Guesty** | Enterprise RBAC | Team permissions, roles |
| **AppFolio** | Compliance-grade audit | Audit trails, SOC 2 |
| **Hostaway** | Analytics excellence | KPI dashboards |

### Secondary
| Platform | Focus |
|----------|-------|
| Cloudbeds | Hotel-grade permissions |
| OwnerRez | Owner-specific access |
| Baselane | Financial analytics |

### Industry Standards (Technical Sources)
| Source | Focus |
|--------|-------|
| Auth0 | RBAC patterns |
| DataDog/NewRelic | Observability |
| Mixpanel/Amplitude | Product analytics |

---

## 📚 RESEARCH QUESTIONS BY SKILL

### SKILL-059: Permission Management

**Core Questions:**
1. What user roles exist in property management?
2. How is Role-Based Access Control (RBAC) structured?
3. What permissions are property-level vs portfolio-level?
4. How are team hierarchies managed?
5. What's the owner vs PM access model?

**Technical Questions:**
- RBAC data model?
- Permission inheritance (role → user)?
- Resource-level permissions (property, booking)?
- API-level authorization?
- Permission caching strategy?

**Standard Roles:**
| Role | Typical Permissions |
|------|---------------------|
| Owner | Read own properties, view reports |
| Property Manager | Full access to assigned properties |
| Team Member | Tasks, messages, limited financial |
| Cleaner/Vendor | Task-specific, mobile app |
| Accountant | Financial data, read-only |
| Admin | Full system access |

**Multi-Tenancy:**
- Portfolio/company level isolation
- Property group permissions
- Cross-portfolio access for enterprise

**Sources to Check:**
- [ ] Guesty team management documentation
- [ ] Auth0 RBAC best practices
- [ ] AppFolio user roles
- [ ] YouTube: "property management team access"
- [ ] SOC 2 access control requirements
- [ ] NIST access control guidelines

---

### SKILL-060: Audit Logging

**Core Questions:**
1. What events must be logged for compliance?
2. What data is captured per audit event?
3. How long are logs retained?
4. How are logs searched and queried?
5. What alerting exists for suspicious activity?

**Technical Questions:**
- Audit log schema?
- Write path (sync vs async)?
- Storage and retention strategy?
- Immutability guarantees?
- PII handling in logs?

**Events to Log:**
| Category | Events |
|----------|--------|
| Authentication | Login, logout, failed attempts, password changes |
| Authorization | Permission changes, role assignments |
| Data Access | View sensitive data, export reports |
| Financial | Payments, refunds, payout changes |
| Configuration | Settings changes, rate updates |
| AI Actions | HITL decisions, agent actions |

**Compliance Requirements:**
| Framework | Logging Requirements |
|-----------|---------------------|
| SOC 2 | Activity logs, access reviews |
| PCI DSS | Cardholder data access |
| GDPR/LGPD | Data access and deletion |
| SOX | Financial transaction trails |

**Sources to Check:**
- [ ] AppFolio audit trail features
- [ ] SOC 2 logging requirements
- [ ] OWASP logging best practices
- [ ] ELK Stack patterns
- [ ] AWS CloudTrail patterns
- [ ] YouTube: "compliance audit logging"

---

### SKILL-061: Notification Management

**Core Questions:**
1. What notification channels are supported (email, SMS, push, in-app)?
2. What events trigger notifications?
3. How do users configure notification preferences?
4. How is notification delivery tracked?
5. What templates are used?

**Technical Questions:**
- Notification routing architecture?
- Template engine (variables, conditionals)?
- Delivery status tracking?
- Rate limiting and throttling?
- Fallback channels?

**Notification Categories:**
| Category | Events | Default Channel |
|----------|--------|-----------------|
| Booking | New, modified, cancelled | Email + Push |
| Payment | Received, failed, payout | Email |
| Task | Assigned, due, overdue | Push + SMS |
| Message | New guest message | Push + Email |
| System | Sync errors, alerts | In-app + Email |

**User Preferences:**
- Per-channel toggles
- Per-category settings
- Quiet hours
- Digest vs immediate
- Language preference

**Sources to Check:**
- [ ] Guesty notification settings
- [ ] SendGrid/Twilio documentation
- [ ] Firebase Push Notifications
- [ ] YouTube: "notification system design"
- [ ] Product notification UX best practices

---

### SKILL-042: Analytics Dashboard

**Core Questions:**
1. What KPIs are essential for property managers?
2. How is data aggregated (property, portfolio, time period)?
3. What visualizations are most useful?
4. What benchmarking is available?
5. What export/reporting options exist?

**Technical Questions:**
- Data warehouse architecture?
- Real-time vs batch analytics?
- Dashboard framework (Metabase, custom)?
- Caching strategy for dashboards?
- Mobile dashboard support?

**Essential KPIs:**
| Category | Metrics |
|----------|---------|
| Revenue | Total revenue, RevPAR, ADR |
| Occupancy | Occupancy rate, booking pace |
| Operations | Response time, task completion |
| Financial | Collection rate, payout accuracy |
| Guest | Review score, repeat guests |

**Dashboard Views:**
- **Portfolio Overview**: All properties at a glance
- **Property Detail**: Deep dive single property
- **Financial Summary**: Revenue, expenses, payouts
- **Operations Health**: Task completion, response times
- **Channel Performance**: By OTA comparison

**Benchmarking:**
- Market comparison (AirDNA, PriceLabs data)
- YoY trends
- Seasonal patterns
- Competitive set

**Sources to Check:**
- [ ] Guesty analytics documentation
- [ ] Hostaway reporting features
- [ ] AirDNA market data
- [ ] PriceLabs portfolio analytics
- [ ] YouTube: "vacation rental analytics"
- [ ] Metabase/Looker patterns

---

## 📄 OUTPUT REQUIREMENTS

### Document Structure

```markdown
# Knowledge Document: Cross-Cutting Platform Features
## Phase 1 Group 6 | Skills: SKILL-059, 060, 061, 042

## 1. Executive Summary
   - Platform foundation capabilities
   - Compliance requirements
   - User experience principles

## 2. Platform Architecture Overview
   - How cross-cutting services integrate
   - Dependency diagram
   - Performance considerations

## 3. SKILL-059: Permission Management
   ### 3.1 RBAC Data Model
   ### 3.2 Standard Roles & Permissions
   ### 3.3 Resource-Level Access
   ### 3.4 Multi-Tenancy Model
   ### 3.5 API Authorization
   ### 3.6 Permission UI/UX

## 4. SKILL-060: Audit Logging
   ### 4.1 Event Taxonomy
   ### 4.2 Log Schema
   ### 4.3 Storage & Retention
   ### 4.4 Query & Search
   ### 4.5 Compliance Mapping
   ### 4.6 Alerting Rules

## 5. SKILL-061: Notification Management
   ### 5.1 Channel Architecture
   ### 5.2 Event → Notification Mapping
   ### 5.3 Template System
   ### 5.4 User Preferences
   ### 5.5 Delivery Tracking
   ### 5.6 Fallback Logic

## 6. SKILL-042: Analytics Dashboard
   ### 6.1 KPI Framework
   ### 6.2 Data Model
   ### 6.3 Dashboard Layouts
   ### 6.4 Visualization Types
   ### 6.5 Export & Reporting
   ### 6.6 Benchmarking

## 7. Integration Patterns
   - How permissions flow through system
   - Audit logging hooks
   - Notification triggers
   - Analytics data collection

## 8. Compliance Matrix
   - SOC 2 requirements mapping
   - GDPR/LGPD considerations
   - PCI DSS (if applicable)

## 9. References
   - 30+ citations
```

### Quality Targets

| Metric | Target |
|--------|--------|
| Document Length | 400-550 lines |
| Citations | 30+ sources |
| Data Models | RBAC schema, audit log schema |
| Compliance Coverage | SOC 2, GDPR, PCI |
| KPI List | 15+ metrics defined |

---

## 💾 SAVE LOCATION

```
knowledge/platform/KD-PHASE1-G6-cross-cutting.md
```

---

## ✅ COMPLETION CHECKLIST

- [ ] All 4 skills researched
- [ ] RBAC model documented
- [ ] Audit events taxonomy defined
- [ ] Notification channels mapped
- [ ] KPI framework created
- [ ] Compliance requirements mapped
- [ ] 30+ sources cited

---

## 🚀 AFTER COMPLETING

```bash
git add -A
git commit -m "Stage 1 COMPLETE: Phase 1 Group 6 - Cross-Cutting Platform Features (4 skills)"
git push
```

