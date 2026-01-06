# Research Prompt: Phase 1 Group 1 - Core Communication Platform

## 🎯 RESEARCH OBJECTIVE

Research and document the **5 core communication skills** needed for a property management platform. These are "table stakes" features that every competitor has - we need best-in-class implementations.

---

## 📋 SKILLS TO RESEARCH

| Skill ID | Name | Priority | Category |
|----------|------|----------|----------|
| SKILL-001 | unified-inbox-management | P0 | communication |
| SKILL-002 | message-triage-routing | P0 | communication |
| SKILL-006 | automated-messaging | P0 | communication |
| SKILL-046 | guest-profile-management | P0 | communication |
| SKILL-085 | no-app-guest-messaging | P0 | communication |

---

## 🏢 PLATFORMS TO ANALYZE

### Primary (Best-in-Class)
| Platform | Why | Focus Areas |
|----------|-----|-------------|
| **Guesty** | Industry leader, enterprise-grade | Unified inbox architecture, team workflows |
| **Hostaway** | 93% automation rate | Message templates, auto-responses |
| **Hospitable** | SMB AI leader | AI suggestions, sentiment detection |

### Secondary (Additional Insights)
| Platform | Focus |
|----------|-------|
| Lodgify | Direct booking focus |
| OwnerRez | Owner communication |
| Cloudbeds | Hotel-grade messaging |

---

## 📚 RESEARCH QUESTIONS BY SKILL

### SKILL-001: Unified Inbox Management

**Core Questions:**
1. How are messages aggregated from multiple channels (Airbnb, Vrbo, Booking.com, email, SMS)?
2. What is the data model for a unified conversation thread?
3. How is real-time sync handled (webhooks vs polling)?
4. How are read/unread states managed across team members?
5. What search and filter capabilities are essential?

**Technical Questions:**
- API polling frequency for each OTA?
- How are message threading conflicts resolved?
- What's the latency from OTA message to inbox display?
- How is attachment handling managed (photos, documents)?

**UX Questions:**
- How do teams collaborate on the same inbox?
- What are the essential keyboard shortcuts?
- How are urgent messages surfaced?

**Sources to Check:**
- [ ] Guesty unified inbox documentation
- [ ] Hostaway inbox features
- [ ] YouTube: "Guesty inbox demo", "Hostaway inbox"
- [ ] G2 reviews mentioning "inbox"
- [ ] Reddit: r/airbnb_hosts "inbox management"

---

### SKILL-002: Message Triage & Routing

**Core Questions:**
1. What rules determine which team member receives a message?
2. How is message urgency/priority determined?
3. What automation triggers exist (keywords, guest type, property)?
4. How are escalations handled?
5. What SLAs can be configured?

**Technical Questions:**
- What's the routing rules data model?
- How is round-robin assignment implemented?
- How are workload balances maintained?
- What happens when assigned person is offline?

**AI Integration Questions:**
- How is intent classification done?
- What confidence thresholds trigger human review?
- How is sentiment used in routing?

**Sources to Check:**
- [ ] Guesty team management docs
- [ ] Hospitable AI routing
- [ ] Intercom/Zendesk routing (industry standard)
- [ ] YouTube: "property management team workflows"

---

### SKILL-006: Automated Messaging

**Core Questions:**
1. What trigger types exist (booking confirmed, check-in, checkout, etc.)?
2. How are message templates structured (variables, conditionals)?
3. What scheduling options are available (relative timing, time zones)?
4. How is personalization handled?
5. What A/B testing capabilities exist?

**Technical Questions:**
- Template variable syntax (Mustache, Jinja, custom)?
- How are timezone conversions handled?
- What's the message queue architecture?
- How are delivery failures handled?

**Best Practices:**
- What's the optimal message timing sequence?
- Which messages have highest open rates?
- What personalization increases engagement?

**Sources to Check:**
- [ ] Hospitable automation documentation
- [ ] Hostaway scheduled messages
- [ ] YouTube: "Airbnb automated messages", "guest communication automation"
- [ ] Blog posts on STR guest communication
- [ ] Mailchimp/SendGrid best practices (email industry)

