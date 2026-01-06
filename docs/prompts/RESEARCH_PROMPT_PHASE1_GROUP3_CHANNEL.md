# Research Prompt: Phase 1 Group 3 - Channel Distribution & OTA Management

## 🎯 RESEARCH OBJECTIVE

Research and document the **4 channel distribution skills**. This is how properties get discovered and booked - OTA connectivity is critical for revenue.

---

## 📋 SKILLS TO RESEARCH

| Skill ID | Name | Priority | Category |
|----------|------|----------|----------|
| SKILL-024 | channel-connection | P0 | channel |
| SKILL-025 | listing-content-sync | P0 | channel |
| SKILL-026 | rate-distribution | P0 | channel |
| SKILL-027 | sync-status-monitoring | P0 | channel |

---

## 🏢 PLATFORMS TO ANALYZE

### Primary (Best-in-Class)
| Platform | Why | Focus Areas |
|----------|-----|-------------|
| **Guesty** | 200+ channel connections | API architecture, sync reliability |
| **Hostaway** | Enterprise channel manager | Rate parity, bulk operations |
| **Cloudbeds** | Hotel-grade distribution | Real-time sync, rate shopping |

### Secondary
| Platform | Focus |
|----------|-------|
| Lodgify | Direct + OTA balance |
| RentalReady | Channel optimization |
| Rentals United | Dedicated channel manager |

### OTA Documentation (Primary Sources)
| OTA | API Docs |
|-----|----------|
| Airbnb | Partner API documentation |
| Vrbo/Expedia | Connectivity Partner API |
| Booking.com | Connectivity API |

---

## 📚 RESEARCH QUESTIONS BY SKILL

### SKILL-024: Channel Connection

**Core Questions:**
1. What is the onboarding flow for connecting a new OTA?
2. What credentials/tokens are required per OTA?
3. How is OAuth/API key management handled?
4. What's the typical connection setup time?
5. How are connection health and status monitored?

**Technical Questions:**
- API vs iCal vs XML feed per OTA?
- Rate limits by OTA?
- Sandbox/test environments available?
- What data is required for initial listing push?

**OTA-Specific Requirements:**
| OTA | Connection Type | Key Requirements |
|-----|-----------------|------------------|
| Airbnb | REST API | OAuth 2.0, listing ID mapping |
| Vrbo | REST API | Property ID, rate plan setup |
| Booking.com | XML/REST | Room types, rate plans, policies |
| Google VR | Feed | Structured data, verification |

**Sources to Check:**
- [ ] Airbnb Partner API documentation
- [ ] Vrbo Connectivity Partner docs
- [ ] Booking.com Connectivity API
- [ ] Guesty channel setup guides
- [ ] YouTube: "connect Airbnb channel manager"
- [ ] Reddit: r/airbnb_hosts "channel manager setup"

---

### SKILL-025: Listing Content Sync

**Core Questions:**
1. What content fields sync to each OTA?
2. How are photos managed and synced?
3. How are amenities mapped across different OTA taxonomies?
4. What character limits apply per OTA?
5. How is content versioning handled?

**Technical Questions:**
- Photo compression/resizing requirements per OTA?
- Amenity mapping tables?
- Description length limits?
- HTML vs plain text support?
- How often can content be updated?

**Content Types:**
| Content | Airbnb | Vrbo | Booking.com |
|---------|--------|------|-------------|
| Title | 50 chars | 80 chars | 40 chars |
| Description | 500 chars | 2000 chars | 400 chars |
| Photos | 50 max | 100 max | 45 max |
| Amenities | Fixed list | Fixed list | Fixed list |

**Sources to Check:**
- [ ] OTA listing requirements documentation
- [ ] Guesty content sync docs
- [ ] Photo optimization best practices
- [ ] YouTube: "optimize Airbnb listing"
- [ ] SEO for vacation rental listings

---

### SKILL-026: Rate Distribution

**Core Questions:**
1. How are base rates pushed to OTAs?
2. How is rate parity maintained or differentiated?
3. How are OTA commissions factored in?
4. What's the latency from rate change to OTA update?
5. How are rate plans/types handled?

