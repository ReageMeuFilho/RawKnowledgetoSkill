# Master Capability Registry

> **Single index** for ALL skills, tools, integrations, data, and MEMORY across ALL verticals
> **Last Updated**: January 2026
> **Production Platform**: Kortix/Suna (Apache 2.0)
> **Brand**: Reage

---

## 🚀 Quick Links

| Document | Purpose |
|----------|---------|
| [SUNA_MAPPING.md](../docs/implementation/SUNA_MAPPING.md) | How specs map to Kortix/Suna code |
| [ENGINEER_QUICKSTART.md](../docs/implementation/ENGINEER_QUICKSTART.md) | Engineer implementation guide |

---

## 📊 Registry Statistics

| Metric | Core | Shared | STR | LTR | HOA | Total |
|--------|------|--------|-----|-----|-----|-------|
| Skills | 0 | 0 | 0 | 0 | 0 | 0 |
| Tools | 0 | 0 | 0 | 0 | 0 | 0 |
| Integrations | 0 | 0 | 0 | 0 | 0 | 0 |
| Data Objects | 0 | 0 | 0 | 0 | 0 | 0 |
| Memory Types | 0 | 0 | 0 | 0 | 0 | 0 |

---

## 🏗️ Registry Structure

```
registry/
├── MASTER_REGISTRY.md              ← You are here (index)
│
├── CAPABILITY REGISTRIES:
│   ├── MASTER_SKILL_REGISTRY.md    ← What agents CAN DO
│   ├── MASTER_TOOL_REGISTRY.md     ← Deterministic functions + Build/Buy decisions
│   ├── MASTER_INTEGRATION_REGISTRY.md  ← External systems (APIs, services)
│   ├── MASTER_DATA_REGISTRY.md     ← Data schemas and entities
│   └── MASTER_MEMORY_REGISTRY.md   ← State/Memory specifications
│
├── BEHAVIORAL REGISTRIES:
│   ├── MASTER_GUARDRAILS_REGISTRY.md   ← Safety rules (what agents CANNOT do)
│   ├── MASTER_PROMPTS_REGISTRY.md      ← System prompts, personas, tone
│   └── MASTER_WORKFLOWS_REGISTRY.md    ← Multi-step conversation flows
│
├── ACTIVATION REGISTRIES:
│   └── MASTER_TRIGGERS_REGISTRY.md     ← Events that start agent activity
│
├── VALIDATION REGISTRIES:
│   └── MASTER_EVALS_REGISTRY.md        ← Test cases and success metrics
│
├── ORGANIZED BY VERTICAL:
│   ├── core/                       # TIER 1: Universal (ALL verticals)
│   │   ├── SKILLS.md
│   │   ├── TOOLS.md
│   │   ├── INTEGRATIONS.md
│   │   └── DATA.md
│   │
│   ├── shared/                     # TIER 2: Cross-Vertical (2+ verticals)
│   │   ├── SKILLS.md
│   │   ├── TOOLS.md
│   │   └── VERTICAL_MAP.md
│   │
│   └── verticals/                  # TIER 3: Vertical-Specific
│       ├── str/SKILLS.md           # STR-only
│       ├── ltr/SKILLS.md           # LTR-only
│       └── hoa/SKILLS.md           # HOA-only
│
└── IMPLEMENTATION GUIDES:
    └── ../docs/implementation/
        ├── SUNA_MAPPING.md         ← Spec → Code mapping
        └── ENGINEER_QUICKSTART.md  ← Implementation guide
```

---

## 📋 Skills Quick Reference

### CORE Skills (All Verticals Use)

| ID | Skill Name | Description | Status |
|----|------------|-------------|--------|
| | | | |

### SHARED Skills (Multiple Verticals)

| ID | Skill Name | Verticals | Description | Status |
|----|------------|-----------|-------------|--------|
| | | | | |

### STR-Specific Skills

| ID | Skill Name | Description | Status |
|----|------------|-------------|--------|
| | | | |

### LTR-Specific Skills

| ID | Skill Name | Description | Status |
|----|------------|-------------|--------|
| | | | |

### HOA-Specific Skills

| ID | Skill Name | Description | Status |
|----|------------|-------------|--------|
| | | | |

---

## 🔧 Tools Quick Reference

### CORE Tools (All Verticals Use)

| ID | Tool Name | Purpose | Status |
|----|-----------|---------|--------|
| | | | |

### SHARED Tools (Multiple Verticals)

| ID | Tool Name | Verticals | Purpose | Status |
|----|-----------|-----------|---------|--------|
| | | | | |

---

## 🔌 Integrations Quick Reference

### CORE Integrations

| ID | Integration | Purpose | Status |
|----|-------------|---------|--------|
| | | | |

### Vertical-Specific Integrations

| ID | Integration | Vertical | Purpose | Status |
|----|-------------|----------|---------|--------|
| | | | | |

---

## 📈 Vertical Overlap Matrix

| Capability Type | STR | LTR | HOA | Notes |
|-----------------|-----|-----|-----|-------|
| Communication | ✅ | ✅ | ✅ | CORE |
| Payments | ✅ | ✅ | ✅ | CORE |
| Maintenance | ✅ | ✅ | ✅ | SHARED |
| Vendor Mgmt | ✅ | ✅ | ✅ | SHARED |
| Rent Collection | ✅ | ✅ | ❌ | SHARED (STR+LTR) |
| Turnover/Cleaning | ✅ | ❌ | ❌ | STR-SPECIFIC |
| Dynamic Pricing | ✅ | ❌ | ❌ | STR-SPECIFIC |
| Lease Management | ❌ | ✅ | ❌ | LTR-SPECIFIC |
| Tenant Screening | ❌ | ✅ | ❌ | LTR-SPECIFIC |
| Board Voting | ❌ | ❌ | ✅ | HOA-SPECIFIC |
| Assessments | ❌ | ❌ | ✅ | HOA-SPECIFIC |

---

## 🔍 How to Use This Registry

### Adding New Capabilities

1. **Check CORE first** - Is this used by ALL verticals?
2. **Check SHARED next** - Is this used by 2+ verticals?
3. **Check vertical-specific** - Is this used by only 1 vertical?
4. **Add to appropriate registry**

### Searching for Existing

1. Search this index first
2. Then drill into specific registry files
3. Use consistent ID prefixes:
   - `CORE-XXX` for core
   - `SHARED-XXX` for shared
   - `STR-XXX`, `LTR-XXX`, `HOA-XXX` for vertical-specific

### Promoting Capabilities

If a capability starts as vertical-specific but later another vertical needs it:
1. Move from `verticals/[old]/` to `shared/`
2. Update ID from `[VERT]-XXX` to `SHARED-XXX`
3. Update all references

