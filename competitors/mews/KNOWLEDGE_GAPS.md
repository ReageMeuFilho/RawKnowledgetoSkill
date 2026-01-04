# Mews Hospitality Platform - Knowledge Gaps

> **Source**: `mews_hospitality_pms_prd_original.md`
> **New Skills Identified**: 15
> **New Knowledge Gaps**: 14

---

## 🔴 NEW Knowledge Gaps from Mews

### KG-MEWS-001: Kiosk Hardware Selection
**Skills Blocked**: SKILL-080 (Kiosk Check-In)
**Question**: What hardware works best for self-service check-in kiosks?
**What We Need**:
- iPad vs Android tablet comparison
- Card reader options (Stripe, Square)
- NFC reader for Digital Key
- Mounting options (wall, stand, counter)
- Thermal printer selection
- Camera for photo capture
- Network considerations

**Source Options**:
- [ ] Kiosk hardware vendor documentation
- [ ] Mews implementation guides

---

### KG-MEWS-002: Kiosk Upsell Optimization
**Skills Blocked**: SKILL-080 (Kiosk Check-In)
**Question**: How to maximize upsell conversion at check-in kiosk?
**What We Need**:
- Optimal offer sequencing
- Pricing strategy for upgrades
- UI/UX best practices
- A/B test learnings
- Conversion benchmarks (2.6x claim)

**Source Options**:
- [ ] Mews case studies
- [ ] Hotel revenue management research

---

### KG-MEWS-003: Digital Key Hardware Requirements
**Skills Blocked**: SKILL-081 (Digital Key)
**Question**: What lock hardware supports BLE/NFC digital keys?
**What We Need**:
- ASSA ABLOY Vingcard specs
- Salto Space requirements
- BLE vs NFC comparison
- Battery life considerations
- Offline operation capabilities
- Retrofit options for existing locks

**Source Options**:
- [ ] Lock manufacturer documentation
- [ ] Property technology consultant

---

### KG-MEWS-004: Apple Wallet Integration
**Skills Blocked**: SKILL-081 (Digital Key)
**Question**: How to implement hotel keys in Apple Wallet?
**What We Need**:
- Apple Wallet API requirements
- App Clip implementation
- Key provisioning workflow
- Revocation process
- Testing requirements
- Certification process

**Source Options**:
- [ ] Apple Developer documentation
- [ ] ASSA ABLOY integration guides

---

### KG-MEWS-005: Flexible Pricing Models
**Skills Blocked**: SKILL-082 (Hourly Booking)
**Question**: How to structure pricing for hourly/day-use bookings?
**What We Need**:
- Hourly rate calculation
- Day-use vs overnight pricing
- Meeting room pricing models
- Minimum booking durations
- Cleaning time buffers
- Dynamic hourly pricing

**Source Options**:
- [ ] Mews documentation
- [ ] Co-working space pricing research

---

### KG-MEWS-006: ML Revenue Management
**Skills Blocked**: SKILL-083 (Atomize RMS)
**Question**: How does ML-based revenue management work?
**What We Need**:
- Demand forecasting models
- Feature engineering for hotels
- Training data requirements
- Real-time vs batch predictions
- Model retraining frequency
- Explainability requirements

**Source Options**:
- [ ] Atomize documentation
- [ ] Revenue management ML papers
- [ ] Hotel data science interviews

---

### KG-MEWS-007: Booking Engine Conversion
**Skills Blocked**: SKILL-084 (Booking Engine)
**Question**: What drives direct booking conversion?
**What We Need**:
- Mobile-first design patterns
- Load time optimization
- A/B testing frameworks
- Social proof implementation
- Trust signals (reviews, badges)
- Cart abandonment recovery
- Checkout optimization

**Source Options**:
- [ ] Mews conversion studies
- [ ] E-commerce optimization research

---

### KG-MEWS-008: Pre-Arrival Data Collection
**Skills Blocked**: SKILL-086 (Data Capture)
**Question**: What data should be collected pre-arrival and how?
**What We Need**:
- Required vs optional fields
- Digital signature capture methods
- ID/passport scanning workflow
- Payment pre-authorization amounts
- GDPR consent handling
- Data retention policies

**Source Options**:
- [ ] Mews compliance documentation
- [ ] Legal/compliance consultant

---

