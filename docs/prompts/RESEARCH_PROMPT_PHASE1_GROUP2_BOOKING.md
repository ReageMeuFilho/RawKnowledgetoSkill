# Research Prompt: Phase 1 Group 2 - Booking & Calendar System

## 🎯 RESEARCH OBJECTIVE

Research and document the **4 core booking and calendar skills**. This is the heart of any property management system - accurate availability and reservation management.

---

## 📋 SKILLS TO RESEARCH

| Skill ID | Name | Priority | Category |
|----------|------|----------|----------|
| SKILL-007 | calendar-sync-management | P0 | booking |
| SKILL-008 | double-booking-prevention | P0 | booking |
| SKILL-009 | date-blocking | P0 | booking |
| SKILL-010 | direct-reservation-creation | P0 | booking |

---

## 🏢 PLATFORMS TO ANALYZE

### Primary (Best-in-Class)
| Platform | Why | Focus Areas |
|----------|-----|-------------|
| **Guesty** | Most sophisticated multi-calendar | Conflict resolution, sync speed |
| **OwnerRez** | Direct booking specialist | Booking engine, owner controls |
| **Lodgify** | Website-first approach | Direct reservation flow |

### Secondary
| Platform | Focus |
|----------|-------|
| Hostaway | Enterprise calendar |
| Hospitable | Simple calendar UX |
| Cloudbeds | Hotel reservation patterns |

---

## 📚 RESEARCH QUESTIONS BY SKILL

### SKILL-007: Calendar Sync Management

**Core Questions:**
1. How is iCal sync implemented (import/export frequency)?
2. What's the sync latency from OTA change to system update?
3. How are partial-day bookings handled?
4. How is timezone management handled across properties?
5. What's the conflict detection mechanism?

**Technical Questions:**
- iCal format parsing edge cases?
- Webhook vs polling for each OTA (Airbnb, Vrbo, Booking.com)?
- How often should external calendars be polled?
- What's the data model for a calendar event?

**Integration Questions:**
- Google Calendar integration?
- Outlook/Exchange integration?
- How are owner personal calendars handled?

**Sources to Check:**
- [ ] Guesty calendar sync documentation
- [ ] Airbnb iCal export format
- [ ] Vrbo calendar sync API
- [ ] YouTube: "vacation rental calendar sync"
- [ ] Reddit: r/airbnb_hosts "calendar sync issues"
- [ ] iCal RFC 5545 specification

---

### SKILL-008: Double-Booking Prevention

**Core Questions:**
1. What mechanisms prevent overlapping reservations?
2. How is the "race condition" problem solved?
3. What buffer time options exist between bookings?
4. How are holds/pending bookings handled?
5. What happens when a double-booking is detected?

**Technical Questions:**
- Database locking strategy?
- How is availability checked atomically?
- What's the booking confirmation flow?
- How are instant-book vs request-to-book handled?

**Edge Cases:**
- Same-day checkout/check-in conflicts?
- Multi-night minimum stay overlaps?
- Timezone boundary bookings?
- Concurrent booking attempts?

**Sources to Check:**
- [ ] Guesty availability management
- [ ] Stripe/booking system concurrency patterns
- [ ] Database locking best practices
- [ ] YouTube: "vacation rental double booking"
- [ ] Airbnb host forums on double bookings

---

### SKILL-009: Date Blocking

**Core Questions:**
1. What types of blocks exist (owner use, maintenance, seasonal)?
2. How are recurring blocks configured?
3. Can blocks be partial-day?
4. How do blocks interact with minimum stay rules?
5. How are blocks synced to OTAs?

**Technical Questions:**
- Block data model (vs reservation)?
- How are block reasons categorized?
- Can blocks be overridden?
- Block audit trail?

**Use Cases:**
- Owner personal use scheduling
- Maintenance windows
- Seasonal closures
- Permit/license restrictions

**Sources to Check:**
- [ ] OwnerRez owner blocking features
- [ ] Lodgify availability controls
- [ ] YouTube: "block dates Airbnb"
- [ ] Property manager forums on blocking strategies

---

### SKILL-010: Direct Reservation Creation

**Core Questions:**
1. What's the manual reservation creation flow?
2. How are direct bookings (non-OTA) handled?
3. What payment options exist for direct bookings?
4. How is pricing calculated for manual reservations?
5. What guest data is required vs optional?

**Technical Questions:**
- Reservation data model?
- State machine for reservation lifecycle?
- How are quotes converted to bookings?
- Invoice generation flow?

**Direct Booking Engine:**
- Website widget integration?
- Quote request flow?
- Guest portal booking flow?
- Repeat guest rebooking?

**Sources to Check:**
- [ ] OwnerRez direct booking engine
- [ ] Lodgify booking widget
- [ ] Guesty direct booking documentation
- [ ] YouTube: "direct booking vacation rental"
- [ ] Blog posts on direct booking strategies

---

## 📄 OUTPUT REQUIREMENTS

### Document Structure

```markdown
# Knowledge Document: Booking & Calendar System
## Phase 1 Group 2 | Skills: SKILL-007, 008, 009, 010

## 1. Executive Summary
   - Key findings across all 4 skills
   - Critical technical decisions
   - Recommended architecture

## 2. SKILL-007: Calendar Sync Management
   ### 2.1 Feature Overview
   ### 2.2 Sync Architecture
   ### 2.3 Data Model (Calendar Event schema)
   ### 2.4 OTA-Specific Considerations
   ### 2.5 Performance Requirements
   ### 2.6 Error Handling

## 3. SKILL-008: Double-Booking Prevention
   ### 3.1 Feature Overview
   ### 3.2 Concurrency Control Strategy
   ### 3.3 Availability Check Algorithm
   ### 3.4 Edge Cases & Solutions
   ### 3.5 Recovery Procedures

## 4. SKILL-009: Date Blocking
   ### 4.1 Feature Overview
   ### 4.2 Block Types & Data Model
   ### 4.3 Recurring Block Logic
   ### 4.4 OTA Sync Behavior
   ### 4.5 UI/UX Considerations

## 5. SKILL-010: Direct Reservation Creation
   ### 5.1 Feature Overview
   ### 5.2 Reservation Data Model
   ### 5.3 Booking Flow (State Machine)
   ### 5.4 Pricing Integration
   ### 5.5 Payment Handling
   ### 5.6 Confirmation & Communication

## 6. Unified Calendar Data Model
   - Core entities and relationships
   - JSON schemas
   - Database design recommendations

## 7. Integration with Other Systems
   - Pricing engine integration
   - Payment system integration
   - Communication system triggers

## 8. References
   - 25+ citations
```

### Quality Targets

| Metric | Target |
|--------|--------|
| Document Length | 350-500 lines |
| Citations | 25+ sources |
| Data Models | JSON schema for reservations, calendar events, blocks |
| Diagrams | Calendar sync flow, booking state machine |

---

## 💾 SAVE LOCATION

```
knowledge/booking/KD-PHASE1-G2-booking-calendar.md
```

---

## ✅ COMPLETION CHECKLIST

- [ ] All 4 skills researched
- [ ] Calendar sync architecture documented
- [ ] Double-booking prevention strategy defined
- [ ] Reservation state machine documented
- [ ] 25+ sources cited
- [ ] Saved to correct location

---

## 🚀 AFTER COMPLETING

```bash
git add -A
git commit -m "Stage 1 COMPLETE: Phase 1 Group 2 - Booking & Calendar System (4 skills)"
git push
```

