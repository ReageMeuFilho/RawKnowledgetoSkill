# Research Prompt: Phase 2 Group 2 - Guest Intelligence

> **For**: AI Research Agent
> **Output**: Knowledge Document → `knowledge/communication/KD-PHASE2-G2-guest-intelligence.md`
> **Priority**: High
> **Date**: January 2026

---

## 🎯 Research Objective

Research and document comprehensive knowledge for implementing **8 Guest Intelligence skills** that enhance guest understanding, personalization, and loyalty management.

---

## 📋 Skills to Research

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| SKILL-048 | duplicate-profile-merging | communication | AI-powered duplicate guest detection and merging |
| SKILL-050 | upsell-management | communication | Personalized upsell recommendations |
| SKILL-051 | pre-arrival-questionnaire | communication | Pre-arrival preference capture |
| SKILL-072 | bad-review-defense-drafting | communication | Negative review response assistant |
| SKILL-093 | loyalty-tier-management | communication | Loyalty program tier management |
| SKILL-047 | guest-preference-tracking | communication | Guest preference learning and storage |
| SKILL-049 | vip-guest-handling | communication | VIP guest treatment protocols |
| SKILL-094 | referral-program-management | communication | Referral tracking and rewards |

---

## 🔍 Research Questions Per Skill

### SKILL-048: Duplicate Profile Merging

**Key Questions**:
1. What signals indicate duplicate guest profiles (email, phone, name fuzzy match)?
2. How do you handle partial matches with confidence scoring?
3. What is the merge conflict resolution strategy?
4. How do you preserve booking history during merges?
5. What privacy/GDPR considerations apply?
6. How do you prevent future duplicates?

**Research Sources**:
- Salesforce CDP duplicate detection
- Segment identity resolution
- Guesty guest management
- CRM data deduplication best practices
- GDPR data consolidation guidelines

### SKILL-050: Upsell Management

**Key Questions**:
1. What upsells work best for STR (early check-in, late checkout, experiences)?
2. When is the optimal time to present upsells (pre-arrival, during stay)?
3. How do you personalize offers based on guest history?
4. What pricing strategies maximize upsell conversion?
5. How do you track upsell revenue attribution?
6. What channels work best for upsell delivery (email, SMS, app)?

**Research Sources**:
- Hotel upselling platforms (Oaky, Nor1)
- Airbnb Experiences model
- Guest messaging upsell patterns
- E-commerce personalization (Amazon)
- Hospitality upselling case studies

### SKILL-051: Pre-Arrival Questionnaire

**Key Questions**:
1. What questions improve guest experience (arrival time, preferences)?
2. How do you balance information gathering vs. friction?
3. What format works best (form, conversational, progressive)?
4. How do you use responses to personalize the stay?
5. What completion rate is achievable?
6. How do you handle non-responders?

**Research Sources**:
- Hospitable check-in questionnaires
- Hotel pre-arrival communication
- Guest experience surveys
- Typeform/Jotform STR templates
- Experience personalization research

### SKILL-072: Bad Review Defense Drafting

**Key Questions**:
1. What response strategies work for different complaint types?
2. How do you maintain brand voice while addressing criticism?
3. What is the optimal response time for negative reviews?
4. How do you balance public response vs. private outreach?
5. What AI guardrails prevent inappropriate responses?
6. How do you escalate serious complaints?

**Research Sources**:
- Guesty review response automation
- GuestRevu review management
- TrustYou response strategies
- Hotel reputation management
- Review response psychology research

### SKILL-093: Loyalty Tier Management

**Key Questions**:
1. What tier structures work for STR (nights, spend, frequency)?
2. What benefits drive loyalty at each tier?
3. How do you communicate tier status and progress?
4. What prevents gaming/abuse of loyalty programs?
5. How do you handle tier downgrades gracefully?
6. What integration with direct booking is needed?

**Research Sources**:
- Hotel loyalty programs (Marriott Bonvoy, Hilton Honors)
- Airbnb Superguest concept
- BILT Rewards structure
- Loyalty program design research
- STR direct booking loyalty examples

### SKILL-047: Guest Preference Tracking

**Key Questions**:
1. What preferences are most valuable to track?
2. How do you capture implicit vs. explicit preferences?
3. How do you share preferences across properties?
4. What is the data retention policy for preferences?
5. How do you handle preference conflicts?
6. How do you surface preferences at the right moment?

**Research Sources**:
- Hotel CRM preference systems
- Customer data platform capabilities
- Personalization engines
- GDPR preference consent
- Guest experience research

### SKILL-049: VIP Guest Handling

**Key Questions**:
1. How do you identify VIP guests (revenue, influence, loyalty)?
2. What special treatment do VIPs receive?
3. How do you alert staff to VIP arrivals?
4. What communication style differs for VIPs?
5. How do you handle VIP complaints with priority?
6. What reporting tracks VIP satisfaction?

**Research Sources**:
- Luxury hotel VIP protocols
- Celebrity/influencer hosting guides
- High-value customer management
- Concierge service standards
- VIP experience case studies

### SKILL-094: Referral Program Management

**Key Questions**:
1. What referral incentives work best (credits, discounts, cash)?
2. How do you track referral attribution?
3. What prevents referral fraud?
4. How do you make referring easy (links, codes)?
5. What is the typical referral conversion rate?
6. How do you nurture referred leads?

**Research Sources**:
- Airbnb referral program
- Dropbox/Uber referral case studies
- ReferralCandy, Friendbuy platforms
- Word-of-mouth marketing research
- STR referral program examples

---

## 🏗️ Architecture Context

### Dependencies (From Phase 1)
- **SKILL-046**: Guest Profile Management (base profile)
- **SKILL-001-002**: Unified Inbox, Message Triage (communication)
- **SKILL-006**: Automated Messaging (delivery)

### Technology Stack
| Component | Technology | Purpose |
|-----------|------------|---------|
| Identity Resolution | Python ML | Deduplication |
| Personalization | Redis + ML | Real-time recommendations |
| Loyalty | PostgreSQL | Tier tracking |
| NLP | OpenAI GPT-4 | Review drafting |
| Communication | Temporal | Workflow orchestration |

### MCP Servers Required
```yaml
mcp_servers:
  - mcp://guest/profile
  - mcp://guest/preferences
  - mcp://loyalty/status
  - mcp://communication/send
  - mcp://ai/draft-response
```

---

## 📄 Output Format

Create a comprehensive knowledge document with:

1. **Executive Summary**
2. **Skill-by-Skill Analysis** (8 skills)
3. **Guest Data Model** - CDP schema design
4. **Personalization Engine** - Algorithm design
5. **Loyalty Program Design** - Tier structure, benefits
6. **AI/ML Components** - NLP for reviews, ML for matching
7. **Privacy & Compliance** - GDPR, data handling
8. **Competitive Comparison**
9. **Implementation Priorities**
10. **Open Questions**

**Quality Requirements**:
- Minimum 2,200 lines
- At least 30 citations/sources
- Include guest data schemas
- Include loyalty program flowcharts

---

## 📤 Delivery Instructions

1. Save to: `knowledge/communication/KD-PHASE2-G2-guest-intelligence.md`
2. Update: `docs/PHASE2_SKILL_TRACKER.md`
3. Notify: Ready for Stage 2

---

**Focus**: Know your guests better than anyone! 👤

