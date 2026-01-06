# Competitive PRD → Unified Skill Registry

> **Goal**: Process multiple competitor PRDs, normalize overlapping features into a single Master Skill Registry, and identify the best source for each skill.

---

## 🎯 The Problem

Different competitors call the same feature different things:

| Competitor | What They Call It |
|------------|-------------------|
| **Guesty** | "Guest Messaging" |
| **Hostaway** | "Communication Center" |
| **Hospitable** | "Unified Inbox" |
| **Lodgify** | "Guest Communication Hub" |

**But it's all the same skill**: `guest-message-responder`

---

## 🔄 The Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│              COMPETITIVE PRD → UNIFIED SKILL REGISTRY                            │
└─────────────────────────────────────────────────────────────────────────────────┘

  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐
  │ Guesty  │  │Hostaway │  │Hospitable│ │ Lodgify │   ... more competitors
  │   PRD   │  │   PRD   │  │   PRD   │  │   PRD   │
  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘
       │            │            │            │
       ▼            ▼            ▼            ▼
  ┌─────────────────────────────────────────────────┐
  │           SKILL EXTRACTION (per PRD)            │
  │  • Extract raw features                         │
  │  • Assign temporary skill IDs                   │
  │  • Note competitor-specific terminology         │
  └─────────────────────────────────────────────────┘
                        │
                        ▼
  ┌─────────────────────────────────────────────────┐
  │           SKILL NORMALIZATION                   │
  │  • Match similar features across PRDs           │
  │  • Assign canonical skill name                  │
  │  • Map competitor terms → canonical term        │
  │  • Identify unique features (only 1 competitor) │
  └─────────────────────────────────────────────────┘
                        │
                        ▼
  ┌─────────────────────────────────────────────────┐
  │         MASTER SKILL REGISTRY                   │
  │  • Single source of truth                       │
  │  • Tracks which competitors have each skill     │
  │  • Identifies "best in class" for sourcing      │
  │  • Comprehensive feature set                    │
  └─────────────────────────────────────────────────┘
                        │
                        ▼
  ┌─────────────────────────────────────────────────┐
  │         SOURCING STRATEGY                       │
  │  • For each skill, learn from best implementer  │
  │  • Combine best practices from multiple sources │
  └─────────────────────────────────────────────────┘
```

---

## 📁 File Structure

```
RawKnowledgetoSkill/
│
├── competitors/                          # Competitor PRDs
│   ├── guesty/
│   │   ├── PRD.md                        # Full PRD
│   │   └── FEATURES_EXTRACTED.md         # Raw feature extraction
│   │
│   ├── hostaway/
│   │   ├── PRD.md
│   │   └── FEATURES_EXTRACTED.md
│   │
│   ├── hospitable/
│   │   ├── PRD.md
│   │   └── FEATURES_EXTRACTED.md
│   │
│   └── lodgify/
│       ├── PRD.md
│       └── FEATURES_EXTRACTED.md
│
├── registry/                             # Master Skill Registry
│   ├── MASTER_SKILL_REGISTRY.md          # The single source of truth
│   ├── SKILL_MAPPING.md                  # Competitor term → Canonical skill
│   ├── COMPETITIVE_MATRIX.md             # Who has what
│   └── BEST_IN_CLASS.md                  # Best source for each skill
│
├── products/                             # Your product definitions
│   └── str-pms/
│       ├── SKILL_INVENTORY.md            # Skills for YOUR product
│       └── SOURCE_PLAN.md
│
├── raw-knowledge/                        # Sourced knowledge
└── skills/                               # Generated skills
```

---

## 📋 Step-by-Step Process

### Step 1: Create Competitor PRDs

For each competitor, create a PRD document:

```markdown
# PRD: [Competitor Name]

## Overview
- **Product**: [Name]
- **Website**: [URL]
- **Target Market**: [Who they serve]
- **Pricing Model**: [How they charge]