### KG-MEWS-009: Front Desk Workflow (SKIP for STR)
**Skills Blocked**: SKILL-087 (Front Desk)
**Note**: Less relevant for STR, but useful for multi-unit buildings

---

### KG-MEWS-010: Overbooking Strategies (SKIP for STR)
**Skills Blocked**: SKILL-088 (Overbooking)
**Note**: STR doesn't typically overbook

---

### KG-MEWS-011: Staff Scheduling (SKIP for STR)
**Skills Blocked**: SKILL-089 (Shift Planning)
**Note**: STR uses contractors, not staff shifts

---

### KG-MEWS-012: Hotel Financial Metrics
**Skills Blocked**: SKILL-091 (GOPPAR)
**Question**: How to calculate GOPPAR for STR?
**What We Need**:
- GOPPAR formula adaptation for STR
- Operational cost categories
- Allocation methodology
- Benchmarking standards
- Reporting frequency

**Source Options**:
- [ ] Hotel finance textbooks
- [ ] STR accounting best practices

---

### KG-MEWS-013: Loyalty Program Design
**Skills Blocked**: SKILL-093 (Loyalty Tiers)
**Question**: How to design loyalty tiers for STR?
**What We Need**:
- Tier structure (how many levels)
- Point earning rules
- Tier benefits by level
- Status qualification criteria
- Recognition at property level
- Cross-property recognition

**Source Options**:
- [ ] Hotel loyalty program research
- [ ] BILT Rewards PRD (already have)

---

### KG-MEWS-014: Package Pricing Strategies
**Skills Blocked**: SKILL-094 (Package Bundling)
**Question**: How to price room + service bundles?
**What We Need**:
- Bundle discount percentages
- Service margin considerations
- Dynamic vs fixed bundles
- Seasonal package variations
- Bundle display in booking flow

**Source Options**:
- [ ] Hotel package pricing research
- [ ] E-commerce bundling strategies

---

## 📋 Knowledge Acquisition Priority for STR

### HIGH Priority (Adopt for STR)
| Gap | Topic | Impact |
|-----|-------|--------|
| KG-MEWS-003 | Digital Key Hardware | Better guest experience |
| KG-MEWS-004 | Apple Wallet | Premium differentiation |
| KG-MEWS-007 | Booking Conversion | Direct booking revenue |
| KG-MEWS-008 | Pre-Arrival Data | Compliance + convenience |

### MEDIUM Priority (Consider)
| Gap | Topic | Impact |
|-----|-------|--------|
| KG-MEWS-012 | GOPPAR | Profitability analytics |
| KG-MEWS-013 | Loyalty Tiers | Repeat booking |
| KG-MEWS-014 | Package Pricing | Revenue optimization |
| KG-MEWS-006 | ML Revenue | Advanced pricing |

### LOW Priority (Skip for now)
| Gap | Topic | Reason |
|-----|-------|--------|
| KG-MEWS-001 | Kiosk Hardware | Premium/enterprise only |
| KG-MEWS-002 | Kiosk Upsell | Premium/enterprise only |
| KG-MEWS-005 | Hourly Booking | Niche use case |
| KG-MEWS-009 | Front Desk | Not relevant for STR |
| KG-MEWS-010 | Overbooking | STR doesn't overbook |
| KG-MEWS-011 | Shift Planning | STR uses contractors |

---

## 🎯 Combined Knowledge Gap Summary

| Source | Total | HIGH | MEDIUM | LOW/Skip |
|--------|-------|------|--------|----------|
| Guesty | 16 | 5 | 7 | 4 |
| Host OS | 9 | 4 | 5 | 0 |
| Mews | 14 | 4 | 4 | 6 |
| **TOTAL** | **39** | **13** | **16** | **10** |

---

## ✅ Key Takeaways from Mews

**What Mews teaches us:**
1. **Digital Key > Access Codes** - Apple Wallet is better UX than codes
2. **No-App Messaging** - Guests prefer SMS links to app downloads
3. **A/B Testing Built-In** - Conversion optimization is a feature
4. **GOPPAR > Revenue** - Profitability matters more than top-line
5. **Pre-Arrival = Time Savings** - Capture data before arrival

**What to SKIP from Mews for STR:**
1. Front desk workflow (no front desk in STR)
2. Overbooking (STR doesn't overbook)
3. Staff shifts (STR uses contractors)
4. Hourly bookings (niche for STR)

