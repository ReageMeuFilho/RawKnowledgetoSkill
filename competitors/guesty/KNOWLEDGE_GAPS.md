# Guesty STR PMS - Knowledge Gaps

> **Source**: `guesty_str_pms_prd_original.md`
> **Skills Identified**: 67
> **Knowledge Gaps**: 42

---

## 🔴 Critical Knowledge Needed (Blocking)

These are HIGH priority skills where we need domain expertise to implement correctly.

### KG-001: Guest Message Response Patterns
**Skills**: SKILL-STR-001, SKILL-STR-003
**Question**: How do experienced STR hosts respond to common guest inquiries?
**What We Need**:
- Sample conversations for: check-in questions, WiFi issues, amenity questions, complaints, maintenance requests
- Tone/style guidelines for different property types (luxury vs budget)
- Escalation criteria: when should AI hand off to human?
- Language/phrases to NEVER use
- Response time expectations by message type

**Source Options**:
- [ ] Interview with experienced Airbnb Superhost (10+ properties)
- [ ] Training videos from STR management courses
- [ ] Real message transcripts (anonymized)

---

### KG-002: Dynamic Pricing Logic
**Skills**: SKILL-STR-042, SKILL-STR-044, SKILL-STR-045, SKILL-STR-046
**Question**: How do revenue managers decide on pricing for different scenarios?
**What We Need**:
- Base rate calculation methodology
- Demand signal interpretation (what indicates high/low demand?)
- Competitor pricing: how much to match vs. undercut vs. premium?
- Seasonal adjustment rules by market type
- Event pricing: how to identify events? how much to increase?
- Lead time pricing: last-minute vs. advance booking rules
- Length of stay discounts: typical discount percentages

**Source Options**:
- [ ] Interview with STR revenue manager
- [ ] PriceLabs/Wheelhouse/Beyond training materials
- [ ] Case studies from STR conferences

---

### KG-003: Cleaning Task Workflow
**Skills**: SKILL-STR-028, SKILL-STR-029, SKILL-STR-030
**Question**: How do property managers coordinate cleaning between guests?
**What We Need**:
- Standard cleaning checklist by property type (studio vs. 4BR)
- Time estimates by property size
- Photo requirements for completion verification
- Quality inspection criteria
- Handling same-day turnovers (checkout 11am, check-in 4pm)
- Deep clean vs. standard clean triggers
- Linen management (in-house vs. service)

**Source Options**:
- [ ] Interview with cleaning company owner
- [ ] TurnoverBnB training materials
- [ ] Property management SOPs

---

### KG-004: Owner Statement Format
**Skills**: SKILL-STR-050, SKILL-STR-054
**Question**: What do property owners need to see in their financial statements?
**What We Need**:
- Required line items (gross revenue, fees, net)
- Tax presentation by jurisdiction
- Expense categorization
- Comparison views (month over month, year over year)
- Payout reconciliation format
- 1099/tax reporting requirements (US)
- Multi-currency handling

**Source Options**:
- [ ] Interview with property management accountant
- [ ] Sample owner statements from existing PMS
- [ ] Trust accounting guidelines

---

### KG-005: OTA Channel Sync Edge Cases
**Skills**: SKILL-STR-021, SKILL-STR-024, SKILL-STR-025
**Question**: What can go wrong with channel synchronization and how to handle it?
**What We Need**:
- Common sync failure scenarios
- Rate/availability conflict resolution
- Airbnb instant book vs. request to book handling
- Booking.com commission model sync
- Handling OTA-specific cancellation policies
- What to do when APIs are down
- Retry strategies and timing

**Source Options**:
- [ ] Interview with channel manager engineer
- [ ] Guesty/Lodgify support documentation
- [ ] OTA partner program guidelines

---

## 🟡 Important Knowledge Needed

### KG-006: Guest Verification Process
**Skills**: SKILL-STR-018, SKILL-STR-019
**Question**: How do hosts verify guests and assess risk?
**What We Need**:
- What ID types to accept?
- Risk scoring factors (review history, verification status, booking patterns)
- When to require verification (all bookings vs. high-value only)
- Handling verification failures
- Privacy/GDPR considerations

**Source Options**:
- [ ] Autohost/Superhog product documentation
- [ ] Interview with host who uses verification

---

### KG-007: Smart Lock Integration
**Skills**: SKILL-STR-038, SKILL-STR-039, SKILL-STR-040, SKILL-STR-041
**Question**: How do hosts manage smart lock access codes?
**What We Need**:
- Code format by lock brand
- Timing: when to generate, when to deliver, when to revoke
- Backup access methods
- Handling lock failures during check-in
- Manager override codes
- Audit trail requirements

**Source Options**:
- [ ] Smart lock manufacturer documentation
- [ ] Interview with property manager using smart locks

---

### KG-008: Pre-Arrival Guest Communication
**Skills**: SKILL-STR-009, SKILL-STR-033
**Question**: What information do guests need before arrival and when?
**What We Need**:
- Pre-arrival timeline (7 days, 3 days, 1 day, day-of)
- Required information per touchpoint
- Upsell timing and messaging
- How to handle unresponsive guests
- Language for different property types

**Source Options**:
- [ ] Hostfully/YourWelcome product materials
- [ ] Sample pre-arrival sequences

---