---

### SKILL-046: Guest Profile Management

**Core Questions:**
1. What data points are captured per guest?
2. How are repeat guests identified across channels?
3. What preferences can be stored?
4. How is guest history displayed?
5. What privacy/GDPR considerations apply?

**Data Model Questions:**
- Guest profile schema?
- How is identity resolution done (email, phone, name matching)?
- What's stored per-stay vs per-guest?
- How long is data retained?

**Feature Questions:**
- VIP/loyalty tagging?
- Blacklist/ban management?
- Guest notes and alerts?
- Booking history aggregation?

**Sources to Check:**
- [ ] Guesty guest management
- [ ] Cloudbeds guest profiles (hotel-grade)
- [ ] CRM best practices (HubSpot, Salesforce patterns)
- [ ] GDPR guest data requirements
- [ ] YouTube: "vacation rental guest management"

---

### SKILL-085: No-App Guest Messaging

**Core Questions:**
1. How is SMS messaging implemented?
2. How is WhatsApp Business API integrated?
3. What are the costs per message by channel?
4. How is two-way conversation maintained?
5. What compliance rules apply (opt-in, TCPA)?

**Technical Questions:**
- SMS provider comparison (Twilio, MessageBird, etc.)?
- WhatsApp Business API requirements?
- How are long messages handled (concatenation)?
- Media message handling (MMS, WhatsApp images)?

**Regional Considerations:**
- WhatsApp dominance in Brazil/Europe
- SMS costs by country
- Local number requirements

**Sources to Check:**
- [ ] Twilio SMS/WhatsApp documentation
- [ ] Hostaway WhatsApp integration
- [ ] YouTube: "WhatsApp for vacation rentals"
- [ ] TCPA compliance guidelines
- [ ] Brazil WhatsApp Business requirements

---

## 📄 OUTPUT REQUIREMENTS

### Document Structure

```markdown
# Knowledge Document: Core Communication Platform
## Phase 1 Group 1 | Skills: SKILL-001, 002, 006, 046, 085

## 1. Executive Summary
   - Key findings across all 5 skills
   - Best-in-class implementations identified
   - Recommended approach for Citadel OS

## 2. SKILL-001: Unified Inbox Management
   ### 2.1 Feature Overview
   ### 2.2 Data Model
   ### 2.3 Technical Architecture
   ### 2.4 Best Implementation (with source)
   ### 2.5 Integration Requirements
   ### 2.6 Performance Metrics

## 3. SKILL-002: Message Triage & Routing
   [Same structure]

## 4. SKILL-006: Automated Messaging
   [Same structure]

## 5. SKILL-046: Guest Profile Management
   [Same structure]

## 6. SKILL-085: No-App Guest Messaging
   [Same structure]

## 7. Cross-Skill Integration
   - How these 5 skills work together
   - Shared data models
   - Common APIs

## 8. Implementation Recommendations
   - Build order
   - Dependencies
   - Estimated complexity

## 9. References
   - 30+ citations
```

### Quality Targets

| Metric | Target |
|--------|--------|
| Document Length | 400-600 lines |
| Citations | 30+ sources |
| Data Models | JSON schema for each skill |
| Diagrams | At least 2 (inbox flow, message routing) |

---

## 💾 SAVE LOCATION

```
knowledge/communication/KD-PHASE1-G1-communication-platform.md
```

---

## ✅ COMPLETION CHECKLIST

- [ ] All 5 skills researched
- [ ] Best-in-class implementation identified for each
- [ ] Data models documented
- [ ] Integration points mapped
- [ ] 30+ sources cited
- [ ] Saved to correct location
- [ ] STATUS.md updated

---

## 🚀 AFTER COMPLETING

```bash
git add -A
git commit -m "Stage 1 COMPLETE: Phase 1 Group 1 - Core Communication Platform (5 skills)"
git push
```

Then notify Cursor AI for Stage 2 (Engineering Prompt creation).