## Features

### Category: Guest Communication
- **Feature**: [Feature Name]
  - Description: [What it does]
  - Capabilities: [Specific functions]
  - Limitations: [What it doesn't do]

### Category: Booking Management
- **Feature**: [Feature Name]
  ...
```

### Step 2: Extract Features → Raw Skills

For each PRD, extract features into a standard format:

```markdown
# Features Extracted: [Competitor]

| Feature ID | Competitor Feature Name | Category | Description |
|------------|------------------------|----------|-------------|
| GUES-001 | Guest Messaging | Communication | Send/receive messages |
| GUES-002 | Automated Responses | Communication | Auto-reply templates |
| GUES-003 | Smart Inbox | Communication | Unified message view |
```

### Step 3: Normalize → Master Registry

Match features across competitors:

```markdown
# Skill Mapping

## Canonical Skill: guest-message-responder

| Competitor | Their Feature Name | Feature ID |
|------------|-------------------|------------|
| Guesty | Guest Messaging | GUES-001 |
| Hostaway | Communication Center | HOST-003 |
| Hospitable | Unified Inbox | HOSP-001 |
| Lodgify | Guest Communication Hub | LODG-002 |

**Normalized Description**: Handle guest messages during all phases of stay
**Best Implementation**: Hospitable (most automation features)
```

### Step 4: Build Master Skill Registry

Single source of truth with all skills:

```markdown
# Master Skill Registry

| Skill ID | Canonical Name | Category | Competitors | Best Source |
|----------|---------------|----------|-------------|-------------|
| STR-001 | guest-inquiry-handler | Communication | G,H,Ho,L | Hospitable |
| STR-002 | guest-message-responder | Communication | G,H,Ho,L | Hospitable |
| STR-016 | dynamic-pricing-adjuster | Revenue | G,H | Guesty |
| STR-045 | vendor-marketplace | Operations | G only | Guesty |
```

---

## 🎯 Normalization Rules

### How to Match Features

1. **Same Function** = Same Skill
   - If two features do the same thing, they're the same skill
   - Ignore naming differences

2. **Superset/Subset** = One Skill with Tiers
   - Basic version: `skill-name-basic`
   - Advanced version: `skill-name-advanced`
   - Or just one skill with capability levels noted

3. **Unique Features** = New Skill
   - If only one competitor has it, still add to registry
   - Mark as "Unique: [Competitor]"

4. **Composite Features** = Multiple Skills
   - If a competitor bundles multiple functions, split into separate skills

### Matching Criteria

| Criteria | Weight |
|----------|--------|
| **Primary Function** | Must match |
| **Input/Output** | Should match |
| **User Story** | Should be similar |
| **Category** | Must match |

---

## 📊 Master Skill Registry Template

```markdown
# Master Skill Registry: STR PMS

> **Last Updated**: [Date]
> **Total Skills**: [Count]
> **Competitors Analyzed**: [List]

---

## Registry Format

### STR-001: guest-inquiry-handler

**Category**: Guest Communication
**Priority**: P0 (MVP)

**Description**: 
Respond to initial booking inquiries with property information, 
availability, and pricing.

**Competitor Coverage**:
| Competitor | Has Feature | Feature Name | Quality |
|------------|-------------|--------------|---------|
| Guesty | ✅ | Guest Messaging | ⭐⭐⭐⭐ |
| Hostaway | ✅ | Inquiry Response | ⭐⭐⭐ |
| Hospitable | ✅ | Smart Inbox | ⭐⭐⭐⭐⭐ |
| Lodgify | ✅ | Communication | ⭐⭐⭐ |

**Best Implementation**: Hospitable
**Why**: Most sophisticated AI-powered response suggestions, 
best template system, highest automation rate.

**Knowledge Sources**:
- Primary: Hospitable documentation + demo
- Secondary: Guesty templates

**Capabilities to Include**:
- [ ] Response templates
- [ ] AI suggestions (from Hospitable)
- [ ] Availability check (all have)
- [ ] Pricing quote generation (Guesty best)

---

### STR-016: dynamic-pricing-adjuster

**Category**: Revenue Management
**Priority**: P1

**Description**: 
Automatically adjust nightly rates based on demand, 
seasonality, and market conditions.

**Competitor Coverage**:
| Competitor | Has Feature | Feature Name | Quality |
|------------|-------------|--------------|---------|
| Guesty | ✅ | Revenue Management | ⭐⭐⭐⭐⭐ |
| Hostaway | ✅ | Dynamic Pricing | ⭐⭐⭐⭐ |
| Hospitable | ❌ | N/A | - |
| Lodgify | ⚠️ | Basic Pricing | ⭐⭐ |

**Best Implementation**: Guesty (via PriceLabs integration)
**Why**: Most sophisticated algorithm, best market data integration,
proven revenue increases.

**Knowledge Sources**:
- Primary: Guesty + PriceLabs documentation
- Secondary: Hostaway pricing guides

**Capabilities to Include**:
- [ ] Demand-based adjustments
- [ ] Competitor rate monitoring (Guesty)
- [ ] Event-based pricing (Guesty)
- [ ] Minimum stay optimization (Hostaway)
```

---

## 🔄 Workflow for Processing New Competitor PRD

When you give me a new competitor PRD:

### Step 1: Extract Features
```
Input: Competitor PRD
Output: FEATURES_EXTRACTED.md with all features listed
```

### Step 2: Match to Existing Registry
```
For each extracted feature:
  - Search Master Registry for matching skill
  - If match found: Add competitor to that skill's coverage
  - If no match: Create new skill entry
```

### Step 3: Update Competitive Matrix
```
Update COMPETITIVE_MATRIX.md to show:
  - Which competitors have which skills
  - Quality ratings
  - Best implementation designation
```

### Step 4: Update Sourcing Strategy
```
For new/improved skills:
  - Identify best source for knowledge
  - Add to SOURCE_PLAN.md
```

---

## 📈 Competitive Matrix View

```markdown
# Competitive Matrix: STR PMS Skills

| Skill | Guesty | Hostaway | Hospitable | Lodgify | Best |
|-------|--------|----------|------------|---------|------|
| guest-inquiry-handler | ✅ | ✅ | ✅⭐ | ✅ | Hospitable |
| guest-message-responder | ✅ | ✅ | ✅⭐ | ✅ | Hospitable |
| booking-creator | ✅⭐ | ✅ | ✅ | ✅ | Guesty |
| dynamic-pricing-adjuster | ✅⭐ | ✅ | ❌ | ⚠️ | Guesty |
| turnover-scheduler | ✅ | ✅⭐ | ❌ | ⚠️ | Hostaway |
| owner-statement-generator | ✅⭐ | ✅ | ❌ | ✅ | Guesty |
| channel-calendar-syncer | ✅ | ✅⭐ | ✅ | ✅ | Hostaway |

Legend:
✅ = Has feature
✅⭐ = Best implementation
⚠️ = Basic/limited
❌ = Doesn't have
```

---

## 🎯 Benefits of This Approach

1. **No Duplication**: Each skill exists once in registry
2. **Best of All Worlds**: Learn from best implementation of each feature
3. **Gap Identification**: See what competitors are missing
4. **Differentiation**: Identify unique skills only you will have
5. **Comprehensive Coverage**: Union of all competitor features
6. **Efficient Sourcing**: Know exactly where to get knowledge

---

## 🚀 Quick Start

1. **Create** `competitors/` folder structure
2. **Add** first competitor PRD
3. **Run** feature extraction
4. **Initialize** Master Skill Registry
5. **Repeat** for each competitor
6. **Normalize** and identify best sources
7. **Source** knowledge from best implementers
8. **Create** skills




