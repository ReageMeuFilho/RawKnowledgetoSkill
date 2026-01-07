# Research Prompt: Phase 2 Group 5 - Enterprise Operations

> **For**: AI Research Agent
> **Output**: Knowledge Document → `knowledge/operations/KD-PHASE2-G5-enterprise-operations.md`
> **Priority**: Medium (Scale enabler)
> **Date**: January 2026

---

## 🎯 Research Objective

Research and document comprehensive knowledge for implementing **8 Enterprise Operations skills** that enable multi-brand, multi-region operations at scale with advanced vendor and staff management.

---

## 📋 Skills to Research

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| SKILL-057 | multi-brand-management | operations | Multi-brand property management |
| SKILL-058 | regional-access-control | operations | Regional/portfolio access controls |
| SKILL-089 | staff-shift-planning | operations | Staff scheduling and shift management |
| SKILL-116 | portfolio-rollup-reporting | operations | Consolidated portfolio reporting |
| SKILL-117 | sla-monitoring | operations | SLA tracking and alerts |
| SKILL-118 | vendor-scorecard | operations | Vendor performance scorecards |
| SKILL-119 | inventory-forecasting | operations | Supply inventory forecasting |
| SKILL-120 | bulk-operations | operations | Bulk rate/content updates |

---

## 🔍 Research Questions Per Skill

### SKILL-057: Multi-Brand Management

**Key Questions**:
1. How do enterprise PMs manage multiple brands (luxury, budget, boutique)?
2. What configuration differs by brand (messaging tone, pricing strategy)?
3. How do you maintain brand consistency across properties?
4. What reporting separates brand performance?
5. How do you handle shared resources across brands?
6. What white-label capabilities are needed?

**Research Sources**:
- Guesty multi-brand features
- Hostaway portfolio management
- Hotel brand management (Marriott, Hilton portfolios)
- Enterprise PM case studies
- White-label platform architectures

### SKILL-058: Regional Access Control

**Key Questions**:
1. How do you structure regional/territorial access?
2. What permissions differ by region (view, edit, finance)?
3. How do you handle cross-region properties?
4. What audit trail is needed for regional actions?
5. How do you manage regional managers vs. central operations?
6. What compliance requirements exist per region?

**Research Sources**:
- Enterprise RBAC patterns
- Guesty team management
- Multi-tenant SaaS architectures
- Geographic data access controls
- Franchise management systems

### SKILL-089: Staff Shift Planning

**Key Questions**:
1. What scheduling algorithms optimize staff coverage?
2. How do you handle availability, preferences, and skills?
3. What labor law constraints apply (overtime, breaks)?
4. How do you integrate with payroll systems?
5. What mobile features do staff need for scheduling?
6. How do you handle last-minute shift changes?

**Research Sources**:
- When I Work scheduling
- Deputy workforce management
- Homebase scheduling
- Hotel staff scheduling systems
- Labor scheduling optimization research

### SKILL-116: Portfolio Rollup Reporting

**Key Questions**:
1. What metrics aggregate well across portfolios?
2. How do you normalize data across different property types?
3. What drill-down capabilities are needed?
4. How do you handle different currencies in rollups?
5. What visualization works for portfolio overview?
6. How frequently should rollups refresh?

**Research Sources**:
- Guesty analytics rollup
- AppFolio portfolio reporting
- Financial consolidation systems
- BI dashboard best practices
- STR portfolio management guides

### SKILL-117: SLA Monitoring

**Key Questions**:
1. What SLAs matter for STR operations (response time, cleaning)?
2. How do you define and track SLA compliance?
3. What alerting prevents SLA breaches?
4. How do you report SLA performance to stakeholders?
5. What penalties/escalations apply to SLA violations?
6. How do you handle SLA exceptions?

**Research Sources**:
- Service management frameworks (ITIL)
- Hotel SLA standards
- Property management SLAs
- Monitoring and alerting systems
- SLA dashboard examples

### SKILL-118: Vendor Scorecard

**Key Questions**:
1. What metrics evaluate vendor performance (quality, timeliness, cost)?
2. How do you collect vendor feedback from staff?
3. What scoring methodology is fair and actionable?
4. How do you use scorecards for vendor selection?
5. What visibility do vendors have to their scores?
6. How do you handle underperforming vendors?

**Research Sources**:
- Vendoroo vendor management
- Procurement scorecard systems
- Supplier performance management
- Hotel vendor evaluation
- Cleaning vendor assessment

### SKILL-119: Inventory Forecasting

**Key Questions**:
1. What supplies need inventory management (linens, amenities)?
2. How do you forecast consumption based on bookings?
3. What reorder points and lead times apply?
4. How do you integrate with supplier ordering?
5. What waste reduction strategies exist?
6. How do you handle seasonal inventory fluctuations?

**Research Sources**:
- Hotel inventory management
- Supply chain forecasting
- Hospitality procurement
- Just-in-time inventory systems
- STR supply management guides

### SKILL-120: Bulk Operations

**Key Questions**:
1. What operations benefit from bulk processing (rate updates, content)?
2. How do you handle partial failures in bulk operations?
3. What validation runs before bulk commits?
4. How do you preview bulk changes before applying?
5. What undo/rollback capabilities are needed?
6. How do you handle rate limiting across channels?

**Research Sources**:
- Guesty bulk editing
- Hostaway mass updates
- Database bulk operation patterns
- ETL/batch processing architectures
- Channel manager bulk sync

---

## 🏗️ Architecture Context

### Dependencies (From Phase 1)
- **SKILL-017-022**: Operations Basics (task management)
- **SKILL-059**: Permission Management (RBAC foundation)
- **SKILL-060**: Audit Logging (compliance)

### Technology Stack
| Component | Technology | Purpose |
|-----------|------------|---------|
| RBAC | PostgreSQL + Redis | Access control |
| Scheduling | Temporal | Shift workflows |
| Reporting | Metabase/Custom | Dashboards |
| Bulk Ops | Celery + Redis | Background processing |
| Inventory | PostgreSQL | Stock tracking |

### MCP Servers Required
```yaml
mcp_servers:
  - mcp://operations/bulk-update
  - mcp://operations/schedule
  - mcp://vendor/scorecard
  - mcp://analytics/rollup
  - mcp://inventory/forecast
```

---

## 📄 Output Format

Create a comprehensive knowledge document with:

1. **Executive Summary**
2. **Skill-by-Skill Analysis** (8 skills)
3. **Enterprise Architecture** - Multi-tenant, multi-brand
4. **Access Control Design** - RBAC hierarchy
5. **Scheduling System** - Algorithm, constraints
6. **Vendor Management** - Scorecard methodology
7. **Bulk Operations** - Processing patterns, failure handling
8. **Competitive Comparison**
9. **Implementation Priorities**
10. **Open Questions**

**Quality Requirements**:
- Minimum 2,200 lines
- At least 30 citations/sources
- Include org hierarchy diagrams
- Include scheduling algorithms

---

## 📤 Delivery Instructions

1. Save to: `knowledge/operations/KD-PHASE2-G5-enterprise-operations.md`
2. Update: `docs/PHASE2_SKILL_TRACKER.md`
3. Notify: Ready for Stage 2

---

**Focus**: Enable operations at massive scale! 🏢