**Technical Questions:**
- Rate push API per OTA?
- Bulk rate update capabilities?
- Length-of-stay pricing support?
- Promotional rate handling?
- Currency conversion?

**Rate Strategies:**
- Rate parity (same everywhere)
- Channel-specific markup (OTA commission baked in)
- Dynamic by demand
- Direct booking discount

**Sources to Check:**
- [ ] Guesty rate management
- [ ] PriceLabs OTA distribution
- [ ] Booking.com rate plan documentation
- [ ] YouTube: "vacation rental pricing strategy"
- [ ] Revenue management best practices

---

### SKILL-027: Sync Status Monitoring

**Core Questions:**
1. How is sync health displayed to users?
2. What error types are tracked?
3. How are sync failures alerted?
4. What retry logic exists?
5. How is sync lag measured?

**Technical Questions:**
- Sync job architecture?
- Error categorization taxonomy?
- Alert thresholds?
- Historical sync logs retention?
- Dashboard metrics?

**Key Metrics to Track:**
| Metric | Description | Target |
|--------|-------------|--------|
| Sync Latency | Time from change to OTA update | <5 min |
| Success Rate | % of syncs completing | >99.5% |
| Error Rate | Failed syncs per day | <0.5% |
| Coverage | Properties successfully connected | 100% |

**Error Categories:**
- Authentication failures
- Rate limit exceeded
- Content validation errors
- Network timeouts
- OTA-side errors

**Sources to Check:**
- [ ] Guesty sync status dashboard
- [ ] Hostaway connection health
- [ ] Observability best practices (DataDog, etc.)
- [ ] YouTube: "channel manager troubleshooting"

---

## 📄 OUTPUT REQUIREMENTS

### Document Structure

```markdown
# Knowledge Document: Channel Distribution & OTA Management
## Phase 1 Group 3 | Skills: SKILL-024, 025, 026, 027

## 1. Executive Summary
   - Key findings
   - OTA landscape overview
   - Recommended architecture

## 2. OTA Landscape Overview
   - Market share by OTA
   - API maturity comparison
   - Integration complexity ranking

## 3. SKILL-024: Channel Connection
   ### 3.1 Connection Architecture
   ### 3.2 OTA-Specific Requirements Table
   ### 3.3 Onboarding Flow
   ### 3.4 Credential Management
   ### 3.5 Health Monitoring

## 4. SKILL-025: Listing Content Sync
   ### 4.1 Content Field Mapping
   ### 4.2 Photo Management
   ### 4.3 Amenity Taxonomy Mapping
   ### 4.4 Content Validation Rules
   ### 4.5 Sync Frequency

## 5. SKILL-026: Rate Distribution
   ### 5.1 Rate Push Architecture
   ### 5.2 Rate Plan Types
   ### 5.3 Parity vs Differentiation Strategies
   ### 5.4 Commission Handling
   ### 5.5 Bulk Operations

## 6. SKILL-027: Sync Status Monitoring
   ### 6.1 Dashboard Design
   ### 6.2 Error Taxonomy
   ### 6.3 Alerting Strategy
   ### 6.4 Retry Logic
   ### 6.5 Reporting Metrics

## 7. Unified Channel Manager Architecture
   - System diagram
   - Data flows
   - Queue management

## 8. References
   - 30+ citations
```

### Quality Targets

| Metric | Target |
|--------|--------|
| Document Length | 400-550 lines |
| Citations | 30+ sources |
| OTA Coverage | Airbnb, Vrbo, Booking.com minimum |
| Diagrams | Channel sync architecture, error flow |

---

## 💾 SAVE LOCATION

```
knowledge/channel/KD-PHASE1-G3-channel-distribution.md
```

---

## ✅ COMPLETION CHECKLIST

- [ ] All 4 skills researched
- [ ] OTA-specific requirements documented
- [ ] Content mapping tables created
- [ ] Rate distribution strategy defined
- [ ] 30+ sources cited

---

## 🚀 AFTER COMPLETING

```bash
git add -A
git commit -m "Stage 1 COMPLETE: Phase 1 Group 3 - Channel Distribution (4 skills)"
git push
```

