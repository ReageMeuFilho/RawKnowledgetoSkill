# Research Prompt: Phase 2 Group 7 - Hospitality Premium

> **For**: AI Research Agent
> **Output**: Knowledge Document → `knowledge/hospitality/KD-PHASE2-G7-hospitality-premium.md`
> **Priority**: Medium (Premium features)
> **Date**: January 2026

---

## 🎯 Research Objective

Research and document comprehensive knowledge for implementing **6 Hospitality Premium skills** that bring hotel-grade experiences to short-term rentals, including concierge services, experience booking, and flexible check-in/out.

---

## 📋 Skills to Research

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| SKILL-087 | front-desk-command-center | hospitality | Hotel-style front desk dashboard |
| SKILL-124 | digital-concierge | hospitality | AI-powered local recommendations |
| SKILL-125 | experience-booking | hospitality | Activity/experience booking integration |
| SKILL-126 | room-upgrade-management | hospitality | Dynamic room upgrade offers |
| SKILL-127 | early-checkin-late-checkout | hospitality | Flexible check-in/out management |
| SKILL-055 | website-seo | channel | SEO optimization for direct bookings |

---

## 🔍 Research Questions Per Skill

### SKILL-087: Front Desk Command Center

**Key Questions**:
1. What do hotel front desk systems look like (Opera, Mews)?
2. What real-time information does front desk staff need?
3. How do you handle walk-ins and same-day requests?
4. What guest lookup capabilities are essential?
5. How do you integrate with access control systems?
6. What communication tools embed in the command center?

**Research Sources**:
- Mews PMS front desk
- Cloudbeds front desk features
- Opera PMS interface
- Hotel front desk workflows
- Boutique hotel operations guides

### SKILL-124: Digital Concierge

**Key Questions**:
1. What local recommendations do guests want most (restaurants, activities)?
2. How do you source and curate local recommendations?
3. What personalization improves recommendation relevance?
4. How do you integrate with booking platforms (OpenTable, Viator)?
5. What conversational interface works best (chat, voice)?
6. How do you handle affiliate/partnership monetization?

**Research Sources**:
- Ivy by GoMoment concierge
- Alice hotel concierge platform
- Airbnb Guidebooks
- Google Places API
- TripAdvisor content integration
- GuestWisely local guides

### SKILL-125: Experience Booking

**Key Questions**:
1. What experience categories are popular (tours, dining, spa)?
2. How do you integrate with Viator, GetYourGuide, etc.?
3. What commission structures are standard?
4. How do you handle experience cancellations?
5. What liability considerations exist?
6. How do you surface experiences at the right moment?

**Research Sources**:
- Airbnb Experiences
- Viator partner program
- GetYourGuide affiliate API
- Hotel experience platforms
- Tour operator integrations

### SKILL-126: Room Upgrade Management

**Key Questions**:
1. What triggers upgrade offers (availability, guest value)?
2. How do you price upgrades dynamically?
3. What communication timing maximizes conversion?
4. How do you handle upgrade inventory management?
5. What upsell techniques work best for STR?
6. How do you track upgrade revenue attribution?

**Research Sources**:
- Oaky hotel upselling
- Nor1 upgrade platform
- Hotel revenue optimization
- Upselling psychology research
- STR upselling case studies

### SKILL-127: Early Check-in / Late Checkout

**Key Questions**:
1. How do you determine availability for early/late requests?
2. What pricing models work (flat fee, hourly)?
3. How do you balance guest requests with cleaning schedules?
4. What automation handles approval workflows?
5. How do you communicate availability proactively?
6. What integration with smart locks is needed?

**Research Sources**:
- Hotel early/late checkout policies
- Airbnb flexible checkout
- STR turnover scheduling
- Smart lock integration patterns
- Guest experience research

### SKILL-055: Website SEO

**Key Questions**:
1. What SEO factors matter most for vacation rental websites?
2. How do you optimize for local search (city + vacation rental)?
3. What content strategy drives organic traffic?
4. How do you handle dynamic content SEO (availability, pricing)?
5. What technical SEO requirements apply (schema, speed)?
6. How do you compete with OTA SEO dominance?

**Research Sources**:
- Lodgify SEO features
- Vacation rental SEO guides
- Local SEO best practices
- Schema.org vacation rental markup
- Direct booking marketing strategies

---

## 🏗️ Architecture Context

### Dependencies (From Phase 1)
- **SKILL-024-027**: Channel Distribution (booking sync)
- **SKILL-022**: Smart Lock Integration (access control)
- **SKILL-017-019**: Task Management (cleaning coordination)

### Technology Stack
| Component | Technology | Purpose |
|-----------|------------|---------|
| Dashboard | React + WebSocket | Real-time UI |
| Concierge AI | OpenAI GPT-4 | Recommendations |
| Experience API | REST integrations | Third-party booking |
| SEO | Next.js SSR | Dynamic pages |
| Pricing | Python | Upgrade pricing |

### MCP Servers Required
```yaml
mcp_servers:
  - mcp://hospitality/dashboard
  - mcp://concierge/recommend
  - mcp://experience/book
  - mcp://upgrade/offer
  - mcp://checkin/flexible
```

---

## 📄 Output Format

Create a comprehensive knowledge document with:

1. **Executive Summary**
2. **Skill-by-Skill Analysis** (6 skills)
3. **Front Desk UX** - Dashboard design patterns
4. **Concierge System** - Recommendation engine, partnerships
5. **Experience Marketplace** - Integration architecture
6. **Upselling Strategy** - Pricing, timing, communication
7. **SEO Technical Guide** - Implementation specifics
8. **Competitive Comparison** - Hotel vs. STR approaches
9. **Implementation Priorities**
10. **Open Questions**

**Quality Requirements**:
- Minimum 1,800 lines
- At least 25 citations/sources
- Include dashboard wireframes
- Include SEO schema examples

---

## 📤 Delivery Instructions

1. Save to: `knowledge/hospitality/KD-PHASE2-G7-hospitality-premium.md`
2. Update: `docs/PHASE2_SKILL_TRACKER.md`
3. Notify: Ready for Stage 2

---

**Focus**: Deliver hotel-quality experiences! 🏨

