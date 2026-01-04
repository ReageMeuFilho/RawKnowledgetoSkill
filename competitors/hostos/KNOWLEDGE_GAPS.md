# Host OS STR PMS - Knowledge Gaps

> **Source**: `hostos_str_prd_original.md`
> **New Skills Identified**: 12
> **New Knowledge Gaps**: 9

---

## 🔴 NEW Critical Knowledge Needed

These gaps are UNIQUE to Host OS features (not in Guesty):

### KG-NEW-001: Split Inventory Management Patterns
**Skills Blocked**: SKILL-068 (Polymorphic Inventory)
**Question**: How do hotels and resorts manage parent/child inventory relationships?
**What We Need**:
- Villa split scenarios (whole vs. partial rental)
- Blocking logic when child is booked vs. parent is booked
- Rate calculation for partial vs. full booking
- OTA handling of parent/child listings
- Multi-unit clustering strategies

**Source Options**:
- [ ] Interview with resort revenue manager
- [ ] Cloudbeds/Mews documentation
- [ ] Hotel PMS best practices

---

### KG-NEW-002: Gap Night Discount Optimization
**Skills Blocked**: SKILL-069 (Gap Night Revenue)
**Question**: What discount percentages and messaging work for gap night offers?
**What We Need**:
- Typical discount ranges (30%? 50%? 70%?)
- Optimal timing for sending offers
- Message templates that convert
- Adjacent guest response rates
- When NOT to offer gap nights

**Source Options**:
- [ ] BestyAI case studies
- [ ] Revenue manager interview
- [ ] A/B test data from STR operators

---

### KG-NEW-003: Room Upgrade Timing and Pricing
**Skills Blocked**: SKILL-070 (Attribute-Based Upgrades)
**Question**: When and how much should we charge for room upgrades?
**What We Need**:
- Optimal timing (72h? 48h? 24h pre-arrival?)
- Pricing strategy (% of difference? fixed amount?)
- Vacancy threshold (when to offer?)
- Message templates
- Conversion benchmarks

**Source Options**:
- [ ] Hotel revenue management training
- [ ] Upsell platform documentation

---

### KG-NEW-004: Airbnb Review Blind Mechanics
**Skills Blocked**: SKILL-071 (Auto-Review Posting)
**Question**: How does Airbnb's review blind work and how to optimize?
**What We Need**:
- Review blind mechanism details
- Optimal timing for host review posting
- Template variety requirements
- Platform TOS compliance
- Risk assessment

**Source Options**:
- [ ] Airbnb host community forums
- [ ] Platform API documentation
- [ ] Experienced Superhost interview

---

### KG-NEW-005: Negative Review Response Patterns
**Skills Blocked**: SKILL-072 (Bad Review Defense)
**Question**: How do successful hosts respond to negative reviews?
**What We Need**:
- Response structure (acknowledge, explain, resolve)
- Tone guidelines
- What to NEVER say
- When to offer compensation
- Platform-specific rules

**Source Options**:
- [ ] Reputation management company
- [ ] Successful Superhost examples
- [ ] PR best practices

---

### KG-NEW-006: Emergency Relocation Protocols
**Skills Blocked**: SKILL-074 (Emergency Relocation)
**Question**: How do PMs handle emergency relocations when unit is unusable?
**What We Need**:
- Decision criteria (when to relocate vs. repair)
- Guest communication scripts
- Alternative unit selection logic
- Compensation guidelines
- OTA notification requirements

**Source Options**:
- [ ] Property management company SOPs
- [ ] Hotel front desk training

---

### KG-NEW-007: Hotel Folio Management
**Skills Blocked**: SKILL-075 (Guest Folio)
**Question**: How do hotels manage post-booking charges?
**What We Need**:
- Common charge categories
- Authorization hold amounts
- Settlement timing
- Dispute handling
- Accounting integration

**Source Options**:
- [ ] Mews documentation
- [ ] Hotel front desk training
- [ ] PMS best practices

---

### KG-NEW-008: Country Guest Registration Requirements
**Skills Blocked**: SKILL-077 (Police Reporting)
**Question**: What are the guest registration requirements by country?
**What We Need**:
- Italy (Schede Alloggiati)
- Spain (Policía Nacional)
- Portugal (SEF)
- France
- Other EU countries
- API endpoints/formats

**Source Options**:
- [ ] CheKin documentation
- [ ] Legal compliance guides
- [ ] Government API specs

---

### KG-NEW-009: Party Prevention Thresholds
**Skills Blocked**: SKILL-078 (Party Prevention Grid)
**Question**: What noise thresholds and escalation timing work?
**What We Need**:
- Noise level thresholds (dB by time of day)
- Duration before escalation
- Escalation sequence timing
- Guest communication scripts
- Security dispatch criteria

**Source Options**:
- [ ] Minut documentation
- [ ] NoiseAware best practices
- [ ] Property manager interviews

---

## 🔄 Enhanced Knowledge for Existing Gaps

These existing gaps need ADDITIONAL information for Host OS features:

| Existing Gap | Enhancement Needed |
|--------------|-------------------|
| KG-001 (Guest Messages) | Add RAG/Knowledge Graph patterns |
| KG-003 (Cleaning Tasks) | Add GPS geofencing, magic link auth |
| KG-004 (Owner Statements) | Add 4-way split accounting |
| KG-005 (Channel Sync) | Add < 30s latency requirements |

---

## 📋 Knowledge Acquisition Priority

### Phase 1: MVP Blockers (Week 1-2)
| Gap | Priority | Skills Blocked |
|-----|----------|----------------|
| KG-NEW-001 | HIGH | Polymorphic Inventory |
| KG-003 + GPS | HIGH | Magic Link App |
| KG-004 + Splits | HIGH | Multi-Stakeholder Payments |

### Phase 2: Core Features (Week 3-4)
| Gap | Priority | Skills Blocked |
|-----|----------|----------------|
| KG-NEW-002 | HIGH | Gap Night Revenue |
| KG-NEW-003 | HIGH | Room Upgrades |
| KG-NEW-009 | HIGH | Party Prevention |
| KG-001 + RAG | HIGH | Knowledge Graph Answers |

### Phase 3: Compliance (Week 5-6)
| Gap | Priority | Skills Blocked |
|-----|----------|----------------|
| KG-NEW-008 | MEDIUM | Police Reporting |
| KG-NEW-004 | MEDIUM | Auto-Review Posting |
| KG-NEW-005 | MEDIUM | Bad Review Defense |
| KG-NEW-006 | MEDIUM | Emergency Relocation |
| KG-NEW-007 | MEDIUM | Guest Folio |

---

## 🎯 Combined Knowledge Gap Summary

| Priority | Guesty Gaps | Host OS Gaps | Total |
|----------|-------------|--------------|-------|
| HIGH | 5 | 4 | 9 |
| MEDIUM | 7 | 5 | 12 |
| LOW | 4 | 0 | 4 |
| **Total** | **16** | **9** | **25** |

---

## 📥 What I Need From You

To build the 12 NEW Host OS skills, I need knowledge for these 9 gaps.

**Fastest path**: If you have access to:
1. Hotel PMS documentation (Mews, Cloudbeds)
2. BestyAI or BoomAI marketing materials
3. CheKin compliance guides
4. Minut/NoiseAware setup docs

These would fill most gaps quickly!