### KG-009: Maintenance Request Handling
**Skills**: SKILL-STR-028, SKILL-STR-031
**Question**: How do hosts handle guest-reported maintenance issues?
**What We Need**:
- Common issue categories (plumbing, HVAC, appliances, etc.)
- Urgency classification criteria
- Response time expectations
- When to compensate guests
- Vendor coordination workflow
- Documentation requirements

**Source Options**:
- [ ] Interview with STR property manager
- [ ] Maintenance SOPs from property management companies

---

### KG-010: Review Request Strategy
**Skills**: WF-STR-011
**Question**: How do hosts maximize positive reviews?
**What We Need**:
- Optimal timing for review requests
- Effective messaging templates
- Handling negative reviews
- Platform-specific review mechanics
- Review response best practices

**Source Options**:
- [ ] Airbnb Superhost training
- [ ] STR community best practices

---

### KG-011: Tax Collection & Remittance
**Skills**: SKILL-STR-052
**Question**: How do hosts handle occupancy taxes across jurisdictions?
**What We Need**:
- Common tax types (occupancy, tourism, sales)
- Tax calculation by jurisdiction
- Remittance schedules
- Record-keeping requirements
- Handling tax-exempt guests

**Source Options**:
- [ ] Avalara/tax compliance provider documentation
- [ ] CPA specializing in STR

---

### KG-012: Damage Claim Processing
**Skills**: SKILL-STR-020, WF-STR-009
**Question**: How do hosts document and recover damage costs?
**What We Need**:
- Documentation requirements (photos, receipts)
- Timeline for filing claims
- Communication with guests about damage
- Insurance vs. deposit claims
- Dispute resolution process

**Source Options**:
- [ ] Airbnb AirCover guidelines
- [ ] CBIZ/insurance provider documentation

---

## 🟢 Nice-to-Have Knowledge

### KG-013: Multi-Unit Building Management
**Skills**: SKILL-STR-035
- Shared amenity management
- Building-wide maintenance coordination
- Revenue aggregation strategies

### KG-014: Direct Booking Website Optimization
**Skills**: SKILL-STR-026, SKILL-STR-027
- SEO strategies for vacation rentals
- Conversion optimization tactics
- Payment gateway selection

### KG-015: Guest Segmentation Strategies
**Skills**: SKILL-STR-013
- Segment definitions (VIP, repeat, at-risk)
- Marketing automation by segment
- Loyalty program design

### KG-016: Competitor Rate Monitoring
**Skills**: SKILL-STR-043
- Comparable property selection criteria
- Rate monitoring frequency
- Response strategies to competitor changes

---

## 📋 Knowledge Acquisition Plan

### Phase 1: Critical (Week 1-2)
| Gap | Priority | Source | Owner | Status |
|-----|----------|--------|-------|--------|
| KG-001 | HIGH | Superhost Interview | TBD | ⬜ Not Started |
| KG-002 | HIGH | Revenue Manager | TBD | ⬜ Not Started |
| KG-003 | HIGH | Cleaning Company | TBD | ⬜ Not Started |
| KG-004 | HIGH | PM Accountant | TBD | ⬜ Not Started |
| KG-005 | HIGH | Channel Expert | TBD | ⬜ Not Started |

### Phase 2: Important (Week 3-4)
| Gap | Priority | Source | Owner | Status |
|-----|----------|--------|-------|--------|
| KG-006 | MEDIUM | Verification Provider | TBD | ⬜ Not Started |
| KG-007 | MEDIUM | Lock Manufacturer | TBD | ⬜ Not Started |
| KG-008 | MEDIUM | Guest Comms Expert | TBD | ⬜ Not Started |
| KG-009 | MEDIUM | Maintenance Manager | TBD | ⬜ Not Started |
| KG-010 | MEDIUM | Superhost | TBD | ⬜ Not Started |
| KG-011 | MEDIUM | Tax CPA | TBD | ⬜ Not Started |
| KG-012 | MEDIUM | Insurance Provider | TBD | ⬜ Not Started |

### Phase 3: Enhancement (Week 5+)
| Gap | Priority | Source | Owner | Status |
|-----|----------|--------|-------|--------|
| KG-013 | LOW | Building PM | TBD | ⬜ Not Started |
| KG-014 | LOW | Marketing Expert | TBD | ⬜ Not Started |
| KG-015 | LOW | CRM Expert | TBD | ⬜ Not Started |
| KG-016 | LOW | Revenue Manager | TBD | ⬜ Not Started |

---

## 📝 Knowledge Input Format

When you provide knowledge, please include:

```markdown
## Knowledge: [Topic]

### Source
- Type: [Interview / Training Video / Document / Personal Experience]
- Date: [When captured]
- Expert: [Name/role if applicable]

### Content
[The actual knowledge - can be transcript, notes, or structured information]

### Key Takeaways
- Bullet point summaries

### Exact Wording to Use
- Phrases the AI should use verbatim

### Things to NEVER Do/Say
- Forbidden actions or phrases
```

---

## 🎯 Next Steps

1. **Review this document** - Are there knowledge gaps I missed?
2. **Prioritize** - Which gaps block your MVP?
3. **Provide knowledge** - Share transcripts, documents, or schedule interviews
4. **I'll process** - Convert knowledge into skill specifications




